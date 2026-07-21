# LTX-2 Deprecation — Migration to LTX-2.3 Forced

**Source:** https://docs.ltx.video/api-changelog/2026/7/2 ; https://help.ltx.io/hc/en-us/articles/37042091564562-Migrating-from-LTX-2-to-LTX-2-3
**Date:** 2026-07-02
**Retrieved:** 2026-07-21

## Content

LTX announced via the API changelog that the original LTX-2 model (`ltx-2-fast`, `ltx-2-pro`) is being deprecated:

- **July 15, 2026** — LTX-2 requests are automatically served by LTX-2.3 (`ltx-2-3-fast` / `ltx-2-3-pro`) with no change to LTX-2 pricing during the transition.
- **August 15, 2026** — LTX-2 is fully removed; requests to the old model IDs return an error.
- Developers must migrate references to `ltx-2-3-fast`/`ltx-2-3-pro` before Aug 15, 2026.

### Known migration issues (from community guides, e.g. WaveSpeed and ltxworkflow.com blogs)

- **LoRA incompatibility**: LTX-2.3 grew from ~19B to 22B parameters and redesigned the VAE/latent space, so LTX-2 LoRAs do not transfer cleanly — one developer reported LoRAs "attach" but produce off-style or collapsed results.
- **Prompt behavior changed**: LTX-2.3 follows positional language ("left/right", "foreground/background") more literally; default contrast/saturation render punchier than LTX-2's neutral presets.
- **Seed behavior differs**: Same seed does not reproduce the same output across versions — outputs diverge after ~10-12 diffusion steps.
- Guidance to developers: LTX-2.3 is a drop-in API replacement (same endpoints/parameters), but avoid switching foundation models mid-production; finish in-flight projects on LTX-2, then migrate cleanly.

This effectively completes Lightricks' transition to LTX-2.3 as the sole supported open/API model line, five months after LTX-2.3's March 2026 launch.
