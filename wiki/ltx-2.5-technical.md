---
title: "LTX-2.5: Technical Architecture"
type: technical
created: 2026-08-24
updated: 2026-08-24
sources:
  - raw/ltx-news-ltx-2-5-release-2026-08-11.md
  - raw/ltx-news-sdr-to-hdr-conversion-ltx-2-5-2026-08-09.md
  - raw/ltx-news-ltx-2-5-api-pricing-and-benchmarks-2026-08.md
tags:
  - ltx-2
  - ltx-2.5
  - architecture
  - vae
  - world-model
  - lightricks
---

# LTX-2.5: Technical Architecture

**Developer:** LTX (spun out of [[lightricks-research-overview|Lightricks]])
**Release Date:** August 11, 2026
**Parameters:** 22B
**Model Page:** [ltx.io](https://ltx.io/newsroom/introducing-ltx-2-5) | [HuggingFace](https://huggingface.co/Lightricks/LTX-2.5)
**Note:** No separate arXiv paper as of 2026-08-24; builds on the [[paper-ltx-2|LTX-2 paper]] (arXiv:2601.03233) and the [[ltx-2.3-technical|LTX-2.3]] revisions

## Summary

LTX-2.5 keeps the 22B asymmetric dual-stream diffusion transformer of [[ltx-2.3-model|LTX-2.3]] but changes how that transformer spends its compute. The headline change is **Diffusion Fidelity Rendering**, an adaptive-compression scheme, paired with a **new diffusion video decoder**, a **Gemma 4 12B text encoder with learned projection**, and RL post-training on a larger filtered dataset. LTX positions the result as a **world model** -- one that holds motion, space and sound consistent across time -- rather than a clip generator.

## Key Technical Changes Over LTX-2.3

### 1. Diffusion Fidelity Rendering (DFR)

The central architectural idea. Motion and structure are built in an **8x temporally compressed latent space** -- cheap, and good at long-range coherence -- while the model separately generates **high-fidelity keyframes that anchor detail**. Crucially, the keyframe count is **adaptive**: it scales with scene complexity and the available compute budget, rather than locking every scene to one fixed compression rate the way a uniform latent pipeline does.

This is what lets LTX-2.5 keep LTX's characteristically aggressive compression ratio (and therefore its speed advantage) without paying for it in fine detail on complex scenes.

### 2. New Diffusion Video Decoder

A diffusion-based video decoder now augments the earlier VAE decoder inherited from the [[ltx-2.3-technical|LTX-2.3 rebuilt VAE]]. Reported effects:

- Sharper faces
- Legible text and signage
- Fewer artifacts in high-motion sequences
- High compression ratio preserved

### 3. Text Encoder: Custom Gemma 4 12B

LTX-2.3's 4x-larger gated-attention text connector is **replaced** by a custom **Gemma 4 12B** encoder with a **learned projection** into the transformer. The encoder ships as its own checkpoint (`gemma4-12b-with-proj-ltx-2.5`, BF16 and ComfyUI int8 convrot).

### 4. Native Multishot Generation

A single generation produces **multiple connected shots** -- wide, medium, close-up -- holding character identity, environment, lighting, voice, style and continuity **across cuts**. This is done inside one generation pass rather than by stitching independent clips, which is the mechanism that makes cross-cut consistency tractable.

### 5. Auto Duration

A **duration-head model patch** ships alongside the weights, letting the model predict clip length from the described action. Exposed on the API as `"duration": null` for text-to-video and image-to-video (cannot be combined with `last_frame_uri`).

### 6. Prompt Enhancer

A dedicated model expands short prompts into richer cinematic and temporal instructions, which LTX says runs "at near-zero extra compute."

### 7. Native EXR / HDR Pipeline

LTX-2.5 **reads and writes cinema-grade EXR natively** in **ACES** and **DaVinci Wide Gamut** -- HDR ACES in, HDR ACES out -- preserving dynamic range, metadata and color with no lossy 8-bit round trip.

The SDR-to-HDR conversion runs as a **video-to-video pass**. The model **rebuilds the light data SDR discarded** rather than stretching existing values, so clipped highlights and crushed shadows return with real detail; LTX frames this as "a reconstruction of the image," not a visual adjustment. Output is a **scene-linear EXR, float16 with roughly 20-bit effective range**, opening directly in DaVinci Resolve, Nuke or Baselight. LTX-2.5 can alternatively return color-matched video in a standard container. Surfaced as the **Video to HDR** tool in [[ltx-explore]]; the API lineage is the `/v2/video-to-video-hdr` endpoint (see [[ltx-api-async-hdr]]), whose research basis was an HDR IC-LoRA on LTX-2.3-22b backed by the paper *LumiVid: HDR Video Generation via Latent Alignment with Logarithmic Encoding*.

### 8. Training

- **Larger filtered dataset** than LTX-2.3
- **RL post-training** aligned to human preference
- **Substantially better distilled model**
- A separate **pretrained, non-SFT checkpoint** tuned for **physical AI / robotics**, released for aggressive domain fine-tuning

## Architecture Specifications

| Component | Specification |
|-----------|--------------|
| Total parameters | 22B |
| Architecture type | Asymmetric dual-stream DiT |
| Audio-video coupling | Bidirectional cross-attention |
| Guidance | Modality-aware classifier-free guidance |
| Text encoder | Custom Gemma 4 12B + learned projection |
| Latent scheme | 8x temporal compression + adaptive keyframes (DFR) |
| Decoder | Diffusion video decoder + VAE decoder |
| Max resolution | 4K (native HDR) |
| Color pipeline | EXR, ACES, DaVinci Wide Gamut |
| Modalities | T2V, I2V, V2V, T2A, A2V |
| Minimum VRAM | 16 GB |

## Core Architecture (Inherited)

Retained from [[ltx-2-architecture|LTX-2]] and [[ltx-2.3-technical|LTX-2.3]]:

- Dual-stream asymmetric diffusion transformer
- Bidirectional audio-video cross-attention with temporal RoPE
- Cross-modality AdaLN conditioning
- Modality-aware classifier-free guidance (modality-CFG)
- Separate video VAE and audio VAE
- 2x latent spatial and 2x latent temporal upscalers for the two-stage pipeline

## Deployment and Optimization

Runs on any GPU with **at least 16GB VRAM**, from data-center hardware down to a Mac, and is deployable on-prem, at the edge, or via the LTX API. The distilled transformer was optimized with [[nvidia-ltx-partnership|NVIDIA]] for local inference on **RTX GPUs and DGX Spark** at reduced VRAM, and ships in **int8 convrot** and **NVFP4** ComfyUI-ready quantizations (see [[fp8-quantization]]).

Vendor-reported: **6.8 seconds** for a 10-second 720p image-to-video clip, self-hosted at steady state on **two NVIDIA GB200 superchips**. This figure is LTX-measured and not independently verified; the same job through LTX's managed API took 23.7 seconds at 1080p. See [[ltx-2.5-model]] and [[ltx-2-benchmarks]] for the full benchmark picture and VentureBeat's finding that the accompanying "one-eighth the cost" claim is unsupported.

## Functional Gaps

LTX-2.5 does **not** implement retake, extend, or reframe. Those remain [[ltx-2.3-model|LTX-2.3]] Pro (`ltx-2-3-pro`) endpoints.

## Relationship to Other Work

LTX-2.5 continues the lineage from [[paper-ltx-video|LTX-Video]] through [[paper-ltx-2|LTX-2]] and [[ltx-2.3-technical|LTX-2.3]]. The [[paper-avcontrol|AVControl]] framework and its downstream applications ([[paper-just-dub-it|JUST-DUB-IT]], [[paper-id-lora|ID-LoRA]]) are built on the LTX-2 backbone that LTX-2.5 extends.

## Related Pages

- [[ltx-2.5-model]] -- Product page, pricing, availability
- [[ltx-2.3-technical]] -- Previous generation technical notes
- [[ltx-2-architecture]] -- Shared architectural foundation
- [[ltx-2-model-variants]] -- Checkpoint inventory
- [[ltx-explore]] -- Video to HDR tool
