---
title: Seedance (ByteDance)
type: competitor
created: 2026-07-06
updated: 2026-07-06
sources:
  - raw/competitor-seedance-25-july-2026.md
tags:
  - competitor
  - video-generation
  - seedance
  - bytedance
  - proprietary
  - cloud-platform
---
# Seedance (ByteDance)

Seedance is ByteDance's AI video generation platform, distributed via API and integrated into third-party developer tools. ByteDance announced the model family in 2025 and has been actively advancing generation quality and duration capabilities.

## Model Versions

### Seedance 2.0 (2026)
- Available via API (accessed through [[competitor-runway|Runway]] platform as of June 2026)
- **4K API:** 150 credits/second (high quality, launched June 24, 2026)
- **2.0 Mini:** 16 credits/second (efficiency tier, launched June 26, 2026)
- Ships with **C2PA watermarking** built in (EU AI Act and California SB 942 compliant)

### Seedance 2.5 (Early July 2026)
Seedance 2.5 is ByteDance's most capable video generation model, announced June 23, 2026 with public launch in early July 2026.

**Key capabilities:**
- **Native 30-second generation:** Single-pass 30-second clips with no stitching or scene cuts
- **Up to 50 multimodal references:** Accepts images, video clips, text descriptions, and other modalities as reference inputs simultaneously
- **Local editing:** Modify specific areas of a generated video without regenerating the full clip
- **Native 4K with 10-bit color depth:** Not upscaled — true native 4K output for professional production
- **Multiple pipelines:** T2V (text-to-video), I2V (image-to-video), V2V (video-to-video)

**Caveats:** All specifications are ByteDance stated claims as of early July 2026. No independent benchmarks have been published.

## Competitive Position

Seedance 2.5's **native 30-second generation** is a significant threshold: competitors like [[competitor-kling|Kling]] and [[competitor-veo|Veo]] top out at 15s and 8s per clip respectively for native generation (though Veo supports 140s+ via chaining). The **50 multimodal references** capability exceeds any current competitor.

However, Seedance does not yet have a direct consumer-facing platform comparable to [[competitor-runway|Runway]] or [[competitor-kling|Kling AI]]. Distribution currently relies on API and platform partnerships.

## Regulatory Compliance
- Seedance 2.0 ships with **C2PA watermarking** built in, compliant with EU AI Act Article 50 (enforcement August 2, 2026) and California SB 942

## See Also
- [[competitor-landscape-overview]]
- [[competitor-runway]]
- [[competitor-kling]]
