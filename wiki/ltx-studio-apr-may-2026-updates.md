---
title: LTX Studio — April–May 2026 Product Updates
type: product
created: 2026-05-19
updated: 2026-05-19
sources:
  - raw/community-ltx-studio-product-updates-apr-may-2026.md
tags:
  - ltx-studio
  - product-updates
  - lightricks
  - multi-model
  - agentic
---
# LTX Studio — April–May 2026 Product Updates

LTX Studio shipped a dense series of product updates between April 19 and May 11, 2026, transforming it from a video generation tool into a **multi-model, multi-tool AI video production platform**. CineD described the Editing Space launch as "LTX Studio taking its next big step."

## April 2026

### Editing Space (April 19, 2026)
Unified image editing workspace consolidating:
- Brush tools
- Upscaling
- Camera angle adjustment
- Visual fine-tuning

All in a single flow, reducing the need to leave the platform for post-generation editing. Community reception: focused on how this reduced round-trips between LTX Studio and external tools.

### Veo 3.1 Lite (April 26, 2026)
Google's Veo 3.1 Lite added to LTX Studio's model roster. Positioned as a cost-effective option for AI video at scale. Expands the multi-model nature of the platform.

### Seedance 2.0 (April 26, 2026)
ByteDance's Seedance 2.0 integrated. Supports text-to-video and image-to-video modes; 4–15 second durations.

### Kling 3.0 Pro (April 27, 2026)
[[competitor-kling|Kling 3.0 Pro]] integrated into LTX Studio — cinematic AI video up to 15 seconds, multi-shot generation with director-style prompting. See [[competitor-kling]] for model details.

### Canvas (April 27, 2026)
Collaborative infinite workspace — teams can generate, iterate, and align on video concepts in real time or asynchronously. Positioned as a Figma-like environment for video production teams. Community highlighted the async collaboration angle as a differentiator for agency workflows.

## May 2026

### ChatGPT Image 2.0 (May 4, 2026)
OpenAI's image generation model integrated into LTX Studio, enabling richer image-based assets without leaving the workflow. Community noted improved detail and accuracy compared to prior image generation options in the platform.

### Flows (May 7, 2026)
Node-based visual workflow builder for automating video production pipelines. Key characteristics:
- Connect prompt, image, video, and upscaling nodes
- Run entire sequences in one click
- "Build once, reuse at any scale" automation layer
- Smart caching: reuses previously generated outputs when inputs haven't changed
- Enterprise [[ltx-studio|Brand Kit]] integration for consistent large-scale production

Community reception: enthusiastic among power users and agencies; some newer users noted a learning curve.

### Video to Video (May 11, 2026)
Three structural control modes for style transfer while preserving motion:
- **Pose control** — extracts skeleton/pose from input video to guide character animation
- **Depth control** — extracts depth map to preserve 3D spatial structure through style transformation
- **Edge control** — extracts outlines to preserve composition while changing appearance

Backed by [[ltx-2.3-model]]'s [[ic-lora|IC-LoRA]] adapters on the 22B DiT backbone.

## Platform Positioning Shift

The April–May update cadence positions LTX Studio as a **model marketplace + production workflow platform** rather than a single-model product. As of May 2026, integrated models include:
- LTX's own [[ltx-2.3-model|LTX-2.3]] (22B open-weights)
- [[competitor-kling|Kling 3.0 Pro]]
- [[competitor-veo|Veo 3.1]] Lite
- Seedance 2.0 (ByteDance)
- ChatGPT Image 2.0 (OpenAI)

This multi-model strategy mirrors [[competitor-runway|Runway Agent]]'s direction (launched May 13, 2026) — both platforms moving toward end-to-end AI production systems rather than clip generators.

## See Also
- [[ltx-studio]] — Full platform overview
- [[ltx-2.3-model]] — Underlying LTX model
- [[ic-lora]] — IC-LoRA control adapters (depth, pose, edge)
- [[competitor-runway]] — Runway's parallel agentic pivot (May 2026)
- [[ltx-studio-platform-reviews]] — User reviews and ratings
