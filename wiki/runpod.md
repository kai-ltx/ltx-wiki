---
title: RunPod
type: entity
created: 2026-04-13
updated: 2026-09-28
sources:
  - raw/hosting-runpod-runcomfy.md
  - raw/inference-providers-overview.md
  - raw/cloud-deployment-platforms.md
  - raw/tutorial-ltx-video-runpod-modal-cloud-gpu-2026.md
  - raw/tutorial-ltx-2-5-runpod-deployment-2026-09.md
tags:
  - hosting
  - cloud
  - gpu-rental
  - runpod
  - comfyui
---

# RunPod

RunPod is a cloud GPU rental service for running LTX Video inference without local hardware. It offers on-demand GPU instances, community templates, and serverless API endpoints. It is commonly paired with ComfyUI for visual workflow-based video generation.

**Website:** https://www.runpod.io
**Setup guide:** https://www.runpod.io/blog/ltxvideo-comfyui-runpod-setup

See also: [[inference-providers-overview]], [[runcomfy]]

## Setup Options

### 1. Manual Setup
Spin up a GPU instance via JupyterLab and terminal, then install ComfyUI and LTX-Video manually. Gives maximum flexibility.

### 2. Community Templates
Pre-configured templates available on Civitai and RunPod marketplace:
- **LTX 13B T2V/I2V - ComfyUI** -- Pre-configured template with workflows included
- **LTX-2 on RunPod** -- Quick setup guide available on Civitai
- **LTX-2.3 Templates** -- Step-by-step guides with RunPod template (v0.39+)

### 3. Serverless Endpoints
Deploy ComfyUI workflows as serverless APIs on RunPod, allowing video generation without manually managing GPU instances.

## LTX-2.3 Setup on RunPod (Step-by-Step)

**Recommended GPU:** A40 (48 GB VRAM) for full-quality LTX-2.3; RTX 4090 (24 GB) usable with fp16 quantization.

1. Create a RunPod pod with the `runpod/pytorch:2.4.0-py3.11-cuda12.4.1-devel-ubuntu22.04` template.
2. SSH into the pod:
   ```bash
   pip install ltx-video diffusers accelerate transformers
   huggingface-cli download Lightricks/LTX-2.3 --local-dir ./models/ltx-2.3
   ```
3. Launch ComfyUI (optional):
   ```bash
   git clone https://github.com/comfyanonymous/ComfyUI
   cd ComfyUI && pip install -r requirements.txt
   python main.py --listen 0.0.0.0 --port 8188
   ```
4. Install LTX Video custom nodes:
   ```bash
   cd custom_nodes
   git clone https://github.com/Lightricks/ComfyUI-LTXVideo
   pip install -r ComfyUI-LTXVideo/requirements.txt
   ```
5. Forward port 8188 via RunPod's proxy URL to access the ComfyUI web UI.

A comprehensive all-in-one tutorial (Windows + RunPod + cloud, ComfyUI, SwarmUI, models, presets, and workflows) is available at:
https://huggingface.co/blog/MonsterMMORPG/ltx-2-z-image-base-full-tutorial-audio-to-video

## LTX-2.5 Setup on RunPod (updated 2026-09-13)

RunPod published a dedicated [[ltx-2.5-model|LTX-2.5]] deployment guide covering GPU sizing and day-zero ComfyUI support (three official templates: Text-to-Video, Image-to-Video, First/Last-Frame-to-Video).

**GPU sizing tiers:**

| Tier | VRAM | Example GPUs | Capability |
|---|---|---|---|
| Entry | 16-24GB | RTX 4090, A5000 | Quantized/int8 only, lower resolutions, offloading required |
| Comfortable | 32-48GB | RTX 5090, L40S | int8 ComfyUI checkpoints run well; bf16 distilled viable at 48GB with offloading |
| Recommended | 80-96GB | RTX PRO 6000, H100, A100 80GB | Full bf16 distilled pipeline, spatial upscaler, higher res, longer multishot |
| Maximal | 141GB+ | H200, B200 | 4K HDR, full dev two-stage pipelines, batch generation, fine-tuning |

**Setup steps:**
1. Deploy a pod with the official ComfyUI template (RTX PRO 6000 or H100 recommended); attach a 100GB+ network volume mounted at `/workspace`.
2. Request/accept the gated HuggingFace license for `Lightricks/LTX-2.5`.
3. Update ComfyUI via the ComfyUI Manager within the pod.
4. Authenticate with the HF CLI (a Read token; fine-grained tokens need the "read access to gated repos" scope — a 401/403 means one of these is missing).
5. Download either the Comfy-optimized int8 checkpoints (ComfyUI-only) or the full bf16 pack (~66 GiB total, for 80GB+ cards / the `ltx-pipelines` Python path). Note: the bundled LTX-specific Gemma 4 text encoder is required — Google's stock Gemma 4 checkpoint fails the compatibility check.
6. Launch ComfyUI, load the LTX-2.5 workflow template, and generate — on a PRO 6000 or H100, first clip renders in well under a minute.

Vendor-reported speed (2x GB200, self-hosted): 6.8s for a 10s/24fps clip. NVIDIA optimization pass: up to 20% faster / 40% memory savings on RTX 6000 PRO vs. prior LTX releases; minimum VRAM floor of 16GB for quantized variants.

## Requirements

- GPU with 24GB+ VRAM recommended for full models; A40 (48 GB) recommended for LTX-2.3 at full quality
- 100GB+ storage for model weights

## Comparison with RunComfy

| Feature | RunPod | [[runcomfy]] |
|---------|--------|----------|
| Type | Raw GPU rental | Managed ComfyUI hosting |
| Setup | Manual or template-based | Pre-configured |
| Interface | JupyterLab / Terminal / API | ComfyUI Playground |
| Flexibility | High (any framework) | ComfyUI-focused |
| Serverless | Yes (endpoints) | Managed |
| Best for | Power users, custom deployments | Quick experiments, non-technical users |

## When to Choose RunPod

RunPod is best suited for:
- Power users who want raw GPU access
- Custom deployments beyond what managed API providers offer
- Running any LTX model variant (user controls what is deployed)
- Building serverless endpoints around ComfyUI workflows
- Cost-sensitive workloads where per-hour GPU rental is cheaper than per-request API pricing

For managed ComfyUI without setup overhead, see [[runcomfy]]. For managed API access, see [[fal-ai]] or [[replicate]].
