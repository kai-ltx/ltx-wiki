# Kling 4.0 Full Launch (Oct 15) and API Rollout (Oct 21), 2026

**Source:** https://blog.sandbase.ai/kling-4-0-launch-what-shipped-2026/
**Date:** 2026-10-23
**Retrieved:** 2026-10-26

## Content

SandBase (an API aggregator that resells Kling access; secondary source with its own API tests) sorted the rollout as of 2026-10-23:

| Date (2026) | Event |
|---|---|
| Sep 28 | Kling 4.0 announced; Kling 4.0 Flash early access for Ultra Yearly subscribers |
| Sep 30 | Kuaishou names Yu Yue director and CEO of Kling AI (36Kr) |
| Oct 15 | Full launch for all users; creation page redesigned; MCP and CLI access mentioned (Kuaishou press release via GlobeNewswire/Yahoo Finance, dated Oct 16, labeled paid release) |
| Oct 16 | Kuaishou shares open up 5%+, back above HK$30, then give back gains |
| Oct 21 | Kling 4.0 API launches with gradual global access (Longbridge/Wallstreetcn, TokenPost); integrations at Meitu, iQiyi, Tencent products |

Kuaishou claims: native single-pass up to 30 s; Omni Reference up to 15 assets plus up to 10 keyframes; up to 10-bit HDR; 4K/1080p/21:9 "will also support". No system card or benchmarks published.

SandBase API tests (Oct 23, four endpoints: text, image, reference, edit):
- Confirmed: 3-30 s single pass (30.04 s clip, $4.71 at 720p), 720p/1080p, 21:9, start/end frames, up to 10 ref images + 5 ref videos, video editing, always-on stereo AAC audio.
- Not available via API: 10 keyframes, multi-shot, elements with voices, 10-bit HDR, 4K (outputs 8-bit yuv420p H.264).
- First 5 s text-to-video call took 339 s (launch-week queue).
- SandBase list price: Kling V4 T2V/I2V/Reference $1.18 per run; Video Edit $8.46 per run.
- Consumer pricing (kie.ai, third-party): 15 credits/s at 1080p, 10 at 720p (450 credits for 30 s 1080p).

Market context: Seedance 2.5 (4-30 s) and Wan 3.0 (2-30 s) also generate 30 s clips; Wan 3.0 is cheaper per second than Kling 4.0, Seedance 2.5 more expensive (SandBase catalog).

Finance (36Kr, 2026-10-16): Kling raised ~$3B at $18B post-money (July); Kuaishou market cap ~US$15.6B on Oct 13 (HK$28.5 record low); Kling 2025 revenue ~CNY 1.1B (<1% of Kuaishou's CNY 142.8B), loss-making; Bloomberg reports IPO prep with CICC, Goldman Sachs, UBS as early as next year.

Corroboration: shattered.io (2026-10-25) dates launch to Oct 15 (TechPilot tracker, KDH News wire), launch promo to Oct 29, and reports Kling replaced Ultra plan with Ultra+ around Oct 17.
