# LTX-2.5 in ComfyUI: Day-One Core Support, Templates, Model Files and Node Settings

**Source:** https://www.instasd.com/post/ltx-2-5-comfyui-day-one-guide
**Source:** https://www.earngenix.com/workflows/ltx-2-5-comfyui
**Date:** 2026-08-12 (InstaSD), 2026-08-13 (Earngenix)
**Retrieved:** 2026-08-24

## Content

### Where support actually landed (core, not the custom-node repo)

- Native LTX-2.5 support merged into **ComfyUI core on 2026-08-11** via PR **Comfy-Org/ComfyUI#15499** ("Add support for LTX 2.5"), with **Kijai as co-author**.
- A second merge the same day, PR **#15501**, added **LTX 2.5 partner nodes for the API path**.
- Both landed **before the v0.32.0 tag**, so a stock updated ComfyUI has them. The in-app workflow templates for 2.5 shipped in the templates package pulled by the same release.
- **Minimum ComfyUI version: 0.32.0.** Older installs show the LTX-2.5 nodes as red "This node type does not exist" boxes.
- Follow-up fix on master **2026-08-12** (after the v0.32.0 tag): *"Fix float64 device in ltx diffusion decoder"* — required if you hit a device/dtype error on decode with the new diffusion decoder. Update past the tag or take nightly.
- As of 2026-08-12 the official custom-node repo **github.com/Lightricks/ComfyUI-LTXVideo** still listed only 2.3 and 2.0 workflows in its README, and docs.comfy.org's LTX tutorial section still stopped at 2.0. Day one belonged to core + the template browser, not the custom repo.

### The three official templates

ComfyUI ships three LTX-2.5 workflow templates, all sharing the same five model files:

| Template file | Mode | Stages |
| --- | --- | --- |
| `video_ltx2_5_t2v.json` | Text-to-video | Two-stage (uses spatial upscaler) |
| `video_ltx2_5_i2v.json` | Image-to-video | Two-stage (uses spatial upscaler) |
| `video_ltx2_5_flf2v.json` | First-frame/last-frame interpolation | **Single-stage — does NOT load the upscaler** |

Node names and ComfyUI folder structure are **unchanged from LTX-2.3** — the migration is mainly swapping model files.

### Model files and folders (ComfyUI int8 pack)

| File | ComfyUI folder |
| --- | --- |
| `ltx-2.5-22b-distilled-transformer-comfy-int8-convrot.safetensors` | `models/diffusion_models/` |
| `gemma4-12b-with-proj-ltx-2.5-comfy-int8-convrot.safetensors` | `models/text_encoders/` |
| `ltx-2.5-video-vae-bf16.safetensors` | `models/vae/` |
| `ltx-2.5-audio-vae-bf16.safetensors` | `models/vae/` |
| `ltx-2.5-latent-spatial-upscaler-x2-bf16-1.0.safetensors` | `models/latent_upscale_models/` |
| `gemma4_e2b_it_bf16.safetensors` (optional, Prompt Enhancer; from `Comfy-Org/gemma-4`) | `models/text_encoders/` |

The `*-comfy-int8-convrot` files are **ComfyUI-only** and are not loadable by `ltx-pipelines`/PyTorch. Repo is **gated**: you must click "Agree and Access" on huggingface.co/Lightricks/LTX-2.5; scripted downloads with a fine-grained token need the **`read-gated-repos` scope** or you get a 403 that looks like a bug.

Recommended distilled set is roughly **66 GiB across five files**; the custom-node repo's stated prerequisites are a **CUDA GPU with 32 GB+ VRAM and 100 GB free disk**.

### Node settings that matter

- **ResolutionSelector** — sets width/height from a megapixel value, auto-rounded to a multiple of 32 (a hard model requirement). 16:9 mapping: 0.2 → 608×352, 0.3 → 736×416, 0.4 → 864×480, 0.5 → 960×544, 0.6 → 1056×608, 0.7 → 1152×640, 0.9 → 1280×736, 1.0 → 1376×768, 1.2 → 1504×832, 1.5 → 1664×928, 2.0 → 1920×1088. On a 16 GB card stay at or below 0.6 MP for first tests.
- **Auto Duration** — the model adjusts actual clip length from the described action; padding a prompt to "fill time" only adds noise.
- **prompt_enhance** toggle — runs the prompt through the small Gemma 4 E2B enhancer first. Earngenix testing recommends **leaving it off**; it occasionally rewrote prompts into unrelated output.
- **LTXVSaveConditioning / LTXVLoadConditioning** — encode a prompt once and reuse the encoding across inference runs to save compute and keep results consistent.
- T2V is built as a single **subgraph node** ("Text to Video (LTX-2.5)") bundling conditioning, sampler, CFG guider and VAE decode; "Enter subgraph" to inspect.
- I2V adds only a **LoadImage** node into the generator. Prompt guidance: describe **only motion/camera/audio**, never re-describe what the source photo already shows, or the subject drifts mid-clip.
- FLF2V uses **two LoadImage nodes** (first frame, last frame) and no upscaler.

### VRAM claims (conflicting — note both)

- Earngenix cites LTX's launch materials for a **16 GB VRAM minimum** for LTX-2.5 in ComfyUI, with 24 GB (RTX 4090) comfortable; NVIDIA optimization guidance for the family suggests **540p / 4s clips / 20 steps for 8–16 GB** cards.
- The ComfyUI-LTXVideo custom-node repo and the official Python path state **32 GB+ VRAM**. The two figures describe different pipelines (int8 Comfy pack vs bf16 PyTorch); do not conflate them.

### First-24-hours bug reports (HF discussions, 19 threads in 15 hours)

- **NVFP4 build of the distilled transformer fails to load in ComfyUI.**
- Basic image-to-video workflow hanging indefinitely when asked for 10 seconds of output.
- No GGUF at launch (community builds followed).
- Full-precision transformer exists only as bf16 (no fp16).
- Apple M5 users reporting VAE errors.
- Missing-node errors `GemmaAPITextEncode` and `LTXFloatToInt` — fixed by fully updating ComfyUI.
- Checkpoints are **not interchangeable between 2.3 and 2.5**, and a LoRA only works with the model it was trained on. Early "my old LoRAs seem fine" reports were from people still loading 2.3 checkpoints in an updated graph.

### Speed reports

- RTX 4080: 5-second 1080p clip in **226 seconds**.
- One r/comfyui tester: LTX-2.5 was **"400% faster"** than LTX-2.3 for text-to-video.
- LTX launch benchmark: 10-second 720p clip in **6.8 seconds on 2× NVIDIA GB200** via ComfyUI.
