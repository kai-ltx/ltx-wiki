# Wan 2.7 Release — Alibaba AI Video Model (April 3, 2026)

**Source:** https://www.mindstudio.ai/blog/wan-2-7-ai-video-model-features-release-timeline
**Secondary:** https://wavespeed.ai/blog/posts/wan-2-7-vs-wan-2-6/
**Date:** 2026-04-03
**Retrieved:** 2026-05-25

## Content

Alibaba released **Wan 2.7** on April 3, 2026, as a substantive upgrade over Wan 2.6 — not an incremental patch.

### Key New Capabilities

- **First-and-last-frame control:** Users can specify exactly where a video starts and ends visually
- **Video-to-video editing:** Instruction-based editing of existing video
- **Multi-reference video input:** Feed multiple reference videos for style/content anchoring
- **Subject referencing (R2V):** Reference-consistent character work
- **3× maximum duration:** Significantly longer output clips vs. 2.6
- **Audio synchronization:** Sound effects and musical cues align with on-screen motion more naturally
- **Temporal consistency improvements:** Fewer flickering faces, fewer mid-clip wardrobe changes, fewer morphing subjects between cuts

### Architecture

**Industry-first MoE (Mixture of Experts) architecture** for video generation:
- `Wan2.7-T2V-A14B`: Text-to-video, MoE design
- `Wan2.7-I2V-A14B`: Image-to-video, MoE design
- Both built on the Wan-Bench 2.0 evaluation framework

### Pricing

- **$6.00/min** — 33% cheaper than older Wan versions while delivering better results
- Available via API providers including fal.ai and Replicate

### Benchmark Performance (Wan 2.2 baseline)

Wan-Bench 2.0 results for Wan 2.2-T2V-A14B (the predecessor):
- #1 in Aesthetic Quality (over Seedance 1.0, Kling 2.0, Sora, Hailuo 02)
- #1 in Motion Dynamics (over Kling 2.0, Sora, Hailuo 02)
- #1 in Text Rendering
- #1 in Camera Control

Wan 2.7 builds on this strong base.

### Competitive Position

Wan 2.7 competes most directly with:
- LTX-2.3 in the open-weight space (both run locally)
- Seedance 2.0, Runway Gen-4, Kling 3.x in quality benchmarks

Differentiators vs. LTX-2.3:
- Open-source with Apache license (same as LTX)
- First/last frame and instruction editing stronger than LTX-2.3 currently
- LTX-2.3 remains faster (18x faster than Wan 2.2 on benchmarks) and supports native synchronized audio
- LTX-2.3 has native portrait mode and IC-LoRA ecosystem; Wan 2.7 has stronger editing pipeline

### Ecosystem

GitHub: https://github.com/Wan-Video/Wan2.2 (Wan 2.2 base; 2.7 releases tracked there)
