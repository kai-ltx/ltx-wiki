---
title: Training Dataset Preparation
type: guide
created: 2026-04-13
updated: 2026-09-28
sources:
  - raw/training-fine-tuning.md
  - raw/python-lora-training-guide.md
  - raw/community-project-lora-training-tools.md
  - raw/tutorial-ltx-2-5-training-data-guide-2026-09.md
tags:
  - training
  - dataset
  - lora
  - captions
---
# Training Dataset Preparation

Proper dataset preparation is critical to successful [[lora-training]] on [[ltx-video-overview|LTX-Video]] models. This page covers format requirements, captioning, sizing guidelines, and public datasets.

## Critical Format Rules

### Frame Count: The 8n+1 Rule

All video clips must have a frame count following the formula **8n+1**:
- Valid frame counts: 1, 9, 17, 25, 33, 41, 49, 57, 65, 73, 81, ..., 121, 161
- If clips have non-conforming frame counts (e.g., 10 or 15 frames), the trainer will either error or pad internally
- Example: 17 frames = 2 x 8 + 1

### Resolution

Width and height must be **divisible by 32**.
- Common resolutions: 512x512, 768x512, 512x768, 720x480
- Videos should ideally match the target generation resolution (e.g., 704x480, 768x512)

### Format

- Video: MP4 or other common video formats
- Images: PNG, JPG
- FPS: 24 or 25 FPS recommended

## Directory Structure

```
dataset/
  video_001.mp4
  video_001.txt       # Caption file
  video_002.mp4
  video_002.txt
  image_001.png
  image_001.txt
  ...
```

Each `.txt` file must contain the text description/caption for the corresponding video or image.

### HuggingFace Datasets Format

Alternatively, use a HuggingFace Dataset:

```python
from datasets import Dataset

dataset = Dataset.from_dict({
    "video": ["path/to/video1.mp4", "path/to/video2.mp4"],
    "text": ["Caption for video 1", "Caption for video 2"]
})
```

## Captioning

Every clip needs a detailed caption containing your **trigger word**. Poor captions produce poor results.

### Caption Guidelines

- English language only
- Detailed and elaborate (matching the model's expected prompt style)
- Include: subject description, actions, visual style, camera movement, lighting, environment
- Place trigger word at the beginning of the caption

### Example Caption

```
MYTRIGGER A woman with flowing red hair walks through a sunlit meadow,
her dress billowing in the gentle breeze. The camera slowly pans from
left to right, following her movement. Warm golden light filters through
the trees, creating dappled shadows on the ground. The scene has a
dreamy, ethereal quality with soft focus in the background.
```

### Trigger Words

- Add a unique, distinctive trigger word to all captions during training
- This allows activating the LoRA style on demand at inference time
- Official examples: `SQUISH`, `CAKEIFY`
- Trigger word patterns:
  - **Squish:** `SQUISH two hands squeezing a squeezable object that is shaped like [object]`
  - **Cakeify:** `CAKEIFY a person using a knife to cut a cake shaped like [object]`

## LTX-2.5 Specifics (per official LTX blog, 2026-09-07)

- **Choosing an approach:** standard LoRA (lightweight adapters, frozen base, single-GPU-capable) is the default for a focused style/subject/effect. Full fine-tuning updates all parameters and needs multiple high-end GPUs (documented FSDP setups: 4-8x H100 80GB). IC-LoRA needs **paired reference + target data** and is for transformations (depth/pose control, style transfer, deblurring, colorization) — see [[python-ic-lora]].
- **Sequence length formula:** `(H/32) * (W/32) * ((F-1)/8 + 1)` — e.g. a 768x448x89 clip works out to 4,032 tokens. The documented guideline: larger spatial dimensions + fewer frames for detailed clips (e.g. 768x448 at 89 frames); smaller spatial dimensions + more frames for motion-heavy clips (e.g. 512x512 at 121 frames).
- **Text encoder compatibility is a hard requirement:** LTX-2.5 must use the LTX-specific fine-tuned Gemma 4 12B encoder, not Google's vanilla Gemma 4 — the pipeline validates encoder version against the checkpoint and will fail the compatibility check otherwise. Older LTX-2/LTX-2.3 checkpoints use a matching Gemma 3 encoder instead. **Migrating a dataset from LTX-2.3 to LTX-2.5 requires reprocessing text features** with the new Gemma 4 encoder (Gemma 3 and Gemma 4 embeddings are not interchangeable) — use a fresh `.precomputed` output directory or pass `--overwrite`.
- **Auto-captioning:** the current LTX Trainer's `caption_videos.py` supports a local `qwen_omni` captioner or the `gemini_flash` API captioner, and can describe both visual content and audio (speech, music, ambient sound). Auto-captions can hallucinate and should be manually reviewed before preprocessing.
- **3-step preprocessing workflow:** (1) optional scene-splitting via `scripts/split_scenes.py input.mp4 scenes_output_dir/ --filter-shorter-than 5s`; (2) optional captioning into a `dataset.json` (CSV/JSON/JSONL accepted; `caption`/`video` columns, `media_path` is a legacy alias for `video`); (3) `scripts/process_dataset.py dataset.json --resolution-buckets "960x544x49" --model-path ... --text-encoder-path ...` to compute and cache latents and text embeddings. Audio latents are extracted automatically unless `--skip-audio` is passed. For IC-LoRA, add a `reference_video` column — `process_dataset.py` auto-detects it.
- **Mixed image+video datasets** need separate resolution buckets per frame count and a training batch size of 1 (images use frame count 1 in the bucket, e.g. `960x544x1`).

## Dataset Size Guidelines

| LoRA Type | Minimum | Recommended | Notes |
|-----------|---------|-------------|-------|
| Style | 10-20 images | 20-50 images | Still frames work well |
| Character | 20-30 images | 40-80 images | Various angles/expressions |
| Motion | 10-15 clips | 20-30 clips | Short coherent video clips |
| Complex | 30-50 items | 80-120 items | For highly specific subjects |
| General (Diffusers) | 50 videos | 50-500 videos | For a specific style |

## Data Quality Tips

- Use high-quality, consistent video data
- Ensure captions accurately describe the video content
- Aim for consistent resolution and frame rate across the dataset
- For character LoRAs, include various angles and expressions
- For motion LoRAs, use video clips (not stills) with coherent movement

## Public Training Datasets

Lightricks provides three public datasets for reproducible training and experimentation:

| Dataset | Purpose | URL |
|---------|---------|-----|
| Squish-Dataset | Object deformation effects | huggingface.co/datasets/Lightricks/Squish-Dataset |
| Cakeify-Dataset | Object-to-cake transformation | huggingface.co/datasets/Lightricks/Cakeify-Dataset |
| Canny-Control-Dataset | Edge-based control training | huggingface.co/datasets/Lightricks/Canny-Control-Dataset |

## References

- [[lora-training]]
- [[training-hyperparameters]]
- [[ltx-video-trainer]]
