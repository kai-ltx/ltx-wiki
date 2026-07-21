# Tutorial — LTX-2.3 Video Outpainting in ComfyUI

**Source:** https://www.mimicpc.com/workflows/ltx-23-video-outpainting-easy-expand-any-video-canvas-in-comfyui ; https://www.youtube.com/watch?v=L22ARC8GzYI ; https://huggingface.co/spaces/linoyts/LTX-2-3-outpaint
**Date:** 2026-07-13 to 2026-07-15 (published shortly after the API feature's 2026-07-13 release)
**Retrieved:** 2026-07-21

## Content

Following the official Video Outpainting/Reframe API launch (2026-07-13), the community shipped ready-to-use tutorials and hosted workflows within days:

- **MimicPC workflow**: "LTX 2.3 Video Outpainting (Easy) — Expand Any Video Canvas in ComfyUI" — a packaged, hosted ComfyUI workflow (no local setup) for canvas expansion using LTX-2.3.
- **YouTube tutorial**: "ComfyUI Tutorial: Extend Your Videos with LTX 2.3 Outpainting" — walkthrough of node setup for outpainting in ComfyUI.
- **HuggingFace Space** `linoyts/LTX-2-3-outpaint`: a hosted, no-install Space demonstrating the outpainting IC-LoRA directly in-browser.
- The underlying LoRA config lives in the Lightricks/LTX-2 GitHub repo at `packages/ltx-trainer/configs/video_outpainting_lora.yaml`, meaning users can also retrain/fine-tune their own outpainting adapters using the official LTX Trainer (unified framework, released June 17, 2026).

**Practical workflow pattern:** upload source video, choose target aspect ratio, the workflow runs two-stage generation (coarse outpaint region, then seam-refinement pass) and outputs an expanded-canvas video with preserved motion/composition in the original frame. Useful for repurposing a single video across multiple social aspect ratios without reshooting.
