---
title: LTX-2 / LTX-2.5 Diffusers and PyTorch API
type: guide
created: 2026-04-13
updated: 2026-08-24
sources:
  - raw/ltx2-diffusers-pipeline-usage.md
  - raw/tutorial-ltx-2-5-python-ltx-pipelines-and-diffusers-2026-08.md
tags:
  - ltx2
  - diffusers
  - huggingface
  - pytorch
  - python
  - api
  - ltx-2-5
---

# LTX-2 Diffusers and PyTorch API

[[ltx2-open-source-overview|LTX-2]] and [[ltx-2.5-model|LTX-2.5]] are available through two Python integration paths: the HuggingFace Diffusers library (higher-level API) and the native PyTorch API (`ltx-pipelines`) which exposes more pipeline variants and advanced configuration.

## Documentation

- Diffusers docs: https://huggingface.co/docs/diffusers/api/pipelines/ltx2
- Native PyTorch API docs: https://docs.ltx.video/open-source-model/integration-tools/pytorch-api

## HuggingFace Diffusers

### Available Pipeline Classes

| Class | Purpose |
|-------|---------|
| `LTX2Pipeline` | Main text-to-video generation |
| `LTX2LatentUpsamplePipeline` | Latent space 2x upsampling (stage 2) |
| `LTX2LatentUpsamplerModel` | Upsampler model component |
| `AutoencoderKLLTX2Audio` | Audio VAE encoder/decoder |
| `FlowMatchEulerDiscreteScheduler` | Recommended scheduler |

### Basic Usage

```python
import torch
from diffusers import FlowMatchEulerDiscreteScheduler
from diffusers.pipelines.ltx2 import LTX2Pipeline, LTX2LatentUpsamplePipeline
from diffusers.pipelines.ltx2.latent_upsampler import LTX2LatentUpsamplerModel

pipe = LTX2Pipeline.from_pretrained(
    "Lightricks/LTX-2",
    torch_dtype=torch.bfloat16
)
pipe.enable_sequential_cpu_offload()

prompt = "A beautiful sunset over the ocean with waves gently rolling"
video = pipe(
    prompt=prompt,
    width=768,
    height=512,
    num_inference_steps=30,
).videos[0]
```

### Memory Optimization

**CPU Offloading:**
```python
pipe.enable_sequential_cpu_offload()  # Recommended for consumer GPUs
```

**FP8 Loading:**
```python
pipe = LTX2Pipeline.from_pretrained(
    "Lightricks/LTX-2",
    variant="fp8",
    torch_dtype=torch.float8_e4m3fn
)
```

### Condition Pipeline

The Diffusers condition pipeline enables flexible video generation with various conditioning inputs, supporting both single-stage and two-stage approaches.

## Native PyTorch API (ltx-pipelines)

The LTX-2 repository provides more pipeline variants than the Diffusers integration.

### Installation

```bash
git clone https://github.com/Lightricks/LTX-2.git
cd LTX-2
pip install -e packages/ltx-core
pip install -e packages/ltx-pipelines
```

### Available Pipelines

| Pipeline | Description |
|----------|-------------|
| TI2VidTwoStagesPipeline | Production-quality with 2x upsampling (recommended) |
| TI2VidTwoStagesHQPipeline | Higher quality using res_2s sampler |
| TI2VidOneStagePipeline | Rapid prototyping |
| DistilledPipeline | Fastest inference with 8 predefined sigmas |
| ICLoraPipeline | Video-to-video transformations |
| KeyframeInterpolationPipeline | Inter-frame generation |
| A2VidPipelineTwoStage | Audio-conditioned generation |

## Two-Stage Generation Pipeline (Recommended)

Both Diffusers and the native API support the recommended two-stage approach:

1. **Stage 1: Generate Base Video** -- Produces coherent video at target resolution using diffusion sampling with CFG
2. **Stage 2: Upsample and Refine** -- Upsamples by 2x, refines details using distilled LoRA for improved fidelity

## Diffusers vs Native API Comparison

| Feature | Diffusers | Native (ltx-pipelines) |
|---------|-----------|----------------------|
| Ease of use | Higher (standard HF patterns) | Lower (custom API) |
| Pipeline variants | Core (text2vid, upsample) | All 7+ variants |
| IC-LoRA support | In progress | Full support |
| Audio-to-video | In progress | Full support |
| Memory management | HF standard offloading | Custom optimizations |
| Integration | Works with HF ecosystem | Standalone |

## System Requirements

- Python 3.10+
- CUDA 12.7+
- PyTorch ~2.7
- NVIDIA GPU with 32GB+ VRAM (recommended)

See [[ltx2-system-requirements]] for full details.

## LTX-2.5 (August 2026)

### Diffusers pack: `Lightricks/LTX-2.5-Diffusers`

Described on the model card as a **dense 19B DiT for video with synchronized 48 kHz stereo audio**. **Not in a tagged diffusers release** as of 2026-08-24 -- install from git:

```bash
pip install git+https://github.com/huggingface/diffusers
```

New classes: **`LTX2ImageToVideoPipeline`** and **`LTX2LatentUpsamplePipeline`**, plus `LTX2LatentUpsamplerModel` and the sigma constants in `diffusers.pipelines.ltx2.utils`.

### Two-stage image-to-video (stage 2 runs at 2x stage-1 resolution)

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

**Stage 2 takes its size from the upsampled latents, so pass no `height`/`width`.**

### New `ltx-pipelines` classes in the 2.5 era

| Class | Purpose |
|---|---|
| `DFRPipeline` | Diffusion Fidelity Rendering, with optional 2x/4x temporal refinement rounds |
| `RetakePipeline` | Regenerate a chosen time region of an existing clip |
| `LipDubPipeline` | Rewrite what a speaker says, preserving voice, with matching lip movement |
| `HDRICLoraPipeline` | Linear float frames via LogC3 inverse decode, for EXR export |
| `NADiffusionDecoder` | The new diffusion video **decoder** class |

`NADiffusionDecoder` is fastest with the `natten` extra, which is **Linux + CUDA only** -- Windows and macOS silently fall back to a slower path.

### Split checkpoints

LTX-2.5 ships **one `.safetensors` per component** rather than a monolith; point each CLI flag or loader at the individual file. Environment for `ltx-pipelines`: **Python >= 3.12, CUDA >= 12.7, PyTorch ~= 2.7**.

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

Use **bf16** checkpoints here; `*-comfy-int8-convrot` files load only in ComfyUI ([[ltx-2.5-comfyui-integration]]). Low-VRAM flags: `--quantization fp8-cast --offload cpu` (see [[ltx-2.5-local-inference]]). Image-to-video adds `--image PATH FRAME_IDX STRENGTH` flags, e.g. `--image path/to/first_frame.jpg 0 1.0` for first-frame conditioning.

### Hard constraints (LTX-2.5)

- `num_frames % 8 == 1` (1, 9, 17, ..., 121)
- Width and height divisible by **32** for one-stage; **64 for two-stage pipelines**
- Omit `--num-frames` to let the duration head pick length from the prompt

### vLLM-Omni

vLLM-Omni supports T2V and first-frame I2V through four pipeline classes selected with `--model-class-name`. The diffusion decoder is driven separately by `LTX2VideoDiffusionDecodePipeline` -- run with `output_type="latent"`, then decode.

### Repo state (retrieved 2026-08-24)

`github.com/Lightricks/LTX-2`: **8.1k stars, 1.3k forks, 87 open issues, 39 commits, and no tagged releases published.** Monorepo packages: `ltx-core`, `ltx-pipelines`, `ltx-trainer`. Its **README quick-start still points at LTX-2.3 weights and Gemma 3**, lagging the 2.5 model card -- do not trust the README for 2.5 setup.

README optimization tips: `--quantization fp8-cast` (bf16 checkpoints) or `fp8-scaled-mm` (Hopper + TensorRT-LLM, fp8 checkpoints); FlashAttention 4 on datacenter Blackwell B200 via `uv pip install 'flash-attn-4==4.0.0b9'` (verified against torch 2.9.1+cu128); xFormers elsewhere (`uv sync --extra xformers`); gradient estimation to cut steps from 40 to 20-30.

### LoRA compatibility

The 2.5 model card states: *"the large majority of LoRAs and IC-LoRAs trained on LTX-2.3 run on LTX-2.5 without changes. A small number of exceptions exist -- validate your adapters before production use."* **This contradicts community reports**, which found checkpoints themselves are not interchangeable and LoRAs only work with the model they were trained on. The **dev** transformer is fully trainable via the LTX-2 Trainer. LTX-2.5's distilled LoRA is **rank-450** (2.3's was rank-384).

## Known Issues

- **Issue #12925:** Distilled checkpoint support in Diffusers
- **Issue #12926:** LTX-2 condition pipeline support
- Image-to-video stability issues documented in HF discussions

## Community Conversions

- **CalamitousFelicitousness/LTX-2.3-distilled-Diffusers** -- Community conversion of LTX-2.3 distilled model to Diffusers format

## See Also

- [[ltx-2.5-model]] · [[ltx-2.5-technical]]
- [[ltx-2.5-local-inference]] · [[ltx-2.5-comfyui-integration]]
- [[ltx2-open-source-overview]]
- [[ltx2-comfyui-integration]]
- [[ltx2-text-to-video-guide]]
- [[ltx2-image-to-video-guide]]
- [[ltx2-system-requirements]]
