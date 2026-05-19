# Wan 2.7 Official Release: Alibaba's Unified Architecture (April 2026)

**Source:** https://textideo.com/blog/wan2-7-officially-released-alibaba-s-unified-architecture-for-image-generation-and-editing
**Date:** 2026-04-22
**Retrieved:** 2026-05-19

## Content

Wan 2.7, Alibaba's latest open-source video generation model, was officially confirmed available on Alibaba's Model Studio and wan.video on April 22, 2026. Cloud platform launch preceded the open-weight release, with model weights expected mid-to-late Q2 2026 (4–8 weeks after cloud launch, consistent with Alibaba's prior release cadence).

### Architecture
- Built on a Mixture-of-Experts (MoE) diffusion transformer with 27 billion total parameters, 14 billion active per inference pass.
- Unified architecture covering text-to-video, image-to-video, reference-to-video with voice cloning, and instruction-based video editing.

### Key New Capabilities in 2.7 vs. 2.6
- **4K image generation** (2K for video output)
- **Up to 9 reference images** for style and content guidance
- **Coherent image set generation** — up to 12 related images per single request
- **Thinking mode** for enhanced compositional reasoning
- **Native audio output** built in
- **First and last frame control** for precise video bookending
- **Multi-reference character consistency** across scenes
- Generates 1080p video up to 15 seconds

### Open Source / Licensing
Apache 2.0 license, no face filters, no regional blocks, no IP moderation — key differentiation from closed commercial models.

### Benchmark Context
Wan 2.7 is positioned to compete directly with Kling 3.0, Runway Gen-4.5, and Google Veo models on the ELO Video Arena leaderboard. Earlier Wan models (2.1, 2.2) had surpassed Sora on VBench prior to Sora's shutdown.

### Prior Version Timeline
- Wan 2.2: released July 28, 2025 (MoE architecture introduced)
- Wan 2.6: released December 2025 (open-source image model)
- Wan 2.7: cloud launch late March / confirmed April 22, 2026; open weights Q2 2026

### Sources
- https://wan27.org/blog/wan-2-7-release-date-open-source
- https://wavespeed.ai/blog/posts/wan-2-7-coming-soon-major-upgrade/
- https://wavespeed.ai/blog/posts/wan-2-7-vs-wan-2-6/
- https://www.mindstudio.ai/blog/wan-2-7-ai-video-model-features-release-timeline
- https://textideo.com/blog/wan2-7-officially-released-alibaba-s-unified-architecture-for-image-generation-and-editing
