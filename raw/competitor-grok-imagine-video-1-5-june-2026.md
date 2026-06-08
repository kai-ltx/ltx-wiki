# Grok Imagine Video 1.5: xAI's Image-to-Video Model With Native Audio

**Source:** https://x.ai/news/grok-imagine-1-5
**Date:** 2026-06-03
**Retrieved:** 2026-06-08

## Content

xAI launched Grok Imagine Video 1.5 as an API preview on June 3, 2026.

### Key Facts

- Model ID in xAI API: `grok-imagine-video-1.5-preview`
- Type: image-to-video (not text-to-video)
- Output resolution: 720p (480p also supported)
- Duration: up to ~6 seconds per clip
- Audio: native synchronized audio (dialogue, SFX, ambient, music) generated in same inference pass

### Performance

- Debuted at #1 on Artificial Analysis Video Arena Image-to-Video leaderboard with Elo 1404 ±6
- This beats all other I2V models at launch date
- xAI claims gains in cloth dynamics, water simulation, hair motion, and object interaction
- High-motion scenes show reduced subject deformation and sharper micro-expressions

### Pricing (preview, subject to change)

- $0.08 per second at 480p
- $0.14 per second at 720p
- $0.01 image input cost
- Rate limit: 60 requests per minute

### How It Works

- Input: source image + text prompt describing motion/camera/atmosphere
- The model animates the scene while staying faithful to the source image
- Prompt controls camera moves, pacing, atmosphere, sound design
- Preservation language in prompts helps anchor visual identity

### Access

- Available via xAI API directly
- Also available via WaveSpeedAI: `wavespeed.ai/models/x-ai/grok-imagine-video-v1.5/image-to-video`
- Available on fal.ai: `fal.ai/models/xai/grok-imagine-video/v1.5/image-to-video`
- Available on Replicate

### Best Use Cases

- Animating product photos with cinematic camera motion
- Character animation from illustrations/portraits
- Social ad variations from hero images
- Storyboard-to-video workflows (stage each frame, animate, chain shots)

### Limitations (preview)

- Identity drift across longer clips
- Prompt overloading when too many motion instructions given
- Audio is plausible but not precisely controllable
- Currently 720p max (no 4K)

### Comparison Notes

- vs Runway Gen-4.5: Runway leads on T2V; Grok I2V leads on I2V leaderboard
- vs Seedance 2.0: Seedance is broader general-purpose; Grok 1.5 is a focused image animator
- vs Wan 2.7: Wan has more workflow tools (editing, extension); Grok 1.5 is simpler I2V
