# Content status

Update this after every page. Status values: `empty` · `stub` · `drafted` · `needs screenshots` · `done`

> **Note on `--strict`:** the deploy workflow builds with `--strict`, which fails if a nav
> entry has no file. Create stub files for every nav entry in step 1 before the first push,
> or temporarily drop `--strict` from `.github/workflows/deploy.yml`.

> **`exclude_docs`:** `docs/_template.md` is excluded from the build in `mkdocs.yml`. Its
> example links (`path.md`, `analysis.md`, `url`) are placeholders that can never resolve, so
> including it in the build fails `--strict`. It stays in `docs/` as authoring reference.

## Setup

| Item | Status |
|---|---|
| `mkdocs.yml` | done |
| `CLAUDE.md` | done |
| `docs/_template.md` | done |
| `.github/workflows/deploy.yml` | done |
| `docs/index.md` (homepage) | drafted — states the 3.7 version pin |
| `.gitignore` | done |
| Pages source set to GitHub Actions in repo settings | **manual — repo owner** |
| Stub files for every nav entry | done — 52 files, `mkdocs build --strict` passes |

## Getting Started

| Page | Status | Screenshots needed |
|---|---|---|
| Overview | stub | |
| Installing and licensing | stub | |
| Projects, maps and layers | stub | |
| Anatomy of the interface | stub | |
| Your first project | stub | |

## Interface — backstage, ribbon, contextual, panes

| Page | Status | Screenshots needed |
|---|---|---|
| Project backstage | stub | |
| Ribbon overview | stub | |
| Map | stub | |
| Insert | stub | |
| Analysis | stub | |
| View | stub | |
| Edit | stub | |
| Imagery | stub | |
| Share | stub | |
| Help | stub | |
| Contextual overview | stub | |
| Feature Layer — Appearance | stub | |
| Feature Layer — Labeling | stub | |
| Feature Layer — Data | stub | |
| Raster Layer | stub | |
| Table | stub | |
| Layout | stub | |
| Panes overview | stub | |
| Contents pane | stub | |
| Catalog pane and view | stub | |
| Geoprocessing pane | stub | |
| Symbology pane | stub | |
| History pane | stub | |

## Wildfire

| Page | Status | US covered | Canada covered |
|---|---|---|---|
| Overview | stub | no | no |
| How fire spread models work | stub | no | no |
| Fuel models — US vs Canada | stub | no | no |
| Terrain inputs | stub | no | no |
| Weather inputs | stub | no | no |
| Preparing a study area | stub | no | no |
| Building a terrain stack | stub | no | no |
| Preparing fuel layers | stub | no | no |
| Exporting to a simulator | stub | no | no |
| Importing results | stub | no | no |
| Mapping burn severity | stub | no | no |
| Simulator overview | stub | no | no |
| FARSITE and FlamMap | stub | n/a | n/a |
| Prometheus and BurnP3 | stub | n/a | n/a |

## Data sources

| Page | Status |
|---|---|
| Overview | stub |
| United States | stub |
| Canada | stub |
| Ontario and local | stub |
| Basemaps and imagery | stub |
| Evaluating a dataset | stub |

## Reference

| Page | Status |
|---|---|
| Keyboard shortcuts | stub |
| Glossary | stub |
| Troubleshooting | stub |

---

## Outstanding screenshots

Add every `<!-- SCREENSHOT NEEDED -->` here as it is created, with the exact path the page
expects, so the repo owner can capture them in batches.

| Path | Page | Captured |
|---|---|---|

---

## Unverified links

Add every `<!-- LINK NEEDED -->` here.

| Tool / dataset | Page | Resolved |
|---|---|---|

---

## Open questions for the repo owner

- Which simulator will the research actually use? This decides which export workflow gets
  the most detail.
- Study area — a specific region, or general-purpose examples?
- ~~Is there a licensed Spatial Analyst extension available?~~ **Answered 2026-08-30: yes.**
  Terrain and fuel workflows can use Spatial Analyst tools directly. Pages should still name
  the extension requirement, since a reader may not have it.
