# LTX "Built for Post-Production" Release Wave (Sep 29 - Oct 2, 2026)

**Source:** https://ltx.io/release-notes
**Date:** 2026-09-29 to 2026-10-02
**Retrieved:** 2026-10-05

## Content

Lightricks shipped a dense run of open-source post-production capabilities across four consecutive release-notes entries, culminating in an Oct 2 bundle announcement titled "LTX for Post-Production." All items are tagged "Open source" (i.e., ship as weights/IC-LoRAs usable locally, not API-exclusive).

**Sep 29, 2026 — Built for Detail and Resolution:**
- **Native Resolution** — processes footage at full delivery resolution on a single GPU; VRAM consumption increases only slightly as resolution climbs.
- **Refine** — an IC-LoRA that improves sharpness in blurry or pixelated footage. Combine with the 8K workflow to upscale to 8K and beyond.
- **Restore** — an IC-LoRA that adds vibrant color and modernizes archival or faded video. Combine with the 8K workflow to reach 8K and beyond.

**Sep 30, 2026 — Built for Color and Dynamic Range:**
- **HDR Native** — takes 16-bit EXR in, returns 16-bit EXR out through an ACES workflow, preserving color/dynamic range so output arrives ready to grade rather than flattened.
- **SDR to HDR (Upgraded)** — expands 8-bit SDR footage into 16-bit EXR in scene-linear ACEScg, ready to grade in a color-managed pipeline or encode for HDR displays.

**Oct 1, 2026 — Built for Compositing:**
- **Layout to Render** — generates a polished render from 3D blocking with a prompt or reference image, maintaining camera, composition, and frame alignment.

**Oct 2, 2026 — "LTX for Post-Production" (umbrella announcement, six capabilities total):**
Combines everything above plus a new capability:
- **Alpha Gen** — generates alpha mattes with soft edges and fine detail, preserving hair, smoke, and partial transparency for compositing.
- Reiterates Layout to Render, HDR Native, SDR to HDR (Upgraded), Native Resolution, and "Refine & Restore" (the Sep 29 Refine/Restore IC-LoRAs, now bundled under one name).

Framing: "Six new and upgraded capabilities give post-production teams more control over compositing, color, detail, and resolution, with outputs they can keep shaping throughout the pipeline."

## Related

Day-one ComfyUI integration for the Native Resolution / Refine / Restore trio shipped the same week — see the companion tutorial raw file on Tiled Fusion workflows (PR #570 in Lightricks/ComfyUI-LTXVideo, merged 2026-09-29).
