# Community Release: LTX-2.3 IC-LoRA Cameraman V1 (May 22, 2026)

**Source:** https://www.stablediffusiontutorials.com/2026/05/ltx2.3-cameraman-ic-lora.html
**Date:** 2026-05-22
**Retrieved:** 2026-05-25

## Content

A community member (Cseti) released **LTX2.3-22B_IC-LoRA-Cameraman_v1** on May 22, 2026, published as a tutorial on Stable Diffusion Tutorials blog and the model on Hugging Face at `Cseti/LTX2.3-22B_IC-LoRA-Cameraman_v1`.

### What It Does

The Cameraman IC-LoRA is an **In-Context LoRA (IC-LoRA) adapter** for LTX-Video 2.3 (22B) that specializes in **video-to-video camera motion transfer**. It solves a long-standing problem in AI video generation: reproducing specific cinematic camera movements from a reference video.

**Supported camera motions:**
- Pans (horizontal rotation)
- Tilts (vertical rotation)
- Zoom-in / zoom-out
- Orbit clockwise/counter-clockwise
- Compound motions: e.g., zoom_in + tilt_up, orbit_cw + pan_left

### Training Details

- **Base model:** LTX-Video 2.3 (22B parameters)
- **Framework:** ltx-trainer (Lightricks official)
- **Strategy:** IC-LoRA video-to-video
- **Dataset:** Curated by camera motion type, balanced across categories
- **Resolution buckets:** 768x512×57, 768x512×89, 768x512×121 frames
- **First-frame conditioning:** Set to 0.2 for scene consistency
- **Checkpoint:** _10500.safetensors (v1)

### Installation & Usage (ComfyUI)

1. Update ComfyUI to latest via Manager
2. Set up base LTX-2.3 (I2V) models
3. Download `LTX2.3-22B_IC-LoRA-Cameraman_v1_10500.safetensors` from HuggingFace
4. Place in `ComfyUI/models/loras/`
5. Load workflow (LTX-2.3-IC-Lora-CameramanV1.json) from HF datasets repo
6. Load reference image + reference video, apply LoRA to LoRA model loader node
7. **Important:** Do NOT include camera movement descriptions in the text prompt — the model reads motion from the reference video directly

### Limitations

- Initial version, trained on "lesser dataset" — may produce unusual results in some cases
- No trigger word needed
- Works best with clear, distinct camera motion in reference video

### Community Reception

Also available as a ComfyUI workflow on RunComfy: https://www.runcomfy.com/comfyui-workflows/ltx-2-3-ic-lora-in-comfyui-v2v-motion-track-video-workflow

Model also uploaded to Civitai: https://civitai.com/models/2525197/cameraman-ic-lora-for-ltx23-22b

### Significance

This release highlights a growing ecosystem of community-built IC-LoRA adapters for LTX-2.3, extending the model's capabilities beyond what Lightricks ships officially. Camera motion control — separate from scene content — is increasingly recognized as a critical dimension of cinematic AI video quality.
