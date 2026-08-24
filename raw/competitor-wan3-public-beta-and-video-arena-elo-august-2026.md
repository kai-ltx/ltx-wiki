# Wan 3.0 Public Beta (Aug 6) Takes #1 in AA Text-to-Video-with-Audio; Full Arena Elo Snapshot

**Source:** https://artificialanalysis.ai/video/leaderboard/text-to-video
**Date:** 2026-08-24
**Retrieved:** 2026-08-24

## Content

Additional sources: https://artificialanalysis.ai/video/leaderboard/image-to-video, https://pexo.ai/blog/what-is-wan-3-0-6318 (2026-08-07)

### CORRECTION FLAG: Wan 3.0 is NOT open weights

Multiple in-window sources contradict the widely repeated "Wan 3.0 = 60B MoE, Apache 2.0" claim. Per Pexo's 2026-08-07 writeup, sourced to Chinese tech press (IT之家, 第一财经, ITBear) dated 2026-08-06: Wan 3.0 is a **closed public beta and paid API from Alibaba Tongyi Lab** — no downloadable 3.0 weights, no Hugging Face checkpoint, no GitHub repo, no ComfyUI node. **Alibaba's openly released Wan weights stop at Wan 2.2.** The article explicitly states that claims of open weights, a specific open-source license, or a parameter count for Wan 3.0 "come from unofficial lookalike sites and are unverified."

Corroborating signal: the Artificial Analysis leaderboard lists Wan 3.0 (Aug 2026) with API pricing "**Coming soon**" and **no Hugging Face open-weights badge**, unlike MiniMax H3, MAGI-2 Preview and all LTX entries which do carry the badge. **The wiki's existing "Wan 3.0 (60B MoE, Apache 2.0)" entry should be reviewed against a primary Alibaba source before being relied on.**

### Wan 3.0 public beta details (2026-08-06)

- **Public beta opened 2026-08-06** (evening, China time). Developer: Alibaba Tongyi Lab.
- Headline capability: **up to 30 seconds in a single continuous shot** ("一镜到底"), enabling uninterrupted camera language (push, pull, pan, track) without stitching clips.
- **Document-to-video** — first in the Wan line to accept **doc, xls, ppt, pdf, md** files (plus web pages) as creative reference. Turns a slide deck or PDF report directly into video.
- Consistency: character, prop and scene held stable via "multi-dimensional feature alignment."
- Extras: smart duration recommendation, video extension.
- Inputs: text / image / audio / video / document.
- **API pricing: ¥0.3 / ¥0.6 / ¥1.2 per second at 480P / 720P / 1080P** (~$0.04 / $0.08 / $0.17 per second). A 30-second 1080P clip runs ~¥36 (~$5).
- Access channels are China-region Alibaba products: Alibaba Cloud Model Studio (百炼), tongyi.aliyun.com/wan, 千问创作 / create.qianwen.com, 万镜一刻, IF STUDIO, 堆友, and a grayscale rollout inside the Qwen app.
- Wan 3.0 produces **visual only — no generated soundtrack** per Pexo's comparison table (note: this conflicts with AA listing it in the "with audio" T2V leaderboard; treat as unresolved).

### Artificial Analysis Text-to-Video Leaderboard — WITH AUDIO (retrieved 2026-08-24)

Flagged as added in the last month: **LTX-2.5 Fast, LTX-2.5 Pro, Wan 3.0, Vidu Q3 Turbo, MiniMax H3**.

| # | Creator | Model | Elo | 95% CI | Samples | Released | API $/min 1080p |
|---|---|---|---|---|---|---|---|
| 1 | Alibaba | Wan 3.0 | 1,244 | -10/10 | 5,679 | Aug 2026 | Coming soon |
| 2 | Google | Gemini Omni Flash | 1,238 | -6/6 | 16,181 | May 2026 | $6.00 |
| 3 | MiniMax | MiniMax H3 (open weights) | 1,228 | -8/8 | 8,316 | Jul 2026 | $7.80 |
| 4 | ByteDance Seed | Dreamina Seedance 2.0 720p | 1,221 | -6/6 | 22,864 | Mar 2026 | $9.07 |
| 5 | Alibaba | Wan2.7-260612 | 1,156 | -6/6 | 17,231 | Jun 2026 | $9.00 |
| 6 | Alibaba-ATH | HappyHorse-1.1 | 1,145 | -6/6 | 17,334 | Jun 2026 | $9.90 |
| 7 | Alibaba-ATH | HappyHorse-1.0 | 1,121 | | 9,311 | Apr 2026 | $13.20 |
| 8 | Alibaba | Wan 2.7 | 1,107 | | 5,749 | Apr 2026 | $9.00 |
| 9 | KlingAI | Kling 3.0 1080p (Pro) | 1,106 | | 20,666 | Feb 2026 | $20.16 |
| 10 | Skywork AI | SkyReels V4 | 1,101 | | 6,231 | Mar 2026 | $21.00 |
| 11 | KlingAI | Kling 3.0 720p (Standard) | 1,098 | | 19,830 | Feb 2026 | $15.12 |
| 12 | Google | Veo 3.1 Lite | 1,090 | | 8,609 | Mar 2026 | $4.80 |
| 13 | Google | Veo 3.1 | 1,089 | | 9,165 | Jan 2026 | $24.00 |
| 14 | KlingAI | Kling 3.0 Omni 720p | 1,089 | | 8,808 | Feb 2026 | $13.44 |
| 15 | KlingAI | Kling 3.0 Omni 1080p | 1,088 | | 8,994 | Feb 2026 | $16.80 |
| 16 | Google | Veo 3.1 Fast | 1,087 | | 18,560 | Jan 2026 | $9.00 |
| 17 | Vidu | Vidu Q3 Pro | 1,075 | | 18,521 | Jan 2026 | $9.60 |
| 18 | PixVerse | PixVerse V6 | 1,072 | | 10,361 | Mar 2026 | $6.90 |
| **19** | **Lightricks** | **LTX-2.5 Pro (open weights)** | **1,063** | **-10/10** | **2,443** | **Aug 2026** | **$10.20** |
| **20** | **Lightricks** | **LTX-2.5 Fast (open weights)** | **1,063** | **-10/10** | **2,365** | **Aug 2026** | **$7.80** |
| 21 | SpaceXAI | grok-imagine-video | 1,062 | | 17,636 | Jan 2026 | $4.20 |
| 22 | Vidu | Vidu Q3 Turbo | 1,032 | | 2,636 | Feb 2026 | $3.90 |
| 23 | Alibaba | Wan 2.6 | 1,025 | | 7,520 | Dec 2025 | $9.00 |
| 24 | ByteDance Seed | Seedance 1.5 pro | 1,000 (anchor) | | 12,046 | Dec 2025 | $11.86 |
| 25 | KlingAI | Kling 2.6 Pro (January) | 982 | | 8,202 | Jan 2026 | $8.40 |
| 26 | Lightricks | LTX-2.3 Fast | 975 | | 11,948 | Mar 2026 | $2.40 |
| 27 | Lightricks | LTX-2.3 Pro | 958 | | 11,370 | Mar 2026 | $4.80 |
| 28 | PixVerse | PixVerse V5.6 | 949 | | 6,819 | Feb 2026 | Coming soon |
| 29 | Lightricks | LTX-2 Fast | 942 | | 6,319 | Oct 2025 | $2.40 |
| 30 | Sapiens AI | Agnes-Video-V2.0 | 916 | | 5,184 | May 2026 | $0.30 |
| 31 | Lightricks | LTX-2 Pro | 915 | | 6,304 | Oct 2025 | $3.60 |

**T2V without audio (top 5):** Gemini Omni Flash 1,322 | MiniMax H3 1,303 | HappyHorse-1.0 1,284 | Dreamina Seedance 2.0 720p 1,267 | HappyHorse-1.1 1,261. Best open weights: MiniMax H3 1,303, then **LTX-2.5 Fast 1,211, LTX-2.5 Pro 1,205**.

### Artificial Analysis Image-to-Video Leaderboard — WITH AUDIO (retrieved 2026-08-24)

Added in the last month: **LTX-2.5 Fast, LTX-2.5 Pro, Vidu Q3 Turbo, MiniMax H3, MAGI-2 Preview**.

1. Dreamina Seedance 2.0 720p — **1,191** (Mar 2026, $9.07/min)
2. MiniMax H3 (open weights) — **1,184** (Jul 2026, $7.80/min)
3. Gemini Omni Flash — **1,182** (May 2026, $6.00/min)
4. grok-imagine-video-1.5 — **1,111** (May 2026, $8.40/min)
5. HappyHorse-1.1 — **1,106** (Jun 2026, $9.90/min)
6. MAGI-2 Preview (Sand.ai, open weights) — **1,100** (Aug 2026, pricing coming soon)
7-10. Wan 2.7 1,085 | SkyReels V4 1,084 | HappyHorse-1.0 1,084 | Veo 3.1 1,084
11-13. grok-imagine-video 1,076 | Veo 3.1 Fast 1,073 | Kling 3.0 1080p Pro 1,072
14-19. Veo 3.1 Lite 1,067 | Kling 3.0 720p 1,066 | PixVerse V6 1,065 | Kling 3.0 Omni 1080p 1,059 | Vidu Q3 Pro 1,059 | Kling 3.0 Omni 720p 1,048
**20. LTX-2.5 Fast — 1,043** ($7.80/min) | 21. Vidu Q3 Turbo 1,039 | **22. LTX-2.5 Pro — 1,016** ($10.20/min)
23-31. Kling 2.6 Pro 1,004 | Seedance 1.5 pro 1,000 | PixVerse V5.6 957 | LTX-2.3 Fast 955 | LTX-2.3 Pro 952 | LTX-2 Fast 929 | Agnes-Video-V2.0 919 | Wan 2.6 892 | LTX-2 Pro 871

**I2V without audio (top 5):** Gemini Omni Flash 1,366 | MiniMax H3 1,346 | Dreamina Seedance 2.0 720p 1,337 | grok-imagine-video-1.5 1,328 | grok-imagine-video 1,325. Best open weights: MiniMax H3 1,346, then **Cosmos3-Super-Image2Video-4Step 1,263 and Cosmos3-Super-Image2Video 1,244** (NVIDIA Cosmos 3 — note these outrank LTX-2.5 on open-weights I2V-no-audio and are not in the with-audio table).

### Key Elo shifts in the 2026-07-21 to 2026-08-24 window

- **Wan 3.0 took #1 in T2V-with-audio (1,244)**, displacing Gemini Omni Flash (1,238) — a 6-point margin against a -10/+10 CI, so effectively a statistical tie (AA lists both in range 1-2).
- **MiniMax H3 entered at #3 T2V-with-audio / #2 I2V-with-audio** and immediately became the top open-weights model in all four AA video categories.
- **MAGI-2 Preview entered I2V-with-audio at #6 (1,100)**.
- **LTX-2.5 Pro/Fast entered at #19-20 T2V-with-audio (both 1,063)** and #20/#22 I2V-with-audio (1,043 / 1,016) — a ~100-148 point improvement over LTX-2.3 but leaving LTX 3rd among open-weights families behind MiniMax H3 and MAGI-2/Cosmos 3.
- Runway has **no model in the top 31 of either T2V or I2V** with-audio leaderboards.
- AA methodology: Elo from blind pairwise user votes; Seedance 1.5 pro is the 1,000 anchor; API pricing reflects cost to generate 1 minute of 1080p at default settings.
