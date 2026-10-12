# Kling 4.0 Pre-Launch Guide (fal.ai): Spec Table, Coming-Soon Flags, Flash vs Full

**Source:** https://fal.ai/learn/tools/what-is-kling-4-0
**Date:** 2026-09-29
**Retrieved:** 2026-10-12

## Content

fal.ai pre-launch explainer (author John Ozuysal) built from Kling's release notes and showcase clips; **no independent testing**. As of the Oct 12 retrieval, no search result showed a dated full public launch of Kling 4.0; Kling has only committed to "October 2026" with no day. Kling 4.0 is "coming to fal soon" via the same API as Kling O3 and Kling 3.0 (endpoint names and pricing to be posted at launch). fal also lists LTX 2.3 (not 2.5) in its video model nav.

**Spec table (Kling 4.0 full / Flash):**
- Text-to-video yes / yes; image-to-video yes / first frame only; Omni Reference yes / yes.
- Duration **3-30 s** (Flash 3-20 s). Resolution 720p/1080p/4K (Flash 720p only). Aspect ratios 21:9 (new), 16:9, 1:1, 9:16, Auto.
- Up to **10 keyframe images**; text input up to **8,000 tokens**; stereo two-channel audio; on-screen text incl. emoji and logos; spoken languages incl. new German and French.
- **10-bit HDR at 1080p/4K is "coming soon"** (Flash is 8-bit SDR).
- References: up to 10 images, up to 5 videos (30 s combined), up to 7 elements (up to 3 video-based), voice reference only for audio, **15 total**.
- Video editing: up to 5 input clips (1 primary), each 3-30 s, 30 s combined. Edits: expressions, body movement, camera position, style, background swap, character replacement, element removal.
- **Video extension up to 2 minutes is also "coming soon"**.

**Editor's caveat (fal):** the 30 s combined cap applies to reference/edit inputs, so with a 3 s minimum per supporting clip a one-supporting-clip edit caps the primary video at 27 s; expect heavy source-footage trimming.

Context: fal's Sep 8 "10 Best AI Video Generators in 2026" lists Seedance 2.5, MiniMax H3 Max, Wan 3.0, Veo 3.1, Kling O3 4K. fal's model nav as of Oct 12 also lists Gemini Omni, Happy Horse 1.1, Happy Oyster, PixVerse V6, Grok Imagine 1.5; Vidu Q4 (3-16 s, 4K, native audio, up to 12 reference images + 3 voice clips) and Kandinsky 6.0 (Lite/Pro/VSR) appear in "Recently Added".
