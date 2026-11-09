# fal Pricing Snapshot (Nov 9) and LTX Community Hub Status

**Source:** https://pricingsaas.com/companies/fal/diffs/2026W44 ; https://ltxworkflow.com/changelog ; https://comfy.org/ltx-2.5/
**Date:** 2026-11-09 (latest fal capture); 2026-10-26 (last fal price change)
**Retrieved:** 2026-11-09

## Content

- PricingSaaS Pulse latest capture of fal's pricing page is **Nov 9, 2026**. No fal pricing change recorded after **Oct 26** (MiniMax H3 Max I2V/T2V cut $0.05 -> $0.03/s, H3 Max Turbo $0.025 -> $0.015/s, Reference-to-Video unchanged at $0.05). **No LTX price change** in the window.
- fal headline rates on the Nov 9 capture: Serverless $6/H200 GPU-hour, $4/RTX PRO 6000 GPU-hour; video examples MiniMax H3 Max $0.05/s (list), Kling 2.5 Turbo Pro $0.07/s.
- fal's LTX-2.5 landing page (fal.ai/ltx-2.5) still lists six LTX-2.5 variants (T2V, I2V, A2V among them) starting at $0.01 per second; fal claims 80+ LTX fine-tunes hosted (per search summary, undated).
- ltxworkflow.com (unofficial hub, not affiliated with Lightricks) changelog newest entry is still **2026-09-19** (24 Creative Lab LoRAs catalogued: 9 for LTX 2.5, 15 for LTX 2.3). It notes LTX 2.5 official files need 24 GB+ VRAM combined (Gemma 4 encoder alone 15.37 GB+); 16 GB cards need GGUF (Q4_K_M 8.41 GB, Q2_K 5.96 GB encoders).
- ComfyUI: no new LTX-2.5 templates found beyond the four native templates (T2V, I2V, FLF2V, DFR) logged on 2026-11-02.
- Security note for integrators: fal and LTX APIs authenticate with bearer API keys. Keep keys in a secrets manager or environment variable, not in workflow JSON shared publicly (CWE-798, hard-coded credentials; OWASP A07:2021).
