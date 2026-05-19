# LTX Video on fal.ai and Replicate: 2026 Pricing and Model Updates

**Source:** https://fal.ai/models/fal-ai/ltx-2/image-to-video ; https://replicate.com/lightricks/ltx-2.3-pro ; https://www.nemovideo.com/blog/ltx-2-3-pricing
**Date:** 2026-04-01
**Retrieved:** 2026-05-19

## Content

### fal.ai LTX-2 Models

Two LTX-2 variants available on fal.ai as of April 2026:

**fal-ai/ltx-2 (Pro)**  
- Endpoint: `https://fal.ai/models/fal-ai/ltx-2/image-to-video`
- Higher fidelity; integrated audio synthesis
- Pricing (effective April 1, 2026):
  - 1080p: $0.06/second of output video
  - 1440p: $0.12/second
  - 2160p (4K): $0.24/second
- Example: 10-second 4K clip = $2.40; 10-second 1080p = $0.60

**fal-ai/ltx-2/text-to-video/fast**  
- Endpoint: `https://fal.ai/models/fal-ai/ltx-2/text-to-video/fast`
- Faster generation, lower cost
- Pricing:
  - 1080p: $0.04/second
  - 1440p: $0.08/second
  - 2160p: $0.16/second

**fal.ai LTX-2.3**  
- Endpoint: `https://fal.ai/ltx-2.3`
- Latest 22B model with native audio-to-video; portrait 9:16 support
- Pricing details at https://fal.ai/pricing (updated April 2026)

### Replicate LTX Models (as of May 2026)

**lightricks/ltx-2.3-pro**  
- URL: https://replicate.com/lightricks/ltx-2.3-pro
- Features: audio-to-video, retake, extend, portrait mode, up to 4K / 50 FPS
- Higher fidelity than Fast variant
- Replicate billing: per-second compute; exact rates not published but comparable to fal.ai Pro tier

**lightricks/ltx-2-fast**  
- URL: https://replicate.com/lightricks/ltx-2-fast
- Built for storyboarding, mobile apps, and high-volume production
- Lower latency; trades some quality for speed

**lucataco/ltx-video-iclora**  
- URL: https://replicate.com/lucataco/ltx-video-iclora
- Community model with IC-LoRA support for style/character consistency
- Multiple versions available (see versions tab)

### Quick-Start Code — fal.ai Python

```python
import fal_client

handler = fal_client.submit(
    "fal-ai/ltx-2/image-to-video",
    arguments={
        "image_url": "https://example.com/frame.jpg",
        "prompt": "cinematic slow zoom, golden hour",
        "resolution": "1080p",
        "duration": 10,
    },
)
result = handler.get()
print(result["video"]["url"])
```

### Quick-Start Code — Replicate Python

```python
import replicate

output = replicate.run(
    "lightricks/ltx-2.3-pro",
    input={
        "prompt": "A surfer rides a wave at sunset",
        "image": open("frame.jpg", "rb"),
        "fps": 24,
        "width": 1280,
        "height": 720,
    }
)
print(output)
```

### References

- https://fal.ai/pricing
- https://fal.ai/learn/devs/ltx-video-2-pro-image-to-video-developer-guide
- https://replicate.com/lightricks
- https://www.nemovideo.com/blog/ltx-2-3-pricing
- https://www.buildmvpfast.com/api-costs/ai-video
