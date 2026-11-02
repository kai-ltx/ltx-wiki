# LTX Blog: "LTX's Latest VFX Tools: Built for the Production Pipeline" (Doug Hogan / Mohamed Oumoumad)

**Source:** https://ltx.io/blog/ltxs-latest-vfx-tools-built-for-the-production-pipeline
**Date:** 2026-10-26
**Retrieved:** 2026-11-02

## Content

- Official LTX blog post (Tutorials category, author "LTX Team"), a video conversation between compositor Doug Hogan and Mohamed Oumoumad walking through the Sep 29 to Oct 2, 2026 post-production capability wave. No new model or adapter is announced; this is a demo/explainer of already-shipped tools.
- Tools covered: Alpha Gen (soft mattes with partial transparency from footage shot without green screen), Refine and Restore (archival footage), upgraded SDR to HDR IC-LoRA (rebuilds highlight range, outputs 16-bit EXR), Native HDR (keeps shot dynamic range).
- Native Resolution described as a tiled workflow: each tile overlaps its neighbour and the blend happens at every denoising step, so tiles resolve into one image. Demo: Doug takes an HD loom plate to 8K HDR and checks the highlight range in Nuke.
- Open weights / fine-tuning angle: Oumoumad notes Alpha Gen is an IC-LoRA trained on rendered footage with clean alpha, and suggests studios can train their own IC-LoRAs for their data.
- Context: the official release-notes page still shows Oct 13, 2026 (LTX Trainer in Explore) as the newest entry as of Nov 2, 2026. No LTX release-notes entries dated Oct 14 to Nov 2.
