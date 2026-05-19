# LTX Studio API & Platform Updates: Async Endpoints, HDR, and Enterprise Features (April–May 2026)

**Source:** https://docs.ltx.video/api-changelog
**Date:** 2026-05-01
**Retrieved:** 2026-05-19

## Content

Based on the LTX Studio API changelog and product release notes, several platform and API-level updates were shipped in the April–May 2026 window alongside the Flows, Video-to-Video, and model releases.

### SDR-to-HDR Conversion (April 2026)

- A new SDR-to-HDR endpoint and in-platform tool was launched, allowing any existing standard dynamic range video to be converted to true High Dynamic Range (HDR) in a single pass.
- Available both as a platform UI feature and via the LTX API.

### Brand Kit (Enterprise, April 2026)

- **Brand Kit** launched as an Enterprise-only feature.
- Designed for organizations managing multiple brands, teams, and large volumes of visual content.
- Enables embedding of brand assets (logos, color palettes, style references) into generation pipelines, including Flows.
- Tightly integrated with the Flows automation feature launched in May 2026.

### LTX API Async Endpoints

- The LTX API (`docs.ltx.video`) added or expanded asynchronous generation endpoints during this period.
- Async endpoints decouple request submission from result polling, enabling scalable integration into production pipelines.
- Documented at https://docs.ltx.video/api-changelog.

### LTX Desktop v1.0.3 (April 3, 2026)

- Preceding the v1.0.5 release, v1.0.3 significantly reduced video memory (VRAM) usage.
- GPUs with 12 GB or more of VRAM can now run the full LTX-2.3 pipeline via LTX Desktop.
- This change materially expanded the addressable consumer hardware base for local LTX-2.3 inference.

### Sources

- https://docs.ltx.video/api-changelog
- https://ltx.studio/release-notes
- https://github.com/Lightricks/LTX-Desktop/releases
- https://ltx.studio/blog-category/product-updates
