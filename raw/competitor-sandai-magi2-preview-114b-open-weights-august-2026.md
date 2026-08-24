# Sand.ai MAGI-2 Preview: 114B MoE Open-Weights Audio-Video Model (Aug 5, 2026)

**Source:** https://comfyui-wiki.com/en/news/2026-08-05-magi-2-preview
**Date:** 2026-08-05
**Retrieved:** 2026-08-24

## Content

Additional sources: https://sand.ai/blog/magi-2-preview (technical report, "MAGI-2 Preview: Scaling Video Generation Models Efficiently"), https://huggingface.co/sand-ai/MAGI-2-preview, https://github.com/SandAI-org/MAGI-2-preview

**Release.** Sand.ai released **MAGI-2 Preview on 2026-08-05** — an open-source **114B-parameter mixture-of-experts** model that generates **10-second videos with synchronized audio** from a text prompt (T2V) or prompt + still image (I2V). Weights, inference code and technical report are all public. Reported license: **Apache 2.0**. Follows MAGI-1 (Sand.ai's autoregressive video model, April 2025); where MAGI-1 studied *how* video should be generated, MAGI-2 asks *how a video generation model should scale*, and the preview validates that its architecture, training system and data pipeline scale together at the 100B level.

**Architecture (MagiMoE)**
- **114B total parameters, ~6B activated per token** (72 of 3,072 head-local expert units per sparse layer).
- Backbone: **40 Transformer layers** (36 sparse, 4 dense boundary layers). Model width 3,072.
- Routed representation: **12 latent heads x 256 dimensions**; each head has its own router and selects **top-6 of 256 narrow experts**.
- Expert FFN: 256 -> 1,280 -> 256, fused SwiGLU.
- Single-stream design: text, video and audio tokens concatenated into one unified sequence processed by the same Transformer backbone — modalities interact throughout the model rather than only at cross-attention interfaces. Visuals and sound generated in one pass, audio then muxed into the output file.
- **Head Parallel** for regular cross-device communication (statically known shapes, preallocated buffers); head-activation exchange mapped onto InfiniBand across nodes, expert-state resharding onto NVLink within nodes. Companion projects: MagiCompiler, MagiAttention.
- Data pipeline shifted from filtering-centric curation to high-throughput data production with precise multimodal annotation.
- Sand.ai claims **1/10 the generation cost of mainstream models**.

**Output / generation**
- Two-stage: **preview stage at 512x896**, **refiner stage upscaling to 1088x1920** (1080p).
- **10-second video with synchronized audio is the only supported duration.**
- Prompting: long structured captions; repo ships system prompts for LLM-based prompt enhancement.

**Deployment cost.** Inference runs through the official Python pipeline (`torchrun`, Docker image provided) and **requires 8 NVIDIA Hopper GPUs**. No ComfyUI custom nodes at time of writing. Complete checkpoint set is **~307 GB** on Hugging Face: 228 GB preview-stage transformer, 14 GB refiner, Qwen3.5-27B text encoder (56 GB), Wan2.2 video VAE, Stable Audio Open 1.0 audio VAE, and a distilled turbo VAE decoder used by default.

**Benchmark standing (Artificial Analysis, as of 2026-08-24).** Listed as **MAGI-2 Preview, released Aug 2026, API pricing "Coming soon."** Image-to-video **with audio**: **#6, Elo 1,100** (95% CI -7/+7, 11,406 samples). Ranked **#2 open-weights I2V-with-audio model** behind MiniMax H3 (1,184) and **ahead of LTX-2.5 Fast (1,043) and LTX-2.5 Pro (1,016)**. Flagged by AA as "added to the leaderboard in the last month." Not present in the text-to-video top-31 at time of retrieval.

**Competitive read for LTX:** a second Apache-2.0-class open-weights entrant landing within days of MiniMax H3, beating LTX-2.5 on I2V-with-audio Elo by ~57-84 points — but at a radically worse accessibility profile (8x Hopper GPUs, 307 GB checkpoints, single fixed 10s duration, no ComfyUI support). LTX's advantage is consumer-hardware deployability and workflow ecosystem, not raw Elo.
