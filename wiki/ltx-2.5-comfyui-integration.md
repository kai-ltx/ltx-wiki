---
title: LTX-2.5 ComfyUI Integration
type: technical
created: 2026-08-24
updated: 2026-08-24
sources:
  - raw/tutorial-comfyui-ltx-2-5-nodes-workflows-2026-08.md
  - raw/tutorial-ltx-2-5-local-vram-quantization-guide-2026-08.md
  - raw/tutorial-ltx-2-5-python-ltx-pipelines-and-diffusers-2026-08.md
tags:
  - ltx-2-5
  - comfyui
  - integration
  - workflows
  - templates
  - quantization
---

# LTX-2.5 ComfyUI Integration

Unlike previous generations, [[ltx-2.5-model|LTX-2.5]] support landed in **ComfyUI core** on day one rather than in the Lightricks custom-node repo. A stock, fully updated ComfyUI has the nodes and the workflow templates; no custom node pack is required.

For the previous generation see [[ltx2-comfyui-integration]] and [[ltx2-comfyui-nodes-reference]].

## Where support actually landed

- Native LTX-2.5 support merged into ComfyUI core on **2026-08-11** via PR **Comfy-Org/ComfyUI#15499** ("Add support for LTX 2.5"), with **Kijai as co-author**.
- A second merge the same day, PR **#15501**, added **LTX 2.5 partner nodes for the API path** (see [[ltx-video-api-models]]).
- Both landed **before the v0.32.0 tag**, so an updated stock install has them. The in-app workflow templates for 2.5 shipped in the templates package pulled by the same release.
- **Minimum ComfyUI version: 0.32.0.** Older installs render the LTX-2.5 nodes as red "This node type does not exist" boxes.
- Follow-up fix on master **2026-08-12** (after the v0.32.0 tag): *"Fix float64 device in ltx diffusion decoder"* — needed if you hit a device/dtype error on decode with the new diffusion decoder. Update past the tag or take nightly.

### Custom-node repo lag

As of 2026-08-12, `github.com/Lightricks/ComfyUI-LTXVideo` still listed only **2.3 and 2.0** workflows in its README, and the docs.comfy.org LTX tutorial section still stopped at **2.0**. Day one belonged to core plus the template browser. (The [[ltx-2.5-technical|LTX-2 monorepo]] shows the same lag: no tagged releases and a README quick-start still pointing at 2.3 weights.)

## The three official templates

All three share the same five model files.

| Template file | Mode | Stages |
| --- | --- | --- |
| `video_ltx2_5_t2v.json` | Text-to-video | Two-stage (uses spatial upscaler) |
| `video_ltx2_5_i2v.json` | Image-to-video | Two-stage (uses spatial upscaler) |
| `video_ltx2_5_flf2v.json` | First-frame/last-frame interpolation | **Single-stage — does NOT load the upscaler** |

Node names and the ComfyUI folder structure are **unchanged from LTX-2.3** — migration is mainly swapping model files.

## Model files and folders (ComfyUI int8 pack)

| File | ComfyUI folder |
| --- | --- |
| `ltx-2.5-22b-distilled-transformer-comfy-int8-convrot.safetensors` | `models/diffusion_models/` |
| `gemma4-12b-with-proj-ltx-2.5-comfy-int8-convrot.safetensors` | `models/text_encoders/` |
| `ltx-2.5-video-vae-bf16.safetensors` | `models/vae/` |
| `ltx-2.5-audio-vae-bf16.safetensors` | `models/vae/` |
| `ltx-2.5-latent-spatial-upscaler-x2-bf16-1.0.safetensors` | `models/latent_upscale_models/` |
| `gemma4_e2b_it_bf16.safetensors` (optional Prompt Enhancer, from `Comfy-Org/gemma-4`) | `models/text_encoders/` |

The `*-comfy-int8-convrot` files are **ComfyUI-only** and are **not** loadable by `ltx-pipelines`/PyTorch — see [[ltx-2.5-local-inference]] for the bf16 path.

A `ltx-2.5-22b-dev-transformer-comfy-int8-convrot.safetensors` exists for the trainable dev transformer, and an NVFP4 build (`ltx-2.5-22b-distilled-transformer-nvfp4.safetensors`) ships as well — but see known bugs below.

### Gated download

The repo `huggingface.co/Lightricks/LTX-2.5` is **gated**: click "Agree and Access" first. Scripted downloads with a fine-grained token need the **`read-gated-repos` scope**, otherwise you get a 403 that looks like a bug.

The recommended distilled set is roughly **66 GiB across five files**; the custom-node repo's stated prerequisites are a **CUDA GPU with 32 GB+ VRAM and 100 GB free disk**.

## Node settings that matter

- **ResolutionSelector** — sets width/height from a megapixel value, auto-rounded to a multiple of 32 (a hard model requirement). 16:9 mapping:

  | MP | Resolution | MP | Resolution |
  | --- | --- | --- | --- |
  | 0.2 | 608×352 | 0.9 | 1280×736 |
  | 0.3 | 736×416 | 1.0 | 1376×768 |
  | 0.4 | 864×480 | 1.2 | 1504×832 |
  | 0.5 | 960×544 | 1.5 | 1664×928 |
  | 0.6 | 1056×608 | 2.0 | 1920×1088 |
  | 0.7 | 1152×640 | | |

  On a 16 GB card stay at or below **0.6 MP** for first tests.
- **Auto Duration** — the model adjusts actual clip length from the described action. Padding a prompt to "fill time" only adds noise. Same duration-head mechanism exposed as `duration: "auto"` on the hosted API ([[ltx-video-api-endpoints]]).
- **prompt_enhance** toggle — routes the prompt through the small Gemma 4 E2B enhancer. Earngenix testing recommends **leaving it off**; it occasionally rewrote prompts into unrelated output.
- **LTXVSaveConditioning / LTXVLoadConditioning** — encode a prompt once and reuse the encoding across runs, saving compute and keeping results consistent.
- T2V ships as a single **subgraph node** ("Text to Video (LTX-2.5)") bundling conditioning, sampler, CFG guider and VAE decode. Use "Enter subgraph" to inspect.
- I2V adds only a **LoadImage** node. Prompt guidance: describe **only motion/camera/audio**, never re-describe what the source photo already shows, or the subject drifts mid-clip.
- FLF2V uses **two LoadImage nodes** (first frame, last frame) and no upscaler.

## VRAM claims (conflicting — both recorded)

| Source | Figure | Pipeline described |
| --- | --- | --- |
| LTX launch materials via Earngenix | **16 GB VRAM minimum** (24 GB / RTX 4090 comfortable) | ComfyUI **int8** pack |
| ComfyUI-LTXVideo repo + official Python path | **32 GB+ VRAM** | **bf16** PyTorch (`ltx-pipelines`) |
| NVIDIA optimization guidance for the family | 540p / 4 s clips / 20 steps on 8–16 GB cards | mixed |

These describe **different pipelines**; do not conflate them. See [[hardware-requirements]] and [[ltx-2.5-local-inference]].

## Known launch bugs (first 24 hours)

HF discussions logged 19 threads in 15 hours:

- **The NVFP4 build of the distilled transformer fails to load in ComfyUI.**
- Basic image-to-video workflow hanging indefinitely when asked for 10 seconds of output.
- **No GGUF at launch** — community builds followed on day two (see [[gguf-quantizations]]).
- The full-precision transformer exists only as **bf16** (no fp16).
- Apple M5 users reporting VAE errors.
- Missing-node errors `GemmaAPITextEncode` and `LTXFloatToInt` — fixed by fully updating ComfyUI.
- **Checkpoints are not interchangeable between 2.3 and 2.5**, and a LoRA only works with the model it was trained on. Early "my old LoRAs seem fine" reports came from people still loading 2.3 checkpoints in an updated graph. (The 2.5 model card claims the large majority of 2.3 LoRAs/IC-LoRAs carry over — community reports disagree; validate your adapters.)

## Speed reports

| Setup | Result |
| --- | --- |
| RTX 4080 | 5-second 1080p clip in **226 seconds** |
| r/comfyui tester, T2V | LTX-2.5 **"400% faster"** than LTX-2.3 |
| LTX launch benchmark, 2× NVIDIA GB200 | 10-second 720p clip in **6.8 seconds** |

## See Also

- [[ltx-2.5-model]] — model overview and variants
- [[ltx-2.5-technical]] — architecture details
- [[ltx-2.5-local-inference]] — the bf16 PyTorch path, quantization and OOM triage
- [[ltx2-comfyui-integration]] — previous-generation ComfyUI guide
- [[ltx2-comfyui-nodes-reference]]
- [[gguf-quantizations]] · [[fp8-quantization]] · [[hardware-requirements]]
