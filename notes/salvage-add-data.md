# Add data to a map

You will finish with your dataset drawn in the map and listed in the Contents pane.

**Use this when:** You have a shapefile, a geodatabase feature class, a raster, a
spreadsheet, or a web service, and you want it in your project.

**Related:** [Catalog pane](../panes/catalog.md) · [Contents pane](../panes/contents.md) ·
[Symbolize a layer](symbolize.md)

## Steps

1. On the **Map** tab, click **Add Data**.
   <!-- VERIFY: is Add Data in the Layer group on the Map tab in 3.7.1? -->
2. Browse to your dataset, select it, and click **OK**.
3. It appears in the **Contents** pane and draws in the map.

!!! tip "The faster route"
    Drag the dataset straight from the [Catalog pane](../panes/catalog.md) onto the map. Same
    result, no dialog. This is what you will actually do once you know where your data is.

Use the small arrow under **Add Data** when your data is not a file you can browse to — a
server path, a URL, or coordinates held in a spreadsheet.
<!-- VERIFY: exact entries in the Add Data dropdown in 3.7.1. -->

## Gotchas

- **Adding a layer does not copy the data.** The layer only points at the file on disk. Move,
  rename, or delete the source and the layer breaks, showing a red exclamation mark in
  Contents. Put your data somewhere permanent *before* you add it.
- **A spreadsheet will not draw anything.** A CSV or Excel file comes in as a table, not a
  layer — it has no geometry yet. To get points from it, run **XY Table To Point** on the
  columns holding your coordinates.
  <!-- VERIFY: is the tool still called XY Table To Point in 3.7.1? -->

!!! warning "The first layer sets the map's coordinate system"
    Everything you add afterwards is reprojected on the fly, *for display only*. Layers can
    look perfectly aligned while still sitting in different coordinate systems underneath.
    That is fine for looking at. It is not fine for analysis, and raster maths will either
    fail or give you quietly wrong results.

## For wildfire work

!!! note "Wildfire"
    Add your DEM first. It sets the map's coordinate system, and terrain is the layer your
    fuel and weather grids all have to align to — so you want the map in the DEM's projection
    rather than the other way round. See
    [Building a terrain stack from a DEM](../wildfire/workflows/terrain-stack.md).

## Where to go next

- [Symbolize a layer](symbolize.md) — your layer arrived in a random colour. This is how you
  fix that.
