---
title: Open-Source Video Generation Landscape
type: analysis
created: 2026-04-13
updated: 2026-08-24
sources:
  - raw/open-source-comparison.md
  - raw/related-work-and-comparisons.md
  - raw/competitor-model-other-notable.md
  - raw/competitor-model-wan-video.md
  - raw/competitor-model-hunyuan-video.md
  - raw/competitor-model-cogvideo.md
  - raw/competitor-model-mochi.md
  - raw/competitor-model-open-sora.md
  - raw/competitor-model-animatediff.md
  - raw/competitor-minimax-h3-omni-modal-video-model-july-2026.md
  - raw/competitor-sandai-magi2-preview-114b-open-weights-august-2026.md
  - raw/competitor-wan3-public-beta-and-video-arena-elo-august-2026.md
tags:
  - comparison
  - video-generation
  - open-source
  - landscape
  - ltx-video
---

# Open-Source Video Generation Landscape

A comprehensive comparison of the major open-source video generation models. The market is described as having its "Stable Diffusion moment," with open-source models rapidly closing the gap with proprietary ones. **The August 2026 section below supersedes the early-2026 comparison that follows it** — the open-weights field changed decisively in a single week.

## August 2026: the open-weights field reshuffles

Two large open-weights audio-video models landed within days of each other, and both beat [[ltx-2.5-model|LTX-2.5]] on Artificial Analysis Elo. A third headline model — Wan 3.0 — turned out **not** to be open weights at all.

### The two new entrants

| Model | Released | Params | Output | License | Hardware floor |
|---|---|---|---|---|---|
| [[competitor-minimax-hailuo\|MiniMax H3]] | weights 2026-08-03 | **33B** omni-modal | 2K (2560x1440), 4-15s, native stereo audio | Open weights, but **excludes local deployment in the US, EU, UK and South Korea** | not published |
| [[competitor-magi-sandai\|MAGI-2 Preview]] (Sand.ai) | 2026-08-05 | **114B MoE**, ~6B active/token | 1088x1920, fixed 10s + synced audio | **Apache 2.0** | **8x NVIDIA Hopper GPUs, ~307 GB checkpoints** |

### The Wan 3.0 correction

[[wan-video|Wan 3.0]] tops AA text-to-video-with-audio at Elo 1,244, and this wiki previously described it as a 60B-MoE Apache-2.0 open-weights model. **That was wrong.** In-window Chinese tech press reporting (2026-08-06/07) describes Wan 3.0 as a **closed public beta and paid API** with no downloadable checkpoint, no Hugging Face repo, no GitHub repo and no ComfyUI node; **Alibaba's openly released Wan weights stop at Wan 2.2**. AA corroborates: Wan 3.0 carries no open-weights badge and lists pricing as "Coming soon." Primary confirmation from Alibaba is still outstanding. Full detail on [[wan-video]].

**Practical consequence:** the frontier of *open* video generation is now MiniMax H3 and MAGI-2, not Alibaba.

### Open-weights Elo standings (Artificial Analysis, 2026-08-24)

| Category | #1 open weights | #2 open weights | #3 open weights |
|---|---|---|---|
| T2V with audio | MiniMax H3 **1,228** | LTX-2.5 Pro **1,063** | LTX-2.5 Fast **1,063** |
| T2V without audio | MiniMax H3 **1,303** | LTX-2.5 Fast **1,211** | LTX-2.5 Pro **1,205** |
| I2V with audio | MiniMax H3 **1,184** | MAGI-2 Preview **1,100** | LTX-2.5 Fast **1,043** (Pro 1,016) |
| I2V without audio | MiniMax H3 **1,346** | NVIDIA Cosmos3-Super-Image2Video-4Step **1,263** | Cosmos3-Super-Image2Video **1,244** |

MiniMax H3 is now the top open-weights model in **every** AA video category, displacing LTX. The gaps are large: **~165 Elo on T2V-with-audio** and **~140 Elo on I2V-with-audio** against LTX-2.5.

### Reassessing where LTX-2.5 sits

LTX-2.5 is **third among open-weights families on raw Elo** — but the ranking inverts on deployability, which is the axis most of the open-weights community actually optimizes for:

| Criterion | MiniMax H3 | MAGI-2 Preview | LTX-2.5 |
|---|---|---|---|
| Usable in US / EU / UK / KR | **No** (license carve-out) | Yes | **Yes** |
| Runs on a single consumer GPU | not demonstrated | **No** (8x Hopper) | **Yes** ([[ltx-2.5-local-inference]]) |
| Checkpoint size | 33B-class | **~307 GB** | consumer-scale, quantized variants |
| ComfyUI support | no | **no** | **yes** ([[ltx-2.5-comfyui-integration]]) |
| Duration flexibility | 4-15s (integer only) | **10s fixed only** | flexible |
| Ecosystem (studio, desktop, API, MCP, LoRA) | app + API | research repo | **full stack** |

**The honest read:** LTX no longer leads open-weights video generation on quality. It leads on *access* — unrestricted licensing in Western markets, consumer-hardware inference, workflow tooling and a LoRA/ComfyUI ecosystem none of the new entrants have. A 114B model needing an 8-GPU Hopper node is open-weights in license only for most of the people who download open video models. That is a real but narrower moat than "best open-source video model," and it is the position the wiki should now describe.

See also: [[competitor-landscape-overview]] for the full cross-market leaderboard, and [[ltx-2.5-model]] for the model itself.

## Model Comparison Table

| Model | Developer | Params | Max Res | FPS | Duration | Audio | VRAM (min) | License |
|-------|-----------|--------|---------|-----|----------|-------|------------|---------|
| [[ltx-2-overview\|LTX-2.3]] | [[lightricks-company\|Lightricks]] | 22B | Native 4K | 50 | 20s | Yes | ~8 GB | Apache 2.0* |
| [[wan-video\|Wan 2.2]] | Alibaba | 1.3B-14B | 1080p | 24 | 5s | No | ~8 GB | Apache 2.0 |
| [[hunyuan-video\|HunyuanVideo 1.5]] | Tencent | 8.3B | 1080p** | 24 | 10s | No | ~14 GB | Community |
| [[cogvideo\|CogVideoX 1.5]] | Zhipu AI | 5B | 1360x768 | 16 | 10s | No | Quantizable | Apache 2.0 |
| [[mochi\|Mochi 1]] | Genmo | 10B | 480p | 30 | 5.4s | No | ~20 GB | Apache 2.0 |
| [[open-sora\|Open-Sora 2.0]] | HPC-AI Tech | 11B | 768px | 24 | 5s | No | 40 GB+ | MIT |
| [[animatediff\|AnimateDiff]] | Community | Varies | 576x1024 | 8-16 | 8s | No | ~13 GB | Apache 2.0 |
| [[stable-video-diffusion\|SVD]] | Stability AI | N/A | 576x1024 | ~14 | 4s | No | ~12 GB | Community |

\* Apache 2.0 with revenue cap for commercial use above $10M
\** 1080p via upscaling; native generation is 480p-720p

## Competitive Positioning

### Where Each Model Leads

- **[[wan-video|Wan 2.2]]** -- Motion realism. Best-in-class motion quality with lowest VRAM entry point (approximately 8 GB for 1.3B model)
- **[[hunyuan-video|HunyuanVideo 1.5]]** -- Multi-person scenes. Cinematic clarity in complex compositions on consumer GPUs
- **[[ltx-2-overview|LTX-2.3]]** -- Speed, audio, and production ecosystem. Native 4K, synchronized audio, faster-than-real-time generation
- **[[cogvideo|CogVideoX]]** -- Fine-tuning. Mature CogKit framework; quantizable to T4 GPUs
- **[[mochi|Mochi 1]]** -- Physics simulation. Strong fluid dynamics and cloth simulation (historically)
- **[[open-sora|Open-Sora 2.0]]** -- Research and cost efficiency. MIT license; $200K training cost
- **[[animatediff|AnimateDiff]]** -- SD 1.5 ecosystem. Works with existing checkpoints and LoRAs

### LTX Competitive Advantages

Based on community consensus and benchmark data:

1. **Speed** -- Best generation speed among open-source models; faster-than-real-time at 720p
2. **Audio-video synchronization** -- Unique among open-source models (LTX-2+)
3. **Native 4K resolution** -- First open-source model to achieve this
4. **Production ecosystem** -- Desktop app, Studio product, MCP integration, NVIDIA partnership
5. **Iteration speed** -- Rapid prototyping and customization through LoRA training

### LTX Competitive Gaps

1. **Motion realism** -- [[wan-video|Wan 2.2]] leads in motion quality
2. **Multi-person scenes** -- [[hunyuan-video|HunyuanVideo]] excels at complex compositions
3. **Detailed prompting required** -- Proprietary models have better out-of-box quality
4. **Anatomy adherence** -- May struggle compared to leading commercial options

## Versus Proprietary Models

| Proprietary Model | Max Duration | LTX-2 Position |
|-------------------|-------------|-----------------|
| Sora 2 (OpenAI) | 16s | Comparable in human preference; surpassed on Artificial Analysis |
| Veo 3 (Google) | 12s | Comparable in human preference; LTX-2 generates up to 20s |
| Runway Gen-4.5 | Varies | LTX-2 competitive; proprietary models have better physics simulation |

## Notable Community Projects

**Wan2GP** is a community project providing a unified interface for running multiple video generation models ([[wan-video|Wan 2.1/2.2]], [[hunyuan-video|HunyuanVideo]], [[ltx-video-overview|LTX Video]], and Flux) on consumer GPUs. Its inclusion of LTX Video as a first-class citizen demonstrates LTX's standing in the ecosystem.

## Other Notable Models

Additional models in the landscape include:

- **ModelScope / ZeroScope** -- Early open-source T2V models; historically important but obsolete
- **Pyramid Flow** -- Efficient pyramid-structured flow matching; limited adoption
- **Latte** -- Research model exploring transformer-based latent diffusion
- **Ovi** -- Two 5B streams fine-tuned from [[wan-video|Wan 2.2]]; LTX-2 significantly outperforms

## See Also

- [[competitor-minimax-hailuo]]
- [[competitor-magi-sandai]]
- [[wan-video]]
- [[competitor-landscape-overview]]
- [[ltx-2.5-model]]
- [[video-generation-architectures]]
- [[ltx-video-overview]]
- [[ltx-2-overview]]
