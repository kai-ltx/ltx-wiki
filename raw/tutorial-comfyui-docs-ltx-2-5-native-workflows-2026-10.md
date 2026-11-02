# ComfyUI Docs: LTX-2.5 Native Workflows (T2V, I2V, FLF2V, DFR)

**Source:** https://docs.comfy.org/tutorials/video/ltx/ltx-2-5
**Date:** 2026-10-27 (approx.; search metadata showed the page about six days old on 2026-11-02, no explicit date on page)
**Retrieved:** 2026-11-02

## Content

Official ComfyUI documentation page for LTX-2.5 native (local) workflows, distinct from the API partner-node guide.

- Four native workflows in Template Library > Video: Text-to-Video, Image-to-Video, FLF2V (first-last frame), and DFR (Diffusion Fidelity Rendering: distilled transformer plus a detailing IC-LoRA; keyframes generated inside the clip reused as guides by later passes; runs from image or text via "Switch to T2V"; has its own page ltx-2-5-dfr).
- Gated weights: must request access to Lightricks/LTX-2.5 and Lightricks/LTX-2.5-22b-IC-LoRA-Pixel-Spatial-Upscaler on Hugging Face and wait for approval; downloads fail otherwise.
- Default model set (T2V/I2V):
  - diffusion_models/ltx-2.5-22b-distilled-transformer-comfy-int8-convrot.safetensors
  - text_encoders/gemma4-12b-with-proj-ltx-2.5-comfy-int8-convrot.safetensors
  - text_encoders/gemma4_e2b_it_int8_convrot.safetensors (optional, Comfy-Org/gemma-4 repo, only for prompt enhancer)
  - vae/ltx-2.5-video-vae-bf16.safetensors, vae/ltx-2.5-audio-vae-bf16.safetensors
  - latent_upscale_models/ltx-2.5-latent-spatial-upscaler-x2-bf16-1.0.safetensors (not used by FLF2V)
- Prompt enhancer off by default; enabling prompt_enhance needs the ~5 GB enhancer model and adds about 1 to 2 minutes.
- Prompting tips: one flowing paragraph with shot type, scene, action, characters, camera; describe audio/dialogue; for I2V describe what happens next and do not re-describe the frame; FLF2V frames should share aspect ratio.
- Cloud: Comfy Cloud updates after ComfyUI stable release; templates missing means outdated ComfyUI.
- Note: the Resources section links github.com/Lightricks/LTX-Video, while LTX-2.x code lives in Lightricks/LTX-2.
