---
title: Runway (Gen-3 / Gen-4 / Agent)
type: competitor
created: 2026-04-13
updated: 2026-08-24
sources:
  - raw/competitor-product-runway.md
  - raw/competitor-runway-agent-launch-may-2026.md
  - raw/competitor-runway-gen45-benchmark-2026.md
  - raw/competitor-runway-june-2026.md
  - raw/competitor-runway-api-additions-july-2026.md
  - raw/competitor-runway-media-router-orchestration-pivot-july-2026.md
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
- **Elo score of 1,247** on the Artificial Analysis Text-to-Video benchmark **at launch** (December 2025). Superseded: as of 2026-08-24 Runway is absent from the AA top-31 in both T2V and I2V with-audio.
- Still Runway's **last frontier video model** as of August 2026 — no Gen 5 announced
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

### API Additions (July 2026)

Runway continued expanding its model-agnostic API marketplace rather than shipping a new flagship model this cycle:
- **July 1, 2026:** Gemini Omni Flash available via the Runway API; Nano Banana 2 Lite added for fast image generation.
- **July 2, 2026:** "Agent Skills" introduced — build ad campaigns, create commercials, and localize ads via simple command prompts (extends the Agent 2.0 marketing focus from June).
- **Mid-July 2026:** Optional `negativePrompt` parameter added for Veo3, Veo3.1, and Veo3.1-fast text-to-video/image-to-video requests; Seedream 5.0 Lite (ByteDance image model) added to the API.

This reinforces Runway's aggregator strategy: bundling its own Gen-4/Gen-4.5/Aleph models with third-party models ([[competitor-veo|Veo]], [[competitor-kling|Kling]], [[competitor-seedance|Seedance/Seedream]], FLUX) under one subscription/API.

### Media Router (July 23, 2026) — the orchestration pivot

On **Thursday 2026-07-23** Runway launched **Runway Media Router** through **Runway Dev**, its developer platform released earlier in July 2026. Media Router automatically selects the best image, video or audio generation model for a request based on whether the developer prioritizes **quality, speed or cost**. Runway claims it is **the first model router built specifically for generative media** (routers are already common for LLMs). It is distinct from the mid-July API marketplace expansion: Media Router is a saved, no-model-specified routing configuration layered on top of Runway Dev's third-party model roster.

**Named Runway Dev customers:** Adobe, Cloudflare, ElevenLabs, Expedia, Shutterstock, Quora — companies building media generation into their own products via Runway's API rather than sending users to Runway's app.

Anthony Maggio, Runway CPO: *"The routing really fits into that overall promise of being the easiest one-stop shop for developers to integrate with any type of generative media model."* Co-founder/co-CEO Anastasis Germanidis: *"You need great models underneath, but the orchestration increasingly matters a lot because people are building entire campaigns with those models... It's something that we increasingly had to build — that intelligence layer that comes on top of the pure pixel models."*

**Geopolitical routing preference.** Maggio noted Chinese generative media models are increasingly popular, but many businesses "might not be comfortable working with models that come out of China," so they can set a preference for **American model providers** — a preference he expects to become more common as the US administration explores bans and sanctions against Chinese open AI models. This is **directly relevant to LTX's positioning as a non-Chinese open-weights option**, and mirrors the license carve-out problem with [[competitor-minimax-hailuo|MiniMax H3]] and the China-region-only access channels for [[wan-video|Wan 3.0]].

**Token pricing context.** Media Router launched weeks after Runway **replaced its unlimited subscription plans with token-based pricing**, a move that drew criticism from some users. Maggio says customers are mainly interested in routing for token pricing and quality — part of 2026's broader enterprise token-bill backlash.

Also in August 2026, the Runway API added **4K output for Seedance 2.0** (`seedance2`) across text, image and video endpoints, and shipped Model Router as a saved routing configuration for video, image and audio.

### The frontier-model gap (as of August 2026)

Runway's **last dedicated frontier video model release remains Gen-4.5, from December 2025**. Aside from **Aleph 2.0** (video editing, May 2026), Runway has not shipped a new frontier video model in months. TechCrunch explicitly asked when Runway plans to release Gen 5 — **no answer was given**.

Per Artificial Analysis, Aleph 2.0 still ranks among leading **video editing** models, but Runway's text-to-video and image-to-video models no longer lead the rankings. **As of 2026-08-24 Runway appears nowhere in the Artificial Analysis top-31 for either text-to-video-with-audio or image-to-video-with-audio.** The top 20 T2V spots are held by Google, ByteDance and Alibaba. For reference, Gen-4.5 topped the AA Text-to-Video Arena at **1,247 Elo** at launch in December 2025 — a figure this page previously cited as a current standing; it is now a historical launch number, not a live ranking.

**Strategic read.** Media Router "assumes that the best model will continue to change" rather than asking developers to bet on one model staying ahead. Runway is repositioning from AI video startup to **infrastructure/orchestration layer for generative media** — if not as the best new AI model, then as the best orchestration layer. Runway valuation: **$3.55B** per PitchBook. Gen-4.5 was internally codenamed "David," trained and served entirely on Nvidia Hopper and Blackwell GPUs; CEO Cristóbal Valenzuela at the time: *"We managed to out-compete trillion-dollar companies with a team of 100 people."*

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
- **No frontier model since Gen-4.5 (December 2025)**; absent from the AA top-31 in both T2V and I2V with-audio as of 2026-08-24
- Token-based pricing replaced unlimited plans in mid-2026, drawing user criticism

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

The July 2026 Media Router launch shifts the comparison again. Runway is no longer primarily competing on model quality — it is competing as an aggregation and routing layer, a strategy that partly converges with [[ltx-studio]]'s own multi-model access. The difference is that LTX pairs multi-model access with a **first-party open-weights model** it controls, while Runway's frontier model has been static since December 2025.

## See Also
- [[competitor-landscape-overview]]
- [[ltx-studio]]
- [[competitor-seedance]] — Seedance 2.0, now 4K via the Runway API
- [[competitor-minimax-hailuo]] — Chinese open-weights model Media Router's geo-preference is designed to route around
