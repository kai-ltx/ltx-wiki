---
title: LTX Ecosystem
type: concept
created: 2026-04-13
updated: 2026-08-24
sources:
  - https://ltx.io/
  - https://ltx.studio
  - https://ltx.dev/
  - https://ltx.io/model
  - https://docs.ltx.video/welcome
  - https://ltx.io/ltx-desktop
  - https://ltx.io/model/ltx-developer-program
  - raw/ltx-news-ltx-explore-launch-july20-2026.md
  - raw/ltx-news-ltx-2-5-release-2026-08-11.md
  - raw/ltx-news-api-changelog-jul21-aug19-2026.md
tags:
  - ltx
  - ecosystem
  - ltx-2.5
  - lightricks
  - ai-video
---

# LTX Ecosystem

LTX is [[lightricks-company]]'s professional AI video ecosystem that brings together a commercial platform, open-source models, desktop tools, APIs, and developer programs. The name represents Lightricks' pivot from consumer mobile apps to professional-grade AI video production.

The current flagship model is **[[ltx-2.5-model|LTX-2.5]]** (August 11, 2026), a 22B open-weights world model with native multishot generation and native 4K HDR/EXR. [[ltx-2.3-model|LTX-2.3]] remains in service alongside it -- it is cheaper per second and is still the only model exposing the retake, extend and reframe endpoints. The original LTX-2 model IDs were removed from the API on August 16, 2026.

## Ecosystem Map

```
Lightricks
├── Consumer Apps
│   ├── Facetune (photo/video retouching)
│   ├── Videoleap (mobile video editing)
│   ├── Photoleap (image editing + GenAI)
│   └── Popular Pays (creator marketing platform)
│
└── LTX (Professional AI Video)
    ├── LTX Studio (ltx.studio) — Commercial web platform
    ├── LTX Explore (app.ltx.io) — No-code self-service tier (July 2026)
    ├── LTX Desktop — Open-source desktop app
    ├── LTX Models
    │   ├── LTX-Video / LTXV (original, 2B/13B)
    │   ├── LTX-2 (DiT audio-video model, removed from API Aug 16 2026)
    │   ├── LTX-2.3 (22B; still sole home of retake/extend/reframe)
    │   └── LTX-2.5 (current flagship, 22B world model, Aug 2026)
    ├── LTX API (api.ltx.io) — Developer video generation API
    ├── ComfyUI-LTXVideo — ComfyUI node integration
    ├── LTX-Video-Trainer — Fine-tuning toolkit
    └── LTX Builders (Developer Program)
```

## Key URLs

| Property | URL | Purpose |
|----------|-----|---------|
| ltx.io | https://ltx.io | Central hub: platform, models, API, enterprise |
| ltx.studio | https://ltx.studio | Commercial AI video creation platform |
| ltx.dev | https://ltx.dev | Developer-focused model access |
| docs.ltx.io | https://docs.ltx.io | API documentation |
| api.ltx.io | https://api.ltx.io | API endpoint (new domain, July 21 2026; `api.ltx.video` still works) |
| GitHub (LTX-2) | https://github.com/Lightricks/LTX-2 | Model code and training |
| GitHub (Desktop) | https://github.com/Lightricks/LTX-Desktop | Desktop app |
| GitHub (ComfyUI) | https://github.com/Lightricks/ComfyUI-LTXVideo | ComfyUI plugin |
| GitHub (Trainer) | https://github.com/Lightricks/LTX-Video-Trainer | Fine-tuning toolkit |
| HuggingFace | https://huggingface.co/Lightricks/LTX-2.5 | Current model weights |

## Product Comparison

| Feature | [[ltx-studio]] | [[ltx-desktop]] | [[ltx-api]] |
|---------|----------------|-----------------|-------------|
| Type | Web platform | Desktop app | HTTP API |
| Cost | $0-$125/mo | Free (Apache 2.0) | Per-second billing |
| Target | Creatives, marketers | Developers, power users | Developers, products |
| Runs on | Cloud (browser) | Local GPU or API | Cloud |
| Model | Multiple (incl. Veo) | LTX-2.3 / LTX-2.5 | LTX-2.3, LTX-2.5 |
| Open Source | No | Yes | No |
| Max Resolution | Varies by plan | 4K | 4K |
| Audio | Yes | Yes | Yes |
| Collaboration | Yes (Pro+) | No | N/A |

## Open Source Components

Application code uses the **Apache 2.0** license:

- [[ltx-desktop]] (full application)
- LTX-2 (model code, pipelines, trainer)
- LTX-Video (original model)
- ComfyUI-LTXVideo (plugin nodes)
- LTX-Video-Trainer (fine-tuning toolkit)

Model weights have a separate license. LTX-2.5 ships under the **LTX-2.x Community License** -- free under $10M ARR, but not OSI open source, with field-of-use restrictions and copyleft on derivatives. See [[ltx-video-licensing]].

## Integration Points

See [[ltx-integration-projects]] for the full integration landscape. Key integration points include:

1. **ComfyUI** - Custom nodes for node-based video workflows
2. **fal.ai** - Third-party API hosting of LTX models
3. **Segmind** - Alternative API access
4. **Modal** - Serverless deployment option
5. **AI Coding Agents** - AGENTS.md/CLAUDE.md support in LTX Desktop repo (see [[ltx-mcp-integration]])

See [[github-official-repositories]] for repository details and [[github-community-tools]] for the broader community tool ecosystem.

## Related Pages

- [[ltx-2.5-model]] -- Current flagship model
- [[ltx-2.3-model]] -- Previous flagship, still API-supported
- [[ltx-explore]] -- Self-service no-code tier
- [[ltx-video-changelog]] -- API changelog
- [[ltx-video-licensing]] -- License terms

## Developer Program

See [[ltx-builders-program]] for details on the invite-only LTX Builders developer program.
