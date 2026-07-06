# Seedance 2.5 — Native 30-Second AI Video, Local Editing, 50 References

**Source:** https://the-decoder.com/bytedances-seedance-2-5-breaks-the-30-second-barrier-for-ai-video-generation/, https://www.techtimes.com/articles/318975/20260624/bytedance-seedance-25-native-30-second-ai-video-no-stitching-required.htm
**Date:** 2026-06-23 (announced); early July 2026 (public launch)
**Retrieved:** 2026-07-06

## Content

ByteDance announced **Seedance 2.5** on June 23, 2026 at its Volcano Engine FORCE conference. Enterprise beta launched immediately; public launch targeted for early July 2026.

### Three Headline Features

**1. Native 30-Second Video (No Stitching)**
The entire 30-second clip is generated in a single pass — no segment stitching. Motion, lighting, and subject identity stay coherent end-to-end because the model reasons about the whole shot at once. This makes Seedance 2.5 the first major closed commercial AI video tool to reach this duration natively (LTX-2.3 generates up to 20s; Wan 3.0 up to 30s but open source).

**2. 50 Multimodal References**
Up to 50 reference inputs (images, video frames, audio, text) in a single generation. Enables reliable character, product, and brand consistency across a full series without drift.

**3. Local Editing**
Target specific areas of a generated 30-second clip and modify them without regenerating the whole video. Fix a hair color, swap a logo, adjust lighting in one section — while preserving visual style and identity elsewhere.

### Technical Specs
- Native 4K with 10-bit color depth (not upscaled)
- T2V, I2V, V2V pipelines
- No independent benchmarks yet — all specs are ByteDance's stated claims from June 23 keynote

### Competitive Impact
Seedance 2.5 directly challenges Wan 3.0 on long-form native generation. Already available via Runway API (as Seedance 2.0 variants) and in LTX Studio. The 30-second single-pass capability is a meaningful advance for storytelling workflows — previous tools required stitching shorter clips together.
