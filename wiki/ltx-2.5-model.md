---
title: LTX-2.5 Model
type: product
created: 2026-08-24
updated: 2026-08-24
sources:
  - raw/ltx-news-ltx-2-5-release-2026-08-11.md
  - raw/ltx-news-ltx-2-5-api-pricing-and-benchmarks-2026-08.md
  - raw/ltx-news-api-changelog-jul21-aug19-2026.md
  - raw/ltx-news-sdr-to-hdr-conversion-ltx-2-5-2026-08-09.md
tags:
  - ltx-2
  - ltx-2.5
  - model
  - world-model
  - foundation-model
---

# LTX-2.5 Model

LTX-2.5 is the current flagship of the [[ltx-2-overview|LTX-2]] family, released **August 11, 2026** and succeeding [[ltx-2.3-model|LTX-2.3]] (March 2026). It keeps the **22 billion parameter** asymmetric dual-stream diffusion transformer, and is marketed as a **world model** rather than a video model -- continuing the "open world models company" repositioning LTX announced on July 8, 2026. LTX calls it "the most capable open weights world model on the market."

## Key Improvements over LTX-2.3

- **Diffusion Fidelity Rendering (DFR):** builds motion and structure in an **8x temporally compressed latent space** while generating high-fidelity keyframes to anchor detail. Keyframe count adapts to scene complexity and compute budget instead of locking every scene to a single compression rate.
- **New diffusion video decoder** (augmenting the earlier VAE decoder): sharper faces, legible text and signage, fewer high-motion artifacts, without giving up LTX's high compression ratio.
- **Native multishot generation:** a single generation produces multiple connected shots (wide / medium / close-up) holding character, environment, lighting, voice, style and continuity across cuts -- rather than stitching separate generations.
- **Auto duration:** the model predicts clip length from the described action.
- **Dedicated prompt enhancer** that expands short prompts into richer cinematic and temporal instructions "at near-zero extra compute."
- **Native 4K HDR and native EXR workflow:** reads and writes cinema-grade EXR in **ACES** and **DaVinci Wide Gamut** (HDR ACES in -> HDR ACES out), preserving dynamic range, metadata and color. See [[ltx-explore|Video to HDR]] for the SDR-to-HDR product surface.
- **Text encoder swapped to a custom Gemma 4 12B** with a learned projection, replacing the LTX-2.3 text connector.
- **Pretrained (non-SFT) checkpoint** tuned for physical AI / robotics, intended for aggressive domain fine-tuning.
- **Larger filtered dataset plus RL post-training** aligned to human preference.
- **Substantially better distilled model**, optimized with [[nvidia-ltx-partnership|NVIDIA]] for local inference on RTX GPUs and DGX Spark at reduced VRAM.
- **Cleaner permissive licensing** with fewer restrictive third-party dependencies.

## Capabilities

Text-to-video, image-to-video, video-to-video, text-to-audio and audio-to-video. Runs on any GPU with **minimum 16GB VRAM**, deployable on-prem, at the edge, or via API -- from data-center GPUs down to a Mac.

**Not supported:** retake, extend and reframe remain **`ltx-2-3-pro` only**. LTX-2.5 does not offer these endpoints.

## API Tiers

| Tier | Max Resolution | Duration Support |
|------|----------------|------------------|
| `ltx-2-5-fast` | 4K | 720p/1080p @ 24/25 fps: 6-20 s (even values); 720p/1080p @ 48/50 fps: 6/8/10 s; 1440p and 4K @ 24/25/48/50 fps: 6/8/10 s |
| `ltx-2-5-pro` | 1080p | 720p/1080p @ 24/25/50 fps: 6/8/10 s only |

Both tiers support text-to-video, image-to-video and audio-to-video, portrait and landscape, camera motion, `last_frame_uri` on image-to-video, and `"duration": null` for automatic duration (the field is still required; cannot be combined with `last_frame_uri`). See [[ltx-2-model-variants]] and [[ltx-video-api-models]].

## Pricing (per second of output, as of 2026-08-24)

| Resolution | `ltx-2-5-fast` | `ltx-2-5-pro` |
|------------|----------------|---------------|
| 720p | $0.09 | $0.12 |
| 1080p | $0.13 | $0.17 |
| 1440p | $0.19 | -- |
| 4K | $0.30 | -- |

LTX-2.3 remains substantially cheaper (e.g. `ltx-2-3-fast` at $0.03/sec for 720p). Full table in [[ltx-video-api-pricing]].

## Vendor-Reported Performance

All figures below were **measured or commissioned by LTX and are not independently verified**.

- **6.8 seconds** to generate a 10-second 720p image-to-video clip, self-hosted at steady state on **two NVIDIA GB200 superchips** -- faster than real time. The same job via LTX's own managed API took **23.7 seconds** (at 1080p; the API had no 720p tier for that measurement).
- LTX's end-to-end timings for rivals on the same task: Gemini Omni Flash 52 s, xAI Grok 1.5 63 s, Google Veo 3.1 70 s (8-second clip), MiniMax H3 180 s, ByteDance Seedance 2.5 317 s, Kling 3.0 Pro 398 s.
- Blind human preference tests (LTX labels these **preliminary**): LTX-2.5 **67% win rate**, Seedance 2.5 65%, Gemini Omni Flash 55%, MiniMax H3 50%, Seedance 2.0 44%, Wan 2.6 42%, FLUX 3 28%.
- LTX claims roughly **one-eighth the cost and one-seventh the render time** of comparable models.

### Independent Scrutiny

VentureBeat (Carl Franzen, 2026-08-11) checked the claims against published rates and found **the "one-eighth the cost" multiple unsupported**: a 10-second 720p clip with audio costs $0.90 on LTX-2.5 Fast versus Veo 3.1 Lite $0.50 (cheaper), Veo 3.1 Fast $1.00, Gemini Omni Flash $1.00, FLUX 3 Video $1.70, HappyHorse 1.0 ~$1.82, Veo 3.1 $4.00. The render-time claim held up better but **shrinks to roughly 2x through LTX's own API**. At publication, Artificial Analysis' text-to-video leaderboards had not yet scored LTX-2.5, and Gemini Omni Flash led both. See [[ltx-2-benchmarks]] and [[competitor-landscape-overview]].

## Weights and Variants

Open weights on Hugging Face (`Lightricks/LTX-2.5`, collection `Lightricks/ltx-25`):

| Artifact | Notes |
|----------|-------|
| `ltx-2.5-22b-dev-transformer-bf16.safetensors` | Base transformer |
| `ltx-2.5-22b-distilled-transformer-bf16.safetensors` | Distilled transformer |
| int8 convrot / NVFP4 distilled variants | ComfyUI-ready quantizations (see [[fp8-quantization]]) |
| `gemma4-12b-with-proj-ltx-2.5` | Text encoder (BF16 and ComfyUI int8 convrot) |
| Video VAE + audio VAE | Separate checkpoints |
| 2x latent spatial + 2x latent temporal upscalers | Two-stage pipeline |
| Distilled LoRA (450), duration-head model patch | Add-ons |

Official ComfyUI templates cover T2V, I2V and first/last-frame-to-video; `Lightricks/ComfyUI-LTXVideo` was updated with 2.5 example workflows (single-stage and two-stage upscaled T2V/I2V, ICLoRA inpainting/outpainting, motion tracking, union control, text-to-audio).

## Licensing

Ships under the **LTX-2.x Community License**: free for organizations under **$10M annual recurring revenue**, negotiated terms above that. It is **not OSI open source** -- it discriminates by revenue and field of use, bans military/warfare/weapons uses outright, requires derivatives (fine-tunes, LoRAs, distillations, and models trained on LTX-2.5 outputs or synthetic data) to be redistributed under the same license, and bars commercial users from training competing AI systems. Details in [[ltx-video-licensing]].

## Launch Partners

ComfyUI (day-one native integration; co-founder & CEO Yoland Yan), **Asteria** (AI film studio; Paul Trillo, co-founder & Executive Creative Director), **Reactor** (real-time generative video developer platform; CEO Alberto Taiuti), **Markov Robotics** (CEO Atharva Gundawar), and **NVIDIA** (Gerardo Delgado Cabrera, Senior Director of Product for Local AI).

LTX co-founder and CEO Zeev Farbman: "World models face challenges that LLMs never had to solve, like holding motion, space, and sound consistent across time, which is why efficiency and control matter so much. By keeping LTX open, we let teams own their hardware, their IP, and their model."

## Adoption

LTX says the model line has passed **33 million downloads**, which it claims makes it the most-used open world model line.

## Links

- **Announcement:** https://ltx.io/newsroom/introducing-ltx-2-5
- **API docs:** https://docs.ltx.io/models/ltx-2-5
- **Release notes:** https://ltx.io/release-notes

## Related Pages

- [[ltx-2-overview]] -- Model family overview
- [[ltx-2.5-technical]] -- Architecture deep dive
- [[ltx-2.3-model]] -- Previous flagship
- [[ltx-2-version-history]] -- Release timeline
- [[ltx-video-changelog]] -- API changelog entries
- [[ltx-2-model-variants]] -- Checkpoints and quantizations
- [[ltx-video-api-pricing]] -- Full API price list
- [[ltx-explore]] -- Self-service surface (Video to HDR)
- [[ltx-ecosystem]] -- Where LTX-2.5 sits in the product stack
