---
title: RunPod
type: entity
created: 2026-04-13
updated: 2026-05-19
sources:
  - raw/hosting-runpod-runcomfy.md
  - raw/inference-providers-overview.md
  - raw/cloud-deployment-platforms.md
  - raw/tutorial-ltx-video-runpod-modal-cloud-gpu-2026.md
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
