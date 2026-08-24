---
title: Grok Imagine Video 1.5 (xAI)
type: competitor
created: 2026-06-08
updated: 2026-08-24
sources:
  - raw/competitor-grok-imagine-video-1-5-june-2026.md
  - raw/competitor-grok-imagine-1080p-update-and-kling-q2-revenue-august-2026.md
tags:
  - competitor
  - video-generation
  - xai
  - image-to-video
  - proprietary
  - cloud-api
---

# Grok Imagine Video 1.5 (xAI)

Grok Imagine Video 1.5 is xAI's image-to-video generation model, launched as an API preview on June 3, 2026. It is notable for debuting at #1 on the Artificial Analysis Video Arena image-to-video leaderboard with an Elo of 1404 ±6.

## Key Facts

- **Developer:** xAI (Elon Musk's AI company)
- **Type:** Image-to-video at launch; **text-to-video added with native 1080p on 2026-08-01**
- **Model ID:** `grok-imagine-video-1.5-preview`
- **Status:** API preview as of June 3, 2026
- **Output:** Up to 720p at launch; **native 1080p as of 2026-08-01** (480p also supported)
- **Duration:** Short clips (~6 seconds)
- **Audio:** Native synchronized audio (dialogue, SFX, ambient, music) in same inference pass

## Performance

- **#1 on Artificial Analysis Video Arena I2V leaderboard** (Elo 1404 ±6) at launch
- xAI claims gains over prior generation in: cloth dynamics, water simulation, hair motion, object interaction
- High-motion scenes: reduced subject deformation and sharper micro-expressions
- Contrast: [[competitor-runway|Runway Gen-4.5]] holds #1 on the Text-to-Video leaderboard (Elo 1247)

## August 1, 2026 Update (build v1.3.28)

An incremental update to Grok Imagine Video 1.5 rolled out **2026-08-01**, distinct from the June 3, 2026 launch:

- **Voice consistency** via a new **multi-channel audio reference** system — anchors generated content to specific voice profiles instead of drifting accents and timbre between scenes. Previous versions had lip-sync and audio generation but unstable cross-scene voice.
- **Native 1080p output** for **both text-to-video and image-to-video** pipelines — no post-processing upscaling step. Framed as a workflow win, not just a quality bump. This supersedes the 720p ceiling described elsewhere on this page, and confirms Grok Imagine now does T2V as well as I2V.
- **Multi-reference support:** up to **7 image references** and **3 audio inputs** simultaneously, for character / environment / object consistency across generations.
- Built on xAI's Aurora-driven models.
- **All new capabilities are subscriber-only.** Free-tier X users have had image and video generation access "pulled back significantly" during 2026 — a deliberate monetization bet.
- **Pricing: $0.08 per second**, reported as one of the cheapest frontier video models on the market. (Artificial Analysis lists grok-imagine-video-1.5 at **$8.40/min** for 1080p, and the older grok-imagine-video at **$4.20/min**.)
- xAI signals continued iterative cadence; community-driven video extension and prompt-based consistency controls are said to be in the pipeline.

### Adjacent Grok Imagine releases (image side)

- **Grok Imagine Image 2.0** launched as the new **Quality Mode** on grok.com/imagine and the Grok iOS/Android apps: stronger instruction following, sharper text, precise region-level editing, smart resize, templates, multi-image compositing, multi-reference generation. As of **2026-08-07** it sat **#2 on Arena leaderboards for both text-to-image and image editing**, behind OpenAI's gpt-image-2.
- **Native meme generation** announced by Elon Musk on **2026-08-09**.

### Arena standing (Artificial Analysis, 2026-08-24)

| Model | Category | Rank | Elo |
|---|---|---|---|
| grok-imagine-video-1.5 | Image-to-video with audio | **#4** | **1,111** |
| grok-imagine-video-1.5 | Image-to-video without audio | #4 | 1,328 |
| grok-imagine-video | Image-to-video with audio | #11 | 1,076 |
| grok-imagine-video | Text-to-video with audio | #21 | 1,062 |

Note the drift from the June 2026 launch claim of "#1 I2V at Elo 1404" — that was AA's I2V board at a different point in time and before [[competitor-minimax-hailuo|MiniMax H3]], Dreamina Seedance 2.0 and Gemini Omni Flash reshaped the top of the table. On the current with-audio board, grok-imagine-video-1.5 sits just below Seedance 2.0 (1,191), MiniMax H3 (1,184) and Gemini Omni Flash (1,182), and comfortably above **LTX-2.5 Fast (1,043)** and **LTX-2.5 Pro (1,016)**.

## How It Works

Grok Imagine Video 1.5 takes a single still image and animates it according to a natural-language prompt. It does not generate scenes from scratch — it starts from the source image and animates it while preserving visual identity. The prompt controls camera movement, pacing, atmosphere, and sound design.

### Inputs

- **Image:** Source still (URL or upload)
- **Prompt:** Natural-language description of motion, camera, atmosphere, and audio
- **Duration:** Configurable
- **Resolution:** 480p or 720p

### Output

- Video clip with natively generated synchronized audio
- Audio includes dialogue, sound effects, ambient sound, and music

## Pricing (Preview, as of June 2026)

| Resolution | Price per second |
|---|---|
| 480p | $0.08 |
| 720p | $0.14 |

- Image input cost: $0.01
- Rate limit: 60 requests per minute

## API Access

- **Direct:** xAI API (`docs.x.ai/developers/models/grok-imagine-video-1.5-preview`)
- **WaveSpeedAI:** `wavespeed.ai/models/x-ai/grok-imagine-video-v1.5/image-to-video`
- **fal.ai:** `fal.ai/models/xai/grok-imagine-video/v1.5/image-to-video`
- **Replicate:** `replicate.com/xai/grok-imagine-video-1.5`

## Best Use Cases

- Animating product photos for ad creatives
- Character animation from illustrations or portraits
- Rapid A/B testing: multiple motion directions from the same hero image
- Storyboard-to-video: stage frames, animate each, chain into longer scenes
- Social clips where visual identity must be preserved

## Prompting Tips

Effective prompts combine camera direction, subject motion, mood, and audio intent:

```
Slow cinematic push-in, warm sunset light, fabric moves gently in the wind,
soft ambient street sound, preserve the subject and composition from the source image.
```

Key components: camera type, subject motion, light mood, audio description, identity-preservation instruction.

## Limitations (Preview)

- Maximum 720p at the June 2026 preview; **native 1080p as of the 2026-08-01 update** (still no 4K)
- Identity drift across longer clips
- Audio is plausible but not precisely controllable
- Max ~6 seconds per clip
- API still in preview; rate limits and latency may shift
- Safety and licensing requirements for commercial use apply

## Competitive Position

| Dimension | Grok Imagine Video 1.5 | Runway Gen-4.5 | [[wan-video\|Wan 2.7]] |
|---|---|---|---|
| Type | Image-to-video | Text-to-video (+ I2V) | Multi-mode |
| I2V leaderboard | #1 (Elo 1404) | Strong | Competitive |
| T2V leaderboard | N/A | #1 (Elo 1247) | Competitive |
| Native audio | Yes | No | Yes |
| Max resolution | 720p | 4K (paid) | 1080p |
| Open weights | No | No | Yes (Apache 2.0) |
| Pricing | $0.08–0.14/s | $0.05–0.50/s | ~$6/min via providers |

## Context: xAI's Entry into Video Generation

Grok Imagine Video 1.5 marks xAI's first significant entry into the video generation space. xAI previously focused on large language models (Grok 1, 2, 3) and image generation (Grok Imagine). The I2V launch signals xAI is broadening into multimodal generation. The model's immediate #1 I2V leaderboard position puts competitive pressure on established players.

Note: Grok 5 (xAI's next LLM) was still in training as of June 2026 with a low-probability June ship date (12–33% on prediction markets).

## See Also

- [[competitor-runway]] — Runway Gen-4.5, #1 text-to-video
- [[competitor-landscape-overview]] — Full competitive map
- [[wan-video]] — Wan 2.7 open-source competitor
- [[competitor-kling]] — Kling 3.0 / O3
- [[inference-providers-overview]] — API providers including WaveSpeedAI and fal.ai
