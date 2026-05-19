---
title: LTX Video 0.9.8
type: release
created: 2026-04-13
updated: 2026-05-19
sources:
  - https://huggingface.co/Lightricks/LTX-Video
  - https://huggingface.co/Lightricks/LTX-Video-0.9.8-13B-distilled
  - https://blog.fal.ai/new-ltxv-0-9-8-model-live-on-fal/
  - https://aicreators.tools/model/video/79
  - https://github.com/Lightricks/LTX-Video
  - raw/ltx-news-ltxv-13b-distilled-0-9-8-may-2026.md
  - raw/ltx-news-ltxv-13b-distilled-game-changer-may-2026.md
tags:
  - ltx-video
  - release
  - 0.9.8
  - 13b
  - 2b
---

# LTX Video 0.9.8

**Release date:** Mid-July 2025

Version 0.9.8 is the latest major release of LTX Video, continuing the [[ltxv-13b|13B model line]] introduced in [[ltx-video-097|v0.9.7]] while reintroducing a lightweight 2B distilled variant to broaden accessibility.

## What Changed from 0.9.7

- **2B distilled variant added** -- brings back the 2B model size (last seen at v0.9.6), now updated with the latest training improvements
- **[[ic-lora|IC-LoRA adapters]] updated** -- depth, pose, canny, and detailer adapters refreshed for 0.9.8
- **[[ltxv-spatial-upscaler|Upscalers]] updated** -- spatial and temporal upscalers compatible with 0.9.8
- **[[multiscale-rendering|Mix mode]] carried forward** -- multi-scale rendering workflow continues
- **Extended video generation** -- up to 60 seconds of continuous generation
- **Improved prompt understanding** -- better comprehension of complex prompts
- **Performance improvements** -- slightly faster than 0.9.7
- **New detailer model** -- `LTX-Video-ICLoRA-detailer-13B-0.9.8`

## Model Variants

### 13B Models

| Variant | Type | File Size |
|---------|------|-----------|
| `ltxv-13b-0.9.8-dev` | Full quality | ~28.6 GB |
| `ltxv-13b-0.9.8-mix` | Multi-scale balanced | ~28.6 GB |
| `ltxv-13b-0.9.8-distilled` | Fast inference | ~28.6 GB |
| `ltxv-13b-0.9.8-fp8` | FP8 quantized | ~15.7 GB |
| `ltxv-13b-0.9.8-distilled-fp8` | Fast + quantized | ~15.7 GB |

### 2B Models (New)

| Variant | Type | File Size |
|---------|------|-----------|
| `ltxv-2b-0.9.8-distilled` | Lightweight distilled | ~6.34 GB |
| `ltxv-2b-0.9.8-distilled-fp8` | Lightweight + quantized | ~4.46 GB |

## VRAM Estimates

| Model | Estimated VRAM |
|-------|---------------|
| 13B dev | ~24+ GB |
| 13B distilled | ~16-20 GB |
| 13B FP8 | ~12-16 GB |
| 2B distilled | ~8-12 GB |
| 2B distilled-fp8 | ~6-8 GB |

## Output Specifications

- **Resolution:** 1216x704 native, best under 720x1280
- **Frame rate:** 30 FPS
- **Maximum frames:** 257 (divisible by 8+1)
- **Duration:** Up to 60 seconds
- **Resolution divisibility:** Must be divisible by 32

## Configuration Files

- `configs/ltxv-13b-0.9.8-dev.yaml`
- `configs/ltxv-13b-0.9.8-distilled.yaml`
- `configs/ltxv-13b-0.9.8-mix.yaml`
- `configs/ltxv-2b-0.9.8-distilled.yaml`

## Key Inference Parameters

| Parameter | Value | Notes |
|-----------|-------|-------|
| `num_inference_steps` | 30 | Default for dev model |
| `denoise_strength` | 0.4 | For upscaling refinement |
| `decode_timestep` | 0.05 | VAE decoding parameter |
| `image_cond_noise_scale` | 0.025 | Conditioning noise scaling |

## Online Availability

- **LTX Studio (13B-mix):** https://app.ltx.studio/motion-workspace?videoModel=ltxv-13b
- **Fal.ai (13B full):** https://fal.ai/models/fal-ai/ltx-video-13b-dev/image-to-video
- **Fal.ai (13B distilled):** https://fal.ai/models/fal-ai/ltx-video-13b-distilled/image-to-video
- **Replicate:** https://replicate.com/lightricks/ltx-video

## 13B Distilled Variant — May 2026 Launch

The LTXV 13B Distilled variant received a major marketing push in May 2026, including an official LTX Studio X thread on approximately May 14, 2026 (starting at status ID 1922676336583234047) with the headline "Big news! We're introducing LTXV 13B Distilled, and it's a game-changer for video generation."

**Key claims from the official announcement:**
- Full multi-scale rendering in as little as **12 seconds** — nearly 5x faster than the base (non-distilled) 13B model
- High-quality results in only **4–8 diffusion steps**
- 5-second 720p video in ~9.5 seconds on an H100, ~1.5 minutes on an RTX 5090
- FP8 quantization support (`ltxv-13b-0.9.8-distilled-fp8.safetensors`)
- Available on fal.ai at `fal-ai/ltxv-13b-098-distilled`
- Compatible with ComfyUI via official `Lightricks/ComfyUI-LTXVideo` nodes

An earlier Show HN thread (Hacker News item ID 43987218, ~May 6, 2026) generated significant discussion about the speed improvements for local inference use cases.

**Distinction from LTX-2.x series:** The 0.9.8 distilled variant is part of the LTXV 0.9.x lineage (video-only, no synchronized audio), separate from [[ltx-2-overview|LTX-2]] / [[ltx-2.3-model|LTX-2.3]] which generate synchronized audio+video. Use 0.9.8 distilled for maximum video-only speed on lightweight hardware.

## Known Issues

- Some users reported generated videos make human skin appear plastic-like (GitHub Issue #230)

## License

All 0.9.8 variants use the **LTX-Video Open-Weights License** (same as 0.9.6+).

## See Also

- [[ltx-video-097]] -- the predecessor release
- [[ltxv-13b]] -- architecture details
- [[ltxv-model-variants]] -- detailed breakdown of all variant types
- [[ic-lora]] -- control adapters updated for 0.9.8
