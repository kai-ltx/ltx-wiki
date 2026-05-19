---
title: LoRA Community Ecosystem
type: reference
created: 2026-04-13
updated: 2026-05-19
sources:
  - raw/social-lora-training-community-ecosystem.md
  - raw/community-project-lora-training-tools.md
  - raw/third-party-lora-training-services.md
  - raw/community-ltx-comfyui-lora-ecosystem-april-may-2026.md
tags:
  - community
  - lora
  - ecosystem
  - civitai
  - huggingface
  - ic-lora
---
# LoRA Community Ecosystem

An active community has formed around [[lora-training]] for [[ltx-video-overview|LTX-Video]] models, sharing trained LoRAs, tools, and knowledge across multiple platforms. See [[lora-ecosystem]] for the full inventory of official and community LoRA adapters.

## Community Sentiment

- Very positive about training ecosystem maturity
- Community values the official trainer being open source
- Multiple cloud training options reduce barrier to entry
- [[ic-lora|IC-LoRA]] seen as innovative and unique capability
- Concern about LoRA compatibility across model versions

## Community-Shared LoRAs

### Civitai

Multiple community-trained LoRAs are shared on Civitai:

- **LTX-2 IC-LoRA Detailer** -- enhances fine visual details and clarity
- **SSX LTX2 T2V** -- text-to-video LoRA trained with the official trainer
- Various style, NSFW, and image-to-video adapter LoRAs

### HuggingFace

| Model Family | Adapter Models | Community Fine-tunes |
|-------------|----------------|---------------------|
| LTX-Video | 24 | 25 |
| LTX-2 | 49 | 54 |
| LTX-2.3 | 20 | 27 |

Notable community contributions on HuggingFace:
- **Phr00t/LTX2-Rapid-Merges** -- community model merges
- **Kijai/LTXV2_comfy**, **Kijai/LTX2.3_comfy** -- widely used quantized variants

## Notable Community LoRA Authors

- **Burgstall** -- Multiple expression LoRAs (amgery, smile, surprise, headbanger)
- **svjack** -- Style LoRAs (anime landscape, pixel art)
- **Pierre-Jean** -- Camera trajectory LoRA
- **Sameric934** -- General LTX-2 video LoRA

## Cross-Version LoRA Transfer

A key community discovery from HuggingFace Discussion #4 on LTX-2.3:

- LTX-2.0 trained LoRAs work **significantly better** on LTX-2.3 than on 2.0 itself
- LoRAs that were unusable for further training on 2.0 become usable on 2.3
- Inference requires reduced strength values when applying 2.0 LoRAs to 2.3

## Training on Quantized Models

From HuggingFace Discussion #92 on LTX-Video:
- LoRA fine-tuning confirmed to work on FP8 quantized models
- Enables training on lower-VRAM hardware (under 24GB)

## Community Resource Hub

**awesome-ltx2** (github.com/wildminder/awesome-ltx2):
- Community-maintained collection of all available resources
- LTX-2 models, encoders, workflows, LoRAs for [[comfyui-ltx-integration-overview|ComfyUI]]
- Central aggregation point for the community

## Uploading LoRAs

### To HuggingFace Hub

```python
from huggingface_hub import HfApi

api = HfApi()
api.upload_folder(
    folder_path="output/ltx-video-lora",
    repo_id="your-username/my-ltx-video-lora",
    repo_type="model",
)
```

## Official IC-LoRA Releases (April–May 2026)

Lightricks shipped several new [[ic-lora|IC-LoRA]] adapters for LTX-2.3 in this period:

### HDR IC-LoRA (~April 23, 2026)
- Adds HDR-style color grading and dynamic range control to generated video
- Initial community reports: tiled VAE decoding caused video flickering (GitHub issue #470, ComfyUI-LTXVideo)
- Fix: switching from tiled to non-tiled (default) VAE decode eliminated flickering
- Lightricks acknowledged and monitored the issue actively

### LipDub IC-LoRA
- Enables dubbing or rephrasing of speech in existing video
- Generates new lip movements and audio matching target text while preserving speaker identity
- Significant for multi-language content creation
- YouTube walkthrough: "LTX 2.3 Just Changed AI Dubbing Forever"

### Union IC-LoRA
- Combines depth and edge control conditions in a **single model** (replaces running two separate adapters)
- Operates on downsampled latents to reduce memory usage and speed up inference
- Important for running on consumer-grade hardware

### ID-LoRA (Identity-Controlled Video)
- Maintains consistent character identity across generated video clips
- Community workflow available on RunComfy.com: "LTX 2.3 ID-LoRA in ComfyUI — Identity-Controlled Video Creator"

## GitHub Activity (April–May 2026)

- **ComfyUI-LTXVideo issue #470** — HDR IC-LoRA flickering: community-diagnosed and resolved within days
- **LTX-2 repo issue #128** — ComfyUI workflow issues with `video_ltx2_t2v_distilled` config: active thread with Lightricks team engagement
- Pattern: active community-to-Lightricks feedback loop, issues resolved quickly

## Ecosystem Scale (May 2026)

| Platform | LTX-Video | LTX-2 | LTX-2.3 |
|----------|-----------|-------|---------|
| HuggingFace adapter models | 24 | 49 | 20 |
| Community fine-tunes | 25 | 54 | 27 |

Common friction points: hardware memory requirements for longer clips; occasional workflow compatibility gaps when Lightricks updates the model between ComfyUI node updates.

## References

- [[lora-training]]
- [[ltx-video-trainer]]
- [[third-party-training-services]]
- [[ic-lora]]
- [[comfyui-ltx-lora-training-control]]
