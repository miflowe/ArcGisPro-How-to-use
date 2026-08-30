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
| `mkdocs.yml` | done — nav restructured to tasks |
| `CLAUDE.md` | done — §1, §2, §3, §4, §9 rewritten for task structure |
| `docs/_template.md` | done — task page template |
| `.github/workflows/deploy.yml` | done |
| `requirements.txt` | done — toolchain pinned |
| `docs/index.md` (homepage) | drafted |
| `.gitignore` | done |
| Pages source set to GitHub Actions in repo settings | done — repo owner |
| First deploy verified live | done |

## What You Can Do

The core of the site. One page per task; the page ends when the task is done.

| Page | Status | Screenshots needed |
|---|---|---|
| Overview (`tasks/index.md`) | stub | |
| Add data to a map | stub | |
| Symbolize a layer | stub | |
| Label features | stub | |
| Work with attribute tables | stub | |
| Edit features | stub | |
| Run an analysis tool | stub | |
| Make a printable map | stub | |
| Share your work | stub | |

## Panes

| Page | Status | Screenshots needed |
|---|---|---|
| Contents pane | stub | |
| Catalog pane and Catalog view | stub | |

## Getting Started

| Page | Status | Screenshots needed |
|---|---|---|
| Overview | stub | |
| Installing and licensing | stub | |
| Projects, maps and layers | stub | |
| Where things live | stub | |
| Your first project | stub | |

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

## Unverified UI details

Every `<!-- VERIFY: ... -->` marker. Claims needing a check against ArcGIS Pro 3.7.1 before
the page can move to `done`.

| Page | What needs checking | Confirmed |
|---|---|---|
| Home | Is the version number shown on the Info page? | no |

---

## Salvage

`notes/salvage-project-backstage.md` is the drafted Project backstage page from the previous
tab-based structure, kept out of `docs/` so it does not build. Its useful content should be
folded into task pages rather than restored as its own page:

- The **default geodatabase** gotcha — a new project silently creates a home folder, a file
  geodatabase and a toolbox, and every tool writes to that geodatabase by default. Belongs in
  `getting-started/core-concepts.md` or `tasks/run-a-tool.md`.
- **Save Project As does not copy the data**, only the `.aprx`. Belongs in
  `tasks/share-your-work.md`. Still unverified.
- **Licensing is where you confirm Spatial Analyst is enabled**, and a missing extension
  looks identical to a missing tool. Belongs in `getting-started/install-and-license.md`.
- **Package Manager requires cloning the default Python environment before installing.**
  Belongs in `tasks/run-a-tool.md` if scripting gets covered. Still unverified.

Delete this section once the content has landed.

---

## Open questions for the repo owner

- Which simulator will the research actually use? This decides which export workflow gets
  the most detail.
- Study area — a specific region, or general-purpose examples?
- ~~Is there a licensed Spatial Analyst extension available?~~ **Answered 2026-08-30: yes.**
  Terrain and fuel workflows can use Spatial Analyst tools directly. Pages should still name
  the extension requirement, since a reader may not have it.
- Does the `Reference` section (shortcuts, glossary, troubleshooting) still earn its place,
  or should it go the way of the tab pages? Not urgent — it is last in the work order.
