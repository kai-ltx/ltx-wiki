# LTXV 13B Distilled v0.9.8 — New Open-Source Model Announcement (May 2026)

**Source:** https://x.com/LTXStudio/status/1919751150888239374
**Date:** 2026-05-06
**Retrieved:** 2026-05-19

## Content

LTX Studio announced a new open-source video model release in early May 2026 via their official X account (tweet thread starting at status ID 1919751150888239374). The announcement described it as "the latest open source video model" and stated it "sets a new bar for speed, quality, and control. It's faster than anything in its class, packed with new features, and ready to run on your own hardware."

This corresponds to the LTXV 13B Distilled v0.9.8 release, a distilled variant of the LTX-Video 13B model with the following characteristics:

### Key Specifications

- **Model**: LTXV 13B (13 billion parameters), distilled variant
- **Version**: 0.9.8-distilled (weights available on Hugging Face at `Lightricks/LTX-Video-0.9.8-13B-distilled`)
- **Generation speed**: Achieves results in 4–8 steps; full multi-scale rendering completed in approximately 12 seconds — nearly 5x faster than the base (non-distilled) 13B model.
- **Hardware target**: Consumer GPUs; 5-second 720p video in ~9.5 seconds on an H100, ~1.5 minutes on an RTX 5090.
- **Weights**: Open, available on GitHub (`Lightricks/LTX-Video`) and Hugging Face.

### Technical Highlights

- Uses multi-scale rendering (MSR) architecture for efficient high-quality generation.
- Distillation reduces required inference steps from ~50 to 4–8 without significant quality loss.
- Supports FP8 quantization (`ltxv-13b-0.9.8-distilled-fp8.safetensors`) for reduced VRAM requirements.
- Compatible with ComfyUI via the official `Lightricks/ComfyUI-LTXVideo` nodes.
- Accessible via third-party APIs including fal.ai (`fal-ai/ltxv-13b-098-distilled`).

### Community Reception

A Hacker News "Show HN" thread (item ID 43987218) generated significant discussion, highlighting the speed improvements as particularly notable for local inference use cases.

### Distinction from LTX-2.x Series

This release is part of the LTXV 0.9.x lineage (video-only, no synchronized audio), distinct from the LTX-2 / LTX-2.3 series (which generates synchronized audio+video). The 0.9.8 distilled variant serves users who need maximum speed with lightweight hardware for video-only generation workflows.

### Sources

- https://x.com/LTXStudio/status/1919751150888239374
- https://huggingface.co/Lightricks/LTX-Video-0.9.8-13B-distilled
- https://github.com/Lightricks/LTX-Video/releases
- https://news.ycombinator.com/item?id=43987218
- https://fal.ai/models/fal-ai/ltxv-13b-098-distilled
