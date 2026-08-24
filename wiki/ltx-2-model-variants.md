---
title: LTX-2 Model Variants and Quantizations
type: reference
created: 2026-04-13
updated: 2026-08-24
sources:
  - raw/ltx2-model-variants-quantizations.md
  - raw/ltx2-capabilities-and-specifications.md
  - raw/ltx-news-ltx23-model-variants-may27-2026.md
  - raw/ltx-news-ltx-2-5-release-2026-08-11.md
  - raw/ltx-news-ltx-2-5-api-pricing-and-benchmarks-2026-08.md
tags:
  - ltx-2
  - ltx-2.5
  - model-variants
  - quantization
  - gguf
  - fp8
  - distillation
  - weights
---

# LTX-2 Model Variants and Quantizations

Official and community weight variants for the [[ltx-2-overview|LTX-2]] model family.

## LTX-2 (19B) Weight Checkpoints

| Checkpoint | Precision | Description | Size |
|-----------|-----------|-------------|------|
| ltx-2-dev | BF16 | Full-precision dev model | ~38GB |
| ltx-2-fp8 | FP8 | Quantized for lower VRAM | ~18-20GB |
| ltx-2-distilled | BF16 | 8-step distilled, CFG=1 | Smaller |
| ltx-2-fp8-distilled | FP8 | Distilled + quantized | Smallest |

## LTX-2.3 (22B) Weight Checkpoints

| Checkpoint | Precision | Description |
|-----------|-----------|-------------|
| ltx-2.3-22b-dev.safetensors | BF16 | Full model (~42GB), for fine-tuning |
| ltx-2.3-22b-distilled.safetensors | BF16 | 8-step distilled, faster inference |
| ltx-2.3-fp8 | FP8 | Lower VRAM setups |
| ltx-2.3-22b-dev-mxfp8 | MXFP8 | Microscaling FP8; transformer-only (Kijai, May 2026) |
| ltx-2.3-22b-distilled-mxfp8 | MXFP8 | Distilled + Microscaling FP8 (Kijai, May 2026) |
| ltx-2.3-22b-dev-nvfp4 | NVFP4 | Official Lightricks; 21.7 GB; RTX 50xx (Blackwell) only |

## LTX-2.5 (22B) Weight Checkpoints

Released August 11, 2026 on Hugging Face as `Lightricks/LTX-2.5` (collection `Lightricks/ltx-25`). See [[ltx-2.5-model]].

| Checkpoint | Precision | Description |
|-----------|-----------|-------------|
| `ltx-2.5-22b-dev-transformer-bf16.safetensors` | BF16 | Base transformer, for fine-tuning |
| `ltx-2.5-22b-distilled-transformer-bf16.safetensors` | BF16 | Distilled transformer, substantially improved over 2.3 |
| distilled transformer, int8 convrot | INT8 | ComfyUI-ready quantization |
| distilled transformer, NVFP4 | NVFP4 | ComfyUI-ready; Blackwell/RTX 50xx |
| `gemma4-12b-with-proj-ltx-2.5` | BF16 / int8 convrot | Text encoder with learned projection (replaces the 2.3 text connector) |
| Video VAE | BF16 | Separate checkpoint |
| Audio VAE | BF16 | Separate checkpoint |
| 2x latent spatial upscaler | -- | Two-stage pipeline |
| 2x latent temporal upscaler | -- | Frame rate doubling |
| Distilled LoRA (450) | -- | Add-on |
| Duration-head model patch | -- | Powers automatic duration |
| Pretrained (non-SFT) checkpoint | BF16 | Tuned for physical AI / robotics domain fine-tuning |

**Minimum VRAM: 16GB** on any GPU -- data-center hardware down to a Mac. The distilled model was optimized with [[nvidia-ltx-partnership|NVIDIA]] for local inference on RTX GPUs and DGX Spark.

## LTX-2.5 API Variants

| Model ID | Max Resolution | Duration Support | Notes |
|----------|----------------|------------------|-------|
| `ltx-2-5-fast` | 4K | 720p/1080p @ 24/25 fps: 6-20 s; 720p/1080p @ 48/50 fps: 6/8/10 s; 1440p/4K @ 24/25/48/50 fps: 6/8/10 s | Speed and low cost |
| `ltx-2-5-pro` | 1080p | 720p/1080p @ 24/25/50 fps: 6/8/10 s only | Higher fidelity |

Both support text-to-video, image-to-video and audio-to-video, portrait and landscape, camera motion, `last_frame_uri` on image-to-video, and `"duration": null` for automatic duration (cannot be combined with `last_frame_uri`). **Neither supports retake, extend or reframe** -- those remain `ltx-2-3-pro` only.

Resolutions: 720p `1280x720`/`720x1280`; 1080p `1920x1080`/`1080x1920`; 1440p `2560x1440`/`1440x2560`; 4K `3840x2160`/`2160x3840`. Prepaid accounts have credits held against the maximum duration for the chosen resolution/fps when using automatic duration, released on completion. Pricing in [[ltx-video-api-pricing]].

The legacy `ltx-2-fast` and `ltx-2-pro` API IDs were **removed on August 16, 2026** and now return an error -- see [[ltx-video-changelog]].

## Upscalers

Operate entirely in latent space (before VAE decode), used in the recommended two-stage pipeline for production quality.

| Upscaler | Function | Version |
|----------|----------|---------|
| Spatial upscaler (1.5x) | Resolution upscaling | LTX-2 and LTX-2.3 |
| Spatial upscaler (2x) v1.1 | Resolution upscaling (updated May 2026) | LTX-2.3 |
| Temporal upscaler | Frame rate doubling | LTX-2.3 and LTX-2.5 |

Example workflow: Generate at 512x768, upscale to 1024x1536. Generate at 24 FPS, temporal upscale to 48 FPS.

## Distilled Model Details

- Trained to replicate the behavior of the full model
- Uses 8 predefined diffusion steps (vs 30-36 for full model)
- CFG set to 1 (no guidance needed)
- Significantly faster inference at cost of some quality
- HuggingFace Spaces demos use distilled variants
- Best for: rapid prototyping, interactive workflows, lower-VRAM setups

## Community GGUF Quantizations

| Provider | Notes |
|---------|-------|
| unsloth/LTX-2-GGUF | Popular community option, multiple quant levels |
| vantagewithai/LTX-2-GGUF | Alternative GGUF set |

### GGUF Performance Examples

- **Q4_K_S** on RTX 3080 (10GB VRAM): 960x544, 5-second clip with audio in ~2-3 minutes
- **Q8_0** on RTX 4070: Better quality, moderate VRAM usage

## NVIDIA Quantizations

See [[ltx-2-nvidia-optimization]] for details.

| Type | Speed | VRAM Reduction | GPUs |
|------|-------|---------------|------|
| NVFP8 | 2x faster | 40% less | RTX 30/40/50 Series |
| NVFP4 | 3x faster | 60% less | RTX 50 Series only |

## Community FP8 / MXFP8 Variants

- **GitMylo/LTX-2-comfy_gemma_fp8_e4m3fn** -- FP8 Gemma text encoder for ComfyUI
- **Kijai/LTXV2_comfy** -- Community ComfyUI-optimized weights (includes Audio VAE, MXFP8 variants)
- **Kijai Audio VAE (May 2026)** -- Standalone audio VAE enabling audio-conditioned generation in ComfyUI workflows
- **Dynamic LoRA rank-105 (Kijai, May 2026)** -- Dynamic-rank LoRA for LTX-2.3

### MXFP8 (Microscaling FP8)
MXFP8 is a newer quantization format (MX-format) offering better accuracy than standard FP8 at similar memory footprint. These are transformer-only weights requiring separate VAE and text encoder files.

## VRAM Requirements by Variant

| Variant | VRAM Required | GPU Examples |
|---------|---------------|-------------|
| Full BF16 (dev) | 32GB+ | A100, H100 |
| FP8 Standard | 16-20GB | RTX 4070 Ti, RTX 3090 |
| FP8 Distilled | 14-16GB | RTX 4060 Ti 16GB |
| GGUF Q8_0 | ~14-16GB | RTX 4070 |
| GGUF Q4_K_S | 8-10GB | RTX 3080, RTX 3070 |
| NVFP4 (RTX 50) | ~13GB | RTX 5070+ |
| Minimum viable | 12GB | RTX 3060 (with offloading) |

## Related Pages

- [[ltx-2-overview]] -- Model overview
- [[ltx-2.5-model]] -- Current flagship
- [[ltx-2.5-technical]] -- LTX-2.5 architecture
- [[ltx-2-huggingface-ecosystem]] -- Where to download
- [[ltx-2-nvidia-optimization]] -- GPU-specific acceleration
- [[ltx-2-capabilities]] -- What each variant can do
- [[ltx-2-lora-training]] -- Fine-tuning these variants
