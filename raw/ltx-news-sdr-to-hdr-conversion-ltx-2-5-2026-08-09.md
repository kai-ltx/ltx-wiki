# SDR to HDR: Automatic HDR Video Conversion with LTX-2.5, Live in LTX Explore

**Source:** https://ltx.io/blog/sdr-to-hdr
**Date:** 2026-08-09
**Retrieved:** 2026-08-24

## Content

Published two days before the LTX-2.5 launch, this post documents LTX-2.5's **SDR-to-HDR** conversion capability and its availability in **LTX Explore** (the self-service platform launched July 20, 2026), where the tool is named **"Video to HDR."**

Key facts:
- The model **rebuilds the light data SDR discarded** rather than stretching existing values, so clipped highlights and crushed shadows come back with real detail. LTX frames it as "a reconstruction of the image," not a visual adjustment.
- Output is a **scene-linear EXR file, float16 with roughly 20-bit effective range**, opening directly in DaVinci Resolve, Nuke or Baselight with **no lossy 8-bit round trip**. In Explore it returns an HDR **.ZIP of per-frame EXR images**.
- Runs as a **video-to-video pass**. LTX-2.5 reads and writes EXR natively, so the graded file is the file the model produced. If the user prefers a standard container, LTX-2.5 can return color-matched video instead of EXR.
- No reshooting and no manual grading — pitched at upgrading existing libraries and AI-generated footage at scale.
- Target users: post-production teams wanting grading headroom, teams upgrading large libraries, studios/developers building HDR delivery into their own pipelines, and creators improving AI-generated video.
- LTX Explore is described as offering **30+ tools** spanning generation, post-production, audio and creative controls; direct link: https://app.ltx.io/workflows/templates/video-to-hdr

Context/lineage: the API side of this capability is the `/v2/video-to-video-hdr` async endpoint (shipped April 23, 2026 in beta, still billed on `ltx-2-3-pro` at $0.20/$0.40/$0.80 per second of input by resolution tier as of 2026-08-24), and the underlying research was an HDR IC-LoRA on LTX-2.3-22b (April 15, 2026), backed by the paper *LumiVid: HDR Video Generation via Latent Alignment with Logarithmic Encoding*. The August 9 post moves the capability onto LTX-2.5 and into the self-service Explore surface.
