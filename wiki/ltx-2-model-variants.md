---
title: LTX-2 Model Variants and Quantizations
type: reference
created: 2026-04-13
updated: 2026-06-01
sources:
  - raw/ltx2-model-variants-quantizations.md
  - raw/ltx2-capabilities-and-specifications.md
  - raw/ltx-news-ltx23-model-variants-may27-2026.md
tags:
  - ltx-2
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

## Upscalers

Operate entirely in latent space (before VAE decode), used in the recommended two-stage pipeline for production quality.

| Upscaler | Function | Version |
|----------|----------|---------|
| Spatial upscaler (1.5x) | Resolution upscaling | LTX-2 and LTX-2.3 |
| Spatial upscaler (2x) v1.1 | Resolution upscaling (updated May 2026) | LTX-2.3 |
| Temporal upscaler | Frame rate doubling | LTX-2.3 only |

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
- [[ltx-2-huggingface-ecosystem]] -- Where to download
- [[ltx-2-nvidia-optimization]] -- GPU-specific acceleration
- [[ltx-2-capabilities]] -- What each variant can do
- [[ltx-2-lora-training]] -- Fine-tuning these variants
