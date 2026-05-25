# Runway Gen-4 and Gen-4.5 — State of Runway AI Video (May 2026)

**Source:** https://runwayml.com/research/introducing-runway-gen-4.5
**Secondary:** https://www.vo3ai.com/blog/runway-gen-4-just-dropped-5-surprising-upgrades-ai-video-makers-need-to-know-2026-05-03
**Date:** 2026-05-03 (Gen-4), 2025-12-01 (Gen-4.5)
**Retrieved:** 2026-05-25

## Content

### Runway Gen-4 (May 3, 2026)

Runway launched Gen-4 on May 3, 2026 as its "most advanced text-to-video model" with a focus on **world consistency**.

**Key features:**
- **Character consistency across scenes:** Reference image system anchors output to specific visual identities (faces, objects, locations persist across shots)
- **Native audio generation:** Audio tracks generated alongside video natively
- **Multi-shot scene direction:** Can follow complex instructions spanning multiple shots while maintaining world state
- **Turbo variant:** Fast generation option for speed-quality tradeoffs
- **Camera motion control:** Precise control over camera movement

### Runway Gen-4.5 (December 1, 2025)

Gen-4.5 is the current top-tier Runway model as of May 2026.

**Benchmark position:** #1 on Artificial Analysis Text-to-Video leaderboard with **1,247 Elo points**, surpassing all other models as of Nov 30, 2025.

**Key capabilities:**
- State-of-the-art motion quality, prompt adherence, and visual fidelity
- Physical accuracy: objects with realistic weight, momentum, force; liquids with proper dynamics
- Complex multi-element scene rendering with precision
- Wide stylistic range: photorealistic, non-photorealistic, cinematic, slice-of-life
- Available across all paid Runway plans at comparable pricing to Gen-4

**Infrastructure:** Built on NVIDIA Hopper and Blackwell GPUs; developed in close collaboration with NVIDIA.

**Limitations documented:**
- Causal reasoning errors (effects precede causes)
- Object permanence issues (objects disappear/appear unexpectedly)
- Success bias (actions disproportionately succeed regardless of setup)

### Other Runway Developments (May 2026)

- **Aleph 2.0**: Upgraded video editing model (announced alongside Gen-4.5 page, 50% off Pro with code RUNWAY50)
- **GWM-1 / General World Models**: Runway is pursuing world model research
- **Robotics product**: Listed in product nav
- **AI Summit 2026**: Runway hosting an AI Summit

### Competitive Position vs. LTX

- Runway Gen-4.5 leads benchmarks but is closed-source, cloud-only
- LTX-2.3 (22B) remains the leading open-source option that runs locally
- Runway's character consistency (reference image system) competes directly with LTX-2.3's IC-LoRA approach
- Both now offer native audio generation
