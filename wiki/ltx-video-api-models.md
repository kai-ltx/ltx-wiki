---
title: LTX Video API Model Tiers
type: reference
created: 2026-04-13
updated: 2026-08-24
sources:
  - https://docs.ltx.video/models
  - https://docs.ltx.video/
  - raw/ltx-news-ltx-2-deprecation-july-2026.md
  - raw/tutorial-ltx-2-5-api-v2-integration-and-model-matrix-2026-08.md
tags:
  - api
  - models
  - ltx-video
  - ltx-2
  - ltx-2-3
  - ltx-2-5
---

# LTX Video API Model Tiers

The [[ltx-video-api]] exposes model IDs across three generations (LTX-2, LTX-2.3 and LTX-2.5) and two tiers (Fast and Pro). These are the API-specific identifiers; for the underlying open-source model weights, see [[ltx-2-huggingface]], [[ltx-2-3-huggingface]] and [[ltx-2.5-model]].

> **Deprecation notice (as of 2026-07-02):** `ltx-2-fast` and `ltx-2-pro` are being retired. As of **July 15, 2026**, requests to these model IDs are automatically served by LTX-2.3 at unchanged LTX-2 pricing. On **August 15, 2026**, the old model IDs will be removed entirely and return an error. All integrations should migrate to `ltx-2-3-fast`/`ltx-2-3-pro` before that date. Known migration gotchas: LTX-2 LoRAs do not transfer cleanly to LTX-2.3 (different parameter count/VAE), prompts resolve more literally (positional language like "left/right" is followed more strictly), default contrast/saturation render punchier, and identical seeds do not reproduce identical output across the two generations. See [[ltx-2-version-history]].

## Available Models

### LTX-2.5 (Latest, launched 2026-08-11)

| Model ID | Tier | Best For |
|----------|------|----------|
| `ltx-2-5-fast` | Fast | Speed, 4K output, long clips, audio-to-video |
| `ltx-2-5-pro` | Pro | Highest per-frame fidelity via Diffusion Fidelity Rendering; caps at 1080p |

Served over the new async `/v2` surface at `api.ltx.io` -- see [[ltx-video-api-endpoints]].

#### LTX-2.5 specification

| Spec | `ltx-2-5-fast` | `ltx-2-5-pro` |
|---|---|---|
| Max resolution | 4K (3840x2160) | 1080p (1920x1080) |
| Frame rate | 24, 48 fps | 24 fps |
| Max single generation | ~20 s (24/25 fps) | ~10 s |
| Audio-to-video | Yes (async-only via `v2/audio-to-video`) | No |
| Automatic Duration | Yes (`duration: null`) | Yes (`duration: null`) |

### LTX-2.3

| Model ID | Tier | Best For |
|----------|------|----------|
| `ltx-2-3-fast` | Fast | Speed-optimized, rapid prototyping |
| `ltx-2-3-pro` | Pro | Highest fidelity, all features, production output |

### LTX-2

| Model ID | Tier | Best For |
|----------|------|----------|
| `ltx-2-fast` | Fast | Speed-optimized, landscape only |
| `ltx-2-pro` | Pro | Higher quality, all features |

## Cross-Generation Capability Matrix

The tier convention broke with LTX-2.5. Despite the name, **`ltx-2-5-pro` is the more restricted variant**.

| Endpoint | `ltx-2-5-fast` | `ltx-2-5-pro` | `ltx-2-3-fast` | `ltx-2-3-pro` |
|---|---|---|---|---|
| Text-to-video | Yes | Yes | Yes | Yes |
| Image-to-video | Yes | Yes | Yes | Yes |
| Audio-to-video | Yes | **No** | No | Yes |
| Retake | No | **No** | No | Yes |
| Extend | No | **No** | No | Yes |
| Reframe | No | **No** | No | Yes |

**Retake, Extend and Reframe remain exclusive to `ltx-2-3-pro`.** If your pipeline edits video rather than generating it, LTX-2.5 offers no upgrade path -- stay on 2.3 Pro. Extend on 2.3 Pro is capped at **505 billed frames**.

## Feature Availability by Tier (LTX-2 / LTX-2.3)

| Task | Fast | Pro |
|------|------|-----|
| Text-to-video | Yes | Yes |
| Image-to-video | Yes | Yes |
| Audio-to-video | No | Yes |
| Retake | No | Yes |
| Extend | No | Yes |

For LTX-2 and LTX-2.3, the Fast tier supports only text-to-video and image-to-video. Audio-to-video, retake, and extend are exclusive to the Pro tier. LTX-2.5 inverts part of this -- see the matrix above.

## Specifications

| Property | Range |
|----------|-------|
| Resolution | Up to 4K (3840x2160) |
| Frame rate | 24-50 fps |
| Duration | Up to 20 seconds (varies by model and resolution) |
| Aspect ratios | LTX-2.3: portrait and landscape; LTX-2: landscape only |

## Generation Differences

- **LTX-2.5** is the current generation (launched 2026-08-11). Fast reaches 4K and ~20 s clips and is the only 2.5 variant with audio-to-video; Pro runs Diffusion Fidelity Rendering but caps at 1080p/24 fps/~10 s and drops all editing endpoints. Both default `duration` to automatic. It is priced roughly 2-3x above LTX-2.3 at every shared resolution -- see [[ltx-video-api-pricing]].
- **LTX-2.3** is the previous generation with improved audio quality, visual fidelity, and prompt adherence. It supports both portrait (e.g., `1080x1920`) and landscape (e.g., `1920x1080`) orientations.
- **LTX-2** is the oldest generation, removed from the API on August 15, 2026. Fast tier is landscape only. Pro tier supports all endpoints.
- **Fast** models are optimized for speed and cost -- ideal for iteration and prototyping.
- **Pro** models deliver the highest output quality and unlock the full feature set.

## Pricing

See [[ltx-video-api-pricing]] for per-second cost tables by model and resolution.

## Related Pages

- [[ltx-video-api]]
- [[ltx-video-api-endpoints]]
- [[ltx-video-api-pricing]]
- [[ltx-2-huggingface]]
- [[ltx-2-3-huggingface]]
- [[ltx-2.5-model]]
- [[fal-ai]] -- the same models under fal endpoint IDs
