# Wan 3.0 — Confirmed Release Details (60B MoE, 4K, 30s)

**Source:** https://flowith.io/blog/wan-3-0-world-class-text-to-video-open-source-free-2026/
**Date:** 2026-06-01
**Retrieved:** 2026-06-15

## Content

Wan 3.0, previously listed as "roadmap mid-2026" in wiki, appears confirmed as released. Web sources and a dedicated product site (wan3pro.com) document the model's specifications and capabilities. The wiki's June 8 entry noted "Wan 3.0 on roadmap for mid-2026 (60B params, 30s clips, unconfirmed)" — these details are now confirmed.

### Architecture

- **60B parameter model** with Mixture-of-Experts (MoE) diffusion transformer architecture
- ~27B active parameters per inference pass (14B active from 60B total per other sources)
- Successor to Wan 2.7 (open-source since May 2026, Apache 2.0)

### Key Capabilities (confirmed vs. Wan 2.7)

| Feature | Wan 2.7 | Wan 3.0 |
|---------|---------|---------|
| Max resolution | 1080p | Native 4K |
| Max duration | 15 seconds | 30 seconds |
| Multi-shot | No | Yes (2–5 min narratives) |
| Open weights | Apache 2.0 | Apache 2.0 |

- Native 4K generation from first frame (not upscaled)
- Up to 30 seconds single-pass (vs. 15s for Wan 2.7)
- Multi-shot storyboard support: automated 2–5 minute narrative generation from a single prompt
- ~40% faster inference than Wan 2.6 via attention optimization
- LoRA fine-tuning support

### Availability

- Weights freely downloadable under Apache 2.0
- Available for local deployment, commercial use, and fine-tuning
- Cloud inference via multiple providers

### Significance for LTX Competitive Landscape

Wan 3.0 arriving with native 4K 30s generation and open weights represents a significant upgrade in the open-source competitor space. LTX-2.3 supports up to 4K at 20 seconds; Wan 3.0 extends to 30 seconds. Both are open-weight under permissive licenses.
