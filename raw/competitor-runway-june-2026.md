# Runway Updates — June 2026

**Source:** https://runwayml.com/changelog, https://releasebot.io/updates/runwayai, https://runwayml.com/news/introducing-agent-2
**Date:** 2026-06-30
**Retrieved:** 2026-06-30

## Content

### Studio Trim (June 18, 2026)
New feature for all Runway plans: **Studio Trim** lets users stitch, reorder, and export a final video all in one place inside Runway Studio. Addresses a long-standing workflow gap — clips can now be assembled into a finished export without leaving the platform.

### Agent 2.0 (June 25, 2026)
Runway introduced **Agent 2.0**, an upgraded agentic experience specifically targeted at **marketers**:
- Analyzes existing ad performance data (Meta, YouTube, TikTok, Google) and builds next-generation ad variants
- Generates full campaign assets — text, image, video — in one conversation
- Automatically cuts to platform-correct aspect ratios: 9:16 (Reels/Stories), 16:9 (YouTube), 1:1 (feed)
- Localizes copy and visuals for new markets without rebuilding from scratch
- Available for all users; promotional code AGENT for 30% off any plan

Agent 2.0 positions Runway not just as a generation tool but as an autonomous marketing execution layer. Different from Agent 1.0 (May 13, 2026) which was a general creative partner; Agent 2.0 is narrowed to marketing/performance use cases.

### Seedance 2.0 4K (June 24, 2026 — API)
Seedance 2.0 now supports 4K output via the Runway API:
- Six new 4K ratio values: 3840:1646 (21:9), 3840:2160 (16:9), 3840:2880 (4:3), 3840:3840 (1:1), 2880:3840 (3:4), 2160:3840 (9:16)
- 4K generations billed at 150 credits per second
- Existing 480p, 720p, 1080p options unchanged

### Seedance 2.0 Mini (June 26, 2026 — API)
New lightweight variant: **Seedance 2.0 Mini** (`seedance2_mini`):
- Faster/cheaper than Seedance 2.0 standard
- Supports T2V, I2V, V2V
- Durations 4–15 seconds, output at 480p or 720p
- Keyframe control, reference images, reference videos, generated audio all supported
- Billed at 16 credits/second (64 credit minimum per generation)

### HappyHorse 1.0 (May 29, 2026 — API, newly documented)
`happyhorse_1_0` — available via Runway API:
- T2V from text prompt or first-frame image; 3–15 second durations
- 10 output dimensions across 720p and 1080p for T2V
- I2V preserves input aspect ratio + optional motion prompt
- This is a third-party/licensed model added to Runway's model marketplace (not a Runway-developed model)
