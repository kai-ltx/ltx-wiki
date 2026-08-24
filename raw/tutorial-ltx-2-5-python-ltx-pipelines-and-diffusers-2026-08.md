# LTX-2.5 Python Integration: ltx-pipelines CLI/API and the Diffusers Two-Stage Pipeline

**Source:** https://huggingface.co/Lightricks/LTX-2.5
**Source:** https://huggingface.co/Lightricks/LTX-2.5-Diffusers
**Source:** https://github.com/Lightricks/LTX-2
**Date:** 2026-08-11 (model card published with LTX-2.5 launch)
**Retrieved:** 2026-08-24

## Content

### Packaging change: split, Comfy-aligned checkpoints

LTX-2.5 ships as **one `.safetensors` per component** rather than a single monolith. Point each CLI flag / loader at the individual file.

**Transformers (DiT), all 22B:**
- `diffusion_models/ltx-2.5-22b-distilled-transformer-bf16.safetensors` — distilled, **fixed 8-step schedule, CFG=1**
- `diffusion_models/ltx-2.5-22b-dev-transformer-bf16.safetensors` — full / trainable
- `diffusion_models/ltx-2.5-22b-distilled-transformer-comfy-int8-convrot.safetensors` — **ComfyUI only**
- `diffusion_models/ltx-2.5-22b-dev-transformer-comfy-int8-convrot.safetensors` — **ComfyUI only**
- `diffusion_models/ltx-2.5-22b-distilled-transformer-nvfp4.safetensors` — NVFP4; ComfyUI, or `ltx-pipelines` with `--quantization nvfp4-prequant` (Blackwell / `ltx-kernels`)

**Other components:**
- `text_encoders/gemma4-12b-with-proj-ltx-2.5-bf16.safetensors` — Gemma 4 12B TE + projections
- `vae/ltx-2.5-video-vae-bf16.safetensors` — DiffVAE (diffusion decoder, higher quality, heavier)
- `vae/ltx-2.5-video-vae-conv-bf16.safetensors` — Conv VAE (faster, lighter)
- `vae/ltx-2.5-audio-vae-bf16.safetensors` — audio VAE + vocoder
- `loras/ltx-2.5-22b-distilled-lora-450-bf16.safetensors` — **rank-450** distilled LoRA for dev-transformer workflows (2.3's was rank-384)
- `model_patches/ltx-2.5-duration-head-bf16.safetensors` — auto duration when `--num-frames` is omitted
- `latent_upscale_models/ltx-2.5-latent-spatial-upscaler-x2-bf16-1.0.safetensors`
- `latent_upscale_models/ltx-2.5-latent-temporal-upscaler-x2-bf16-1.0.safetensors`

### Option A — `ltx-pipelines` (official PyTorch path)

Environment: **Python >= 3.12, CUDA >= 12.7, PyTorch ~= 2.7**.

```bash
git clone https://github.com/Lightricks/LTX-2.git
cd LTX-2
uv sync
source .venv/bin/activate
```

Weight download (gated repo — `hf auth login` first):

```bash
hf download Lightricks/LTX-2.5 \
  diffusion_models/ltx-2.5-22b-distilled-transformer-bf16.safetensors \
  text_encoders/gemma4-12b-with-proj-ltx-2.5-bf16.safetensors \
  vae/ltx-2.5-video-vae-bf16.safetensors \
  vae/ltx-2.5-audio-vae-bf16.safetensors \
  model_patches/ltx-2.5-duration-head-bf16.safetensors \
  latent_upscale_models/ltx-2.5-latent-spatial-upscaler-x2-bf16-1.0.safetensors \
  --local-dir models/ltx-2.5
```

Distilled text-to-video:

```bash
uv run python -m ltx_pipelines.distilled \
  --transformer-path       models/ltx-2.5/diffusion_models/ltx-2.5-22b-distilled-transformer-bf16.safetensors \
  --text-encoder-path      models/ltx-2.5/text_encoders/gemma4-12b-with-proj-ltx-2.5-bf16.safetensors \
  --video-vae-path         models/ltx-2.5/vae/ltx-2.5-video-vae-bf16.safetensors \
  --audio-vae-path         models/ltx-2.5/vae/ltx-2.5-audio-vae-bf16.safetensors \
  --duration-head-path     models/ltx-2.5/model_patches/ltx-2.5-duration-head-bf16.safetensors \
  --spatial-upsampler-path models/ltx-2.5/latent_upscale_models/ltx-2.5-latent-spatial-upscaler-x2-bf16-1.0.safetensors \
  --prompt "A golden retriever running through a sunny meadow, cinematic lighting" \
  --seed 42 --output-path output_distilled.mp4
```

Image-to-video adds one or more `--image PATH FRAME_IDX STRENGTH` flags (frame 0 = first-frame conditioning), e.g. `--image path/to/first_frame.jpg 0 1.0`.

Low-VRAM flags: `--quantization fp8-cast --offload cpu`. Use **bf16** checkpoints with `ltx-pipelines`; `*-comfy-int8-convrot` files are not loadable here.

Python API using the same split paths:

```python
from ltx_pipelines.distilled import DistilledPipeline
from ltx_pipelines.utils.model_paths import ModelPaths

model_paths = ModelPaths.from_split(
    transformer_path="models/ltx-2.5/diffusion_models/ltx-2.5-22b-distilled-transformer-bf16.safetensors",
    text_encoder_path="models/ltx-2.5/text_encoders/gemma4-12b-with-proj-ltx-2.5-bf16.safetensors",
    video_vae_path="models/ltx-2.5/vae/ltx-2.5-video-vae-bf16.safetensors",
    audio_vae_path="models/ltx-2.5/vae/ltx-2.5-audio-vae-bf16.safetensors",
    duration_head_path="models/ltx-2.5/model_patches/ltx-2.5-duration-head-bf16.safetensors",
)

pipe = DistilledPipeline(
    model_paths=model_paths,
    spatial_upsampler_path="models/ltx-2.5/latent_upscale_models/ltx-2.5-latent-spatial-upscaler-x2-bf16-1.0.safetensors",
)
```

New pipeline classes in the 2.5 era: **`DFRPipeline`** (Diffusion Fidelity Rendering, with optional 2x/4x temporal refinement rounds), **`RetakePipeline`** (regenerate a chosen time region), **`LipDubPipeline`** (rewrite what a speaker says, preserving voice, with matching lip movement), **`HDRICLoraPipeline`** (linear float frames via LogC3 inverse decode for EXR export). The new diffusion video decoder class is **`NADiffusionDecoder`**; it is fastest with the `natten` extra, which is **Linux + CUDA only** (Windows/macOS silently fall back to a slower path).

### Option C — Diffusers

Diffusers-compatible pack: **`Lightricks/LTX-2.5-Diffusers`** (described as a dense 19B DiT for video with synchronized 48 kHz stereo audio). **Not in a diffusers release yet** as of the window:

```bash
pip install git+https://github.com/huggingface/diffusers
```

Two-stage image-to-video (stage 2 runs at 2× stage-1 resolution):

```python
import torch
from diffusers import LTX2ImageToVideoPipeline, LTX2LatentUpsamplePipeline
from diffusers.pipelines.ltx2.latent_upsampler import LTX2LatentUpsamplerModel
from diffusers.pipelines.ltx2.utils import (
    DEFAULT_NEGATIVE_PROMPT, DISTILLED_SIGMA_VALUES, STAGE_2_DISTILLED_SIGMA_VALUES,
)
from diffusers.utils import encode_video, load_image

MODEL_ID = "Lightricks/LTX-2.5-Diffusers"
HEIGHT, WIDTH, NUM_FRAMES, FRAME_RATE = 544, 960, 121, 24.0

pipe = LTX2ImageToVideoPipeline.from_pretrained(MODEL_ID, dtype=torch.bfloat16)
pipe.enable_model_cpu_offload()
pipe.vae.enable_tiling()

latent_upsampler = LTX2LatentUpsamplerModel.from_pretrained(
    MODEL_ID, subfolder="latent_upsampler", dtype=torch.bfloat16).to("cuda")
upsample_pipe = LTX2LatentUpsamplePipeline(vae=pipe.vae, latent_upsampler=latent_upsampler)

shared = dict(
    image=load_image("path/to/first_frame.jpg"),
    prompt="The camera slowly dollies out as wind moves through the grass",
    negative_prompt=DEFAULT_NEGATIVE_PROMPT, frame_rate=FRAME_RATE,
    guidance_scale=1.0, audio_guidance_scale=1.0, stg_scale=0.0, audio_stg_scale=0.0,
    modality_scale=1.0, audio_modality_scale=1.0,
    generator=torch.Generator("cuda").manual_seed(42), return_dict=False,
)

stage_1_latents, audio_latents = pipe(
    height=HEIGHT, width=WIDTH, num_frames=NUM_FRAMES,
    sigmas=DISTILLED_SIGMA_VALUES, output_type="latent", **shared)

upsampled_latents = upsample_pipe(
    latents=stage_1_latents, output_type="latent", return_dict=False)[0]

video, audio = pipe(
    num_frames=NUM_FRAMES, sigmas=STAGE_2_DISTILLED_SIGMA_VALUES,
    latents=upsampled_latents, audio_latents=audio_latents,
    noise_scale=STAGE_2_DISTILLED_SIGMA_VALUES[0], output_type="np", **shared)

encode_video(video[0], fps=int(FRAME_RATE), output_path="output_i2v_two_stage.mp4",
             audio=audio[0].float().cpu(),
             audio_sample_rate=pipe.vocoder.config.output_sampling_rate)
```

Stage 2 takes its size from the upsampled latents, so pass no `height`/`width`.

Also noted: **vLLM-Omni** supports T2V and first-frame I2V through four pipeline classes selected with `--model-class-name`; the diffusion decoder is driven separately by `LTX2VideoDiffusionDecodePipeline` (run with `output_type="latent"`, then decode).

### Hard constraints

- `num_frames % 8 == 1` (1, 9, 17, …, 121)
- Width and height divisible by **32** (one-stage); the LTX quantization guide notes **divisible by 64 for two-stage pipelines**
- Omit `--num-frames` to let the duration head pick length from the prompt (LTX-2.5+)

### LoRA compatibility

Per the model card: "the large majority of LoRAs and IC-LoRAs trained on LTX-2.3 run on LTX-2.5 without changes. A small number of exceptions exist — validate your adapters before production use." Note this contradicts community reports; checkpoints themselves are not interchangeable. The **dev** transformer is fully trainable via the LTX-2 Trainer.

### Repo state

`github.com/Lightricks/LTX-2` at retrieval: **8.1k stars, 1.3k forks, 87 open issues, 39 commits, no tagged releases published.** Monorepo packages: `ltx-core`, `ltx-pipelines`, `ltx-trainer`. Its README quick-start still pointed at **LTX-2.3** weights and Gemma 3 as of retrieval, i.e. lagging the 2.5 model card. Optimization tips from the README: `--quantization fp8-cast` (bf16 checkpoints) or `fp8-scaled-mm` (Hopper + TensorRT-LLM, fp8 checkpoints); FlashAttention 4 on datacenter Blackwell B200 via `uv pip install 'flash-attn-4==4.0.0b9'` (verified against torch 2.9.1+cu128); xFormers elsewhere (`uv sync --extra xformers`); gradient estimation to cut steps from 40 to 20–30.
