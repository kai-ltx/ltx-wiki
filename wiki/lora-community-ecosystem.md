---
title: LoRA Community Ecosystem
type: reference
created: 2026-04-13
updated: 2026-06-30
sources:
  - raw/social-lora-training-community-ecosystem.md
  - raw/community-project-lora-training-tools.md
  - raw/third-party-lora-training-services.md
  - raw/community-ltx-comfyui-lora-ecosystem-april-may-2026.md
  - raw/tutorial-3dreal-lora-fal-june-2026.md
tags:
  - community
  - lora
  - ecosystem
  - civitai
  - huggingface
  - ic-lora
---
# LoRA Community Ecosystem

An active community has formed around [[lora-training]] for [[ltx-video-overview|LTX-Video]] models, sharing trained LoRAs, tools, and knowledge across multiple platforms. See [[lora-ecosystem]] for the full inventory of official and community LoRA adapters.

## Community Sentiment

- Very positive about training ecosystem maturity
- Community values the official trainer being open source
- Multiple cloud training options reduce barrier to entry
- [[ic-lora|IC-LoRA]] seen as innovative and unique capability
- Concern about LoRA compatibility across model versions

## Community-Shared LoRAs

### Civitai

Multiple community-trained LoRAs are shared on Civitai:

- **LTX-2 IC-LoRA Detailer** -- enhances fine visual details and clarity
- **SSX LTX2 T2V** -- text-to-video LoRA trained with the official trainer
- Various style, NSFW, and image-to-video adapter LoRAs

### HuggingFace

| Model Family | Adapter Models | Community Fine-tunes |
|-------------|----------------|---------------------|
| LTX-Video | 24 | 25 |
| LTX-2 | 49 | 54 |
| LTX-2.3 | 20 | 27 |

Notable community contributions on HuggingFace:
- **Phr00t/LTX2-Rapid-Merges** -- community model merges
- **Kijai/LTXV2_comfy**, **Kijai/LTX2.3_comfy** -- widely used quantized variants

## Notable Community LoRA Authors

- **Burgstall** -- Multiple expression LoRAs (amgery, smile, surprise, headbanger)
- **svjack** -- Style LoRAs (anime landscape, pixel art)
- **Pierre-Jean** -- Camera trajectory LoRA
- **Sameric934** -- General LTX-2 video LoRA


## Notable Community IC-LoRAs (June 2026)

### 3DREAL IC-LoRA (June 26, 2026)

Released by **Lovis Odin** (@OdinLovis) in collaboration with **fal.ai**, the **LTX-2.3 3DREAL IC-LoRA** converts rough 3D renders and CG viewport blockouts into photorealistic, cinematic video while preserving the original camera path and composition.

**Key properties:**
- Base model: LTX-2.3 (22B)
- Trigger word: `3DREAL`
- Two variants: **Light** (faithful to input) and **Strong** (aggressive photorealism)
- Pipeline: I2V / V2V
- License: custom (not Apache 2.0)

**Access:**
- fal.ai endpoint (no download): `fal-ai/ltx-2.3-quality/render-to-real`
- LoRA weights on HuggingFace: `fal/LTX-2.3-3DREAL-LoRA`
- ComfyUI compatible via local LoRA loading

**Use cases:** 3D previz, game engine viewport to cinematic trailer, architecture walkthrough, camera angle exploration. Particularly useful for preserving exact camera motion from 3D software while replacing synthetic textures with photorealistic output.

This adapter enables a new workflow: rough out scenes in Blender/Unreal/game engines, then use 3DREAL to deliver a photorealistic preview — without committing to expensive final renders. Bridges 3D production pipelines with AI video generation in a way that preserves the director's compositional intent.

### Cameraman V1 IC-LoRA (May 22, 2026)

Camera motion transfer LoRA by **Cseti** — extracts camera motion from a reference video and applies it to LTX-2.3 generation. Released on CivitAI and noted in prior wiki updates.

## Cross-Version LoRA Transfer

A key community discovery from HuggingFace Discussion #4 on LTX-2.3:

- LTX-2.0 trained LoRAs work **significantly better** on LTX-2.3 than on 2.0 itself
- LoRAs that were unusable for further training on 2.0 become usable on 2.3
- Inference requires reduced strength values when applying 2.0 LoRAs to 2.3

## Training on Quantized Models

From HuggingFace Discussion #92 on LTX-Video:
- LoRA fine-tuning confirmed to work on FP8 quantized models
- Enables training on lower-VRAM hardware (under 24GB)

## Community Resource Hub

**awesome-ltx2** (github.com/wildminder/awesome-ltx2):
- Community-maintained collection of all available resources
- LTX-2 models, encoders, workflows, LoRAs for [[comfyui-ltx-integration-overview|ComfyUI]]
- Central aggregation point for the community

## Uploading LoRAs

### To HuggingFace Hub

```python
from huggingface_hub import HfApi

api = HfApi()
api.upload_folder(
    folder_path="output/ltx-video-lora",
    repo_id="your-username/my-ltx-video-lora",
    repo_type="model",
)
```

## Official IC-LoRA Releases (April–May 2026)

Lightricks shipped several new [[ic-lora|IC-LoRA]] adapters for LTX-2.3 in this period:

### HDR IC-LoRA (~April 23, 2026)
- Adds HDR-style color grading and dynamic range control to generated video
- Initial community reports: tiled VAE decoding caused video flickering (GitHub issue #470, ComfyUI-LTXVideo)
- Fix: switching from tiled to non-tiled (default) VAE decode eliminated flickering
- Lightricks acknowledged and monitored the issue actively

### LipDub IC-LoRA
- Enables dubbing or rephrasing of speech in existing video
- Generates new lip movements and audio matching target text while preserving speaker identity
- Significant for multi-language content creation
- YouTube walkthrough: "LTX 2.3 Just Changed AI Dubbing Forever"

### Union IC-LoRA
- Combines depth and edge control conditions in a **single model** (replaces running two separate adapters)
- Operates on downsampled latents to reduce memory usage and speed up inference
- Important for running on consumer-grade hardware

### ID-LoRA (Identity-Controlled Video)
- Maintains consistent character identity across generated video clips
- Community workflow available on RunComfy.com: "LTX 2.3 ID-LoRA in ComfyUI — Identity-Controlled Video Creator"

## Community LoRA Releases — May 2026

A burst of new community IC-LoRA adapters for LTX-2.3 was released the week of May 19–25, 2026:

### IC-LoRA Cameraman V1 (Cseti, May 22, 2026)
The first community-built **camera motion transfer** LoRA for LTX-2.3 22B. Unlike the official camera control LoRAs (which use preset movements), Cameraman V1 reads camera behavior from a reference video and replicates it — pans, tilts, zoom-in/out, orbits, and compound combinations.

- HuggingFace: `Cseti/LTX2.3-22B_IC-LoRA-Cameraman_v1`
- Civitai: https://civitai.com/models/2525197/cameraman-ic-lora-for-ltx23-22b
- ComfyUI workflow (RunComfy): V2V Motion Track workflow
- Tutorial: https://www.stablediffusiontutorials.com/2026/05/ltx2.3-cameraman-ic-lora.html
- Key rule: Don't describe camera movement in the text prompt — model reads it from reference video

See [[camera-control-loras]] for full installation and usage details.

### ID LoRA LipSync (May 2026)
Companion release for **character identity + LipSync** in LTX-2.3. Maintains consistent character appearance across shots while synchronizing lip movements with audio.
- Tutorial: https://www.stablediffusiontutorials.com/2026/05/ltx2.3-id-lora.html

These two releases significantly expand the composable IC-LoRA toolkit available for LTX-2.3 beyond what Lightricks ships officially.

## GitHub Activity (April–May 2026)

- **ComfyUI-LTXVideo issue #470** — HDR IC-LoRA flickering: community-diagnosed and resolved within days
- **LTX-2 repo issue #128** — ComfyUI workflow issues with `video_ltx2_t2v_distilled` config: active thread with Lightricks team engagement
- Pattern: active community-to-Lightricks feedback loop, issues resolved quickly

## Ecosystem Scale (May 2026)

| Platform | LTX-Video | LTX-2 | LTX-2.3 |
|----------|-----------|-------|---------|
| HuggingFace adapter models | 24 | 49 | 20 |
| Community fine-tunes | 25 | 54 | 27 |

Common friction points: hardware memory requirements for longer clips; occasional workflow compatibility gaps when Lightricks updates the model between ComfyUI node updates.

## References

- [[lora-training]]
- [[ltx-video-trainer]]
- [[third-party-training-services]]
- [[ic-lora]]
- [[comfyui-ltx-lora-training-control]]
