# New IC-LoRA Adapters: HDR, LipDub, Union+MotionTrack Official Release + NVFP4 Blackwell

**Source:** https://ltxworkflow.com/changelog
**Date:** 2026-06-03
**Retrieved:** 2026-06-01

## Content

Lightricks officially released several new IC-LoRA adapters and model variants, as documented on ltxworkflow.com (a third-party ComfyUI hub). Note: the changelog entry is dated 2026-06-03, two days after retrieval — these are imminent/announced releases.

### New Official IC-LoRA Adapters (Lightricks)

**IC-LoRA Union Control (Canny + Depth combined)**
- Combines Canny edge detection and Depth map into a single unified control adapter for LTX-2.3
- Previously the Union Control for LTX-2.3 was Depth + Pose + Canny; this variant specifically combines Canny + Depth as a simpler pairing.

**IC-LoRA Motion Track Control**
- Guides video motion using sparse point trajectories
- Users define a handful of tracking points that the model follows through the generation
- Listed as official Lightricks release for LTX-2.3

**IC-LoRA HDR + Scene Embeddings**
- Enables 16-bit HDR video generation
- Supports SDR-to-HDR conversion via LogC3 color space
- Allows embedding of scene-level HDR metadata into generation

**IC-LoRA LipDub**
- Joint audio-visual lip-dubbing adapter
- Based on JustDubIt research
- Generates synchronized lip motion from an audio track reference

### New Model Variants

**LTX 2.3 Dev NVFP4** (21.7 GB)
- Official Lightricks quantization targeting Blackwell architecture (NVIDIA RTX 50xx series)
- Follows NVFP8 (previously released); NVFP4 achieves further compression

**Gemma 3 12B IT Text Encoder**
- Two variants: FP8 (13.2 GB) and full precision (~24 GB), from Comfy-Org
- Listed as required for all ComfyUI LTX 2.3 workflows going forward
- Replaces or supplements existing text encoder options

### Context
The ltxworkflow.com changelog entry (2026-06-03) indicates these are newly released to HuggingFace and/or ComfyUI Manager around that date. This adds to the IC-LoRA family for LTX-2.3 which previously had Union Control, Motion Track, Cameraman V1 (community), and ID LoRA (community).
