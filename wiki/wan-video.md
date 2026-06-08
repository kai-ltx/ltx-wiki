---
title: Wan Video
type: concept
created: 2026-04-13
updated: 2026-06-08
sources:
  - raw/competitor-model-wan-video.md
  - raw/open-source-comparison.md
  - raw/related-work-and-comparisons.md
  - raw/competitor-wan-2-7-release-april-2026.md
  - raw/competitor-ai-video-landscape-june-2026.md
tags:
  - competitor
  - alibaba
  - video-generation
  - open-source
  - moe
---

# Wan Video

Wan Video is Alibaba's open-source video generation model family, developed by the Tongyi Lab. It is widely regarded as one of the top open-source video generation models as of early 2026, particularly praised for its motion realism. The series has evolved rapidly through Wan 2.1, Wan 2.1-VACE, Wan 2.2, and Wan 2.2-S2V.

## Key Facts

- **Developer:** Alibaba (Tongyi Lab)
- **Parameters:** 1.3B (lightweight), 5B (mid), 14B (full)
- **Architecture:** Mixture of Experts (MoE) diffusion backbone
- **Max resolution:** 1080p native (Wan 2.2)
- **FPS:** 24 fps
- **Duration:** Up to 5 seconds per generation
- **License:** Apache 2.0
- **Downloads:** 6.9M+ on Hugging Face and ModelScope

## Version History

### Wan 2.1 (February 2025)
- Four models: 14B and 1.3B parameter variants
- Top of the VBench leaderboard at time of release
- First video generation model supporting text effects in Chinese and English
- Generates 5-second 480p video in under 4 minutes on an RTX 4090

### Wan 2.1-VACE (May 2025)
- Video All-in-one Creation and Editing model
- First open-source model providing unified video generation and editing
- Supports camera trajectory controls, subject locking, background stabilization

### Wan 2.2 (2025)
- Introduces Mixture of Experts (MoE) architecture with high-noise and low-noise expert models
- Full HD (1080p) output without upscaling
- Same VRAM footprint as Wan 2.1 on significantly more training data
- Variants: T2V-1.3B, T2V-A14B, I2V-5B, I2V-A14B, TI2V-5B

### Wan 2.2-S2V (August 2025)
- Speech-to-Video model for digital human creation
- Converts portrait photos into film-quality avatars capable of speaking, singing, and performing

### Wan 2.6 (December 2025)
- Open-source image model (text-to-image focus)

### Wan 2.7 (Cloud launch April 3, 2026; open weights confirmed available as of May 2026)
- **Architecture:** MoE diffusion transformer — 27B total parameters, 14B active per inference pass
- **Unified architecture** covering text-to-video, image-to-video, reference-to-video with voice cloning, and instruction-based video editing
- **4K image generation** (2K for video output)
- **Up to 9 reference images** for style and content guidance
- **Coherent image set generation** — up to 12 related images per single request
- **Thinking mode** for enhanced compositional reasoning
- **Native audio output** built in (first Wan version with this)
- **First and last frame control** for precise video bookending
- **Multi-reference character consistency** across scenes
- Generates 1080p video up to 15 seconds
- Apache 2.0 license, no face filters, no regional blocks
- API pricing: **$6.00/min** (33% cheaper than prior Wan versions) via providers including fal.ai and Replicate
- Competes directly with [[competitor-kling|Kling 3.0]], [[competitor-runway|Runway Gen-4.5]], and Veo models on ELO leaderboard


### Wan 3.0 (Alibaba roadmap target: mid-2026)
- **Status:** In development; no public release as of June 2026
- **Reported specs (unconfirmed):** ~60B parameters, native 4K output, 30-second continuous generation in a single pass
- **Open weights expected** per Alibaba's public roadmap pattern
- Source: Wavespeed AI reporting (May 2026); timeline unconfirmed — treat as Q3 risk

## Capabilities

- Text-to-video, image-to-video, text+image-to-video (TI2V)
- Speech-to-video (S2V variant)
- Video editing and creation (VACE variant)
- Advanced camera trajectory controls (pans, zooms, focus pulls)
- Subject locking and background stabilization
- LoRA fine-tuning support
- Motion intensity control

## Strengths

- **Highest motion realism** among open-source models as of March 2026
- **MoE architecture** distributes denoising across specialized experts, scaling efficiently
- **Lowest entry barrier** -- 1.3B model runs on approximately 8 GB VRAM
- **Native 1080p** without upscaling (Wan 2.2)
- **Apache 2.0 license** permits unrestricted commercial use
- **Drop-in weight swap** from Wan 2.1 to 2.2 with no infrastructure changes

## Weaknesses

- **Slower generation** -- 10-14x slower than [[ltx-2.3-model|LTX-2.3]] on equivalent hardware (12–18 min vs. 1–2 min real-world)
- **High VRAM for best quality** -- 14B model needs 20+ GB VRAM for longer clips; 60-80 GB for full precision
- **No native audio** — Wan 2.2 and earlier; Wan 2.7 adds native audio
- **Shorter clip duration** — earlier versions limited to ~5 seconds; 2.7 supports up to 15 seconds
- **Open weights available** — Wan 2.7 cloud launched April 3, 2026; open weights confirmed available under Apache 2.0 as of May 2026

## Comparison to LTX

In the [[open-source-video-generation-landscape]], Wan 2.2 leads in motion realism and cinematic quality for detailed, longer-form work. However, [[ltx-2.3-model|LTX-2.3]] is dramatically faster (10–14x in community benchmarks, ~18x per LTX-2 paper on H100), generates native 4K with synchronized audio, and offers a broader product ecosystem (desktop app, studio, MCP integration). Community consensus splits along use case lines: LTX for speed/social/iteration; Wan for cinematic/high-detail longer-form work.

Wan 2.7 (2026) narrows the gap with native audio, up to 15-second clips, and MoE efficiency improvements, but open weights are delayed. LTX-2.3 still holds the #1 open-weight model position on the Artificial Analysis leaderboard (Elo 1121) as of March 2026, ahead of Wan 2.2.

For a detailed community benchmark comparison, see [[ltx-model-comparisons]].

## See Also

- [[open-source-video-generation-landscape]]
- [[hunyuan-video]]
- [[video-generation-architectures]]
