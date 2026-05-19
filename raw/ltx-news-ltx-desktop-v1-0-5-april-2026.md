# LTX Desktop v1.0.5 Release — April 28, 2026

**Source:** https://github.com/Lightricks/LTX-Desktop/releases
**Date:** 2026-04-28
**Retrieved:** 2026-05-19

## Content

Lightricks released LTX Desktop v1.0.5 on April 28, 2026, the open-source desktop application for local video generation with LTX models. This followed the v1.0.3 release on April 3, 2026 (which significantly reduced VRAM usage, enabling GPUs with 12 GB+ VRAM to run the app).

### v1.0.5 Bug Fixes

- **First Launch / API Key**: LTX API key set during first launch was not reflected in the UI without a restart — fixed.
- **LTX API Insufficient Funds**: Error now shows a dedicated message with a button linking to the LTX API console to purchase credits (previously the error was generic with no actionable guidance).
- **A2V (Audio-to-Video) Local Generations**: Local A2V generations were unnecessarily restricted to landscape aspect ratio and specific resolutions — restrictions removed, enabling portrait and custom resolution A2V.
- **Backend Launch Error**: In specific failure cases, a launch error could appear with no message and a non-functional retry button — fixed.

### v1.0.5 Improvements

- App version is now logged at startup in reported log files, aiding bug investigation.
- Added volume control for video assets directly from the Gen Space asset thumbnails.

### Context

LTX Desktop is the standalone, locally-runnable version of the LTX Studio platform, released alongside LTX-2.3 in March 2026. It allows consumer GPU owners (12 GB+ VRAM) to run the full LTX-2.3 model pipeline offline. The v1.0.x release series has been iterating rapidly with quality-of-life and compatibility improvements since March 2026.

### Sources

- https://github.com/Lightricks/LTX-Desktop/releases
- https://github.com/Lightricks/LTX-Desktop
