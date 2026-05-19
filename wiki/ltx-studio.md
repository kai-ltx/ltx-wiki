---
title: LTX Studio
type: product
created: 2026-04-13
updated: 2026-05-19
sources:
  - https://ltx.studio
  - https://ltx.studio/pricing
  - https://ltx.studio/blog/ltx-studio-plans
  - https://ltx.studio/blog/top-ltx-studio-features
  - https://ltx.studio/solutions/use-cases
  - https://en.wikipedia.org/wiki/LTX_Studio
  - https://ltx.studio/blog/ltx-2-the-complete-ai-creative-engine-for-video-production
  - https://www.cined.com/ltx-studio-takes-its-next-big-step-editing/
  - raw/ltx-news-ltx-studio-canvas-seedance2-april-2026.md
  - raw/ltx-news-ltx-studio-flows-video-to-video-may-2026.md
  - raw/ltx-news-ltx-studio-api-async-hdr-may-2026.md
  - raw/community-ltx-studio-product-updates-apr-may-2026.md
tags:
  - ltx-studio
  - ai-video
  - platform
  - lightricks
  - saas
---

# LTX Studio

LTX Studio is [[lightricks-company]]'s flagship cloud-based AI video production platform, part of the [[ltx-ecosystem]]. Launched in February 2024 (beta) and opened to the public in August 2024, it is a web-based platform that turns creative ideas into professional videos, covering scripting, storyboarding, editing, and final delivery.

- **Website:** https://ltx.studio
- **Playground:** https://app.ltx.studio/ltx-2-playground/t2v

## Target Audience

- Filmmakers and production teams (pre-production visualization, storyboarding, shot planning)
- Marketing and advertising professionals (campaign videos, social media content)
- Creative agencies (concept validation, client pitches, rapid iteration)
- Content creators (YouTube, Instagram, TikTok content at professional grade)
- Enterprise teams (branded content at scale with collaboration features)

## Core Features

### Script-to-Video Pipeline

- Upload or write scripts automatically divided into scenes and shots
- AI extracts characters and objects as reusable "Elements"
- Choice between FLUX or Nano Banana image models for storyboard generation
- Set aspect ratio upfront for all shots

### Storyboard Generator

- Rebuilt for speed and creative control (5x faster than previous versions)
- Shot-by-shot visual generation from scripts
- Reusable elements system for consistency

### Character Consistency

- Define a character's age, ethnicity, hairstyle, wardrobe, and facial details once
- System maintains exact appearance across every shot in the project
- "Trained Actors" system for pre-built consistent characters
- Saved Elements for custom character persistence

### Advanced Camera Controls

- Keyframe-based crane lifts, 3D orbit, tracking shots
- Sketch objects onto the canvas
- Professional camera motion presets: dolly, crane, pan, handheld
- Rivals professional pre-visualization software

### Audio Design

- SFX and soundtrack generation within the platform
- Music and ambient audio generated to match scene mood
- Voice-over support for narration
- AI voiceover and lip sync
- Audio persists across visual regenerations

### Video Generation Models

- Supports multiple AI video generation models
- Veo 2 model (available from Standard tier)
- Veo 3.1 model (available from Pro tier)
- LTX's own models including [[ltx-2-overview]]
- Kling 3.0 Pro ([[competitor-kling|Kling AI]]) — cinematic AI video up to 15 seconds, multi-shot, director-style prompting (integrated April 27, 2026)
- Veo 3.1 Lite (Google) — cost-effective option for AI video at scale (integrated April 26, 2026)
- Seedance 2.0 (ByteDance) — Standard and Fast variants (integrated April 26, 2026)
- ChatGPT Image 2.0 (OpenAI) — integrated for image generation layer (May 4, 2026)

### Editing Space (April 19, 2026)

Unified image editing workspace consolidating brush tools, upscaling, camera angle adjustment, and visual fine-tuning into a single flow. CineD described this as "LTX Studio taking its next big step." Reduces the need to leave the platform for post-generation editing.

### Canvas (Collaborative Infinite Workspace)

Released late April 2026. See [[ltx-studio-canvas]] for full details.

- Teams generate, iterate, and align concepts in real time or asynchronously
- Combines image/video moodboards, visual ideation, and team collaboration
- Seamless transition from concept to production: storyboards → video generation → audio → timeline → export
- Primary visual ideation layer before full production commitment

### Flows (Workflow Automation)

Launched May 7, 2026. See [[ltx-studio-flows]] for full details.

- Visual node-based workflow builder: connect prompt, image, video, and upscaling nodes
- Smart caching: previously generated outputs reused when inputs haven't changed
- Enterprise Brand Kit integration for consistent large-scale production
- Supported node types: text/prompt, image input, video generation, upscaling, audio, export

### Video-to-Video with IC-LoRA Controls

Launched May 11, 2026.

- **Pose Control**: Extracts skeleton/pose from input video to guide character animation
- **Depth Control**: Extracts depth map to preserve 3D spatial structure through style transformation
- **Edge Control**: Extracts outlines to preserve composition while changing appearance
- Backed by [[ltx-2.3-model]]'s IC-LoRA adapters on the 22B DiT backbone
- See [[ic-lora]] for technical details

### SDR-to-HDR Conversion

Launched April 2026.

- One-click SDR-to-HDR conversion for any existing video
- Available as both a platform UI feature and via the [[ltx-video-api|LTX API]] (`POST /v2/video-to-video-hdr`)
- See [[ltx-api-async-hdr]] for API usage

### Brand Kit (Enterprise)

Launched April 2026, Enterprise plan only.

- Embed brand assets (logos, color palettes, style references) into generation pipelines
- Tightly integrated with [[ltx-studio-flows|Flows]] for consistent large-scale branded content

### Editing Capabilities

- In-app timeline-based editing module
- Export .xml files to Premiere Pro and DaVinci Resolve
- Non-destructive take management
- Animatics conversion from storyboards

### Collaboration and Export

- Project collaboration (up to 3 collaborators on Pro plan)
- Pitch deck generation
- Multiple resolution options
- Commercial-use licensing (Standard tier and above)

## Pricing (as of 2026)

| Plan | Monthly Price | Credits/Month | Key Features |
|------|--------------|---------------|--------------|
| Free | $0 | 800 (one-time) | Personal use only |
| Lite | $15/mo ($12 yearly) | 8,640 | Personal use only |
| Standard | $35/mo ($28 yearly) | 28,000 | Commercial use, Veo 2, trained actors |
| Pro | $125/mo ($100 yearly) | 110,000 | Veo 3.1, collaboration (3 users) |
| Enterprise | Custom | Unlimited | Custom model training, SSO, compliance |

### Credit Costs

- 10-second video at 720p: ~20 credits
- 10-second video at 1080p: ~40 credits

## Motion Workspace

In addition to the full production pipeline, LTX Studio offers a lightweight Motion Workspace for quick video generation:

| Interface | URL | Model |
|-----------|-----|-------|
| Motion Workspace (13B Mix) | https://app.ltx.studio/motion-workspace?videoModel=ltxv-13b | 13B mixed quality |
| Motion Workspace (Distilled) | https://app.ltx.studio/motion-workspace?videoModel=ltxv | 13B distilled (faster) |

## API Access

LTX Studio itself does **not** expose a programmatic API. For API-based video generation, use:

- [[ltx-video-api]] -- the official REST API at `api.ltx.video`
- Third-party hosts (fal.ai, Replicate, Segmind)
- Self-hosted inference with the open-source model weights

## Distinction from Open-Source Tools

LTX Studio is the commercial platform built on LTX Video models. It is distinct from:

- [[ltx-video-overview]] / [[ltx-2-overview]] - open-source model weights
- [[ltx-desktop]] - open-source desktop application
- [[ltx-integration-projects]] - ComfyUI nodes and other open-source tooling

## Use Cases

- Film and television pre-production
- Advertising concept validation
- Short films and web series
- Music videos
- Social media content (Instagram, TikTok, YouTube Shorts)
- Product marketing videos
- Brand storytelling
- UGC content
