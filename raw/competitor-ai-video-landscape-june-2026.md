# AI Video Generation Landscape — June 2026 Update

**Source:** https://wavespeed.ai/blog/posts/ai-video-generation-news-2026/
**Date:** 2026-06-04
**Retrieved:** 2026-06-08

## Content

Monthly roundup from WaveSpeed AI covering the state of AI video generation as of June 4, 2026.

### Model Landscape Status

As of June 2026, the following models are the main players:

| Model | Company | Release | Key Capability |
|---|---|---|---|
| Runway Gen-4.5 | Runway | Dec 1 2025 | #1 T2V (Elo 1247), 60s clips, NVIDIA |
| Seedance 2.0 | ByteDance | Feb 12 2026 | #1 T2V briefly (Elo 1213), native audio |
| Kling 3.0 / O3 | Kuaishou | Feb 5 2026 | Native 4K, multi-shot, native audio |
| LTX-2.3 | Lightricks | Mar 5 2026 | Open-source, 22B, native audio, 4K |
| Veo 3.1 Lite | Google | Mar 31 2026 | Budget API tier at $0.05/s |
| Wan 2.7 | Alibaba | Mar 2026 | Open weights available (Apache 2.0) |
| Grok Imagine Video 1.5 | xAI | Jun 3 2026 | #1 I2V (Elo 1404), native audio |

### Sora API Sunset

- OpenAI announced March 24, 2026: Sora consumer app and API discontinuation
- Sora app went dark April 26, 2026
- **Sora API scheduled to sunset September 24, 2026**
- Builders on Sora need migration plan; window is shorter than it looks

### Wan 3.0 Roadmap

- Alibaba public roadmap targets mid-2026 for Wan 3.0
- Reported specs: 60B parameters, native 4K, 30-second continuous generation
- Open weights expected (as with all Wan models)
- Timeline unconfirmed; treat as Q3 risk

### Seedance 2.0 Developer API Delay

- Seedance 2.0 official developer API still not released as of late May 2026
- Third-party platforms have integrated under licensing terms
- ByteDance reportedly delayed while copyright disputes with Hollywood studios are unresolved
- When official endpoint lands, cost math for aggregator-based access changes

### Capability Trends as of June 2026

1. **Native audio** is now table stakes — Seedance 2.0, Veo 3.1, Kling 3.0, LTX-2.3, Grok Imagine Video 1.5 all produce native audio
2. **4K output** is broadly available: Kling 3.0 (native 4K), LTX-2.3, Runway Gen-4.5 (4K via subscription)
3. **60+ second clips**: Kling 3.0 supports 60s, Runway Gen-4.5 supports 60s; coherence degrades at length
4. **C2PA watermarking**: Seedance 2.0 ships with C2PA watermarking built in; TikTok labeled 1.3B+ AI videos using C2PA

### Industry Moves

- **OpenAI-Disney partnership**: Reported ~$1B deal for licensed character generation
- **Runway $315M raise**: Capital going to production-pipeline layer (pre-vis, storyboarding, VFX)
- **Luma valuation at $4B**: Production-tool layer is where investors are betting

### EU AI Act Article 50

- Enforcement begins **August 2, 2026**
- Requires machine-readable marking on all AI-generated video distributed to EU audiences
- Multi-layered approach required: embedded metadata + pixel-level watermarks + fingerprinting
- Fines up to €15M or 3% of worldwide annual turnover
- **Transition**: AI systems already on market before Aug 2 get until **December 2, 2026** (per AI Omnibus provisional agreement, May 2026)
- California SB 942: disclosure requirements for AI-generated content, in effect since January 1, 2026
