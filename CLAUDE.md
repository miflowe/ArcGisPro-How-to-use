# CLAUDE.md — Project brief

This repo builds a documentation site that teaches ArcGIS Pro, organized around **what the
reader is trying to do**, plus a second half covering wildfire simulation workflows.

Audience: researchers and students who have ArcGIS Pro open on a second monitor and want
to know what a button does and when to use it. Assume GIS-curious, not GIS-expert.

---

## 1. Non-negotiables

**Version pin: ArcGIS Pro 3.7.1.** Every page assumes 3.7.1 — the build the repo owner runs
and checks button names against. (The 3.7 line released May 2026.) If a feature arrived in a
specific release, say so inline. The homepage states the pinned version.

**Never copy Esri's documentation text.** Esri docs are copyrighted. Write original
explanations in your own words. Link out with `[Esri reference →](url)` for detail. If you
cannot explain a tool without paraphrasing Esri closely, write one honest sentence and let
the link carry the rest.

**Never invent a URL.** If you need an Esri doc link and don't have a verified one, write
`<!-- LINK NEEDED: <tool name> -->` and add it to `CONTENT_STATUS.md`. A wrong link is
worse than a missing one.

**Never invent UI details.** If you are unsure whether a button exists in 3.7.1, what it is
called, or where it sits, mark it `<!-- VERIFY: ... -->` rather than guessing, and log it in
`CONTENT_STATUS.md`. The value of this site is accuracy; a confidently wrong button name
destroys trust in the whole page. Assistant knowledge of 3.7.1 specifically is thin — this
mechanism is load-bearing, not a formality.

---

## 2. Structure: tasks, not tabs

The site is organized by task. One page per thing you want to accomplish, and the page ends
when the task is done.

This was a deliberate change away from a page-per-ribbon-tab structure. The reason matters,
because it will be tempting to drift back:

- A tab page has no natural end. There is always another button, so the page grows until it
  is unreadable.
- Its page count is set by Esri's ribbon rather than by what a reader needs.
- The reader's question is "how do I label my features", not "what is on the Labeling tab".

**Do not add a page per ribbon tab, pane, or contextual tab.** The "which tab is this on?"
need is served by one page — `getting-started/where-things-live.md` — which is a lookup
table, not an essay.

Two exceptions, both kept because you use them constantly rather than because they are UI
surfaces: `panes/contents.md` and `panes/catalog.md`. The Catalog page must explain that the
Catalog *pane* and Catalog *view* are different things.

Where UI vocabulary is still needed on a task page, name the tab and group only so the
reader can find the button — "**Map** tab → **Add Data**" — then move on.

---

## 3. Page template and length

Every task page follows `docs/_template.md`.

**Concision is a hard requirement, not a preference.** Target one screen of reading plus the
steps. If a page is getting long, it is probably two tasks — split it.

There is no coverage quota. An earlier version of this brief required every button to appear
in a reference table; that rule is gone, because it forced pages to document things like
"Save Project — saves the project" and buried the useful content.

Write only what a reader cannot guess:

- **Use this when** — the concrete situation that brings someone to the page.
- **Steps** — the path that works. Not every alternative Esri offers.
- **Gotchas** — what silently loses work or gives wrong results. Usually the most valuable
  thing on the page.

Omit any button whose name explains it. Omit steps the reader would take unprompted. If a
section has nothing real in it, delete the section rather than padding it.

---

## 4. Screenshots

Path convention: `docs/assets/images/<section>/<page>-<thing>.png`

- Task page: `docs/assets/images/tasks/add-data-browse-dialog.png`
- Pane: `docs/assets/images/panes/contents-pane.png`

The repo owner takes the screenshots. Never generate or fabricate an image.

**Write the image markdown anyway, inside the comment:**

```markdown
<!-- SCREENSHOT NEEDED: docs/assets/images/tasks/add-data-browse-dialog.png
     Delete these two comment lines once the file exists, to publish the image.
![The Add Data browse dialog](../assets/images/tasks/add-data-browse-dialog.png)
-->
```

This is deliberate. `mkdocs build --strict` fails on a link to a missing image, so markdown
written *outside* a comment turns CI red on every page that is waiting on a screenshot.
Inside the comment the path and alt text are recorded and greppable, and the build stays
green. Log each one in `CONTENT_STATUS.md`.

Use screenshots where they save the reader a hunt — a dialog, a specific button. A page does
not need one to be publishable.

---

## 5. Writing style

- Second person. "You'll use this when..." not "The user may utilize..."
- Short sentences. No marketing voice, no "powerful," "seamless," "robust."
- Lead with what the thing is *for*, not what it *is*.
- Use MkDocs Material admonitions, sparingly:
  - `!!! tip` — a genuine shortcut or time-saver
  - `!!! warning` — something that loses work or silently gives wrong results
  - `!!! note "Wildfire"` — how this tool connects to fire modeling
- No emoji. No horizontal rules mid-page — headings give enough separation.
- Bold sparingly; it stops working if every third phrase is bold.

---

## 6. Wildfire half of the site

The repo covers **both** the US and Canadian fire modeling ecosystems. These are genuinely
different systems, not dialects — different fuel classifications, different fire behavior
equations, different data providers.

- **US:** Scott & Burgan / Anderson fuel models, LANDFIRE fuel and topography layers,
  FARSITE / FlamMap / FSPro, IFTDSS.
- **Canada:** the Canadian Forest Fire Danger Rating System (CFFDRS), specifically the Fire
  Behaviour Prediction (FBP) System fuel types, and Prometheus / BurnP3 for simulation.

Where a workflow differs by country, use Material **content tabs**:

```markdown
=== "United States"
    Steps using LANDFIRE fuel layers...

=== "Canada"
    Steps using FBP fuel type grids...
```

Never silently blend the two. A reader following a US fuel model with Canadian data will
get plausible-looking, wrong output — the most dangerous failure mode for this site.

Every wildfire workflow page ends with a **Limitations** section stating what the model
does not account for. These are research tools; the site should not read like the outputs
are ground truth.

---

## 7. Data source pages

Each data source gets a short entry: what it contains, spatial resolution, temporal
coverage, format, licence/cost, and how to load it into ArcGIS Pro. Verify every download
link before publishing; mark unverified ones `<!-- LINK NEEDED -->`.

Sources to cover (verify all URLs — do not assume):

*US:* LANDFIRE, USGS 3DEP elevation, National Interagency Fire Center open data, MTBS burn
severity, NASA FIRMS active fire detections, RAWS weather stations.

*Canada:* Canadian Wildland Fire Information System (CWFIS), National Fire Database,
NRCan CDEM/HRDEM elevation, Canadian forest fuel type grids, Environment and Climate Change
Canada weather, provincial open data portals (Ontario GeoHub for local work).

---

## 8. Build

```bash
pip install -r requirements.txt
mkdocs serve      # local preview at localhost:8000
mkdocs build --strict   # what CI runs; must pass before pushing
```

Versions are pinned in `requirements.txt` because MkDocs 2.0 is a breaking rewrite with no
migration path. Do not install `mkdocs-material` unpinned.

Deployment is automatic via `.github/workflows/deploy.yml` on push to `main`. In repo
Settings → Pages, set Source to **GitHub Actions**.

---

## 9. Order of work

Do not attempt the whole site in one pass. **One page per commit**, commit message
`docs: add <page name>`. Update `CONTENT_STATUS.md` after each page.

The repo owner checks button names against the running software, so pages land one at a time
and get reviewed before the next one starts. Do not batch pages.

Suggested sequence:

1. ~~Scaffold~~ — done. Every nav entry has a stub and `mkdocs build --strict` passes.
2. `tasks/add-data.md` — first real task page, and the one that sets the tone for length.
3. The rest of `What You Can Do`, in nav order.
4. `panes/contents.md`, then `panes/catalog.md`.
5. `getting-started/where-things-live.md` — write this once the task pages have shown which
   tab locations actually get referenced.
6. The rest of `Getting Started`.
7. Data source pages.
8. Wildfire workflows last — they cross-link into everything above.
