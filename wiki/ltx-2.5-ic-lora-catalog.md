---
title: LTX-2.5 IC-LoRA Catalog
type: technical
created: 2026-10-12
updated: 2026-10-12
sources:
  - raw/ltx-news-ltx-2-5-ic-lora-catalog-official-docs-2026-10.md
  - raw/tutorial-ltx-2-5-ic-lora-ingredients-colorization-day-to-night-recipes-2026-10.md
tags:
  - ltx-2-5
  - ic-lora
  - adapters
  - vfx
  - post-production
  - ingredients
  - colorization
---

# LTX-2.5 IC-LoRA Catalog

The official LTX docs now publish a versioned catalog of task-specific [[ic-lora|IC-LoRA]] adapters, split into those usable with [[ltx-2.5-model|LTX-2.5]] and those that remain LTX-2.3-only. Adapters live in the Hugging Face **LTX-2.5 Creative Lab** collection (15 items at retrieval on 2026-10-12). All are gated repos under the `ltx-2.x-community-license` and run on the distilled LTX-2.5 stack in ComfyUI or via `ltx_pipelines.ic_lora`.

The docs give one blunt rule: **the model card is the source of truth** for inputs, prompt wording, loader and settings, and an LTX-2.3-trained card is not a guarantee of LTX-2.5 compatibility. Several LTX-2.5 workflows deliberately load an LTX-2.3 checkpoint, so do not swap similarly named files.

## Catalog (LTX-2.5 column = where the adapter works today)

| Adapter | Purpose | Checkpoint generation |
|---|---|---|
| Union Control | depth + canny + pose in one adapter | LTX-2.3 checkpoint, LTX-2.5 workflow |
| Motion Control | spline trajectories via Draw Tracks / Sparse Track Editor nodes | LTX-2.3 checkpoint, LTX-2.5 workflow |
| Ingredients | reference-sheet consistency for characters, props, locations | dedicated LTX-2.5 adapter |
| Pixel Spatial Upscaler | generative 2x (LTX-2.5) upscale from ~280p drafts | LTX-2.5 (2x only); LTX-2.3 has 2x and 4x |
| In-Outpainting | extend canvas / fill masked regions | LTX-2.3 checkpoint |
| Instant Shave | beard and stubble removal | LTX-2.3 checkpoint |
| Water Simulation | rain, rivers, surf, splashes, reflections | LTX-2.5 |
| Colorization | color for grayscale footage | LTX-2.5 |
| Decompression / Deblurring | artifact removal / sharpness restoration | LTX-2.5 |
| Day to Night | same shot re-rendered at night | LTX-2.5 |
| Clean Plate | remove moving subjects, rebuild background | LTX-2.5 |
| SDR to HDR | EXR (scene-linear ACEScg) plus BT.2020/HLG master | LTX-2.5 (separate from the legacy LogC3 HDR adapter) |
| Layout to Render | 3D playblast to finished shot | LTX-2.5 |
| Refine Details / Restore | synthesized detail (Tiled Fusion) / restoration | LTX-2.5; the Tiled Fusion graph selects Refine Details only |
| Alpha Gen (Beta) | grayscale alpha matte from RGB video | LTX-2.5 |

**LTX-2.3-only:** Cross-Eyed, Dub-It (Beta, lip-synced speech regeneration, see [[paper-just-dub-it]]), Relight (Sun Direction).

The post-production subset (SDR to HDR, Layout to Render, Alpha Gen, Refine/Restore, Native Resolution) is the "Built for Post-Production" wave covered in [[ltx-2.5-comfyui-integration]] and [[ltx-2.5-model]].

## Ingredients (Reference Sheet Control)

- **Input:** one composite reference sheet (a clean panel per element, black background, no text) fed as a **static video of at least 121 frames** at output resolution.
- **Prompt:** two parts, `Reference sheet: ...` then `Generated video: ...` (action, dialogue, camera).
- **Trained bucket:** 768x448, 121 frames, 24 fps only; other sizes are out of distribution. 12,000 steps, rank 128, on the LTX-2.5-22B dev base.
- **Tips:** larger panels transfer better; give each character a face close-up plus turnaround; elements missing from the sheet will not appear.
- **Uptake:** by far the most downloaded adapter in the set (7,623 monthly downloads and 55 likes at retrieval, versus a few hundred for Colorization and Day-to-Night). Demos are brand-mascot ads and multi-character dialogue scenes, which makes it the LTX answer to reference-based consistency, a gap against [[competitor-kling|Kling]]'s 15-asset Omni Reference and [[competitor-veo|Veo]]'s "Ingredients to Video".
- **Gotcha:** the shipped ComfyUI workflow currently loads the LTX-2.3 Ingredients checkpoint while the LTX-2.5 card names a different file. Use exactly what the workflow or card specifies.

## Colorization

- Restores color to grayscale or desaturated footage while preserving identity, framing and geometry; it is not a deblur, denoise or upscale model.
- **Prompt convention:** `Reference shows {gray scene}. Edited shows the same scene with natural colors restored. COLORIZE {vivid color description}. Subject identity, framing, and background geometry are identical to the reference; only color information differs...`
- **Trained at 960x544x121 @ 24 fps**; far higher resolutions weaken the effect.
- **Recipe:** distilled pipeline, stage-1-only native hi-res (`--skip-stage-2 --tile-reference-encode`), strength 1.0, seed 42. The distilled checkpoint uses fixed sigmas, so there is **no CFG and no negative prompt**. Drop strength to 0.8-0.9 for color bleed.

## Day-to-Night Relighting

- Re-renders a daytime clip as the same shot at night, frame for frame. Trained on **192 motion-aligned day/night pairs**, rank 32, 3,000 steps.
- **Trained at 768x448 / 448x768, 97 frames @ 24 fps (~4 s);** longer clips drift late. Re-encode the reference to clean 24 fps H.264 first because the loader does not resample time.
- **Settings:** 30 steps, guidance 3.0 to 4.0 (lower is brighter, higher is darker), STG `stg_v` scale 1.0 block 29. The prompt steers night style and color temperature; no mask support.

## Timeline and caveats

- **2026-06-17:** [[ltx-video-trainer|LTX Trainer]] launched with ten demo IC-LoRAs (LTX-2.3 era) and a first-party agentic skill that lets an agent run the training loop. Training a custom LoRA on a ~19B base was estimated at hundreds to thousands of dollars in GPU time by one reviewer.
- **~2026-09-08 to 09-10:** per a search-engine summary (not confirmed on a primary page), LTX-2.5 ports of the V2V IC-LoRAs shipped. Treat the exact dates as unverified; the adapters were a wiki coverage gap rather than a new release in the 2026-10-05 to 10-12 window.
- No community reaction threads specific to these adapters were found this cycle.

## See Also

- [[ic-lora]] -- technique overview and earlier adapter generations
- [[ltx-2.5-model]] -- base model
- [[lora-ecosystem]] -- full LoRA inventory
- [[training-dataset-preparation]] -- dataset prep for custom IC-LoRAs
