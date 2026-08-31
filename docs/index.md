# ArcGIS Pro for wildfire simulation

How to use ArcGIS Pro to prepare inputs for wildfire spread models, run them, and map the
results — for both the United States and Canada.

The ArcGIS Pro instructions live inside the workflows rather than in a separate manual. You
learn to add data, clip rasters, and script with Python while doing the thing you actually
came here to do.

!!! note "Version"
    Every page assumes **ArcGIS Pro 3.7.1**.

## Start here

- [Wildfire overview](wildfire/index.md) — what this covers and what it does not.
- [Fuel models — US vs Canada](wildfire/concepts/fuel-models.md) — read before you choose an
  ecosystem to work in. It decides everything downstream.
- [Simulators — how to choose](wildfire/simulators/index.md)

!!! warning "US and Canadian fire models are not interchangeable"
    Scott & Burgan / Anderson fuel models and the Canadian FBP System fuel types are
    different classifications feeding different equations. Mixing them produces output that
    looks plausible and is wrong. Every workflow page here separates the two.

## The workflow, start to finish

1. [Preparing a study area](wildfire/workflows/study-area.md)
2. [Building a terrain stack from a DEM](wildfire/workflows/terrain-stack.md)
3. [Preparing fuel layers](wildfire/workflows/fuel-layers.md)
4. [Exporting to a simulator](wildfire/workflows/export-to-simulator.md)
5. [Bringing results back into ArcGIS Pro](wildfire/workflows/import-results.md)
6. [Mapping burn severity](wildfire/workflows/burn-severity.md)

## Where the data comes from

- [Data sources](data-sources/index.md) — what each dataset contains, its resolution, and how
  to load it.
