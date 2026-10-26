# LTX Desktop Major Update (v1.3.0): Built-in LoRAs, Batch Queue, Remote Generation

**Source:** https://ltx.io/release-notes ; https://github.com/Lightricks/ltx-desktop/issues
**Date:** 2026-10-09
**Retrieved:** 2026-10-26

## Content

Official LTX release-notes entry dated October 9, 2026 ("Open source"): "A major update to LTX Desktop makes it easier to create, refine, and manage video projects locally."

- **New creative capabilities:** 13 built-in LoRAs, plus IC-LoRAs for AlphaGen, Deblur, Colorization, Clean Plate, Decompression, Water Simulation, Day to Night, Restore and Layout to Render. Adds Retake, Extend and improved prompt enhancement.
- **More control:** fast-preview resolutions; seed control for consistent results.
- **Remote generation:** generate on the desktop and monitor sessions from a mobile device or another browser on the same Wi-Fi network.
- **Batch generation:** queue multiple generations in the background; reorder or cancel jobs.
- **Redesigned experience:** new homepage, quick search, updated Explore form with gallery cards, asset library, batch-generation queue.
- **Simpler setup:** improved installer, first-run onboarding, clearer system requirements, settings pages with model management.

Version numbering: GitHub issues #181 (2026-10-19) and #183 (2026-10-22) reference "LTX Desktop 1.3.0" / "1.3", confirming the update shipped as v1.3.x. A search summary reports a v1.3.1 bug-fix release on 2026-10-19 (Retake/Extend on 2.3 while 2.5 active; 20 s 1080p on 32 GB cards). The GitHub releases page fetched this run still showed 1.2.7 (2026-08-26) as latest, likely a cached view, so v1.3.1 is unverified.

Prior releases (GitHub, for context): 1.2.0 (2026-08-14) local LTX 2.5 Fast; 1.2.4 (2026-08-19) opt-in updates and Stop for local jobs; 1.2.5 (2026-08-20) local 2.5 Retake/Extend; 1.2.6 (2026-08-23) last-frame image, Gemini 3.5 Flash-Lite default for Enhance; 1.2.7 (2026-08-26) Apple Silicon memory spike fix and AMD ROCm FP8 fix.

Security note: release notes do not say how remote generation authenticates other devices on the LAN. v1.0.2 (2026-03-12) changelog says the backend was switched to "listen on free port and require auth" (PR #35), which suggests auth exists, but the remote-generation feature's auth model is not documented.
