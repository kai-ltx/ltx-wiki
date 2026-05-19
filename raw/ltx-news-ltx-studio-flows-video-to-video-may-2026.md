# LTX Studio May 2026 Launches: Flows Automation & Video-to-Video Controls

**Source:** https://ltx.studio/release-notes
**Date:** 2026-05-07
**Retrieved:** 2026-05-19

## Content

LTX Studio shipped two major feature launches in the first two weeks of May 2026:

### Flows — Node-Based Workflow Automation (May 7, 2026)

LTX Studio announced Flows on May 7, 2026 via the product release notes and official blog (https://ltx.studio/blog/ltx-studio-flows).

- **What it is**: A visual, node-based workflow builder that lets users connect prompt, image, video, and upscaling nodes into a repeatable pipeline, then run everything in one click.
- **Smart caching**: Previously generated outputs are reused when inputs haven't changed, saving compute credits.
- **Brand Kit integration**: Enterprise users can embed brand kit assets into Flows for consistent large-scale production.
- **Build once, reuse at scale**: Once a Flow is saved, it can be triggered repeatedly without manual re-configuration.
- **Supported node types**: text/prompt nodes, image input, video generation (any LTX Studio model), upscaling, audio, and export nodes.
- Positioned as LTX Studio's answer to automation needs for content studios producing high volumes of branded video.

### Video-to-Video with Pose/Depth/Edge Controls (May 11, 2026)

LTX Studio launched Video-to-Video controls on May 11, 2026, bringing LTX-2.3's IC-LoRA-based control framework to the platform UI.

- **Three control modes**:
  1. **Pose Control**: Extracts skeleton/pose data from an input video and uses it to guide motion in the generated output (useful for character animation and dance transfers).
  2. **Depth Control**: Extracts depth map from input video; preserves 3D spatial structure while allowing full style/content transformation.
  3. **Edge Control**: Extracts edge/outline from input video; preserves composition and shapes while fully changing appearance.
- Users upload a reference video, choose a control mode, write a prompt, and generate a stylistically transformed version.
- This feature was available in LTX Studio before the standalone open-source IC-LoRA weights were publicly released.
- Backed by LTX-2.3's architecture, which natively supports these control signals through IC-LoRA adapters trained on the 22B DiT backbone.

### ChatGPT Image 2.0 Integration (May 4, 2026)

Also launched in early May 2026:

- ChatGPT Image 2.0 (OpenAI) integrated directly into LTX Studio's image generation layer.
- Described as offering "more detail, more accuracy, and more creative control without leaving the workflow."
- Accessible from within the LTX Studio Gen Space alongside native LTX image generation.

### Sources

- https://ltx.studio/release-notes
- https://ltx.studio/blog/ltx-studio-flows
- https://ltx.studio/platform/ai-video-to-video
- https://www.mindstudio.ai/blog/how-to-use-ltx-23-video-to-video-controls-pose-depth-edge
