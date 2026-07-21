# Video Outpainting API (Reframe) — LTX Ships Production Aspect-Ratio Reframing

**Source:** https://ltx.io/release-notes ; https://docs.ltx.video/api-changelog/2026/7/13
**Date:** 2026-07-13
**Retrieved:** 2026-07-21

## Content

LTX shipped a production-grade "Video Outpainting" (internally/marketing-named "Reframe") API endpoint that reframes video to new aspect ratios by generating new pixels beyond the original frame, rather than cropping.

**What shipped:**
- New Reframe API endpoint
- Native 1080p output
- Supports source videos up to 60 seconds

**Supported aspect ratios:**
- 1:1 (720x720, 1080x1080)
- 4:5 (720x900, 1080x1350)
- 5:4 (900x720, 1350x1080)
- 9:16 (720x1280, 1080x1920)
- 16:9 (1280x720, 1920x1080)

**Key capabilities:**
- Expands the canvas without modifying existing pixels; only generates the newly exposed regions
- Preserves composition, motion, on-screen text, logos, and overall visual consistency
- Stable across large aspect-ratio jumps (e.g., 16:9 to 9:16)
- Designed for production pipeline integration (e.g., repurposing a single hero video into multiple social aspect ratios)

**Technical approach** (per community writeups, e.g. Medium "LTX Reframe Solved the Biggest Headache in Multi-Platform Video" and MimicPC ComfyUI workflow guide): two-stage seam blending — coarse generation of the new region first, followed by refined boundary smoothing — plus mask-conditioned outpainting so the model distinguishes "new canvas" pixels from "original" pixels, avoiding visible seams.

A related outpainting IC-LoRA for LTX-2.3 (community-trained, not the same as the official API endpoint) is also circulating — e.g. a HuggingFace Space `linoyts/LTX-2-3-outpaint` and ComfyUI workflows referencing `video_outpainting_lora.yaml` in the Lightricks/LTX-2 GitHub repo — indicating outpainting has become a first-class capability across both the API and open-source/ComfyUI paths.
