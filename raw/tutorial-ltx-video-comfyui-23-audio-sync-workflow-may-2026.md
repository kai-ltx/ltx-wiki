# LTX-2.3 Audio-Synced Video Workflow in ComfyUI (May 2026)

**Source:** https://apatero.com/blog/comfyui-ltx-2-3-audio-video-workflow-tutorial-2026
**Date:** 2026-05-01
**Retrieved:** 2026-05-19

## Content

LTX-2.3 received day-0 support in ComfyUI and enables native audio-to-video generation — including lip-sync — as a single-pass generation step, not a post-process overlay.

### Model Overview

- LTX-2.3 is a 22B parameter DiT-based audio-video foundation model, released March 5, 2026 under Apache 2.0.
- Outputs up to 4K at 50 FPS, clips up to 20 seconds.
- Supports text-to-video, image-to-video, and audio-to-video in one unified model.

### Audio-to-Video Workflow Structure

1. Load a portrait image via `LoadImage` node.
2. Provide speech audio via `LoadAudio` or capture live with `RecordAudio`.
3. Feed both streams into the `LTX-2.3 generator` node, which synthesizes frames where the subject speaks in sync with the audio.
4. Encode resulting frames to MP4 using `SaveVideo`.

LTX-2.3's native audio VAE handles lip-sync, mouth movement, facial expressions, and natural head motion all in one generation pass.

### ComfyUI Requirements

- ComfyUI v0.16+
- LTX-2.3 model checkpoint (~44 GB full, ~22 GB for fp16 quantization)
- At least 24 GB VRAM (e.g., RTX 4090 or A100)
- `ComfyUI-LTXVideo` custom node pack from `github.com/Lightricks/ComfyUI-LTXVideo`

### Key New Nodes (released April 1, 2026)

- `LTXVConditioning` — multimodal conditioning combining text + audio + image
- `LTXVScheduler` — step/CFG scheduler tailored to LTX-2.3's distilled model
- `EmptyLTXVLatentVideo` — creates appropriately sized latent tensors for LTX-2.3
- `LTXVSaveConditioning` / `LTXVLoadConditioning` — cache encoded prompts for reuse across runs (reduces latency on iterative workflows)
- `Multimodal Guider` — tune prompt adherence and cross-modal (audio/visual) consistency independently

### Portrait (9:16) Support

LTX-2.3 natively supports portrait orientation. Workflow uses `896×1584` resolution at 24 or 48 FPS for social/mobile output. No crop or resize post-process needed.

### Workflow JSON

Published workflow available at:  
- https://www.comfy.org/workflows/video_ltx2_3_ia2v-adca306765ce/  
- https://docs.comfy.org/tutorials/video/ltx/ltx-2-3

### References

- https://blog.comfy.org/p/ltx-23-day-0-supporte-in-comfyui
- https://github.com/Lightricks/ComfyUI-LTXVideo
- https://www.nextdiffusion.ai/tutorials/ltx-2-3-image-to-video-with-custom-audio-in-comfyui
