# ComfyUI IC-LoRA Motion Track Workflow for LTX-2.3

**Source:** https://www.runcomfy.com/comfyui-workflows/ltx-2.3-ic-lora-in-comfyui-v2v-motion-track-video-workflow
**Date:** 2026-06-03
**Retrieved:** 2026-06-08

## Content

### Overview

RunComfy published a ComfyUI workflow for LTX-2.3 IC-LoRA Motion Track video-to-video generation. This enables fine-grained motion control using sparse point trajectories within ComfyUI.

### Workflow Steps

1. Load LTX-2.3-22b base model + IC-LoRA Motion Track Control adapter (`Lightricks/LTX-2.3-22b-IC-LoRA-Motion-Track-Control`)
2. Provide a reference video
3. Extract point tracks using SpatialTrackerV2 (or draw manually using colored spline overlays)
4. Use tracks as conditioning signal alongside text prompt
5. Generate video that follows the defined motion trajectories

### Union Control ComfyUI Workflow (Additional)

Also available on comfy.org: "AI on the Lot 2026_LTX-2.3_IC LoRA (Union Control)" — this workflow combines Canny + Depth control signals in a single adapter pass for video editing.

### Python Usage

GitHub issue #203 in Lightricks/LTX-2 documents how to use both `IC-LoRA-Union-Control` and `IC-LoRA-Motion-Track-Control` via Python. Key points:
- Both adapters load on top of the LTX-2.3-22b base
- Union Control accepts a dict of control types
- Motion Track accepts trajectory tensors (sparse point tracks)

### LTX-2.3 Diffusers Status

- As of June 2026, Diffusers support for LTX-2.3 is still listed as "coming soon"
- Modular support for LTX-2 (19B) is in Diffusers
- LTX-2.3 (22B) requires Python 3.12+, CUDA 12.7+, PyTorch 2.7
- Official inference recommended via `ltx-video` PyPI package or LTX-2 GitHub repo

### fal.ai LTX Pricing (June 2026)

- LTX Video 2.0 Pro on fal.ai: $0.06/s at 1080p, $0.12/s at 1440p, $0.24/s at 2160p
- LTX-2-19B on fal.ai: $0.0018/megapixel (a 121-frame 1280×720 video ≈ $0.20)
- Both LTX-2 and LTX-2.3 checkpoints available on Replicate
