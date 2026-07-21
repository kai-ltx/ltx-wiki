---
title: LTX Video API Model Tiers
type: reference
created: 2026-04-13
updated: 2026-07-21
sources:
  - https://docs.ltx.video/models
  - https://docs.ltx.video/
  - raw/ltx-news-ltx-2-deprecation-july-2026.md
tags:
  - api
  - models
  - ltx-video
  - ltx-2
  - ltx-2-3
---

# LTX Video API Model Tiers

The [[ltx-video-api]] exposes four model IDs across two generations (LTX-2 and LTX-2.3) and two tiers (Fast and Pro). These are the API-specific identifiers; for the underlying open-source model weights, see [[ltx-2-huggingface]] and [[ltx-2-3-huggingface]].

> **Deprecation notice (as of 2026-07-02):** `ltx-2-fast` and `ltx-2-pro` are being retired. As of **July 15, 2026**, requests to these model IDs are automatically served by LTX-2.3 at unchanged LTX-2 pricing. On **August 15, 2026**, the old model IDs will be removed entirely and return an error. All integrations should migrate to `ltx-2-3-fast`/`ltx-2-3-pro` before that date. Known migration gotchas: LTX-2 LoRAs do not transfer cleanly to LTX-2.3 (different parameter count/VAE), prompts resolve more literally (positional language like "left/right" is followed more strictly), default contrast/saturation render punchier, and identical seeds do not reproduce identical output across the two generations. See [[ltx-2-version-history]].

## Available Models

### LTX-2.3 (Latest)

| Model ID | Tier | Best For |
|----------|------|----------|
| `ltx-2-3-fast` | Fast | Speed-optimized, rapid prototyping |
| `ltx-2-3-pro` | Pro | Highest fidelity, all features, production output |

### LTX-2

| Model ID | Tier | Best For |
|----------|------|----------|
| `ltx-2-fast` | Fast | Speed-optimized, landscape only |
| `ltx-2-pro` | Pro | Higher quality, all features |

## Feature Availability by Tier

| Task | Fast | Pro |
|------|------|-----|
| Text-to-video | Yes | Yes |
| Image-to-video | Yes | Yes |
| Audio-to-video | No | Yes |
| Retake | No | Yes |
| Extend | No | Yes |

The Fast tier supports only text-to-video and image-to-video. Audio-to-video, retake, and extend are exclusive to the Pro tier.

## Specifications

| Property | Range |
|----------|-------|
| Resolution | Up to 4K (3840x2160) |
| Frame rate | 24-50 fps |
| Duration | Up to 20 seconds (varies by model and resolution) |
| Aspect ratios | LTX-2.3: portrait and landscape; LTX-2: landscape only |

## Generation Differences

- **LTX-2.3** is the latest generation with improved audio quality, visual fidelity, and prompt adherence. It supports both portrait (e.g., `1080x1920`) and landscape (e.g., `1920x1080`) orientations.
- **LTX-2** is the previous generation. Fast tier is landscape only. Pro tier supports all endpoints.
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
