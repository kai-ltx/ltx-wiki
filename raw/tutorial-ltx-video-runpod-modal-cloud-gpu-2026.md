# Running LTX Video 2.3 on RunPod and Modal (2026 Guide)

**Source:** https://ltx-23.app/blog/ltx-video-23-runpod ; https://modal.com/docs/examples/ltx ; https://modal.com/docs/examples/image_to_video
**Date:** 2026-04-15
**Retrieved:** 2026-05-19

## Content

### LTX-2.3 on RunPod

LTX Video 2.3 is one of the best open-source AI video models, generating cinematic footage from text or images at native 4K. RunPod provides on-demand GPU pods suitable for running it.

**Recommended GPU:** A40 (48 GB VRAM) for full-quality LTX-2.3; RTX 4090 (24 GB) usable with fp16 quantization.

**Setup Steps (RunPod):**

1. Create a RunPod pod with the `runpod/pytorch:2.4.0-py3.11-cuda12.4.1-devel-ubuntu22.04` template.
2. SSH into the pod and install dependencies:
   ```bash
   pip install ltx-video diffusers accelerate transformers
   ```
3. Download the LTX-2.3 model checkpoint from Hugging Face:
   ```bash
   huggingface-cli download Lightricks/LTX-2.3 --local-dir ./models/ltx-2.3
   ```
4. Launch ComfyUI (if using workflow-based generation):
   ```bash
   git clone https://github.com/comfyanonymous/ComfyUI
   cd ComfyUI && pip install -r requirements.txt
   python main.py --listen 0.0.0.0 --port 8188
   ```
5. Install the LTXVideo custom nodes:
   ```bash
   cd custom_nodes
   git clone https://github.com/Lightricks/ComfyUI-LTXVideo
   pip install -r ComfyUI-LTXVideo/requirements.txt
   ```
6. Forward port 8188 via RunPod's proxy URL to access the ComfyUI web UI.

**Comprehensive tutorial** (Windows + RunPod + cloud):  
https://huggingface.co/blog/MonsterMMORPG/ltx-2-z-image-base-full-tutorial-audio-to-video  
Covers ComfyUI, SwarmUI, models, presets, and workflows for both local and cloud deployment.

---

### LTX-Video on Modal

Modal provides serverless GPU execution with automatic cold-start management.

**Text-to-Video example:**  
https://modal.com/docs/examples/ltx

Key facts:
- A 20-second 480p video at moderate quality takes ~2 seconds on a warm Modal container.
- Modal handles model caching, GPU allocation, and HTTP serving automatically.

**Basic Modal deployment pattern:**

```python
import modal

app = modal.App("ltx-video")
image = modal.Image.debian_slim().pip_install(
    "ltx-video", "diffusers", "accelerate", "transformers", "torch"
)

@app.function(gpu="A100", image=image, timeout=300)
def generate_video(prompt: str, num_frames: int = 120) -> bytes:
    from ltx_video.pipelines import LTXVideoPipeline
    pipe = LTXVideoPipeline.from_pretrained("Lightricks/LTX-2.3")
    pipe = pipe.to("cuda")
    result = pipe(prompt=prompt, num_frames=num_frames)
    return result.video_bytes

@app.local_entrypoint()
def main():
    video = generate_video.remote("A surfer at golden hour, cinematic")
    with open("output.mp4", "wb") as f:
        f.write(video)
```

**Image-to-video on Modal:**  
https://modal.com/docs/examples/image_to_video  
Demonstrates animating a still image using LTX-Video's image conditioning pipeline.

---

### LTX-2 PyTorch API (self-hosted)

Official docs: https://docs.ltx.video/open-source-model/integration-tools/pytorch-api  
PyPI package: https://pypi.org/project/ltx-video/

```bash
pip install ltx-video
```

Provides native Python pipelines without needing diffusers, with access to IC-LoRA, advanced guidance parameters, and all LTX-2.3 features.

### References

- https://www.runpod.io/blog/ltxvideo-open-source-video
- https://ltx-23.app/blog/ltx-video-23-runpod
- https://modal.com/docs/examples/ltx
- https://modal.com/docs/examples/image_to_video
- https://huggingface.co/blog/MonsterMMORPG/ltx-2-z-image-base-full-tutorial-audio-to-video
