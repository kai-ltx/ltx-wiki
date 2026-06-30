---
title: Runway (Gen-3 / Gen-4 / Agent)
type: competitor
created: 2026-04-13
updated: 2026-06-30
sources:
  - raw/competitor-product-runway.md
  - raw/competitor-runway-agent-launch-may-2026.md
  - raw/competitor-runway-gen45-benchmark-2026.md
  - raw/competitor-runway-june-2026.md
tags:
  - competitor
  - video-generation
  - runway
  - proprietary
  - cloud-platform
  - agentic
---
# Runway (Gen-3 / Gen-4 / Agent)

Runway is the industry-standard AI video generation platform, widely considered the professional benchmark in the space. Founded in 2018, Runway has been a pioneer in creative AI tools and is used by major studios, agencies, and individual creators. The platform offers Gen-3 Alpha and Gen-4 models alongside a comprehensive creative suite for video generation, editing, and manipulation.

## Model Versions

### Gen-3 Alpha (June 2024)
- Improved fidelity, temporal consistency, and expressive human motion
- Supports keyframes (first/last in Alpha; first/middle/last in Turbo)
- Available in standard and Turbo variants

### Gen-4 (March 2025)
- Major upgrade with character consistency via reference images
- Enhanced spatial understanding across camera angles
- 4K resolution output (up from 1080p in Gen-3)
- Better prompt adherence for complex instructions
- Does not currently support keyframes

### Gen-4 Turbo (2026)
- Fastest variant for rapid iteration
- Lower credit cost per generation
- Slightly reduced quality vs. standard Gen-4

### Gen-4.5 (December 2025)
- Runway's current flagship video model
- **Elo score of 1,247** on Artificial Analysis Text-to-Video benchmark (top position as of June 2026, confirmed)
- Ahead of Google Veo 3.1, Kling 3.0, and Sora 2 on that benchmark
- Supports text-to-video and image-to-video; 2–10 second clip durations

### Runway Agent (May 13, 2026)
- Agentic creative partner: takes a user from idea to fully finished, sound-designed, edited video through a single conversation
- Covers concept, story beats, visual direction, voiceover, dialogue, music, and final assembly
- Targets brand teams, marketers, creative agencies, and filmmakers
- Positions Runway as an end-to-end AI production system, not just a clip generator
- Alongside the Agent launch, API additions included: Seedance 2.0 (April), OpenAI GPT Image 2 (April 23), Gemini 3 Pro Image / Nano Banana Pro (April 30)

### Studio Trim (June 18, 2026)
New feature for all plans: **Studio Trim** lets users stitch, reorder, and export a final video all in one place inside Runway Studio. Clips assembled into a finished export without leaving the platform.

### Agent 2.0 (June 25, 2026)
Runway upgraded its Agent to **Agent 2.0**, reoriented specifically toward **marketers and performance teams**:
- Analyzes existing ad performance data (Meta, YouTube, TikTok, Google) and builds next-generation ad variants
- Generates full campaign assets in one conversation (text, image, video)
- Auto-cuts to platform-correct aspect ratios: 9:16 (Reels/Stories), 16:9 (YouTube), 1:1 (feed)
- Localizes copy and visuals across markets without rebuilding from scratch
- Available all users; 30% launch discount with code AGENT

Agent 2.0 narrows the agentic use case from general creative production (Agent 1.0) to marketing execution specifically, competing with ad-tech platforms and social content tools in addition to video generators.

### Seedance 2.0 4K (June 24, 2026 — API)
Seedance 2.0 now supports **native 4K output** via the Runway API:
- Six new 4K ratios: 3840:1646 (21:9), 3840:2160 (16:9), 3840:2880 (4:3), 3840:3840 (1:1), 2880:3840 (3:4), 2160:3840 (9:16)
- 4K billed at 150 credits/second; 480p/720p/1080p unchanged

### Seedance 2.0 Mini (June 26, 2026 — API)
New lightweight variant `seedance2_mini` added to the API:
- T2V, I2V, V2V; 4–15 second durations at 480p or 720p
- Keyframe control, reference images, reference videos, generated audio
- Billed at 16 credits/second (64 credit minimum)

### HappyHorse 1.0 (May 29, 2026 — API)
`happyhorse_1_0` — a third-party licensed model available in Runway's model marketplace:
- T2V and I2V; 3–15 second durations at 720p–1080p
- 10 output dimensions for T2V; I2V preserves input aspect ratio

## Key Features

### Character Consistency
Reference image system maintains exact character appearance (face, clothing, physical features) across multiple scenes with different camera angles and lighting. Best-in-class for narrative content requiring recurring characters.

### Creative Suite
- **Aleph:** In-video manipulation tool for direct editing
- **Act-Two:** Motion capture integration
- **Multi-Motion Brush:** Fine-grained control over motion within the frame
- **Camera controls:** Dedicated camera control system
- **Upscaling:** Built-in resolution enhancement
- **Lip sync and audio tools** (newer additions)

### Resolution and Duration
- Standard tier: 1080p
- Pro/Enterprise: Native 4K
- Up to 60 seconds of continuous video with temporal consistency

## Pricing (2026)

| Plan | Price | Credits/Month |
|------|-------|---------------|
| **Free** | $0 | 125 (one-time) |
| **Basic** | $12/mo | 625 |
| **Standard** | $28/mo | 625 |
| **Pro** | $76/mo | 2,250 |
| **Enterprise** | Custom | Custom |

Credit costs: Gen-4 ~12 credits/s, Gen-4 Turbo ~5 credits/s. Credits do NOT roll over between months.

## Strengths
- Industry-standard status with proven enterprise adoption
- Best-in-class character consistency using reference images
- Comprehensive creative suite (Aleph, Act-Two, Multi-Motion Brush, lip sync)
- Native 4K output on Pro tier
- Up to 60 seconds continuous generation
- Strong temporal consistency
- API access and enterprise features (SSO, compliance, custom models)

## Weaknesses
- No native audio generation (requires separate audio work)
- Credits don't roll over (use-it-or-lose-it)
- Expensive at scale
- Gen-4 lacks keyframe support (regression from Gen-3)
- No open-source model; fully proprietary, no local deployment
- No integrated storyboarding (separate tools, not unified workflow)
- Slower than some competitors ([[competitor-veo|Veo 3]] generates ~2.2x faster)

## Comparison to LTX Studio

**Runway's advantages:**
- More mature platform with deeper editing capabilities
- Strongest character consistency in the industry
- Longer continuous generation (60 seconds)
- Industry-standard status with proven enterprise adoption

**[[ltx-studio]] advantages:**
- Unified production workflow (script to storyboard to timeline to export)
- Multi-model access (not locked to one model family)
- Open-source model ([[ltx-2.3-model]]) available for local deployment via [[ltx-desktop]]
- Native audio generation via [[ltx-2-overview|LTX-2]]
- [[mcp-video-integrations|MCP integration]] for AI-agent workflows

With the May 2026 launch of Runway Agent, Runway now directly competes with [[ltx-studio]]'s end-to-end production workflow rather than being a clip-generator-only tool. Teams evaluating the two platforms should weigh Runway Agent's conversational assembly approach against [[ltx-studio]]'s node-based Flows and multi-model marketplace.

Teams choosing between them often use Runway for individual clip quality and [[ltx-studio]] for full project workflow.

## See Also
- [[competitor-landscape-overview]]
- [[ltx-studio]]
- character consistency
