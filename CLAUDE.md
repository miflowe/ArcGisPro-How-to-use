# CLAUDE.md — Project brief

This repo builds a documentation site that teaches ArcGIS Pro, organized to mirror the
software's own interface, plus a second half covering wildfire simulation workflows.

Audience: researchers and students who have ArcGIS Pro open on a second monitor and want
to know what a button does and when to use it. Assume GIS-curious, not GIS-expert.

---

## 1. Non-negotiables

**Version pin: ArcGIS Pro 3.7.** Every page assumes 3.7 (released May 2026). If a feature
arrived in a specific release, say so inline. The homepage states the pinned version.

**Never copy Esri's documentation text.** Esri docs are copyrighted. Write original
explanations in your own words. Link out with `[Esri reference →](url)` for detail. If you
cannot explain a tool without paraphrasing Esri closely, write one honest sentence and let
the link carry the rest.

**Never invent a URL.** If you need an Esri doc link and don't have a verified one, write
`<!-- LINK NEEDED: <tool name> -->` and add it to `CONTENT_STATUS.md`. A wrong link is
worse than a missing one.

**Never invent UI details.** If you are unsure whether a button exists on a tab in 3.7, or
which group it sits in, mark it `<!-- VERIFY: ... -->` rather than guessing. The value of
this site is accuracy; a confidently wrong button name destroys trust in the whole page.

---

## 2. The UI model this site is built on

ArcGIS Pro's interface has four layers. Getting these right is the point of the site —
Esri's own docs blur them and that is the confusion we exist to fix.

1. **The backstage** — clicking *Project* leaves the ribbon and opens a full-screen view:
   New, Open, Save, Save As, Portals, Licensing, Options, Package Manager, Add-In Manager.
   It is not a ribbon tab. It gets its own top-level nav section.

2. **Core ribbon tabs** — Map, Insert, Analysis, View, Edit, Imagery, Share, Help. Present
   whenever a map view is active. (Map is replaced by Layout when a layout view is active.)

3. **Contextual tabs** — appear only when something is selected. `Feature Layer` is a *tab
   set* containing the sub-tabs Appearance, Labeling, and Data. Labeling and Data are NOT
   siblings of Map or Insert. Same pattern for Raster Layer, Table, and Layout. Every
   contextual page must open with a **When it appears** line.

4. **Panes and views** — Contents, Catalog, Geoprocessing, Symbology, History, Modify
   Features. Note the Catalog *pane* and Catalog *view* are different things and the page
   for Catalog must explain the difference explicitly.

---

## 3. Page template

Every ribbon/contextual/pane page follows `docs/_template.md`. Do not improvise structure.

Coverage rule, two tiers:

- **Tier 1 — prose.** Per ribbon group, pick the 2–5 tools a wildfire researcher will
  actually touch. Each gets a short subsection: what it does, and a **Use this when** line
  giving a concrete situation. This is where the site earns its keep.
- **Tier 2 — table.** Every *remaining* button in that group gets a row in the group's
  reference table: `| Button | What it does | Esri |`. One line each, no more. This is how
  we achieve complete coverage without writing 600 essays.

Together, tiers 1 and 2 must account for every button in the group. If a group is small
(≤3 buttons), skip the table and give everything prose.

---

## 4. Screenshots

Path convention: `docs/assets/images/<section>/<page>-<thing>.png`

- Full ribbon strip: `docs/assets/images/ribbon/map-ribbon.png`
- A single group: `docs/assets/images/ribbon/map-navigate-group.png`
- Pane: `docs/assets/images/panes/contents-pane.png`

The repo owner takes the screenshots. **Write the image markdown anyway**, with the correct
path and real alt text, followed by `<!-- SCREENSHOT NEEDED -->`, and log it in
`CONTENT_STATUS.md`. Never generate or fabricate an image.

Every page needs at minimum a full-ribbon-strip image at the top.

---

## 5. Writing style

- Second person. "You'll use this when..." not "The user may utilize..."
- Short sentences. No marketing voice, no "powerful," "seamless," "robust."
- Lead with what the thing is *for*, not what it *is*.
- Use MkDocs Material admonitions, sparingly:
  - `!!! tip` — a genuine shortcut or time-saver
  - `!!! warning` — something that loses work or silently gives wrong results
  - `!!! note "Wildfire"` — how this tool connects to fire modeling
- No emoji. No horizontal rules mid-page.
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
pip install mkdocs-material
mkdocs serve      # local preview at localhost:8000
```

Deployment is automatic via `.github/workflows/deploy.yml` on push to `main`. In repo
Settings → Pages, set Source to **GitHub Actions**.

---

## 9. Order of work

Do not attempt the whole site in one pass. Suggested sequence:

1. Scaffold: `mkdocs.yml`, homepage, template, empty stub pages for every nav entry so the
   site builds and navigates from day one.
2. `Getting Started` and the `Project` backstage page.
3. Panes: Contents, Catalog. (Readers need these before any ribbon tab makes sense.)
4. Core ribbon tabs, in this order: Map, View, Insert, Analysis, Edit, Imagery, Share, Help.
5. Contextual tabs: Feature Layer set, then Raster Layer, Table, Layout.
6. Data source pages.
7. Wildfire workflows last — they cross-link into everything above.

**One page per commit.** Commit message format: `docs: add <page name>`. After each page,
update `CONTENT_STATUS.md`.
