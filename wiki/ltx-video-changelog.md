---
title: LTX Video Changelog
type: analysis
created: 2026-04-13
updated: 2026-08-24
sources:
  - raw/ltx-video-version-changelog-improvements.md
  - raw/ltx-video-version-changes-changelog.md
  - raw/ltx-video-capabilities-per-version.md
  - raw/ltx-news-api-changelog-jul21-aug19-2026.md
  - raw/ltx-news-ltx-2-5-release-2026-08-11.md
tags:
  - ltx-video
  - changelog
  - api
  - ltx-2.5
  - improvements
  - versions
---
# LTX Video Changelog

Detailed version-by-version changes for [[ltx-video-overview|LTX-Video]]. For a high-level timeline, see [[ltx-video-versions]].

## v0.9.0 -- Initial Release (November 2024)

**New:**
- First public release of LTX-Video by [[lightricks-company]]
- 2B parameter [[diffusion-transformer]]-based video generation model
- Novel [[video-vae|Video-VAE]] with 1:192 compression ratio (32x32x8, 128 channels)
- Denoising decoder (VAE performs final diffusion step in pixel space)
- Reconstruction GAN loss for VAE training
- Video DWT loss for high-frequency detail preservation
- T5-XXL text encoder with cross-attention conditioning
- RoPE with normalized fractional coordinates
- QK normalization with RMSNorm
- Per-token timestep conditioning for image-to-video
- Rectified-flow training with velocity prediction
- Multi-resolution training
- Text-to-video and image-to-video capabilities
- 768x512 at 24 FPS, up to 257 frames
- Faster-than-real-time generation (2s for 5s video on H100)
- Research paper published: arXiv:2501.00103
- Open-source on GitHub and Hugging Face
- Diffusers integration (`LTXPipeline`, `LTXImageToVideoPipeline`)

---

## v0.9.0 to v0.9.1 (November 2024 to December 2024)

**Improved:**
- Smoother motion with more natural and fluid video movement
- Improved physics with better physical plausibility in generated scenes
- Cleaner visuals with reduced artifacts and visual noise
- Significant boost to image-to-video quality
- Training-free video enhancement capability added
- Resolution upgraded from 768x512 to 1216x704 at 30 FPS

**Unchanged:**
- Same 2B parameter architecture
- Same inference requirements and API

---

## v0.9.1 to v0.9.5 (December 2024 to March 5, 2025)

**New:**
- Multi-keyframe conditional support (generate from first, last, or any intermediate frame)
- Video extension with greater flexibility (forward and backward)
- Commercial license introduced (OpenRail-M, replacing RAIL-M)
- [[comfyui-ltx-integration-overview]] with day-1 support
- LoRA support added
- Training datasets released (Squish, Cakeify)

**Improved:**
- Resolution and quality enhancements with reduced artifacts and smoother visuals
- Longer video generation support
- Better prompt understanding and adherence

**Unchanged:**
- Same 2B parameter architecture
- 1216x704 native resolution, 30 FPS

---

## v0.9.5 to v0.9.6 (March 2025 to April 2025)

**New:**
- First dev/distilled model split
  - `ltxv-2b-0.9.6-dev` -- Full-quality for final outputs
  - `ltxv-2b-0.9.6-distilled` -- 15x faster, 8 diffusion steps, no CFG/STG needed
- Real-time video generation achieved on consumer hardware

**Improved:**
- Enhanced prompt adherence
- Smoother motion
- Finer details with more realistic and coherent outputs
- Ultra-fast inference (8 diffusion steps for distilled model)

**Unchanged:**
- 2B parameters
- Same base [[ltx-video-architecture|architecture]]

---

## v0.9.6 to v0.9.7 (April 2025 to May 6, 2025)

This was the largest single update in LTX-Video's history.

**New:**
- **13B parameter model** -- 6.5x increase from 2B, massive quality improvement
- **Multiscale rendering** -- drafts at lower detail first, progressively adds structure, lighting, micro-motion; for 1080p: renders at 960x540 then upscales 2x; 30x faster than comparable-sized models
- **FP8 quantization** -- official quantized models with ~50% memory reduction
- **ICLoRA conditioning adapters:** depth, pose, canny edge, detailer
- **Spatial upscaler** -- 2x resolution increase in latent space
- **Mix mode** -- multi-scale workflow combining dev and distilled models
- **LoRA128 adapter** -- convert dev to distilled behavior
- **Multi-condition generation** -- condition on multiple images/videos at different frame positions
- **LoRA fine-tuning support**
- **New Diffusers API:** `LTXConditionPipeline`, `LTXLatentUpsamplePipeline`, `LTXVideoCondition`

**Improved:**
- Breakthrough prompt adherence and physical understanding
- Enhanced video length up to 60 seconds
- Simplified [[comfyui-ltx-integration-overview]] flows (new nodes for img2vid, img2vid+extension, img2vid+keyframes)

**Models added:** 12 new variants (see [[ltx-video-model-variants]])

---

## v0.9.7 to v0.9.8 (May 2025 to Mid-July 2025)

**New:**
- **IC-LoRA control models** officially launched (depth, pose, canny edge)
- **Detailer model** for enhancing fine details (LTX-Video-ICLoRA-detailer-13B-0.9.8)
- **New 2B distilled checkpoints** -- both standard and FP8 versions
- **Video-to-video generation** -- conditioning on video segments
- **Multi-condition generation** refined
- **Temporal upscaler** -- frame interpolation added
- **2B distilled-fp8** -- most efficient variant ever (~4.46 GB)

**Improved:**
- Better prompt understanding and detail generation
- Slightly faster than 0.9.7
- Extended video generation confirmed at 60 seconds

**Pipeline change:** `LTXConditionPipeline` now supports multi-condition workflows

**Models added:** 7 new variants (see [[ltx-video-model-variants]])

**Known issues:**
- Some users reported plastic-looking skin in certain generations (GitHub Issue #230)
- Many 0.9.8 model pages on Hugging Face are gated

---

---

## LTX API Changelog -- July 21 to August 19, 2026

Seven entries landed on the [[ltx-video-api-models|LTX API]] changelog in this window (newest first). LTX's product release-notes page lists **no** Studio-side or open-source entries between July 20, 2026 ([[ltx-explore|LTX Explore]]) and August 11, 2026 (LTX-2.5), so the API changelog is the only record of incremental platform change over that stretch.

### August 19, 2026 -- Audio-to-video generation params

Audio-to-video now accepts `fps` (default 24), `last_frame_uri` (requires `image_uri`), and `camera_motion`, matching text-to-video and image-to-video. Available on `v2/audio-to-video` (async) and `v1/audio-to-video` (sync).

### August 18, 2026 -- Audio-to-video resolution parity

Audio-to-video gains the same resolution tiers as text-to-video and image-to-video: `ltx-2-5-fast` up to 4K, `ltx-2-5-pro` up to 1080p, `ltx-2-3-pro` up to 4K. Maximum input audio length varies by model and tier -- e.g. `ltx-2-3-pro` accepts up to 20 seconds at 720p/1080p and up to 10 seconds at 1440p/4K. New tiers bill at standard published rates ([[ltx-video-api-pricing]]).

### August 16, 2026 -- LTX-2 removal completed

`ltx-2-fast` and `ltx-2-pro` are no longer available; requests specifying them return an error. This closes out the July 2, 2026 deprecation notice, which had scheduled removal for August 15. Migration path: LTX-2.3 (`ltx-2-3-fast`, `ltx-2-3-pro`) or LTX-2.5 (`ltx-2-5-fast`, `ltx-2-5-pro`). See [[ltx-2-version-history]].

### August 11, 2026 -- LTX-2.5 on the API

New models for text-to-video, image-to-video and audio-to-video, portrait and landscape: **`ltx-2-5-fast`** up to 4K, **`ltx-2-5-pro`** at 720p and 1080p. Audio-to-video initially generated at 1080p on both (superseded by the August 18 parity change). Both accept camera motion, `last_frame_uri` on image-to-video, and `"duration": null` for automatic duration. Retake, extend and reframe are **not** supported and remain `ltx-2-3-pro` only. See [[ltx-2.5-model]].

### August 10, 2026 -- Automatic duration

Text-to-video and image-to-video accept `"duration": null` on `ltx-2-5-fast`, letting the model choose clip length from the prompt. Shipped one day ahead of the public LTX-2.5 launch.

### August 2, 2026 -- 720p tier on LTX-2.3

Text-to-video and image-to-video gained a 720p output tier on [[ltx-2.3-model|LTX-2.3]] (`1280x720` landscape, `720x1280` portrait), priced at $0.03/sec on `ltx-2-3-fast` and $0.04/sec on `ltx-2-3-pro`.

### July 21, 2026 -- New API domain `api.ltx.io`

The LTX API is now served at `https://api.ltx.io`, and docs and code samples use it going forward. Existing integrations on `https://api.ltx.video` keep working unchanged -- no migration required.

## Architecture Constants (LTX-Video v0.9.x)

These fundamental design choices remained constant throughout the LTX-Video line:

- [[diffusion-transformer]]-based architecture (built on Pixart-alpha)
- [[video-vae|Video-VAE]] with 32x32x8 compression, 128 channels
- T5-XXL text encoder
- RoPE positional embeddings
- Cross-attention text conditioning
- Per-token timestep conditioning for I2V
- Rectified-flow training framework
- Resolution divisible by 32
- Frame count divisible by 8 + 1
- Maximum ~257 frames
- 24-30 FPS output

## References

- [[ltx-video-overview]] -- Model family overview
- [[ltx-video-versions]] -- Version timeline
- [[ltx-video-capabilities]] -- Capability matrix
- [[ltx-video-model-variants]] -- Complete model inventory
- [[ltx-video-architecture]] -- Core architecture details
- [[ltx-2-version-history]] -- LTX-2 / LTX-2.3 / LTX-2.5 release timeline
- [[ltx-video-api-models]] -- Current API model IDs
- [[ltx-video-api-pricing]] -- Per-second pricing
