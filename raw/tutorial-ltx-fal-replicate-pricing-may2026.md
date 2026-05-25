# LTX Video Inference Provider Pricing Update — May 2026

**Source:** https://fal.ai/models/fal-ai/ltx-2/text-to-video/fast
**Secondary:** https://www.nemovideo.com/blog/ltx-2-3-pricing
**Date:** 2026-05-25
**Retrieved:** 2026-05-25

## Content

Current pricing for LTX Video (LTX-2 / LTX-2.3) across inference providers as of May 2026.

### fal.ai Pricing

| Tier | Price | Resolution |
|------|-------|-----------|
| LTX Video 2.0 Fast | $0.04/second | 1080p |
| LTX Video 2.0 Pro | $0.10/second | 1080p |

fal.ai lists "LTX Video 2.0 Fast" as a distinct model endpoint for rapid text-to-video generation.

### General Market Context

The AI API provider comparison (fal.ai vs Replicate vs others) shows LTX as one of the most cost-effective options in the market. For a 10-second 1080p video:
- LTX Fast: ~$0.40
- LTX Pro: ~$1.00

### LTX-2.3 Diffusers Support Status

As of May 2026, **Diffusers support for LTX-2.3 is listed as "coming soon"** by Lightricks. Current options:
1. **Native ltx-pipelines package** — full feature access including audio-video
2. **LTX-2 in Diffusers** — already supported (LTX-2, not 2.3)
3. **ComfyUI nodes** — official Lightricks nodes support LTX-2.3

For production Python workloads requiring LTX-2.3 features (audio sync, portrait mode, new VAE), the native ltx-pipelines package is the recommended path while Diffusers support catches up.

### Provider Ecosystem Summary (May 2026)

- **fal.ai**: LTX Video 2.0 (Fast/Pro), pay-per-second pricing
- **Replicate**: LTX-2.3 available (check replicate.com for current pricing)
- **Segmind**: LTX Video support
- **WaveSpeed AI**: LTX-2.3 inference with their optimization stack
- **Modal**: GPU cloud deployment
- **RunPod**: GPU cloud deployment
- **RunComfy**: ComfyUI workflows including Cameraman IC-LoRA
