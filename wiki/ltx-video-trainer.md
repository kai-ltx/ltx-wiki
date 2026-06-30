---
title: LTX Video Trainer
type: tool
created: 2026-04-13
updated: 2026-06-30
sources:
  - raw/ltx-video-trainer.md
  - raw/training-fine-tuning.md
  - raw/community-project-lora-training-tools.md
  - raw/ltx-news-trainer-unified-june-2026.md
tags:
  - trainer
  - tool
  - lora
  - fine-tuning
  - open-source
---
# LTX Video Trainer

The LTX ecosystem includes official training tools for [[lora-training]] and fine-tuning. Both are open source and developed by [[lightricks-company]].

## LTX-2 Trainer — Unified Framework (June 17, 2026)

- **Location:** github.com/Lightricks/LTX-2/tree/main/packages/ltx-trainer
- **Part of the LTX-2 monorepo** alongside ltx-core and ltx-pipelines
- Major upgrade released June 17, 2026: unified training across all modalities from a single configuration file

### 13 Supported Training Modes

**Video:** T2V · I2V · Video extension (forward + backward) · Inpainting · Outpainting

**Audio:** T2A · Audio extension (forward + backward) · Audio inpainting

**Cross-modal:** A2V (audio-to-video) · V2A (video-to-audio)

**Reference / IC-LoRA:** V2V · A2A · AV2AV (joint audio-video-to-audio-video IC-LoRA)

### Composable Conditioning

Combine references, masks, first frames, prefixes, suffixes, audio, and video signals within a single training workflow. Supports advanced pipelines including AV2AV IC-LoRA, audio inpainting, and custom multimodal pipelines.

### Agentic Configuration Generation

A new agentic skill lets users generate LoRA and IC-LoRA training configurations through **Claude and other LLM-based agents** using natural language — no manual YAML editing required. This integrates LTX training with the broader AI agent ecosystem.

### Hardware Requirements

- **CUDA 13+** recommended; Linux required
- **80GB+ VRAM** for standard config
- **32GB VRAM** (e.g., RTX 5090) supported via low-VRAM config with INT8 quantization
- Gemma Text Encoder (local directory) required alongside LTX-2 checkpoint

### Installation

```bash
git clone https://github.com/Lightricks/LTX-2.git
cd LTX-2
uv sync --frozen
source .venv/bin/activate

# Or install the trainer package directly
pip install -e packages/ltx-trainer
```

### Training Time

Training can complete in **less than an hour** for motion, style, or likeness LoRA adaptation.

### Pre-trained LoRA Models (Official)

| Model | Type |
|-------|------|
| Camera control LoRA | Standard |
| Pose guidance LoRA | Standard |
| Depth control IC-LoRA | IC-LoRA |
| Edge detection IC-LoRA | IC-LoRA |
| Detailer IC-LoRA | IC-LoRA |

## LTX-Video-Trainer (Legacy Community Trainer)

- **Repository:** github.com/Lightricks/LTX-Video-Trainer
- **License:** Apache 2.0
- **Authors:** Matan Ben Yosef, Naomi Ken Korem, Tavi Halperin (2025)

### Supported Models (Legacy)

- LTX-Video 2B (original)
- LTXV 13B (added May 2025)

### Training Types

- **Standard LoRA training** — custom styles, characters, effects
- **[[ic-lora|IC-LoRA]] training** — depth map, pose skeleton, canny edge map control
- **Full fine-tuning** — complete model weight updates

The LTX-2 Unified Trainer (above) supersedes this for LTX-2 and LTX-2.3 models.

## Community Training Tools

### ai-toolkit (Ostris)

Third-party training toolkit supporting LTX Video LoRA training.

- **Repository:** github.com/ostris/ai-toolkit
- See [[training-hyperparameters]] for configuration example

### eisneim — LTX LoRA Training (i2v & t2v)

Community-created training code; supports both image-to-video and text-to-video LoRA training.

- **Repository:** github.com/eisneim/ltx_lora_training_i2v_t2v
- MIT license

### HuggingFace finetrainers

- Added T2V LoRA fine-tuning support for LTX Video in December 2024
- Scalable and memory-optimized training

## Community Support

- Discord: discord.gg/ltxplatform
- GitHub issues for bug reports and feature requests

## References

- [[lora-training]]
- [[training-hyperparameters]]
- [[training-dataset-preparation]]
- [[ic-lora]]
- [[third-party-training-services]]
- [[lora-community-ecosystem]]
