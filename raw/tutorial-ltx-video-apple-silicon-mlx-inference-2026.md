# LTX-2 / LTX-2.3 on Apple Silicon with MLX (2026)

**Source:** https://github.com/james-see/ltx-video-mac ; https://github.com/dgrauet/ltx-2-mlx ; https://github.com/Blaizzy/mlx-video
**Date:** 2026-04-20
**Retrieved:** 2026-05-19

## Content

Multiple community projects now enable running LTX-2 and LTX-2.3 natively on Apple Silicon (M-series Macs) using Apple's MLX framework — no external GPU or cloud required.

---

### 1. ltx-video-mac — Native SwiftUI App

**Repo:** https://github.com/james-see/ltx-video-mac  
**Docs/homepage:** https://james-see.github.io/ltx-video-mac/

A native macOS application (SwiftUI) that runs LTX-2 natively on Apple Silicon using MLX.

Features:
- Text-to-video with synchronized audio from text prompts
- Single-click model download from Hugging Face on first run (15–30 min depending on model size and connection)
- Model cached locally for subsequent runs
- No Python environment required

---

### 2. ltx-2-mlx — Pure MLX Python Port

**Repo:** https://github.com/dgrauet/ltx-2-mlx

Pure MLX port of LTX-2 (supporting LTX-2.3) for Apple Silicon. Three-package monorepo mirroring the reference structure:
- `ltx_inference` — core inference
- `ltx_pipelines` — pipeline abstractions (text2video, image2video, audio2video)
- `ltx_training` — LoRA fine-tuning on Metal

Runs natively on Metal (Apple GPU).

**Install:**
```bash
pip install mlx mlx-lm
git clone https://github.com/dgrauet/ltx-2-mlx
cd ltx-2-mlx
pip install -e .
```

**Basic text-to-video:**
```python
from ltx_pipelines import LTX2TextToVideoPipeline

pipe = LTX2TextToVideoPipeline.from_pretrained("Lightricks/LTX-2.3")
result = pipe(
    prompt="A mountain stream at dawn, gentle mist rising",
    num_frames=48,
    fps=24,
    width=704,
    height=480,
)
result.save("output.mp4")
```

---

### 3. LTX-2-MLX (Acelogic) — Automatic Version Detection

**Repo:** https://github.com/Acelogic/LTX-2-MLX

Native Apple Silicon implementation supporting:
- LTX-2.0 (19B parameters)
- LTX-2.3 (22B parameters)
- Automatic version detection from the checkpoint

---

### 4. mlx-video — Multi-Model Package

**Repo:** https://github.com/Blaizzy/mlx-video

Broader MLX package for inference and fine-tuning of image/video/audio generation models on Mac. Supports LTX-2 among other models.

**CLI example:**
```bash
# Distilled (fastest) pipeline
mlx-video generate --model ltx-2 --pipeline distilled \
  --prompt "A surfer rides a wave at sunset" \
  --frames 60 --fps 24 --output surf.mp4

# Dev pipeline (higher quality)
mlx-video generate --model ltx-2 --pipeline dev \
  --prompt "Timelapse of clouds over mountains" \
  --frames 120 --fps 30 --output clouds.mp4
```

---

### Performance Notes

- Tested on M3 Max (128 GB unified memory): LTX-2.3 22B runs at approximately 2–4 seconds per frame at 480p
- fp16 quantization recommended for M2/M3 with 24–32 GB RAM
- 4K generation requires 64 GB+ unified memory (M2 Ultra / M3 Ultra / M4 Max)

### References

- https://github.com/james-see/ltx-video-mac
- https://github.com/dgrauet/ltx-2-mlx
- https://github.com/Acelogic/LTX-2-MLX
- https://github.com/Blaizzy/mlx-video
