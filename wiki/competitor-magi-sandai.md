---
title: MAGI-2 Preview (Sand.ai)
type: competitor
created: 2026-08-24
updated: 2026-08-24
sources:
  - raw/competitor-sandai-magi2-preview-114b-open-weights-august-2026.md
  - raw/competitor-wan3-public-beta-and-video-arena-elo-august-2026.md
tags:
  - competitor
  - video-generation
  - sand-ai
  - magi
  - open-weights
  - mixture-of-experts
---
# MAGI-2 Preview (Sand.ai)

**MAGI-2 Preview** is Sand.ai's open-source **114B-parameter mixture-of-experts** audio-video model, released **2026-08-05** under a reported **Apache 2.0** license. It generates **10-second videos with synchronized audio** from a text prompt (T2V) or prompt plus still image (I2V). Weights, inference code and the technical report ("MAGI-2 Preview: Scaling Video Generation Models Efficiently") are all public.

It follows MAGI-1, Sand.ai's autoregressive video model from April 2025. Where MAGI-1 studied *how* video should be generated, MAGI-2 asks *how a video generation model should scale* — the preview exists to validate that its architecture, training system and data pipeline scale together at the 100B level.

## Key Facts

- **Developer:** Sand.ai
- **Released:** 2026-08-05
- **Parameters:** 114B total, **~6B activated per token**
- **License:** Apache 2.0 (reported)
- **Output:** 1088x1920 (1080p), fixed 10 seconds, synchronized audio
- **Hardware floor:** 8 NVIDIA Hopper GPUs
- **Distribution:** [huggingface.co/sand-ai/MAGI-2-preview](https://huggingface.co/sand-ai/MAGI-2-preview), [github.com/SandAI-org/MAGI-2-preview](https://github.com/SandAI-org/MAGI-2-preview)

## Architecture (MagiMoE)

- **114B total parameters, ~6B activated per token** — 72 of 3,072 head-local expert units per sparse layer.
- Backbone: **40 Transformer layers** (36 sparse, 4 dense boundary layers). Model width 3,072.
- Routed representation: **12 latent heads x 256 dimensions**; each head has its own router and selects **top-6 of 256 narrow experts**.
- Expert FFN: 256 -> 1,280 -> 256, fused SwiGLU.
- **Single-stream design** — text, video and audio tokens are concatenated into one unified sequence processed by the same Transformer backbone, so modalities interact throughout the model rather than only at cross-attention interfaces. Visuals and sound are generated in one pass; audio is then muxed into the output file.
- **Head Parallel** for regular cross-device communication (statically known shapes, preallocated buffers). Head-activation exchange is mapped onto InfiniBand across nodes; expert-state resharding onto NVLink within nodes. Companion projects: MagiCompiler, MagiAttention.
- Data pipeline shifted from filtering-centric curation to high-throughput data production with precise multimodal annotation.
- Sand.ai claims **1/10 the generation cost of mainstream models**.

## Generation Pipeline

Two-stage:
1. **Preview stage** at 512x896
2. **Refiner stage** upscaling to 1088x1920 (1080p)

**10 seconds with synchronized audio is the only supported duration.** Prompting expects long structured captions; the repo ships system prompts for LLM-based prompt enhancement.

## Deployment Cost

Inference runs through the official Python pipeline (`torchrun`, Docker image provided) and **requires 8 NVIDIA Hopper GPUs**. No ComfyUI custom nodes at time of writing.

The complete checkpoint set is **~307 GB** on Hugging Face:

| Component | Size |
|---|---|
| Preview-stage transformer | 228 GB |
| Refiner | 14 GB |
| Qwen3.5-27B text encoder | 56 GB |
| Wan2.2 video VAE | — |
| Stable Audio Open 1.0 audio VAE | — |
| Distilled turbo VAE decoder (used by default) | — |

## Benchmark Standing (Artificial Analysis, 2026-08-24)

Listed as **MAGI-2 Preview, released Aug 2026, API pricing "Coming soon."**

- **Image-to-video with audio: #6, Elo 1,100** (95% CI -7/+7, 11,406 samples)
- **#2 open-weights I2V-with-audio model**, behind [[competitor-minimax-hailuo|MiniMax H3]] (1,184) and **ahead of LTX-2.5 Fast (1,043) and LTX-2.5 Pro (1,016)**
- Flagged by AA as "added to the leaderboard in the last month"
- **Not present in the text-to-video top-31** at time of retrieval

## Strengths

- Genuine Apache 2.0 open weights with no geographic carve-out — unlike [[competitor-minimax-hailuo|MiniMax H3]]
- Beats LTX-2.5 on I2V-with-audio Elo by ~57-84 points
- Unified single-stream audio-video generation in one pass
- Full public release: weights, inference code, technical report, compiler and attention libraries

## Weaknesses

- **8x Hopper GPUs required** — no consumer-hardware path at all
- **~307 GB** of checkpoints to fetch before a single generation
- **Single fixed 10-second duration**, no other options
- No ComfyUI support at release
- No T2V leaderboard presence yet; no published API pricing
- "Preview" status — this is a scaling validation release, not a productized model

## Comparison to LTX

MAGI-2 is the second Apache-2.0-class open-weights entrant to land within days of [[competitor-minimax-hailuo|MiniMax H3]], and it beats [[ltx-2.5-model|LTX-2.5]] on I2V-with-audio Elo — but at a **radically worse accessibility profile**: 8x Hopper GPUs, 307 GB of checkpoints, a single fixed 10-second duration, and no ComfyUI integration.

The contrast is the clearest statement of LTX's current position in the open-weights field: **LTX's advantage is consumer-hardware deployability and workflow ecosystem, not raw Elo.** A model that requires an 8-GPU Hopper node is open-weights in license only for the overwhelming majority of the community that runs [[ltx-2.5-local-inference|LTX locally]] on a single consumer card.

See [[open-source-video-generation-landscape]] for the full open-weights comparison.

## See Also
- [[competitor-minimax-hailuo]] — the other August 2026 open-weights entrant
- [[open-source-video-generation-landscape]]
- [[competitor-landscape-overview]]
- [[ltx-2.5-model]]
- [[wan-video]]
