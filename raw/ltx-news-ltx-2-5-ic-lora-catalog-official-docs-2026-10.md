# LTX-2.5 IC-LoRA Catalog: Official Docs Snapshot (Ingredients, Colorization, Day-to-Night, Restoration, VFX)

**Source:** https://docs.ltx.io/open-source-model/integration-tools/ic-lo-ra-adapters
**Date:** 2026-10-12 (living docs page, snapshot at retrieval; adapter port dates per secondary source below)
**Retrieved:** 2026-10-12

## Content

The official LTX docs page "IC-LoRA Adapters" now carries a versioned **LTX IC-LoRA catalog** split into "Available with LTX-2.5" and "LTX-2.3-only adapters", and points to two Hugging Face collections: **LTX-2.5 Creative Lab** (collection page showed 15 items, "updated 7 days ago" at retrieval) and LTX-2.3 Creative Lab. The page banner also repeats that **V1 video generation endpoints stop working after October 26, 2026 at 11:59 PM UTC** (migrate to V2; already tracked in [[ltx-video-api-endpoints]]).

Doc guidance: "The model card is the source of truth for an adapter's required inputs, prompt wording, loader, and settings. A model card trained on LTX-2.3 is not, by itself, a guarantee of LTX-2.5 compatibility." Some LTX-2.5 workflows intentionally load an LTX-2.3-trained adapter; do not substitute similarly named checkpoints.

### Available with LTX-2.5 (16 rows)
| Adapter | What it does | Notes |
|---|---|---|
| Union Control | depth + canny + pose in one checkpoint | adapter card is the LTX-2.3 checkpoint; LTX-2.5 distilled workflow provided |
| Motion Control | sparse spline trajectories (LTX Draw Tracks, LTX Sparse Track Editor nodes) | LTX-2.3 checkpoint, LTX-2.5 workflow |
| Ingredients | reference-sheet consistency (characters, props, locations) | dedicated LTX-2.5 adapter + single-stage distilled workflow; the workflow JSON currently loads the LTX-2.3 Ingredients checkpoint while the LTX-2.5 card names a separate LTX-2.5 checkpoint, so follow the exact file the workflow or card specifies |
| Pixel Spatial Upscaler | creative 2x (LTX-2.5) / 2x+4x (LTX-2.3) upscale, generative not faithful | recommended: draft at ~280p then upscale |
| In-Outpainting | extend canvas / fill masked regions | LTX-2.3 checkpoint |
| Instant Shave | removes beards/stubble | LTX-2.3 checkpoint, generic V2V workflow |
| Water Simulation | rivers, rain, surf, splashes, wet reflections | LTX-2.5 adapter |
| Colorization | restores color to grayscale/desaturated video | LTX-2.5 adapter |
| Decompression | removes compression artifacts | LTX-2.5 adapter |
| Deblurring | restores sharpness to out-of-focus video | LTX-2.5 adapter |
| Day to Night | re-renders daytime shot as same shot at night | LTX-2.5 adapter |
| Clean Plate | removes moving subjects to rebuild background plate | LTX-2.5 adapter |
| SDR to HDR | SDR to HDR EXR (scene-linear ACEScg) + BT.2020/HLG master | LTX-2.5 files `...sdr-to-hdr-1.0` and `...-scene-emb`; legacy LTX-2.3 HDR adapter uses a separate LogC3 stack |
| Layout to Render | 3D viewport/playblast to finished shot | LTX-2.5 adapter |
| Refine Details | synthesized detail via Tiled Fusion Upscale workflow | Restore adapter is published separately and NOT selected by that graph |
| Restore | separate LTX-2.5 restoration adapter | |

**Alpha Gen (Beta)** also has an LTX-2.5 adapter: frame-aligned grayscale alpha matte, empty prompt, strength 1.0, source limited to 1920x1088, 121 frames or fewer recommended (8n+1 up to 145 may work, longer unsupported), no prompt/mask subject selection.

### LTX-2.3-only adapters
Cross-Eyed, Dub-It (Beta, lip-synced speech regeneration), Relight (Sun Direction).

## Timeline context (secondary sources)

- **2026-06-17:** Lightricks launched LTX Trainer (framework for LoRA/IC-LoRA training across video, audio, cross-modal, reference-conditioned) with ten demo effects (Water Simulation, Ingredients, In/Outpainting, Day to Night, Colorization, Instant Shave, Cross-Eyed, Deblurring, Decompression) plus a first-party agentic skill that lets an agent drive training end to end. Source: https://www.scopeful.org/blog/ltx-trainer-10-fine-tunable-effects (published 2026-06-18). Scopeful's cost estimate for training a custom LoRA on a ~19B base: "hundreds to thousands of dollars" of GPU time.
- **~2026-09-08 to 09-10:** a search-engine summary (not verified against a primary page) dates the LTX-2.5 ports of the video-to-video IC-LoRAs (Deblur, Decompression, Colorization, Water Simulation, Clean Plate, Day-to-Night, Ingredients, a Cinemagraph style LoRA, a Slow Motion Control I2V LoRA) to Sep 8-10. So these are a coverage gap in the wiki, not brand-new in the Oct 5-12 window.
- Hugging Face downloads (last month, retrieval): Ingredients 7,623; Day-To-Night 562; Colorization 509. Likes: Ingredients 55, Day-To-Night 9, Colorization 7. Ingredients is clearly the breakout adapter.
