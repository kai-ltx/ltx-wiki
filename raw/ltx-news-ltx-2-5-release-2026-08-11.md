# LTX-2.5 Released: Open-Weights World Model with Native Multishot, Diffusion Fidelity Rendering, Day-One ComfyUI Support

**Source:** https://ltx.io/newsroom/introducing-ltx-2-5
**Date:** 2026-08-11
**Retrieved:** 2026-08-24

## Content

LTX (the open world model company spun out of Lightricks) released **LTX-2.5** on **August 11, 2026**. Positioned as "the most capable open weights world model on the market," it succeeds LTX-2.3 (March 2026). Framed as a **world model**, not just a video model — continuing the "open world models company" repositioning announced July 8, 2026.

### Architecture / specs
- **22B-parameter asymmetric dual-stream diffusion transformer**, joint video+audio generation via bidirectional cross-attention with modality-aware classifier-free guidance.
- **Text encoder: custom Gemma 4 12B** with a learned projection (replacing the LTX-2.3 text connector).
- Supports text-to-video, image-to-video, video-to-video, text-to-audio, audio-to-video.
- Runs on any GPU with **minimum 16GB VRAM**; deployable on-prem, at the edge, or via API; runs from data-center GPUs down to a Mac.

### What's new (per LTX release notes and press release)
- **Diffusion Fidelity Rendering (DFR)** — builds motion/structure in an **8x temporally compressed latent space** while generating high-fidelity keyframes to anchor detail; adapts keyframe count to scene complexity and compute budget instead of locking every scene to one compression rate.
- **New diffusion video decoder** (augmenting the earlier VAE decoder) — sharper faces, legible text/signage, fewer high-motion artifacts, while keeping LTX's high compression ratio.
- **Native multishot generation** — a single generation produces multiple connected shots (wide/medium/close-up) holding character, environment, lighting, voice, style and continuity across cuts, rather than stitching separate shots.
- **Auto duration** — model predicts clip length from the described action.
- **Dedicated prompt enhancer** — expands short prompts into richer cinematic/temporal instructions "at near-zero extra compute."
- **Native 4K HDR + native EXR workflow** — reads and writes cinema-grade EXR in **ACES** and **DaVinci Wide Gamut**, preserving dynamic range, metadata and color (HDR ACES in → HDR ACES out).
- **Pretrained (non-SFT) checkpoint** tuned for physical AI / robotics, for aggressive domain fine-tuning.
- **Larger filtered dataset + RL post-training** aligned to human preference.
- **Substantially better distilled model**; optimized with **NVIDIA** for local inference on **NVIDIA RTX GPUs and DGX Spark** with reduced VRAM.
- **Cleaner permissive licensing** — reduced restrictive third-party dependencies.

### Availability and licensing
- Open weights on Hugging Face (`Lightricks/LTX-2.5`, collection `Lightricks/ltx-25`), **native day-one ComfyUI support** (strategic launch partnership), and the LTX API for managed generation.
- **Free for organizations under $10M annual recurring revenue**; larger companies negotiate a license. Ships under the **LTX-2.x Community License** (not OSI open source — discriminates by revenue and field of use). Military/warfare/weapons uses banned outright. Derivatives (fine-tunes, LoRAs, distillations, models trained on LTX-2.5 outputs/synthetic data) must be redistributed under the same license; commercial users barred from training competing AI systems.
- LTX says its models have passed **33 million downloads**, making it the most-used open world model line.

### Launch partners
ComfyUI (day-one native integration), **Asteria** (AI film studio; Paul Trillo, co-founder & Executive Creative Director, quoted praising the ACES workflow), **Reactor** (real-time generative video developer platform; CEO Alberto Taiuti), **Markov Robotics** (CEO Atharva Gundawar), and **NVIDIA** (Gerardo Delgado Cabrera, Senior Director of Product for Local AI).

### Quotes
Zeev Farbman, co-founder & CEO, LTX: "World models face challenges that LLMs never had to solve, like holding motion, space, and sound consistent across time, which is why efficiency and control matter so much. By keeping LTX open, we let teams own their hardware, their IP, and their model."

Yoland Yan, co-founder & CEO, ComfyUI: "With LTX-2.5 running natively in ComfyUI, a developer can go from an idea to a working world-model pipeline in an afternoon, and an enterprise can take that same pipeline straight into production on its own hardware."

### Weights / variants on Hugging Face
- Base: `ltx-2.5-22b-dev-transformer-bf16.safetensors`
- Distilled: `ltx-2.5-22b-distilled-transformer-bf16.safetensors`
- ComfyUI-ready quantizations: int8 convrot and NVFP4 variants of the distilled transformer
- Text encoder: `gemma4-12b-with-proj-ltx-2.5` (BF16 and ComfyUI int8 convrot)
- Separate video VAE and audio VAE; 2x latent spatial and 2x latent temporal upscalers
- Add-ons: distilled LoRA (450) and a duration-head model patch
- Official ComfyUI templates for T2V, I2V, first/last-frame-to-video; `Lightricks/ComfyUI-LTXVideo` wrapper updated with 2.5 example workflows (single-stage and two-stage upscaled T2V/I2V, ICLoRA inpainting/outpainting, motion tracking, union control, text-to-audio).

**Additional sources:** https://ltx.io/release-notes ; https://comfyui-wiki.com/en/news/2026-08-11-ltx-2-5-open-weights-release ; https://ltx.io/blog/the-foundation-film-is-made-on
