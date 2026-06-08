# LTX-2.3 IC-LoRA Union Control and Motion Track Control — New HuggingFace Adapters

**Source:** https://huggingface.co/Lightricks/LTX-2.3-22b-IC-LoRA-Motion-Track-Control
**Date:** 2026-06-03
**Retrieved:** 2026-06-08

## Content

Two new official IC-LoRA adapters for LTX-2.3 confirmed on HuggingFace:

### IC-LoRA Union Control (LTX-2.3 and LTX-2-19b variants)

- HuggingFace repos: `Lightricks/LTX-2.3-22b-IC-LoRA-Union-Control` and `Lightricks/LTX-2-19b-IC-LoRA-Union-Control`
- Combines multiple control signals (depth, pose, canny/edge) in a single adapter pass
- Eliminates need to swap between separate depth, pose, and edge IC-LoRA adapters
- Workflow use case: modify a frame from an existing video using canny edge control and propagate the change across the clip
- ComfyUI workflow available on comfy.org: "AI on the Lot 2026_LTX-2.3_IC LoRA (Union Control)"

### IC-LoRA Motion Track Control (LTX-2.3-22b)

- HuggingFace repo: `Lightricks/LTX-2.3-22b-IC-LoRA-Motion-Track-Control`
- Guides motion of objects or regions in generated video using sparse point trajectories
- User provides reference video with colored spline overlays indicating desired motion paths
- Model generates video that follows those trajectories
- Point tracks can be extracted from existing videos via SpatialTrackerV2 or drawn manually
- ComfyUI workflow: "LTX 2.3 IC-LoRA in ComfyUI — V2V Motion Track Video Workflow" on RunComfy

### GitHub Issue Reference

- GitHub issue #203 in Lightricks/LTX-2 repo documents Python usage for both IC-LoRA-Union-Control and Motion-Control adapters together

### Practical Impact

These two adapters complete the core IC-LoRA control suite for LTX-2.3:
- **Union Control** = multi-signal structural control in one adapter
- **Motion Track** = sparse trajectory-based motion guidance
- Combined with existing Depth, Pose, Canny, Detailer, HDR, and LipDub adapters, the LTX-2.3 adapter family is now the most comprehensive open-weights control system in video generation
