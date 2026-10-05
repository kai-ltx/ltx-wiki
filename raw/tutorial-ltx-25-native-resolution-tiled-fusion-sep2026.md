# LTX-2.5 Native Resolution: ComfyUI Tiled Fusion Workflows for Single-GPU 4K/8K V2V

**Source:** https://artrealmai.com/article/ltx-2-5-native-resolution-tiled-fusion (cross-referencing https://comfyui-wiki.com/en/news/2026-09-29-ltx-2-5-native-resolution and the ComfyUI-LTXVideo repo)
**Date:** 2026-09-30 (article); underlying PR merged 2026-09-29
**Retrieved:** 2026-10-05

## Content

**ComfyUI-LTXVideo PR #570** (commit `5722b53`, merged **2026-09-29**) added two new example workflow graphs under `example_workflows/2.5/`: `LTX-2.5_V2V_TiledFusion_Native_4K_8K.json` and `LTX-2.5_V2V_TiledFusion_Upscale.json`. These implement the "Native Resolution" capability announced the same week on ltx.io/release-notes (see companion LTX-news raw file).

**How Native Resolution works (two-stage ladder):**
1. **Composition stage** — resize source to `initial_canvas_size`, run a full-frame pass so the whole frame stays in model context (published example graph uses the Day-to-Night IC-LoRA for this stage).
2. **Refine stage** — enlarge the latent via `ltx-2.5-latent-spatial-upscaler-x2-bf16-1.0.safetensors` (applied twice for the 8K path), then run **Tiled Fusion** with the **Refine Details** IC-LoRA, a fresh look/style prompt, and the original clip (resized to output size) as the stage-2 guide.

**Critical distinction — `LTXVTiledFusionSampler` is NOT `LTXVTiledSampler`:**
- The older `LTXVTiledSampler` samples/blends tiles semi-independently.
- **Tiled Fusion** keeps one shared latent canvas and one shared noise field, steps overlapping spatial crops at every denoise step, and fuses them back so regions share a trajectory — this is what lets FullHD/4K/8K outputs avoid "stitched tile" seams. Overlap reduces seam risk but doesn't eliminate it; inspect tile boundaries and low-frequency gradients on delivery.
- Tiled Fusion addresses diffusion-sampling memory; for decode-only memory pressure, use separate tiled VAE decode nodes after sampling — the two are not interchangeable.

**Get Tiling Sizes node:** emits model-legal canvases (multiples of 32, frame count `8n+1`) from three parameters: `tile_size` (qHD/HD/FullHD sampling tile), `initial_canvas_size` (stage-1 canvas), `output_size` (FullHD/4K/8K). These presets are not a VRAM guarantee — actual peak memory still depends on tile size, temporal window, model stack, and decode settings; benchmark before committing a hero clip.

**Refine Details and Restore IC-LoRAs** (new HF repos under Lightricks, drop into `ComfyUI/models/loras/`):
- **Refine Details** — rebuilds fine texture/edges/grain on soft, compressed, generated, or already-upscaled footage. Trained at 1024x576 tiles; use the tiled workflow even at Full HD.
- **Restore** — cleans/colorizes damaged archive material (low-res web rips, low-bitrate broadcast transfers, tape, sepia/B&W scans). Workflow order matters: **Restore first, then Refine** — refining first can sharpen existing damage and mute inferred color.
- Both are explicitly generative/interpretive tools — they synthesize plausible detail/color rather than recovering lost information; treat rebuilt faces, lettering, and objects as interpretations, not restorations.
- **For 8K specifically**, Lightricks recommends a progressive path: refine to 4K first, Lanczos-resize toward 8K, then an optional gentle second pass — a direct 8K refine risks inventing texture because tiles see content beyond the adapter's trained scale.

**Audio handling:** source audio is encoded, held fixed during generation, then decoded and muxed back into the output video, so dialogue/music beds survive the upscale pass unchanged.

**Access note:** Lightricks HF repos for these components remain gated (request access required) — consistent with the gating friction logged separately in this week's community-reception raw file.

## How to use

```
# Update the official LTX video node pack (Lightricks/ComfyUI-LTXVideo), then load:
# example_workflows/2.5/LTX-2.5_V2V_TiledFusion_Native_4K_8K.json
# example_workflows/2.5/LTX-2.5_V2V_TiledFusion_Upscale.json
```
Pull the version-matched distilled transformer, Gemma-4 text encoder, video/audio VAEs, latent spatial upscaler, and the needed IC-LoRA per the workflow's Model Links note. Run the published graph unmodified before tweaking overlap, streaming windows, or sampler family.
