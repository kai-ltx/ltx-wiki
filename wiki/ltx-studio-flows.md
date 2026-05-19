---
title: LTX Studio Flows
type: product
created: 2026-05-19
updated: 2026-05-19
sources:
  - raw/ltx-news-ltx-studio-flows-video-to-video-may-2026.md
  - raw/ltx-news-ltx-studio-api-async-hdr-may-2026.md
tags:
  - ltx-studio
  - flows
  - automation
  - workflow
  - node-based
  - lightricks
---

# LTX Studio Flows

Flows is a visual, node-based workflow automation system inside [[ltx-studio]], launched on May 7, 2026. It lets users connect generation steps into repeatable pipelines and run them in one click.

- **Announcement:** https://ltx.studio/blog/ltx-studio-flows
- **Platform:** https://ltx.studio (available from Standard plan and above)
- **Launch Date:** May 7, 2026

## What Flows Does

Flows addresses the bottleneck of manually re-configuring generation settings for each new project. By building a Flow once, teams can:

- Trigger the same multi-step pipeline repeatedly without manual re-configuration
- Apply consistent settings and brand identity across high-volume production
- Reuse cached outputs when inputs haven't changed (smart caching)

## Node Types

| Node Type | Description |
|-----------|-------------|
| Text / Prompt | Write or template the generation prompt |
| Image Input | Supply a source image for conditioning |
| Video Generation | Run any LTX Studio model (LTX, Veo, Seedance 2.0, etc.) |
| Upscaling | Apply spatial or resolution upscaling to generated output |
| Audio | Add or generate audio for the video |
| Export | Define the output format and delivery destination |

Nodes connect via visual edges. The output of one node feeds directly into the next.

## Smart Caching

When a Flow is re-run and inputs to a node haven't changed, the previously generated output for that node is reused automatically. This avoids burning compute credits on identical steps, making iterative refinement and large batch runs more economical.

## Brand Kit Integration (Enterprise)

Enterprise plan users can embed [[ltx-studio]] Brand Kit assets directly into Flows:

- Brand logos, color palettes, and style references are injected into generation prompts or conditioning nodes
- Ensures consistent visual identity across all outputs from a Flow
- Designed for organizations managing multiple brands or large-scale content operations

See [[ltx-studio]] for Brand Kit feature details.

## Supported Models in Flows

Any video generation model available in LTX Studio's Gen Space can be used within a Flow node:

- LTX-2.3 ([[ltx-2.3-model]])
- Veo 3.1 ([[competitor-veo]])
- Seedance 2.0 (ByteDance)
- ChatGPT Image 2.0 (for image generation nodes)

## Relationship to Other LTX Studio Features

- **[[ltx-studio-canvas|Canvas]]**: Canvas is the ideation phase; once a concept is validated, a Flow automates full production runs.
- **Video-to-Video Controls**: Pose/Depth/Edge control nodes can be incorporated into a Flow for consistent video transformation pipelines.
- **[[ltx-api-async-hdr|Async API]]**: Flows-like async patterns are also available programmatically via the LTX API's async endpoints.

## Use Cases

- Marketing teams generating hundreds of ad variants from a single template
- Content studios maintaining brand consistency across a campaign
- Pre-production teams automating storyboard-to-animatic pipelines
- Agencies running A/B creative tests at scale

## References

- [[ltx-studio]] — LTX Studio platform overview
- [[ltx-studio-canvas]] — Canvas ideation workspace (launched alongside Flows)
- [[ltx-2.3-model]] — Primary video generation model powering Flows
- [[ltx-api-async-hdr]] — Async API pattern for programmatic pipeline integration
- [[ic-lora]] — IC-LoRA control adapters used in Video-to-Video Flow nodes
