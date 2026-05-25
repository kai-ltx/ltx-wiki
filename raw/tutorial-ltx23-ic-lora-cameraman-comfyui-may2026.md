# Tutorial: LTX-2.3 IC-LoRA Cameraman V1 in ComfyUI (May 2026)

**Source:** https://www.stablediffusiontutorials.com/2026/05/ltx2.3-cameraman-ic-lora.html
**Secondary:** https://www.runcomfy.com/comfyui-workflows/ltx-2-3-ic-lora-in-comfyui-v2v-motion-track-video-workflow
**Date:** 2026-05-22
**Retrieved:** 2026-05-25

## Content

Community tutorial published May 22, 2026 covering the **IC-LoRA Cameraman V1** adapter for LTX-Video 2.3.

### What It Solves

Most AI video models generate random or weakly-controlled camera movement. The Cameraman LoRA solves this by reading cinematic motion patterns directly from a reference video and replicating them:
- Pans, tilts, zooms (simple)
- Orbit shots, compound motions (complex)
- Smooth motion transfer without descriptor prompts

### Setup Requirements

1. ComfyUI (updated to latest)
2. Base LTX-2.3 I2V models and VAE
3. `LTX2.3-22B_IC-LoRA-Cameraman_v1_10500.safetensors` from: `https://huggingface.co/Cseti/LTX2.3-22B_IC-LoRA-Cameraman_v1`
4. Place LoRA in `ComfyUI/models/loras/`

### Workflow

- Download: `LTX-2.3-IC-Lora-CameramanV1.json` from HuggingFace datasets
- Load reference image + reference video into respective nodes
- Load LTX-2.3 model + VAE + text encoders normally
- Load IC-LoRA into **LoRA model loader only** node (not standard LoRA stack)
- Prompt: **do NOT describe camera movements** — the model infers them from reference video

### Key Prompting Rule

> "Avoid using overly descriptive prompts related to camera movements as they can contradict the model's output. The model can easily sense and replicate the motion from your reference video."

### RunComfy Workflow

Available as a hosted ComfyUI workflow at RunComfy for one-click use:
- URL: https://www.runcomfy.com/comfyui-workflows/ltx-2-3-ic-lora-in-comfyui-v2v-motion-track-video-workflow
- Labeled as "V2V Motion Track Video Workflow"

### Related Resource

Also see: LTX-2.3 ID LoRA LipSync tutorial (also May 2026) at:
https://www.stablediffusiontutorials.com/2026/05/ltx2.3-id-lora.html
