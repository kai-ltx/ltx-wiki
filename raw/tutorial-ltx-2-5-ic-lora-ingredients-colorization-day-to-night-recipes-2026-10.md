# LTX-2.5 IC-LoRA Recipes: Ingredients, Colorization, Day-to-Night (Hugging Face Model Cards)

**Source:** https://huggingface.co/Lightricks/LTX-2.5-22b-IC-LoRA-Ingredients ; https://huggingface.co/Lightricks/LTX-2.5-22b-IC-LoRA-Colorization ; https://huggingface.co/Lightricks/LTX-2.5-22b-IC-LoRA-Day-To-Night
**Date:** 2026-09 (model cards, undated; collection updated within the last two weeks at retrieval)
**Retrieved:** 2026-10-12

## Content

All three adapters: base LTX-2.5-22B, IC-LoRA (video-to-video), reference downscale factor 1, license `ltx-2.x-community-license`, gated Hugging Face repos (must accept terms/share contact info), weights in `.safetensors` v0.9, run via `uv run python -m ltx_pipelines.ic_lora` on the distilled LTX-2.5 base (needs distilled transformer, `gemma4-12b-with-proj-ltx-2.5-bf16`, video+audio VAE, spatial upsampler) or in ComfyUI with the LoRA at strength 1.0.

### Ingredients (Reference Sheet Control)
- Control signal: a single composite **reference sheet** image (one clean panel per element, black background, no text), supplied as a **static video** looped to at least 121 frames at output resolution/fps.
- Prompt format: `Reference sheet: <panel descriptions>` then `Generated video: <action, dialogue, camera>`.
- Trained bucket: **768x448, 121 frames, 24 fps** only; other resolutions/lengths are out of distribution. 12,000 steps, rank 128, AdamW-8bit, LR 1.3e-4 then 1.3e-5. Base used: LTX-2.5-22B **dev**.
- Tips: bigger panels carry over better; character needs a front face close-up plus turnaround; only elements on the sheet are reproduced; reference under 121 frames breaks encoding.
- ComfyUI: `LTX-2.5_ICLoRA_Ingredients_Single_Stage_Distilled.json` (in ComfyUI-LTXVideo `example_workflows/2.5/`). Example demos include brand-mascot commercials and multi-character dialogue scenes with audio.
- Suggested negative prompt: `worst quality, inconsistent motion, blurry, jittery, distorted`.

### Colorization
- Restores color to grayscale/monochrome/desaturated footage; only color changes (identity, framing, geometry preserved). Not a deblur/denoise/upscale model.
- Prompt convention: `Reference shows {grayscale scene}. Edited shows the same scene with natural colors restored. COLORIZE {vivid color description}. Subject identity, framing, and background geometry are identical to the reference; only color information differs between reference and edited.`
- Trained at **960x544x121 @ 24fps** (landscape and portrait); far higher resolution weakens the effect. 1,500 steps, rank 128, proprietary dataset.
- Production recipe: distilled `ic_lora` pipeline, **stage-1-only native hi-res** (`--skip-stage-2 --tile-reference-encode`, 2x canvas), strength 1.0, seed 42; distilled uses fixed sigmas so **no CFG and no negative prompt**. Troubleshooting: lower strength to 0.8-0.9 for bleed/oversaturation; keep stage-1-only recipe to avoid identity drift.

### Day-to-Night Relighting
- Re-renders a daytime clip as the same shot at night, frame-for-frame composition and motion. Dataset: **192 motion-aligned day/night video pairs**. Rank 32, 3,000 steps, LR 2e-4.
- Trained at 768x448 / 448x768, 97 frames @ 24fps (~4s); longer clips drift toward the end. Re-encode reference to clean H.264 at 24 fps first (loader does not resample temporally); frames must satisfy `frames % 8 == 1`, dims divisible by 32.
- Settings: 30 steps, guidance 3.0-4.0 (lower = brighter/more detail, higher = darker/stronger night), STG `stg_v` scale 1.0 block [29]. Prompt steers night style and color temperature ("warm tungsten" vs "cool white LED"). Negative prompt suggested: `daytime, bright sunlight, blue sky, overexposed, worst quality, inconsistent motion, blurry, jittery, distorted`.
- Indoor and heavy artificial-light scenes work but are outside the primary training distribution; no mask support.
- ComfyUI: `LTX-2.5_V2V_ICLoRA_Single_Stage_Distilled.json` generic V2V IC-LoRA workflow.
