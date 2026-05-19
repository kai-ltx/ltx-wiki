# LTX Video ComfyUI and LoRA Ecosystem — Community Activity April–May 2026

**Source:** https://github.com/Lightricks/ComfyUI-LTXVideo | https://github.com/Lightricks/LTX-2 | https://github.com/Lightricks/LTX-2/issues/128 | https://github.com/Lightricks/ComfyUI-LTXVideo/issues/470 | https://www.runcomfy.com/comfyui-workflows/ltx-2-3-id-lora-in-comfyui-identity-controlled-video-creator | https://www.youtube.com/watch?v=pF9wv-yqnhI
**Date:** 2026-04-23
**Retrieved:** 2026-05-19

## Content

### Overview
The LTX Video open-source community on GitHub and Hugging Face showed sustained activity in April–May 2026, with Lightricks shipping new IC-LoRAs and the community raising and resolving issues around integrations.

### New LoRA Releases (April–May 2026)

**HDR IC-LoRA** (released ~April 23, 2026)
Lightricks released an HDR IC-LoRA for LTX-2.3. Initial community reports flagged issues: tiled VAE decoding caused visible video flickering (GitHub issue #470 on ComfyUI-LTXVideo). Community resolution: switching from tiled to non-tiled (default) VAE decode eliminated the flickering. The issue was actively monitored and acknowledged by Lightricks.

**LipDub IC-LoRA**
Released for LTX-2.3 — enables dubbing or rephrasing of speech in video by generating new lip movements and audio matching target text while preserving speaker identity. Community reception: described as a significant advancement for multi-language content creation. YouTube walkthrough titled "LTX 2.3 Just Changed AI Dubbing Forever" attracted community attention.

**Union IC-LoRA**
Combines depth and edge control conditions in a single model. Operates on downsampled latents to reduce memory usage and speed up inference — community noted this as important for running on consumer-grade hardware.

**ID-LoRA (Identity-Controlled Video)**
Community workflow on RunComfy.com: "LTX 2.3 ID-LoRA in ComfyUI — Identity-Controlled Video Creator." Enables consistent character identity across generated video clips.

### GitHub Activity and Community Issues

**ComfyUI Workflow Issues (LTX-2 repo, Issue #128)**
Community users reported challenges with the `video_ltx2_t2v_distilled` ComfyUI workflow configuration. Active thread with Lightricks team engagement.

**ComfyUI-LTXVideo repo (Issue #470)**
HDR IC-LoRA flickering issue: community-diagnosed and resolved within days of the LoRA release. Demonstrates active community-to-Lightricks feedback loop.

### Ecosystem Scale
- LTX-2 official GitHub repo: https://github.com/Lightricks/LTX-2 — official Python inference and LoRA trainer package
- ComfyUI-LTXVideo: https://github.com/Lightricks/ComfyUI-LTXVideo — official ComfyUI integration
- Community LoRAs distributed via Hugging Face (e.g., Lightricks/LTX-Video-Squish-LoRA)

### Sentiment
Community developers express appreciation for the open weights, active GitHub presence, and LoRA trainer tooling. Common friction points: hardware memory requirements for longer clips, occasional workflow compatibility gaps when Lightricks updates the model between ComfyUI node updates.
