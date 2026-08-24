# Community VRAM Findings and Local-Setup Workarounds for LTX-2.5 (Aug 12-24, 2026)

**Source:** https://smeltcore.com/recipes/ltx-2-5-on-rtx-4090-fitting-the-22b-audio-video-dit-in-24-gb-via-comfyui-int8 and https://huggingface.co/Lightricks/LTX-2.5/discussions/15
**Date:** 2026-08-12 (recipe) / 2026-08-16 to 2026-08-19 (HF thread)
**Retrieved:** 2026-08-24

## Content

Official docs list a **32GB VRAM minimum** for the standard Python local workflow (plus 32GB
system RAM, ~100GB storage, CUDA 12.7+/13.2+, Python 3.12+). The dominant community activity in
the window was getting LTX-2.5 under that floor.

### The structural constraint (verified from published file sizes)

Smeltcore's RTX 4090 recipe, published 2026-08-12, states the core problem plainly: the int8
transformer the ComfyUI template loads is **20.03 GiB** and the **Gemma 4 12B text encoder is a
further 14.32 GiB — 34.34 GiB of weights for a 24 GiB card**. "They never coexist. ComfyUI
encodes the prompt, frees the encoder, then loads the transformer."

Critically: "**the symptom of an over-full 24 GB card here is thrashing, not an exception.**
If the Gemma 4 12B encoder is still resident when sampling begins... weights stream over PCIe
every step." The recipe explicitly warns against `--highvram`, which does the opposite of what
is needed.

Published transformer builds and 24GB verdicts:

| Build | On-disk | Fits 24GB? |
|---|---|---|
| dev / distilled bf16 | 42.02 GB (39.13 GiB) | No — 15.13 GiB over |
| dev / distilled `comfy-int8-convrot` | 21.50 GB (20.03 GiB) | Yes (both, identical size) |
| distilled nvfp4 | 18.72 GB (17.44 GiB) | No — requires Blackwell SM>=10 |

Full ComfyUI template download: **six files, 49.99 GB**. The 10.28 GB Prompt Enhancer
(`Comfy-Org/gemma-4`, ungated) is **not skippable** even with the enhancer toggled off, because
ComfyUI validates the whole graph before execution. The CLI route needs the bf16 set instead,
~66 GiB.

The recipe is explicit that its 4090 figures are **derived arithmetic, not measured**:
"currently returns `verdict: unknown` with zero benchmarks. Nothing here was measured by us."

### The most-cited community workaround: VAE decode tiling

HF discussion **#15, "LTX 2.5 I2V basic workflow on ComfyUI is stuck forever if try to generate
10sec video"** (`Mike128`, 2026-08-16) is the single most useful local-inference thread.

- OP (RTX 3090, 128GB RAM): "works great and fast for 5sec vids (**like 2mn30 or so without Sage
  Attention**)... but if I try 10sec (in medium res) it gets stuck forever in the decoding phase."
- Fix from `Hole-A`: "Go into the subgraph and **change the VAE Decode (Tiled) node's tile size
  from 768 to 512**." Confirmed working by OP.
- Alternative fix from `ScottishPowers` (RTX 5070 Ti): `temporal_size: 64`,
  `temporal_overlap: 16`.
- **The problem is not just low-VRAM cards.** `DAK25` hit the identical freeze on a **RTX 5090
  32GB + 192GB DDR5** at 720x1280/15s FLF2V: "the entire generation process before decoding VAE
  takes 1.5 minutes on my card, but then the actual decoding takes another 1.5 minutes (with
  SageAttention enabled)." This rebutted another user's claim that the 3090 was simply too weak.

### Lightricks' technical explanation (art-alex, LTX.io org, ~2026-08-19)

"Currently we have 2 decoders: Diffusion VAE decoder and Convolution VAE decoder. The convolution
decoder is the one you all know from LTX-2.3 — it works well and produces decent results. **The
diffusion decoder is completely new and produces much higher quality output than the convolution
one. That quality comes at a cost in performance and VRAM: it operates much closer to pixel
resolution... so it has to process roughly 500x more tokens for a 1080p, 121-frame video.** If
you're running the distilled pipeline at 1080p, the diffusion decoder will end up dominating your
total generation time. Adjusting tiling is a good way to make the diffusion decoder workable on
consumer hardware. As a general rule: bigger tiles decode faster but carry more OOM risk; smaller
tiles are safer on VRAM but slower... We're continuing to optimize the diffusion decoder's
performance."

Follow-up in the same thread: asked whether an int8_convrot diffusion VAE exists, art-alex
confirmed **"we didn't release any official int8_convrot checkpoints of the diffusion VAE. We are
exploring all the options to optimize the VAE with minimal quality loss."** The VAEs are bf16-only.

### Community quantizations (early, low uptake as of 2026-08-12)

- `Abiray/LTX-2.5-Distilled-GGUF` published Q3_K_M through Q8_0 (11.53-23.63 GB) within a day of
  release; smeltcore recorded **0 downloads as of 2026-08-12**.
- `QuantStack` created an `LTX-2.5-GGUF` repo on 2026-08-11 but **had uploaded no model file** as
  of 2026-08-12.
- `guillaume127/LTX-2.5-FP8` — ungated third-party conversion, used by others to read the gated
  transformer's safetensors header. Its author documents that the Gemma 4 12B encoder alone
  "consumes about 14.6 GB" and leaving it resident triggers dynamic VRAM loading.
- `BennyDaBall/LTX-2.5-22b-distilled-nvfp4-comfy` and `vonkaiser/LTX-2.5-FP8-NVFP4`,
  `rockerBOO/ltx-2.5-nvfp4-convrot` also appeared in-window.
- Standing request thread: HF discussion #18, "We need gguf and gguf workflow."

Smeltcore's verdict on GGUF: "Not yet... The int8-convrot checkpoint is the vendor's own artifact,
is what the official template loads, and already fits, so an unvalidated quant buys you nothing on
a 24 GB card."

### Reported real-world timings on consumer hardware (community anecdote)

- RTX 3060 12GB: 15s @960x544 T2V in ~5 min (HF #25) — but a Reddit report gives 10s @0.5MP in
  ~180s.
- RTX 3090 24GB: 5s I2V in ~2m30 without Sage Attention.
- RTX 5060 16GB: 30s @448x1024 with distilled + LoRA in ~7 min.
- RTX 4080 16GB: <1 min for 5s @1080p; 15s @1080p in ~8 min.
- RTX 5090: ~2 min for 10s @720p.
- NVIDIA A4500 via WanGP/Pinokio: 10s @480p in ~3 min; WanGP claims **6GB+ VRAM** support.
- 6GB GPUs via cgpixel23's ComfyUI workflow: 1344x768 7s clip in ~10 min.

### Upscaler footgun flagged by the community

Core ComfyUI LTX-2.5 templates load `ltx-2.5-latent-spatial-upscaler-x2-bf16-1.0.safetensors`,
while the separate `ComfyUI-LTXVideo` node pack's own LTX-2.5 example workflows load the **2.3**
file `ltx-2.3-spatial-upscaler-x2-1.1.safetensors`. Both are correct for their respective
workflows. The two differ by only 35,192 bytes (995,743,560 vs 995,778,752), "so a swap is easy to
make and hard to notice." The *temporal* upscaler genuinely is byte-identical across repos
(261,944,000 bytes), which is likely the source of the confusion.

### Related long-standing grievance (context, opened outside window)

`Lightricks/LTX-Desktop` issue #16 (opened 2026-03-05, since closed) argued LTX Desktop
"hard-gates local inference at 32GB VRAM, forcing any GPU below that threshold into API-only
mode," and that this "contradicts both the open-source ethos of the project and the marketing
claims about consumer hardware support." Included here only as background — it predates the
research window and is not LTX-2.5 feedback.
