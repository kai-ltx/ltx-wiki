# Tencent HY-World-2.0 and HunyuanWorld-Voyager: 3D World Model Releases (April 2026)

**Source:** https://github.com/Tencent-Hunyuan/HunyuanWorld-Voyager
**Date:** 2026-04-16
**Retrieved:** 2026-05-19

## Content

Tencent released two significant Hunyuan-related models in the April 2026 timeframe:

### HY-World-2.0 (April 16, 2026)
Tencent released HY-World-2.0 on April 16, 2026, described as a state-of-the-art 3D world model. This is an evolution of the HunyuanWorld ecosystem. Full technical specifications were not yet widely documented at time of retrieval.

### HunyuanWorld-Voyager (Open-Sourced April–May 2026)
HunyuanWorld-Voyager was open-sourced on GitHub and represents the world's first ultra-long-range world model with native 3D reconstruction.

**Key capabilities:**
- Generates interactive RGBD video sequences conditioned on camera input.
- Supports real-time 3D reconstruction from a single input image.
- Exports point cloud videos directly to 3D formats without requiring COLMAP or other external tooling.
- A scalable data engine automates camera pose estimation and metric depth prediction for arbitrary videos.
- Training data: 100,000+ video clips combining real-world captures and synthetic Unreal Engine renders.

**Benchmark:**
- Ranked #1 on Stanford's WorldScore benchmark with a score of 77.62, surpassing WonderWorld (72.69) and CogVideoX-I2V (62.15).

**Use cases:** VR, gaming, simulations, spatial intelligence applications.

### HunyuanVideo 1.5 (Background Context — released November 2025)
The most recent core video generation model is HunyuanVideo-1.5 (released November 21, 2025):
- 8.3B parameters; runs on consumer GPUs with 14 GB VRAM.
- Selective and sliding tile attention (SSTA) makes it 1.87x faster than prior versions.
- Supports 1080p output, text-to-video and image-to-video.
- 480p image-to-video step-distilled variant (December 5, 2025) generates in 8–12 steps, 75% faster on RTX 4090.

### Sources
- https://github.com/Tencent-Hunyuan/HunyuanWorld-Voyager
- https://x.com/TencentHunyuan/status/1962741518797836708
- https://dataconomy.com/2026/03/16/deepseek-v4-and-tencents-new-hunyuan-model-to-launch-in-april/
- https://www.techspot.com/news/109328-tencent-voyager-ai-can-turn-one-photo-explorable.html
- https://news.futunn.com/en/post/61536268/tencent-hunyuan-voyager-3d-world-model-released
