---
title: Apple Silicon Setup
type: guide
created: 2026-04-13
updated: 2026-05-19
sources:
  - raw/tutorial-apple-silicon-setup.md
  - raw/github-community-tools-wrappers.md
  - raw/tutorial-ltx-video-apple-silicon-mlx-inference-2026.md
tags:
  - apple-silicon
  - mac
  - mps
  - setup
  - tutorial
---

# Apple Silicon Setup

Community members have documented how to run [[ltx-video-overview|LTX-Video]] on Apple Silicon Macs (M1, M3, M4). The process requires specific PyTorch version configuration to avoid output corruption.

## Critical Requirement: Torch Version

**Torch 2.5 or above causes noise output on Apple Silicon.** This is the single most important detail for Mac users.

**Solution:** Downgrade to Torch 2.4.1:

```bash
pip install torch==2.4.1
```

This breaks compatibility with JC2 (which requires Torch 2.5+). Users must choose between JC2 compatibility and LTX-Video on Apple Silicon.

## Performance by Hardware

| Mac Model | RAM | Processing Time |
|-----------|-----|----------------|
| MacBook Pro M4 | 48GB | Working (time not specified) |
| MacBook Pro M3 | -- | ~5 minutes per video |
| MacBook Pro M1 | 16GB | ~15 minutes per video |

## Recommended Settings

- **Model:** Use the 2B parameter model for best compatibility
- **Frame limit:** Keep videos to roughly 4 seconds to avoid quality degradation
- **Resolution:** Start with lower resolutions

## Known Issues

1. **Noise output with Torch 2.5+** -- Generated video appears as noise and lines if the wrong Torch version is used
2. **Quality degradation with many frames** -- Limit to roughly 4 seconds
3. **ComfyUI noise** -- Same Torch version issue manifests in ComfyUI

## Community Resources

- YouTube guide by monk05 for M4 setup: https://www.youtube.com/watch?v=lvD9l4b2pzQ

## MLX Support Status

While there is no official MLX implementation from [[lightricks-company|Lightricks]], the community has developed multiple MLX ports that bypass the PyTorch/Torch version issues entirely:

### Blaizzy/mlx-video (190 stars)

The most mature MLX port. Supports [[ltx-2-overview|LTX-2]] (19B), Wan2.1 (1.3B/14B), and Wan2.2.

- **URL:** https://github.com/Blaizzy/mlx-video
- **LTX-2 features:** Text-to-video, image-to-video, audio-to-video, joint audio-video, 2x spatial upscaling, Gemma prompt enhancement
- **Pipelines:** distilled, dev, dev-two-stage, dev-two-stage-hq
- **Requirements:** macOS Apple Silicon, Python >= 3.11, MLX >= 0.22.0

### james-see/ltx-video-mac (137 stars)

Native macOS SwiftUI app using MLX framework for [[ltx-2-overview|LTX-2]] generation.

- **URL:** https://github.com/james-see/ltx-video-mac
- **Releases:** 83 (latest v2.3.52, April 2026)
- **Features:** Synchronized audio, text-to-speech (ElevenLabs/MLX-Audio), 54 music genre presets
- **Requirements:** macOS 14.0+, Apple Silicon, 32GB RAM minimum (64GB+ recommended)

### baisampayans/ltx-mlx (1 star)

Pure MLX implementation claiming 3.4x faster than PyTorch for LTX-Video inference.

- **URL:** https://github.com/baisampayans/ltx-mlx

### dgrauet/ltx-2-mlx — Pure MLX Python Port

Pure MLX port of LTX-2 (supporting LTX-2.3) for Apple Silicon. Three-package monorepo:

- `ltx_inference` — core inference
- `ltx_pipelines` — pipeline abstractions (text2video, image2video, audio2video)
- `ltx_training` — LoRA fine-tuning on Metal

Runs natively on Metal (Apple GPU). Install: `pip install mlx mlx-lm` then `pip install -e .` from the repo root.

```python
from ltx_pipelines import LTX2TextToVideoPipeline

pipe = LTX2TextToVideoPipeline.from_pretrained("Lightricks/LTX-2.3")
result = pipe(prompt="A mountain stream at dawn", num_frames=48, fps=24, width=704, height=480)
result.save("output.mp4")
```

- **URL:** https://github.com/dgrauet/ltx-2-mlx

### Acelogic/LTX-2-MLX — Automatic Version Detection

Native Apple Silicon implementation with automatic version detection from the checkpoint:

- Supports LTX-2.0 (19B parameters) and LTX-2.3 (22B parameters)
- Automatically selects the correct model configuration
- **URL:** https://github.com/Acelogic/LTX-2-MLX

See [[github-community-tools]] for more community tools.

## Performance Notes (Apple Silicon)

| Mac Hardware | RAM | Performance |
|---|---|---|
| M3 Max | 128 GB unified memory | LTX-2.3 22B at ~2–4 seconds/frame at 480p |
| M2/M3 (24–32 GB RAM) | — | fp16 quantization recommended |
| M2 Ultra / M3 Ultra / M4 Max | 64 GB+ | 4K generation viable |

CLI example via `mlx-video`:
```bash
mlx-video generate --model ltx-2 --pipeline distilled \
  --prompt "A surfer rides a wave at sunset" \
  --frames 60 --fps 24 --output surf.mp4
```

## See Also

- [[hardware-requirements]] -- General GPU and VRAM guidance
- [[hardware-accessibility]] -- Running on low-end hardware
- [[installation-quickstart]] -- General installation instructions
- [[github-community-tools]] -- Full community tools listing
