---
title: LTX Explore
type: product
created: 2026-07-21
updated: 2026-08-24
sources:
  - raw/ltx-news-ltx-explore-launch-july20-2026.md
  - raw/ltx-news-sdr-to-hdr-conversion-ltx-2-5-2026-08-09.md
tags:
  - ltx-explore
  - hdr
  - ltx-2.5
  - product
  - no-code
  - lightricks
  - self-service
---

# LTX Explore

LTX Explore is a self-service, no-code product launched by Lightricks on July 20, 2026, positioned as "All the Power of LTX. None of the Setup." It sits as a new access tier between the full [[ltx-studio]] production suite and the raw [[ltx-video-api|LTX API]], available directly at app.ltx.io.

## Positioning

| Tier | Audience | Setup Required |
|------|----------|-----------------|
| LTX API ([[ltx-video-api]]) | Engineers, production integrations | API keys, code, polling logic |
| [[ltx-studio]] | Production teams, agencies | Account, project setup, workflow learning curve |
| **LTX Explore** | Creatives, designers, marketers, producers | None -- browser only |

## Key Features

- **30+ production-ready capabilities**: generation, post-production, audio processing, creative controls, styles, effects, camera motion, and more, all exposed through simple prompts
- **One prompt, one click**: no API integration, no technical setup, no engineering required
- **Community-driven expansion**: new LoRAs and IC-LoRAs are added weekly by the LTX team and the broader creator community; each new asset becomes an available capability automatically, with no action required from existing users


## Video to HDR (SDR-to-HDR)

Announced August 9, 2026, two days before the [[ltx-2.5-model|LTX-2.5]] launch, **Video to HDR** is Explore's SDR-to-HDR conversion tool (direct link: https://app.ltx.io/workflows/templates/video-to-hdr).

- Runs as a **video-to-video pass** on LTX-2.5.
- The model **rebuilds the light data SDR discarded** rather than stretching existing values, so clipped highlights and crushed shadows come back with real detail. LTX frames it as "a reconstruction of the image," not a visual adjustment.
- Output is **scene-linear EXR, float16 with roughly 20-bit effective range**, opening directly in DaVinci Resolve, Nuke or Baselight with **no lossy 8-bit round trip**. In Explore the job returns an **HDR .ZIP of per-frame EXR images**.
- LTX-2.5 reads and writes EXR natively, so the graded file is the file the model produced. If a standard container is preferred, LTX-2.5 can return color-matched video instead of EXR.
- No reshooting and no manual grading -- pitched at upgrading existing libraries and AI-generated footage at scale.
- Target users: post-production teams wanting grading headroom, teams upgrading large libraries, studios and developers building HDR delivery into their own pipelines, and creators improving AI-generated video.

Lineage: the API-side equivalent is the `/v2/video-to-video-hdr` async endpoint (beta since April 23, 2026, still billed on `ltx-2-3-pro` at $0.20 / $0.40 / $0.80 per second of input by resolution tier as of 2026-08-24 -- see [[ltx-api-async-hdr]]). The underlying research was an HDR IC-LoRA on LTX-2.3-22b (April 15, 2026), backed by the paper *LumiVid: HDR Video Generation via Latent Alignment with Logarithmic Encoding*. The August 9 post moves the capability onto LTX-2.5 and into the self-service Explore surface.

## Strategic Context

LTX Explore continues Lightricks' pattern of adding lighter-weight surfaces on top of the core model line -- now [[ltx-2.5-model|LTX-2.5]], previously [[ltx-2.3-model|LTX-2.3]] -- following [[ltx-studio-canvas|Canvas]] (April 2026) and [[ltx-studio-flows|Flows]] (May 2026) -- aimed at widening the top of the funnel for creators who want neither a full production-suite subscription nor a developer API integration.

## See Also
- [[ltx-2.5-model]]
- [[ltx-2.5-technical]]
- [[ltx-api-async-hdr]]
- [[ltx-studio]]
- [[ltx-studio-canvas]]
- [[ltx-studio-flows]]
- [[ltx-video-api]]
- [[ltx-ecosystem]]
