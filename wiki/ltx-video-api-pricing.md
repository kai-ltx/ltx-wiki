---
title: LTX Video API Pricing
type: reference
created: 2026-04-13
updated: 2026-08-24
sources:
  - https://docs.ltx.video/pricing
  - https://ltx.io/model/api/pricing
  - raw/tutorial-ltx-2-5-api-v2-integration-and-model-matrix-2026-08.md
  - raw/tutorial-ltx-2-5-fal-six-endpoints-pricing-2026-08.md
tags:
  - api
  - pricing
  - ltx-video
  - costs
  - ltx-2-5
---

# LTX Video API Pricing

The [[ltx-video-api]] bills per second of output video. Higher resolution and premium (Pro) models cost proportionally more. There are no minimum charges, and failed generations (4xx/5xx errors) are not billed.

## Text-to-Video and Image-to-Video

Pricing is the same for both endpoints.

### ltx-2-5-fast (launched August 11, 2026)

| Resolution | Cost per Second | 10-second clip |
|-----------|----------------|----------------|
| 720p | $0.09 | $0.90 |
| 1080p | $0.13 | $1.30 |
| 1440p | $0.19 | $1.90 |
| 4K | $0.30 | $3.00 |

### ltx-2-5-pro (launched August 11, 2026)

| Resolution | Cost per Second | 10-second clip |
|-----------|----------------|----------------|
| 720p | $0.12 | $1.20 |
| 1080p | $0.17 | $1.70 |

`ltx-2-5-pro` does not offer 1440p or 4K. See [[ltx-video-api-models]] for the capability matrix.

### LTX-2.5 vs LTX-2.3 at shared resolutions

| Resolution | ltx-2-3-fast | ltx-2-5-fast | ltx-2-3-pro | ltx-2-5-pro |
|---|---|---|---|---|
| 720p | $0.03 | $0.09 | $0.04 | $0.12 |
| 1080p | $0.06 | $0.13 | $0.08 | $0.17 |
| 1440p | $0.12 | $0.19 | $0.16 | -- |
| 4K | $0.24 | $0.30 | $0.32 | -- |

**LTX-2.3 is cheaper than LTX-2.5 at every resolution and tier.** At 720p, 2.3 Fast is one-third the price of 2.5 Fast. Since Retake, Extend and Reframe are 2.3-Pro-exclusive anyway, edit-heavy pipelines have no cost or capability reason to move.

### Competitive per-second cost at 720p

From LTX launch materials:

| Model | $/second at 720p |
|---|---|
| Veo 3.1 Lite | $0.05 |
| **LTX-2.5 Fast** | **$0.09** |
| Veo 3.1 Fast | $0.10 |
| Gemini Omni Flash | $0.10 |
| **LTX-2.5 Pro** | **$0.12** |
| FLUX 3 Video | $0.17 |
| Veo 3.1 | $0.40 |

LTX-2.5 Fast sits second-cheapest overall and is the **only open-weights model in its price bracket**.

### ltx-2-fast

| Resolution | Cost per Second |
|-----------|----------------|
| 1920x1080 | $0.04 |
| 2560x1440 | $0.08 |
| 3840x2160 | $0.16 |

### ltx-2-pro

| Resolution | Cost per Second |
|-----------|----------------|
| 1920x1080 | $0.06 |
| 2560x1440 | $0.12 |
| 3840x2160 | $0.24 |

### ltx-2-3-fast (updated April 1, 2026)

| Resolution | Cost per Second | Previous Price |
|-----------|----------------|---------------|
| 1920x1080 / 1080x1920 | $0.06 | $0.04 |
| 2560x1440 / 1440x2560 | $0.12 | $0.08 |
| 3840x2160 / 2160x3840 | $0.24 | $0.16 |

### ltx-2-3-pro (updated April 1, 2026)

| Resolution | Cost per Second | Previous Price |
|-----------|----------------|---------------|
| 1920x1080 / 1080x1920 | $0.08 | $0.06 |
| 2560x1440 / 1440x2560 | $0.16 | $0.12 |
| 3840x2160 / 2160x3840 | $0.32 | $0.24 |

## Audio-to-Video, Retake, and Extend

All three endpoints are Pro tier only, priced the same regardless of model generation:

| Model | Resolution | Cost per Second |
|-------|-----------|----------------|
| ltx-2-pro | 1920x1080 | $0.10 |
| ltx-2-3-pro | 1920x1080 | $0.10 |

## Cost Examples

### 8-second video at 1080p

| Model | Total Cost |
|-------|-----------|
| ltx-2-fast | $0.32 |
| ltx-2-pro | $0.48 |
| ltx-2-3-fast | $0.48 |
| ltx-2-3-pro | $0.64 |

### 10-second video at 4K

| Model | Total Cost |
|-------|-----------|
| ltx-2-fast | $1.60 |
| ltx-2-pro | $2.40 |
| ltx-2-3-fast | $2.40 |
| ltx-2-3-pro | $3.20 |

## Important Notes

- Billing is based on **output duration**, not generation time.
- Failed generations (4xx/5xx errors) are **not billed**.
- A `402 insufficient_funds_error` is returned when the account lacks credits.
- Credits are managed in the developer console -- https://console.ltx.io for the v2/LTX-2.5 surface, https://console.ltx.video/ for the older one.
- Third-party resellers price LTX-2.5 identically per second: fal.ai matches the Fast tier exactly at $0.09/$0.13/$0.19/$0.30. See [[fal-ai]].
- fal.ai bills **audio-to-video per second of input audio**, not output.
- No free tier has been documented.

## Related Pages

- [[ltx-video-api]]
- [[ltx-video-api-models]]
- [[ltx-video-api-endpoints]]
- [[ltx-video-api-errors]]
- [[fal-ai]]
- [[ltx-2.5-model]]
