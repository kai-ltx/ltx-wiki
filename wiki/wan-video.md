---
title: Wan Video
type: concept
created: 2026-04-13
updated: 2026-08-24
sources:
  - raw/competitor-model-wan-video.md
  - raw/open-source-comparison.md
  - raw/related-work-and-comparisons.md
  - raw/competitor-wan-2-7-release-april-2026.md
  - raw/competitor-ai-video-landscape-june-2026.md
  - raw/competitor-wan-30-confirmed-release.md
  - raw/competitor-wan3-public-beta-and-video-arena-elo-august-2026.md
tags:
  - competitor
  - alibaba
  - video-generation
  - open-source
  - moe
---

# Wan Video

Wan Video is Alibaba's video generation model family, developed by the Tongyi Lab. Through Wan 2.2 it was an open-weights family and is widely regarded as one of the top open-source video generation models as of mid-2026, particularly praised for its motion realism. **From Wan 2.7 onward the openness picture is mixed, and Wan 3.0 appears to be closed** — see [Correction (2026-08-24)](#correction-2026-08-24) below.

## Key Facts

- **Developer:** Alibaba (Tongyi Lab)
- **Parameters:** 1.3B (lightweight), 5B (mid), 14B (full) — earlier versions; Wan 2.7: 27B MoE (14B active). **No verified parameter count exists for Wan 3.0.**
- **Architecture:** Mixture of Experts (MoE) diffusion backbone
- **License:** Apache 2.0 for the openly released checkpoints. **Alibaba's openly released Wan weights stop at Wan 2.2.**

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
- **Last Wan release with confirmed openly published weights from Alibaba.**

### Wan 2.2-S2V (August 2025)
- Speech-to-Video model for digital human creation
- Converts portrait photos into film-quality avatars capable of speaking, singing, and performing

### Wan 2.6 (December 2025)
- Open-source image model (text-to-image focus)

### Wan 2.7 (Cloud launch April 3, 2026)
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
- API pricing: **$6.00/min** (33% cheaper than prior Wan versions) via providers including fal.ai and Replicate
- **Openness caveat:** this page previously stated "open weights available Apache 2.0 as of May 2026." Given that in-window reporting says Alibaba's open Wan weights stop at 2.2, that claim should also be re-verified against a primary Alibaba/Hugging Face source.

### Wan 3.0 — Closed Public Beta and Paid API (public beta 2026-08-06)

**Wan 3.0 is a closed public beta and paid API from Alibaba Tongyi Lab. It is not, on current evidence, an open-weights release.** There is no downloadable Wan 3.0 checkpoint, no Hugging Face repository, no GitHub repository and no ComfyUI node.

- **Public beta opened 2026-08-06** (evening, China time).
- Headline capability: **up to 30 seconds in a single continuous shot** ("一镜到底"), enabling uninterrupted camera language (push, pull, pan, track) without stitching clips.
- **Document-to-video** — first in the Wan line to accept **doc, xls, ppt, pdf, md** files (plus web pages) as creative reference. Turns a slide deck or PDF report directly into video.
- **Consistency:** character, prop and scene held stable via "multi-dimensional feature alignment."
- **Extras:** smart duration recommendation, video extension.
- **Inputs:** text / image / audio / video / document.
- **API pricing: ¥0.3 / ¥0.6 / ¥1.2 per second at 480P / 720P / 1080P** (~$0.04 / $0.08 / $0.17 per second). A 30-second 1080P clip runs ~¥36 (~$5).
- **Access channels are China-region Alibaba products:** Alibaba Cloud Model Studio (百炼), tongyi.aliyun.com/wan, 千问创作 / create.qianwen.com, 万镜一刻, IF STUDIO, 堆友, and a grayscale rollout inside the Qwen app.
- **Audio:** Pexo's comparison table states Wan 3.0 produces **visual only — no generated soundtrack**. This conflicts with Artificial Analysis listing Wan 3.0 in the *text-to-video with audio* leaderboard; treat as unresolved.
- **Benchmark:** Wan 3.0 took **#1 in AA text-to-video-with-audio at Elo 1,244** (-10/+10, 5,679 samples, Aug 2026), displacing Gemini Omni Flash (1,238) — a 6-point margin against a ±10 CI, so effectively a statistical tie. AA lists API pricing as "Coming soon" and shows **no Hugging Face open-weights badge**.

#### Correction (2026-08-24)

**What this wiki previously claimed:** that Wan 3.0 was a released open-weights model — "~60B total parameters, ~14B active per inference pass," native 4K from the first frame, ~40% faster inference than Wan 2.6, automated 2-5 minute multi-shot narrative, and "Apache 2.0 — freely downloadable, commercial use permitted."

**What the new evidence says:** Pexo's 2026-08-07 writeup, sourced to Chinese tech press (IT之家, 第一财经, ITBear) dated 2026-08-06, describes Wan 3.0 as a **closed public beta and paid API** with no downloadable weights, no Hugging Face checkpoint, no GitHub repo and no ComfyUI node, and states that **Alibaba's openly released Wan weights stop at Wan 2.2**. It explicitly says claims of open weights, a specific open-source license, or a parameter count for Wan 3.0 "come from unofficial lookalike sites and are unverified." Corroborating signal: the Artificial Analysis leaderboard lists Wan 3.0 (Aug 2026) with API pricing "Coming soon" and **no open-weights badge**, unlike [[competitor-minimax-hailuo|MiniMax H3]], [[competitor-magi-sandai|MAGI-2 Preview]] and every LTX entry, all of which do carry it.

**Status:** the "60B MoE / Apache 2.0 / native 4K / 40% faster" figures have been removed from the Wan 3.0 section above as unverified. **Primary confirmation from Alibaba is still outstanding** — no Alibaba statement, model card or license text has been located either confirming or denying an open Wan 3.0 release. If Alibaba does publish 3.0 weights, this section should be revised again against that primary source.

## Capabilities

- Text-to-video, image-to-video, text+image-to-video (TI2V)
- Speech-to-video (S2V variant)
- Video editing and creation (VACE variant)
- Advanced camera trajectory controls (pans, zooms, focus pulls)
- Subject locking and background stabilization
- LoRA fine-tuning support (open checkpoints)
- Motion intensity control
- Document-to-video (Wan 3.0 beta only)

## Strengths

- **Highest motion realism** among open-source models (through Wan 2.2)
- **MoE architecture** distributes denoising across specialized experts, scaling efficiently
- **Apache 2.0 license** on the openly released checkpoints permits unrestricted commercial use
- **Wan 3.0:** 30s single continuous shot and document-to-video are genuinely novel capabilities
- **Lowest entry barrier** — 1.3B model runs on approximately 8 GB VRAM
- **#1 on AA T2V-with-audio** (Wan 3.0, Elo 1,244)

## Weaknesses

- **Wan 3.0 is not self-hostable** — closed beta, paid API, China-region access channels only
- **Open lineage has stalled at 2.2**, so the frontier Wan model is no longer an open-weights competitor
- **Slower generation** than LTX (10-14x in community benchmarks on earlier versions)
- **High VRAM for best quality** — 14B+ models need 20+ GB VRAM for longer clips
- **No product ecosystem** — model only, no studio or desktop app (unlike LTX which has [[ltx-studio]] and [[ltx-desktop]])

## Comparison to LTX

In the [[open-source-video-generation-landscape]], Wan through 2.2 leads in motion realism for cinematic, longer-form work, and LTX is dramatically faster with a far broader product ecosystem (desktop app, studio, API, MCP integration).

The 2026-08 correction changes the strategic read materially: **Wan 3.0 is not an open-weights competitor to [[ltx-2.5-model|LTX-2.5]]**. It is a closed Chinese-market API that happens to top the AA text-to-video-with-audio leaderboard. The open-weights competition LTX actually faces in August 2026 comes from [[competitor-minimax-hailuo|MiniMax H3]] and [[competitor-magi-sandai|MAGI-2 Preview]], not from Alibaba's frontier model.

Community consensus (open checkpoints): LTX for speed/social/iteration; Wan for cinematic/high-detail longer-form work.

For a detailed community benchmark comparison, see [[ltx-model-comparisons]].

## See Also

- [[open-source-video-generation-landscape]]
- [[competitor-minimax-hailuo]]
- [[competitor-magi-sandai]]
- [[hunyuan-video]]
- [[video-generation-architectures]]
