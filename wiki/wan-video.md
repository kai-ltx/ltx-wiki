---
title: Wan Video
type: concept
created: 2026-04-13
updated: 2026-06-15
sources:
  - raw/competitor-model-wan-video.md
  - raw/open-source-comparison.md
  - raw/related-work-and-comparisons.md
  - raw/competitor-wan-2-7-release-april-2026.md
  - raw/competitor-ai-video-landscape-june-2026.md
  - raw/competitor-wan-30-confirmed-release.md
tags:
  - competitor
  - alibaba
  - video-generation
  - open-source
  - moe
---

# Wan Video

Wan Video is Alibaba's open-source video generation model family, developed by the Tongyi Lab. It is widely regarded as one of the top open-source video generation models as of mid-2026, particularly praised for its motion realism. The series has evolved rapidly through Wan 2.1, Wan 2.1-VACE, Wan 2.2, Wan 2.7, and Wan 3.0.

## Key Facts

- **Developer:** Alibaba (Tongyi Lab)
- **Parameters:** 1.3B (lightweight), 5B (mid), 14B (full) — earlier versions; Wan 2.7: 27B MoE (14B active); Wan 3.0: 60B MoE (~14B active)
- **Architecture:** Mixture of Experts (MoE) diffusion backbone
- **License:** Apache 2.0

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

### Wan 2.7 (Cloud launch April 3, 2026; open weights available Apache 2.0 as of May 2026)
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

### Wan 3.0 (Released mid-2026; open weights Apache 2.0)
- **Status:** Confirmed released. Previously listed as "roadmap" — now confirmed with detailed specs and web coverage.
- **Architecture:** MoE diffusion transformer — ~60B total parameters, ~14B active per inference pass
- **Resolution:** Native **4K from first frame** (not upscaled; vs. 1080p max for Wan 2.7)
- **Duration:** Up to **30 seconds** per single pass (vs. 15s for Wan 2.7)
- **Multi-shot storyboarding:** Automated 2–5 minute narrative generation from a single prompt
- **Inference speed:** ~40% faster than Wan 2.6 via attention optimization
- **LoRA fine-tuning** support
- **License:** Apache 2.0 — freely downloadable, commercial use permitted

#### Wan 3.0 vs. Wan 2.7 Comparison

| Feature | Wan 2.7 | Wan 3.0 |
|---------|---------|---------|
| Parameters | 27B MoE (14B active) | 60B MoE (~14B active) |
| Max resolution | 1080p | Native 4K |
| Max duration | 15 seconds | 30 seconds |
| Multi-shot narrative | No | Yes (2–5 min) |
| Native audio | Yes | Yes |
| Open weights | Apache 2.0 | Apache 2.0 |
| Inference speed | Baseline | ~40% faster |

## Capabilities

- Text-to-video, image-to-video, text+image-to-video (TI2V)
- Speech-to-video (S2V variant)
- Video editing and creation (VACE variant)
- Advanced camera trajectory controls (pans, zooms, focus pulls)
- Subject locking and background stabilization
- LoRA fine-tuning support
- Motion intensity control

## Strengths

- **Highest motion realism** among open-source models
- **MoE architecture** distributes denoising across specialized experts, scaling efficiently
- **Apache 2.0 license** permits unrestricted commercial use
- **Wan 3.0:** native 4K, 30s, multi-shot narration — closes gap with proprietary models
- **Lowest entry barrier** -- 1.3B model runs on approximately 8 GB VRAM

## Weaknesses

- **Slower generation** than [[ltx-2.3-model|LTX-2.3]] (10–14x in community benchmarks on earlier versions)
- **High VRAM for best quality** -- 14B+ models need 20+ GB VRAM for longer clips
- **No product ecosystem** — model only, no studio or desktop app (unlike LTX which has [[ltx-studio]] and [[ltx-desktop]])

## Comparison to LTX

In the [[open-source-video-generation-landscape]], Wan leads in motion realism for cinematic, longer-form work. LTX-2.3 is dramatically faster and offers a broader product ecosystem (desktop app, studio, API, MCP integration). With Wan 3.0 reaching native 4K and 30s generation (vs. LTX-2.3's 20s cap), Wan has closed the duration gap. LTX-2.3 still leads on generation speed and product breadth.

Community consensus: LTX for speed/social/iteration; Wan for cinematic/high-detail longer-form work.

For a detailed community benchmark comparison, see [[ltx-model-comparisons]].

## See Also

- [[open-source-video-generation-landscape]]
- [[hunyuan-video]]
- [[video-generation-architectures]]
