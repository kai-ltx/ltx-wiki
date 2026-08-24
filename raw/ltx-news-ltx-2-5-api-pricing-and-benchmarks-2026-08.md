# LTX-2.5 API: Pricing, Variant Limits, and Vendor Benchmark Claims

**Source:** https://docs.ltx.io/pricing
**Date:** 2026-08-11
**Retrieved:** 2026-08-24

## Content

### API variants and limits (docs.ltx.io/models/ltx-2-5)
Two API variants: **`ltx-2-5-fast`** (speed/low cost, up to 4K) and **`ltx-2-5-pro`** (higher fidelity, tops out at 1080p). Both support text-to-video, image-to-video and audio-to-video, in portrait and landscape. Neither supports retake, extend, or reframe (those remain `ltx-2-3-pro` only).

Duration/FPS support matrix:
- `ltx-2-5-fast`: 720p and 1080p at 24/25 fps → 6, 8, 10, 12, 14, 16, 18, **20 seconds**; 720p/1080p at 48/50 fps → 6, 8, 10 s; 1440p and 4K at 24/25/48/50 fps → 6, 8, 10 s.
- `ltx-2-5-pro`: 720p and 1080p at 24/25/50 fps → 6, 8, 10 s only.
- Resolutions: 720p `1280x720`/`720x1280`; 1080p `1920x1080`/`1080x1920`; 1440p `2560x1440`/`1440x2560`; 4K `3840x2160`/`2160x3840`.
- **Automatic duration**: send `"duration": null` (field still required) on text-to-video and image-to-video; cannot be combined with `last_frame_uri`. Prepaid accounts have credits held against the maximum duration for the chosen resolution/fps, released on completion.

### API pricing, per second of output (as of 2026-08-24)
`ltx-2-5-fast` (text-to-video, image-to-video, audio-to-video, all identical):
- 720p — **$0.09/sec**
- 1080p — **$0.13/sec**
- 1440p — **$0.19/sec**
- 4K — **$0.30/sec**

`ltx-2-5-pro`:
- 720p — **$0.12/sec**
- 1080p — **$0.17/sec**

For comparison, LTX-2.3 remains substantially cheaper: `ltx-2-3-fast` $0.03 (720p) / $0.06 (1080p) / $0.12 (1440p) / $0.24 (4K); `ltx-2-3-pro` $0.04 / $0.08 / $0.16 / $0.32. Audio-to-video on `ltx-2-3-pro`: $0.06 / $0.10 / $0.18 / $0.34.
Other endpoints (still LTX-2.3 Pro only): Retake $0.10/sec at 1080p; Extend $0.10/sec at 1080p (capped at 505 billed frames, ~21 s at 24fps); HDR Upscale $0.20 (≤1080p) / $0.40 (≤1440p) / $0.80 (≤4K) per second of input; Video Reframe $0.10 (720p) / $0.20 (1080p) per second of input.

### Vendor-reported speed and quality claims (all measured or commissioned by LTX; not independently verified)
- **6.8 seconds** to generate a 10-second 720p image-to-video clip, self-hosted at steady state on **two NVIDIA GB200 superchips** — faster than real time. The same job through LTX's own managed API took **23.7 seconds** (at 1080p; the API has no 720p tier for that measurement).
- LTX's end-to-end measurements of rivals on the same task: Gemini Omni Flash 52 s, xAI Grok 1.5 63 s, Google Veo 3.1 70 s (8-second clip), MiniMax H3 180 s, ByteDance Seedance 2.5 317 s, Kuaishou Kling 3.0 Pro 398 s.
- Blind human preference tests: **LTX-2.5 67% win rate**, Seedance 2.5 65%, Gemini Omni Flash 55%, MiniMax H3 50%, Seedance 2.0 44%, Wan 2.6 42%, FLUX 3 28%. LTX labels these results **preliminary**.
- LTX claims roughly **one-eighth the cost and one-seventh the render time** of comparable models.

### Independent scrutiny (VentureBeat, 2026-08-11)
VentureBeat's Carl Franzen checked the claims against published rates and found the one-eighth cost multiple unsupported: a 10-second 720p clip with audio costs $0.90 on LTX-2.5 Fast vs Veo 3.1 Lite $0.50 (cheaper), Veo 3.1 Fast $1.00, Gemini Omni Flash $1.00, FLUX 3 Video $1.70, HappyHorse 1.0 ~$1.82, Veo 3.1 $4.00. The render-time claim is better supported but shrinks to ~2x through LTX's own API. As of publication, **Artificial Analysis' text-to-video leaderboards did not yet score LTX-2.5**, and Gemini Omni Flash led both.

**Additional sources:** https://docs.ltx.io/models/ltx-2-5 ; https://venturebeat.com/technology/ltx-2-5-can-generate-a-10-second-ai-video-from-an-image-in-just-6-8-seconds-on-nvidia-superchips-and-its-open-weights
