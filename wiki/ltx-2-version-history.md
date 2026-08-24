---
title: LTX-2 Version History
type: reference
created: 2026-04-13
updated: 2026-08-24
sources:
  - raw/ltx2-version-history-and-releases.md
  - raw/comfyui-ltx-version-history.md
  - raw/ltx-news-ltx-2-deprecation-july-2026.md
  - raw/ltx-news-ltx-2-5-release-2026-08-11.md
  - raw/ltx-news-api-changelog-jul21-aug19-2026.md
tags:
  - ltx-2
  - ltx-2.5
  - version-history
  - releases
  - timeline
  - comfyui
---

# LTX-2 Version History

A chronological record of [[ltx-2-overview|LTX-2]] releases and updates.

## Release Timeline

### LTX-2 Announcement -- October 2025

- Lightricks announced LTX-2 as a rename from LTXV
- First DiT-based audio-video foundation model
- Native 4K resolution at up to 50 FPS
- Synchronized audio and video generation in one pass
- API access initially rolled out to early partners
- **Not yet open source** at this point

### LTX-2 Open-Source Release -- January 6, 2026

- Complete codebase, weights, and tooling made publicly available
- **Parameters:** 19 billion (14B video + 5B audio)
- Apache 2.0 license for code; free for companies under $10M annual revenue
- Full access to model weights, inference pipelines, and training code
- ArXiv paper published: 2601.03233
- Download statistics: 84,353 downloads in December 2025 on Hugging Face; 795 GitHub stars at launch

### End-of-January LTX-2 Update -- Late January 2026

Focused on builder-requested improvements for real-world workflows. This was an incremental drop, not a version bump:

- New [[ltx-2-lora-training|IC-LoRA union control model]] supporting depth, pose, and edges automatically
- New ComfyUI nodes to remove Gemma text encoder from the critical path (addressing VRAM management)
- Saveable/loadable text conditioning as `.safetensors` files

### LTX-2.3 -- March 2026

- **Parameters:** 22 billion (upgraded from 19B)
- **Architecture:** DiT-based audio-video foundation model
- Released alongside [[ltx-desktop|LTX Desktop]]
- **Major new features:**
  - [[audio-video-generation|Audio generation]] -- First open-source model with synchronized audio-video output
  - Gemma 3 12B text encoder (upgraded from previous encoders)
  - Spatial upscalers (2x and 1.5x latent-space upscaling)
  - Temporal upscaler (2x frame rate doubling)
  - [[comfyui-ltx-node-reference|MultimodalGuider]] -- Independent audio/video guidance control
  - [[comfyui-ltx-node-reference|LTXVNormalizingSampler]] -- Statistical normalization for quality
  - GemmaAPITextEncode -- Free API-based text encoding
  - Conditioning save/load for reuse across sessions
  - ID-LoRA for identity-preserving audio-video generation
  - Union IC-LoRA combining Canny + Depth + Pose
  - Camera control LoRAs (dolly, jib movements)
  - Motion tracking via sparse point trajectory tracking
- **Model files:** `ltx-2.3-22b-dev.safetensors` (full), `ltx-2.3-22b-distilled.safetensors` (fast, 8-step generation), plus spatial/temporal upscaler models
- **ComfyUI:** Full workflow examples on docs.comfy.org; one-stage and two-stage pipeline support; desktop auto-installer utility; upstream ID-LoRA integration (PR #13111, March 2026)
- See [[ltx-2.3-model]] for full details

### LTX-2.5 -- August 11, 2026

- **Parameters:** 22 billion (unchanged from LTX-2.3)
- Positioned as an **open-weights world model**, not just a video model -- continuing the "open world models company" repositioning of July 8, 2026
- **Major new features:**
  - **Diffusion Fidelity Rendering** -- motion/structure built in an 8x temporally compressed latent space with adaptive high-fidelity keyframes
  - **New diffusion video decoder** augmenting the VAE decoder (sharper faces, legible text, fewer high-motion artifacts)
  - **Native multishot generation** -- multiple connected shots with continuity across cuts in one generation
  - **Auto duration** -- model predicts clip length from the prompt
  - **Dedicated prompt enhancer**
  - **Native 4K HDR + native EXR** in ACES and DaVinci Wide Gamut; SDR-to-HDR conversion (see [[ltx-explore|Video to HDR]])
  - **Text encoder switched to custom Gemma 4 12B** with learned projection (replacing the LTX-2.3 text connector)
  - **Pretrained non-SFT checkpoint** for physical AI / robotics fine-tuning
  - Larger filtered dataset plus RL post-training; substantially better distilled model
  - Runs on any GPU with **16GB VRAM minimum**
- **Model files:** `ltx-2.5-22b-dev-transformer-bf16.safetensors`, `ltx-2.5-22b-distilled-transformer-bf16.safetensors`, int8 convrot and NVFP4 quantizations, `gemma4-12b-with-proj-ltx-2.5` text encoder, separate video/audio VAEs, 2x spatial and 2x temporal latent upscalers, distilled LoRA (450), duration-head patch
- **ComfyUI:** native day-one support via a strategic launch partnership; official T2V / I2V / first-last-frame templates
- **API:** `ltx-2-5-fast` (up to 4K) and `ltx-2-5-pro` (up to 1080p). Neither supports **retake, extend or reframe** -- those remain `ltx-2-3-pro` only
- **Licensing:** LTX-2.x Community License; free under $10M ARR, not OSI open source (see [[ltx-video-licensing]])
- Launch partners: ComfyUI, Asteria, Reactor, Markov Robotics, [[nvidia-ltx-partnership|NVIDIA]]
- LTX reports the model line has passed **33 million downloads**
- See [[ltx-2.5-model]] and [[ltx-2.5-technical]] for full details

## Version Comparison

| Feature | LTX-2 (Jan 2026) | LTX-2.3 (Mar 2026) | LTX-2.5 (Aug 2026) |
|---------|-------------------|---------------------|---------------------|
| Parameters | 19B | 22B | 22B |
| VAE / decoder | Original | Redesigned VAE (sharper) | + diffusion video decoder |
| Portrait support | Limited | Native 1080x1920 | Native, all tiers |
| Max FPS | 50 | 50 (48 FPS practical) | 50 |
| Text encoding | Standard connector | 4x larger, gated attention (Gemma 3 12B) | Custom Gemma 4 12B + learned projection |
| Audio quality | Good | Filtered training data, new vocoder | RL post-trained, multishot voice continuity |
| Upscalers | Spatial only | Spatial (1.5x/2x) + Temporal | 2x spatial + 2x temporal (latent) |
| Latent scheme | Uniform | Uniform | Diffusion Fidelity Rendering (adaptive) |
| Multishot | No | No | Native |
| HDR / EXR | No | HDR upscale endpoint | Native 4K HDR, EXR in ACES / DWG |
| Retake / extend / reframe | No | Yes (Pro only) | **No** -- still LTX-2.3 Pro only |
| LTX Desktop | No | Yes | Yes |
| LoRA compatibility | LTX-2 LoRAs | Not backward compatible | Retraining required again |

### LTX-2 Deprecation -- July 2026

- Announced July 2, 2026 via the API changelog.
- **July 15, 2026:** `ltx-2-fast`/`ltx-2-pro` API requests are automatically served by LTX-2.3 at unchanged pricing.
- **August 15, 2026:** scheduled removal date for the `ltx-2-fast`/`ltx-2-pro` model IDs.
- **August 16, 2026 -- removal completed.** The API changelog confirms `ltx-2-fast` and `ltx-2-pro` are no longer available; requests specifying them now return an error. Migration path is LTX-2.3 (`ltx-2-3-fast`, `ltx-2-3-pro`) or LTX-2.5 (`ltx-2-5-fast`, `ltx-2-5-pro`). See [[ltx-video-changelog]].
- Completes the transition to the LTX-2.3 / LTX-2.5 model lines as the only supported API options.
- Migration caveats documented by the community: LoRAs don't transfer (parameter count and VAE changed), prompts resolve more literally, default color grading is punchier, and identical seeds diverge after ~10-12 steps between generations.

## No Intermediate Versions

There is no LTX-2.1, LTX-2.2 or LTX-2.4. Versioning went LTX-2 (base) -> LTX-2.3 -> LTX-2.5.

## Related Pages

- [[ltx-2-overview]] -- Model overview
- [[ltx-2.3-model]] -- LTX-2.3 details
- [[ltx-2.5-model]] -- LTX-2.5 details
- [[ltx-2.5-technical]] -- LTX-2.5 architecture
- [[ltx-video-changelog]] -- API-level change log
- [[ltx-video-to-ltx-2-evolution]] -- Pre-LTX-2 history
- [[ltx-2-community-reception]] -- How each release was received
- [[ltx-video-versions]] -- Pre-LTX-2 version timeline (v0.9.x)
- [[comfyui-ltx-integration-overview]] -- ComfyUI integration timeline
- [[audio-video-generation]] -- Audio-video generation (LTX-2.3)
- [[ltx-awesome-resources]] -- Community resource directory
