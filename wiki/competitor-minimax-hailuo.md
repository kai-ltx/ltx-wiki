---
title: MiniMax H3 / Hailuo 3.0
type: competitor
created: 2026-08-24
updated: 2026-08-24
sources:
  - raw/competitor-minimax-h3-omni-modal-video-model-july-2026.md
  - raw/competitor-wan3-public-beta-and-video-arena-elo-august-2026.md
tags:
  - competitor
  - video-generation
  - minimax
  - hailuo
  - open-weights
  - omni-modal
---
# MiniMax H3 / Hailuo 3.0

MiniMax H3 (consumer branding: **Hailuo 3.0**) is MiniMax's omni-modal video generation model, launched **2026-07-31** via the platform API (model ID `MiniMax-H3`) and the Hailuo AI consumer app (hailuoai.video). Open weights followed on **2026-08-03** as `MiniMaxAI/MiniMax-H3` on Hugging Face — a **33B-parameter** omni-modal model. It is, as of 2026-08-24, the **top open-weights video model in every Artificial Analysis category**, displacing LTX.

## Key Facts

- **Developer:** MiniMax (China)
- **Teased:** 2026-07-30 · **Launched:** 2026-07-31 · **Open weights published:** 2026-08-03
- **Parameters:** 33B (open-weights release)
- **Output:** 2K (2560x1440), 4-15 seconds (integer durations only), native stereo audio
- **License carve-out:** the reported license **excludes local deployment in the US, EU, UK and South Korea** — a significant restriction for Western self-hosters

## Positioning

MiniMax frames H3 not as a text-to-video model with add-ons but as a **general-purpose multimodal generation model** that reads text, images, video and audio as one unified context and returns video with native stereo sound. It collapses what were previously separate expert models (T2V, I2V, first/last frame, subject reference, motion reference, video editing) into a single pretraining paradigm where reference and editing relationships are expressed in natural language.

Example prompt published by MiniMax: *"reference the camera movement from Video 1, have the character in Image 2 sing, match the vocals to Audio 3."*

**Positioned industries:** advertising, branding, e-commerce, product design, UI/UX, gaming, film pre-visualization, retail catalog media.

## Architecture — Four Technical Components

1. **Contextual Omni Representation** — captioning rebuilt to describe the *relationship* between context and target video. ~100K tokens of source material distilled to ~4K tokens on average.
2. **H3-VAE** — full tokenizer overhaul; high compression ratio delivers a stated **4x gain in effective sequence length**, the enabling technology for native 2K.
3. **H3-Omni Transformer** — explicitly abandons the Hailuo-02 architecture; separates understanding and generation workloads. Reported **end-to-end training throughput up nearly 30%**.
4. **In-Context Regeneration** — replaces bolt-on super-resolution; the base model regenerates its own low-res output in-context, re-reading the original multimodal context. Recovers small text and fine detail (relevant to brand/product rendering).

## API and Input Limits

Single endpoint, async three-step flow (create task, poll `task_id`, download `content.url`). Three entry modes: text-to-video, first/last-frame image-to-video, and reference generation.

| Constraint | Limit |
|---|---|
| Reference images | up to 9 |
| Reference videos | up to 3 (2-15s each, <=15s total) |
| Reference audio clips | up to 3 (audio cannot be sent without an accompanying image or video) |
| Mixed input cap | 12 files total |
| Prompt length | <=7,000 chars |
| Request body | <=64 MB |
| Per-asset size | video <=50 MB, image <=30 MB, audio <=15 MB |
| Formats | H.264/H.265, JPG/PNG/WEBP/HEIC/HEIF, WAV/MP3 |

## Pricing

MiniMax claims that at 2K, H3's per-second price is **less than a third** of mainstream models; at 768p, **less than half** the price of mainstream 720p.

- Third-party trackers report **$0.13 per second** pay-as-you-go at 2K (~$1.95 for a 15s clip). Treat as reported, not primary — MiniMax's own pay-as-you-go page still listed only Hailuo 2.3 tiers at the time.
- Artificial Analysis lists H3 API pricing at **$7.80/min** for 1 minute of 1080p at default settings — the same headline rate as [[ltx-2.5-model|LTX-2.5 Fast]].

## Benchmark Standing (Artificial Analysis, 2026-08-24)

| Category | Rank | Elo | Notes |
|---|---|---|---|
| Text-to-video **with audio** | #3 | **1,228** (-8/+8, 8,316 samples) | behind Wan 3.0 (1,244) and Gemini Omni Flash (1,238) |
| Text-to-video **without audio** | #2 | **1,303** | behind Gemini Omni Flash (1,322) |
| Image-to-video **with audio** | #2 | **1,184** | behind Dreamina Seedance 2.0 720p (1,191), ahead of Gemini Omni Flash (1,182) |
| Image-to-video **without audio** | #2 | **1,346** | behind Gemini Omni Flash (1,366) |
| Video editing | #1 | — | AA lists H3 as leading video editing |

**Now the top open-weights video model in every AA category**, displacing LTX:
- Best open-weights T2V with audio: 1,228 vs LTX-2.5 Pro/Fast at 1,063
- Best open-weights T2V without audio: 1,303 vs LTX-2.5 Fast 1,211
- Best open-weights I2V with audio: 1,184 vs [[competitor-magi-sandai|MAGI-2 Preview]] 1,100 and LTX-2.5 Fast 1,043

## Strengths

- Single unified omni-modal model replacing a fleet of task-specific experts
- Native 2K (2560x1440) with stereo audio in one pass
- Top open-weights model on all four AA video leaderboards; #1 in video editing
- Aggressive pricing claims (2K at under a third of mainstream per-second cost)
- Rich reference conditioning: 9 images + 3 videos + 3 audio clips in one request

## Weaknesses

- **License excludes local deployment in the US, EU, UK and South Korea** — the open weights are not usable by most Western self-hosters
- Duration capped at 15 seconds, integer values only
- Cloud service is China-based; the same data-sovereignty and [[competitor-landscape-overview|EU AI Act Article 50]] questions that apply to [[competitor-kling|Kling]] apply here
- Open-weights claim is undercut in practice by the geographic carve-out — "open weights" as a badge, not as a deployable right in LTX's core markets

## Comparison to LTX

H3 opens a **~165 Elo gap over LTX-2.5 Pro/Fast on open-weights T2V-with-audio** (1,228 vs 1,063) and **~140 Elo on open-weights I2V-with-audio** (1,184 vs 1,043). On raw quality, LTX no longer leads the open-weights field.

The structural opening is the license. Because H3's regional exclusion covers the US, EU, UK and South Korea, **LTX-2.5 remains the strongest genuinely deployable open-weights option in those markets** — and [[competitor-runway|Runway's Media Router]] geopolitical-preference feature (American-provider routing) points at the same demand: enterprises that will not or cannot run Chinese models. LTX's remaining differentiators are consumer-hardware deployability, unrestricted commercial licensing, and the [[ltx-studio]] / [[ltx-desktop]] / ComfyUI ecosystem — not raw Elo.

See [[open-source-video-generation-landscape]] for the full open-weights ranking.

## See Also
- [[competitor-landscape-overview]]
- [[competitor-magi-sandai]] — the other August 2026 open-weights entrant
- [[open-source-video-generation-landscape]]
- [[ltx-2.5-model]]
- [[wan-video]]
