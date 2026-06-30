# LTX-2.3 3DREAL IC-LoRA — 3D Render to Photorealistic Video (June 26, 2026)

**Source:** https://comfyui-wiki.com/en/news/2026-06-29-ltx-2-3-3dreal-lora-render-to-real
**Date:** 2026-06-26
**Retrieved:** 2026-06-30

## Content

On June 26, 2026, **Lovis Odin** (@OdinLovis) in collaboration with **fal.ai** released the **LTX-2.3 3DREAL IC-LoRA**, an in-context LoRA adapter for LTX-Video that converts rough 3D renders and CG viewport blockouts into photorealistic, cinematic-quality video — while faithfully preserving the original composition, camera movement, and scene layout.

### What It Does

Turns a low-poly 3D blockout, Blender viewport render, game-engine output, or any CG/synthetic render into a fully photorealistic video. **Key innovation:** the exact camera path and composition from the 3D input are preserved — 3D artists iterate in their familiar tools, then use the adapter for final photorealistic polish.

### Key Features

- **Preserves camera motion and composition** — follows the exact camera path from the 3D input
- **IC-LoRA architecture** — uses LTX-Video's in-context LoRA mechanism for stable, predictable results
- **Two variants:** Light (faithful, close to input) and Strong (more aggressive photorealism)
- **Trigger word:** prepend `3DREAL` to your prompt
- Optional first-frame photoreal reference image to guide style

### Model Details

| Property | Value |
|----------|-------|
| Base model | Lightricks LTX-Video (LTX-2.3) |
| Architecture | IC-LoRA |
| Pipeline | Image-to-Video / Video-to-Video |
| Trigger word | `3DREAL` |
| Release date | June 26, 2026 |
| Created by | Lovis Odin with fal.ai |

### Access

- **fal.ai endpoint (no download required):** `fal-ai/ltx-2.3-quality/render-to-real` at https://fal.ai/models/fal-ai/ltx-2.3-quality/render-to-real
- **Local LoRA weights:** `3DREAL-light.safetensors` and `3DREAL-strong.safetensors`
- **HuggingFace:** https://huggingface.co/fal/LTX-2.3-3DREAL-LoRA

### Use Cases

- 3D artists previewing photorealistic results before committing to a full render
- Game developers turning engine viewports into cinematic trailers
- Architecture visualization — blockout geometry to realistic walkthrough
- Pre-visualization — camera angle exploration with instant photorealistic feedback
