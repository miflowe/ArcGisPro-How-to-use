# TEMPLATE — do not publish this page

Copy this for every workflow page. Keep it short. If a section has nothing worth saying,
delete the section — do not pad it.

**Target length: one screen of reading, plus the steps.** If a page is getting long, it is
probably two workflows. Split it.

## What to leave out

This is the important half of the template.

- **Any button whose name explains it.** No "Save Project — saves the project."
- **Anything the reader would do without being told.** They can find a Cancel button.
- **Esri's full option list.** Cover the path that works; link out for the rest.
- **Fire science the reader does not need to act on.** Cite it, do not teach it.

The page earns its keep on three things: **when you'd want this**, **what silently goes
wrong**, and **what the model cannot tell you**. Everything else is filler.

## The US/Canada rule

Never blend the two ecosystems. Where steps differ by country, use content tabs:

```markdown
=== "United States"
    Steps using LANDFIRE fuel layers...

=== "Canada"
    Steps using FBP fuel type grids...
```

If a page is entirely country-agnostic, say so in one line rather than adding empty tabs.

---

# <Workflow name, as a verb phrase: "Building a terrain stack from a DEM">

<One sentence: what you will have when you are done.>

**Use this when:** <the concrete situation that sends someone to this page.>

**You will need:** <inputs and any extension, e.g. a DEM covering the study area, Spatial
Analyst.>

**Related:** [Preparing a study area](study-area.md) ·
[Terrain inputs](../concepts/terrain.md)

## Steps

<!-- SCREENSHOT NEEDED: docs/assets/images/wildfire/<page>-<thing>.png
     Delete these two comment lines once the file exists, to publish the image.
![Real alt text describing what the screenshot shows](../../assets/images/wildfire/<page>-<thing>.png)
-->

1. <Numbered steps. This is where the ArcGIS Pro instruction lives — name the tab and group
   only where the reader needs it to find the button, then stop.>
2. <Do not narrate the obvious middle. Get to the end.>

<Two or three sentences after the steps only if there is a real choice to explain — which of
two routes to take, or what a parameter actually controls.>

## Gotchas

- <Something that loses work or silently gives wrong results. Real ones only. Mismatched cell
  sizes, unprojected rasters, and fuel codes that do not match the simulator's expectations
  are the recurring ones in this domain.>

## Limitations

<Required on every workflow page. What the model does not account for. These are research
tools and the site must not read as though the outputs are ground truth. Be specific — "does
not model spotting" beats "has limitations".>

## Where to go next

- [<The workflow that follows this one>](path.md)
