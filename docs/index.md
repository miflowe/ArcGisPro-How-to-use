# ArcGIS Pro for wildfire simulation

How to use ArcGIS Pro to prepare inputs for wildfire spread models, run them, and map the
results — for both the United States and Canada.

ArcGIS Pro instruction lives inside the pages that need it, not in a separate manual.

!!! note "Version"
    Every page assumes **ArcGIS Pro 3.7.1**.

## Start here

- [Wildfire](wildfire/index.md) — what this covers and what it does not.
- [Data sources](wildfire/maps/data-sources.md) — where to download the terrain, fuel and
  weather data, and what each dataset actually contains.
- [Working with maps](wildfire/maps/working-with-maps.md) — getting that data into ArcGIS Pro
  and what you can do with it once it is there.
- [Python scripts](wildfire/scripts/index.md) — download a script, see what it does and what
  it needs, and run it.

!!! warning "US and Canadian fire models are not interchangeable"
    Scott & Burgan / Anderson fuel models and the Canadian FBP System fuel types are
    different classifications feeding different equations. Mixing them produces output that
    looks plausible and is wrong. Any page covering both separates them explicitly.
