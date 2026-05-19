---
title: HunyuanWorld (Tencent 3D World Models)
type: competitor
created: 2026-05-19
updated: 2026-05-19
sources:
  - raw/competitor-tencent-hyworld-2-april-2026.md
tags:
  - competitor
  - tencent
  - 3d-world-model
  - spatial-intelligence
  - open-source
---
# HunyuanWorld (Tencent 3D World Models)

Tencent's HunyuanWorld line represents a pivot from 2D video generation toward **3D world simulation and spatial intelligence**. Released in April–May 2026, it is distinct from [[hunyuan-video]] (which focuses on 2D video generation) and represents a separate research direction targeting VR, gaming, and simulation use cases.

## HY-World-2.0 (April 16, 2026)

Released as a state-of-the-art **3D world model** — an evolution of the HunyuanWorld ecosystem. Full technical specifications not yet widely documented at initial release.

## HunyuanWorld-Voyager (Open-sourced April–May 2026)

The more significant release: open-sourced on GitHub, described as the world's first ultra-long-range world model with **native 3D reconstruction**.

### Key Capabilities
- Generates **interactive RGBD video sequences** conditioned on camera input
- **Real-time 3D reconstruction** from a single input image
- Exports **point cloud videos directly to 3D formats** — no COLMAP or external tooling required
- Scalable data engine automates camera pose estimation and metric depth prediction for arbitrary videos
- Training data: 100,000+ video clips combining real-world captures and synthetic Unreal Engine renders

### Architecture
- Takes a single image + camera trajectory as input
- Produces geometrically consistent RGBD video sequences
- Scalable data pipeline enables training on large, diverse video collections

### Benchmark
- **#1 on Stanford's WorldScore benchmark** with a score of **77.62**
  - Surpasses WonderWorld (72.69) and CogVideoX-I2V (62.15)

### Use Cases
- Virtual Reality (VR) environment generation
- Game world simulation and prototyping
- Spatial intelligence research
- Interactive 3D content from single images

### Availability
- Open-sourced on GitHub: https://github.com/Tencent-Hunyuan/HunyuanWorld-Voyager

## Relationship to HunyuanVideo

HunyuanWorld-Voyager is architecturally and functionally different from [[hunyuan-video]]:

| Aspect | HunyuanVideo | HunyuanWorld-Voyager |
|--------|-------------|---------------------|
| Output | 2D video (RGB) | 3D world (RGBD + point cloud) |
| Input | Text/image prompt | Image + camera trajectory |
| Use case | Video generation | World simulation / VR / gaming |
| Resolution focus | 1080p playback quality | Geometric accuracy |
| Benchmark | Artificial Analysis Elo | WorldScore (Stanford) |

## Relevance to LTX

HunyuanWorld-Voyager does not compete directly with [[ltx-2-overview|LTX-2]] or [[ltx-studio]] — it targets a different output modality (3D worlds vs. 2D video). However, it signals Tencent's broader ambitions in spatial intelligence and that the competitive landscape is expanding beyond traditional video generation.

## See Also
- [[hunyuan-video]] — Tencent's 2D video generation model family
- [[competitor-landscape-overview]]
- [[open-source-video-generation-landscape]]

## References
- https://github.com/Tencent-Hunyuan/HunyuanWorld-Voyager
- https://www.techspot.com/news/109328-tencent-voyager-ai-can-turn-one-photo-explorable.html
