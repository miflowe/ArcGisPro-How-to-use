# Content status

Update this after every page. Status values: `empty` · `stub` · `drafted` · `needs screenshots` · `done`

> **Note on `--strict`:** the deploy workflow builds with `--strict`, which fails if a nav
> entry has no file, or if a page links to a missing file or image. Every nav entry currently
> has a stub and the build passes.

> **Screenshot convention:** image markdown is written *inside* the
> `<!-- SCREENSHOT NEEDED: ... -->` comment. Delete the two comment lines once the file
> exists and the image publishes. This keeps CI green without weakening validation, and
> without fabricating placeholder images. See `CLAUDE.md` §4.

> **`exclude_docs`:** `docs/_template.md` is excluded from the build in `mkdocs.yml`. Its
> example links are placeholders that can never resolve, which would fail `--strict`. It
> stays in `docs/` as authoring reference.

## Setup

| Item | Status |
|---|---|
| `mkdocs.yml` | done — nav is Home + Wildfire + Data Sources |
| `CLAUDE.md` | done — rewritten for wildfire-only scope |
| `docs/_template.md` | done — workflow page template |
| `.github/workflows/deploy.yml` | done |
| `requirements.txt` | done — toolchain pinned |
| `docs/index.md` (homepage) | drafted |
| `.gitignore` | done |
| Pages source set to GitHub Actions in repo settings | done — repo owner |
| First deploy verified live | done |

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

## Unverified UI details

Every `<!-- VERIFY: ... -->` marker. Claims needing a check against ArcGIS Pro 3.7.1 before
the page can move to `done`.

| Page | What needs checking | Confirmed |
|---|---|---|

---

## Salvage

`notes/` holds drafted pages from the two previous structures. They are outside `docs/` so
they do not build. Fold the useful content into workflow pages; do not restore the pages.

**`notes/salvage-add-data.md`** — drafted "Add data to a map" page:

- **The first layer sets the map's coordinate system**, and everything added afterwards is
  reprojected on the fly *for display only*. Layers look aligned while sitting in different
  systems underneath, which is how raster maths silently produces wrong output. This is the
  most important gotcha we have written so far — it belongs in
  `wildfire/workflows/terrain-stack.md`.
- **A layer points at the file, it does not copy it.** Moving the source breaks the layer.
- **A CSV or Excel table has no geometry** until you run XY Table To Point. Relevant wherever
  weather station data gets loaded — `wildfire/concepts/weather.md`.

**`notes/salvage-project-backstage.md`** — drafted Project backstage page:

- **The default geodatabase** — a new project silently creates a home folder, geodatabase and
  toolbox, and every tool writes there by default. Belongs in
  `wildfire/workflows/study-area.md`.
- **Licensing is where you confirm Spatial Analyst is enabled**, and a missing extension looks
  identical to a missing tool. Belongs in the "You will need" line of the first workflow page
  that requires it.
- **Package Manager requires cloning the default Python environment before installing.**
  Belongs wherever Python scripting lands. Still unverified.

Delete each bullet once the content has landed.

---

## Open questions for the repo owner

- Which simulator will the research actually use? This decides which export workflow gets
  the most detail.
- Study area — a specific region, or general-purpose examples?
- ~~Is there a licensed Spatial Analyst extension available?~~ **Answered 2026-08-30: yes.**
  Terrain and fuel workflows can use Spatial Analyst tools directly. Pages should still name
  the extension requirement, since a reader may not have it.
