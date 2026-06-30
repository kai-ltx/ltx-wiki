# LTX Trainer — Unified Training Framework (June 17, 2026)

**Source:** https://ltx.io/release-notes
**Date:** 2026-06-17
**Retrieved:** 2026-06-30

## Content

Lightricks released a major upgrade to LTX Trainer on June 17, 2026 — the open-source training framework for LTX models. The new version introduces **unified training across all modalities**: video, audio, cross-modal, and reference-conditioned (IC-LoRA) workflows, all from a single configuration file.

### 13 Training Modes

**Video:**
- T2V (text-to-video)
- I2V (image-to-video)
- Video extension (forward + backward)
- Inpainting
- Outpainting

**Audio:**
- T2A (text-to-audio)
- Audio extension (forward + backward)
- Audio inpainting

**Cross-modal:**
- A2V (audio-to-video)
- V2A (video-to-audio)

**Reference / IC-LoRA:**
- V2V (video-to-video)
- A2A (audio-to-audio)
- AV2AV (audio-video-to-audio-video joint IC-LoRA)

### Composable Conditioning

Combine references, masks, first frames, prefixes, suffixes, audio, and video signals within a single training workflow. Supports advanced pipelines including AV2AV IC-LoRA, audio inpainting, reference-conditioned training, and custom multimodal pipelines.

### Agentic Configuration Generation

A new agentic skill lets users generate LoRA and IC-LoRA training configurations through **Claude and other LLM-based agents** using natural language instructions — no manual YAML editing required.

### Requirements

- LTX-2 Model Checkpoint (local `.safetensors`)
- Gemma Text Encoder (local directory)
- Linux with CUDA 13+ (recommended)
- 80GB+ VRAM recommended; 32GB RTX 5090 supported via low-VRAM config with INT8 quantization

### Repository

- GitHub: https://github.com/Lightricks/LTX-2 (packages/ltx-trainer)
- Documentation: https://github.com/Lightricks/LTX-2/blob/main/packages/ltx-trainer/README.md
