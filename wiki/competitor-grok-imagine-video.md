---
title: Grok Imagine Video 1.5 (xAI)
type: competitor
created: 2026-06-08
updated: 2026-06-08
sources:
  - raw/competitor-grok-imagine-video-1-5-june-2026.md
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
- **Type:** Image-to-video (not text-to-video)
- **Model ID:** `grok-imagine-video-1.5-preview`
- **Status:** API preview as of June 3, 2026
- **Output:** Up to 720p, 480p also supported
- **Duration:** Short clips (~6 seconds)
- **Audio:** Native synchronized audio (dialogue, SFX, ambient, music) in same inference pass

## Performance

- **#1 on Artificial Analysis Video Arena I2V leaderboard** (Elo 1404 ±6) at launch
- xAI claims gains over prior generation in: cloth dynamics, water simulation, hair motion, object interaction
- High-motion scenes: reduced subject deformation and sharper micro-expressions
- Contrast: [[competitor-runway|Runway Gen-4.5]] holds #1 on the Text-to-Video leaderboard (Elo 1247)

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

- Maximum 720p (no 4K support at launch)
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
