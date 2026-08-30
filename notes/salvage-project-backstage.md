# The Project backstage

Everything that acts on the *project as a whole* rather than on your map: creating and
opening projects, saving, portal connections, licensing, application settings, and the
Python environment.

**How to get there:** Click **Project** at the far left of the ribbon. The entire window is
replaced by a full-screen view. Click the back arrow at the top-left to return to your map.
<!-- VERIFY: does Esc also close the backstage in 3.7.1? -->

**Related:** [Anatomy of the interface](../getting-started/interface-anatomy.md) ·
[Catalog pane and Catalog view](panes/catalog.md) · [Share tab](ribbon/share.md)

## At a glance

<!-- SCREENSHOT NEEDED: docs/assets/images/interface/project-backstage.png
     Delete these two comment lines once the file exists, to publish the image.
![The Project backstage in ArcGIS Pro 3.7.1, showing the ten-item sidebar on the left and the New page on the right](../assets/images/interface/project-backstage.png)
-->

The backstage is a vertical list of ten items down the left side. Clicking one fills the
large panel on the right. There are no ribbon groups, no galleries, and no contextual tabs
here — it is a different kind of screen, not a tab.

That distinction is the thing worth internalising. If you are hunting for **Options** or
**Licensing** on the Map or View tabs, you will never find them. They are not on the ribbon
at all. Anything that concerns the project rather than the map lives back here.

In sidebar order, the ten items are: New, Open, Info, Save Project, Save Project As,
Portals, Licensing, Options, Package Manager, Add-In Manager.

## Starting, opening and saving projects

The first five items in the sidebar. These are the ones you touch daily.

### New

Creates a project. You pick a template first — a map, a catalog, a scene, or no template at
all — and then a name and a folder.

The folder choice matters more than it looks. Creating a project does not just write one
file. It creates a **home folder** containing the `.aprx` project file, a **file geodatabase**
named after the project, and a **toolbox**.
<!-- VERIFY: in 3.7.1, is the default toolbox created as .atbx? And is a toolbox still created automatically for every new project? -->
That geodatabase becomes the project's default output location, so every tool you run writes
there unless you say otherwise.

**Use this when:** Starting a new fire modelling study area. Put the project somewhere with
room to grow and a path you can live with — LANDFIRE and DEM tiles are large, and the
default geodatabase is where your intermediate rasters will pile up.

### Open

Opens an existing project, from a recent list, by browsing the file system, or from a portal.

**Use this when:** Returning to work. Worth knowing that the recent list is per-installation,
not per-project, so it will not follow you to another machine.
<!-- VERIFY: is the recent projects list per-user or per-installation in 3.7.1? -->

### Everything else in this group

| Button | What it does | Esri |
|---|---|---|
| Info | <!-- VERIFY: what does the Info page show? Project path, default geodatabase, toolbox, ArcGIS Pro version number, metadata? Need this filled in before publishing. --> | — <!-- LINK NEEDED: Project Info page --> |
| Save Project | Writes changes to the current `.aprx` | — |
| Save Project As | Writes the project to a new `.aprx`, then continues working in the new one | — <!-- LINK NEEDED: Save a project --> |

## Portals, licensing and settings

Three items that configure ArcGIS Pro itself rather than your project. Small group, so all
three get prose.

### Portals

Manages the ArcGIS Online or ArcGIS Enterprise connections you can sign in to, and sets
which one is active.

**Use this when:** Your institution hosts data on its own Enterprise portal and you need to
add it, or you need to switch between a university portal and ArcGIS Online.

### Licensing

Shows your license level and, below it, the list of extensions with whether each one is
enabled.

**Use this when:** A geoprocessing tool you expected is missing or greyed out. Check here
first — a missing extension looks exactly like a missing tool, and this page tells you which
it is.

### Options

Application and project settings. This is where defaults live: the project's default
geodatabase and toolbox, geoprocessing behaviour, display and navigation preferences.

**Use this when:** You want tool outputs going somewhere other than the default geodatabase
for the rest of the session. Changing it here is far less error-prone than re-typing an
output path on every tool.

!!! warning "Some Options are per-project, some are application-wide"
    Changing a project setting affects only the open project. Changing an application
    setting follows you into every project you open afterwards. The dialog does distinguish
    them, but it is easy to change one thinking you changed the other.
    <!-- VERIFY: how does the Options dialog in 3.7.1 label the project vs application split? Section names needed. -->

## Extending ArcGIS Pro

Two items, both prose.

### Package Manager

Manages the Python environment behind ArcGIS Pro — which conda packages are installed, and
which environment is active.

**Use this when:** You need a package `arcpy` does not ship with, for scripted fuel or
terrain processing. Also where you go when a Python script that works in your own
environment fails inside Pro.

!!! warning "Clone before you install"
    The default Python environment that ships with ArcGIS Pro is read-only. To add packages
    you clone it first, then install into the clone and activate it. Trying to install
    directly into the default environment fails.
    <!-- VERIFY: is the default environment still named arcgispro-py3 in 3.7.1, and is cloning still required before installing? -->

### Add-In Manager

Lists the add-ins installed for your user account and lets you see where each was loaded
from.

**Use this when:** Auditing what a shared machine has installed, or confirming an add-in a
colleague sent you actually loaded.

## For wildfire work

!!! note "Wildfire"
    Two items here gate the fire modelling half of this site.

    **Licensing** is where you confirm the **Spatial Analyst** extension is enabled. Nearly
    every terrain and fuel raster step depends on it — slope and aspect derivation,
    reclassification, raster algebra. Check it before starting
    [Building a terrain stack from a DEM](../wildfire/workflows/terrain-stack.md), not
    halfway through.

    **Package Manager** matters once you outgrow clicking. Batch-processing fuel grids
    across a large study area, or preparing inputs for
    [Prometheus or BurnP3](../wildfire/simulators/prometheus-burnp3.md), is far easier in a
    script than in the Geoprocessing pane.

## Gotchas

- **A new project silently decides where your data goes.** The default geodatabase is
  created inside the project home folder and every tool writes there by default. Months
  later that folder holds gigabytes of intermediate rasters you have no memory of creating.
  Set the output location deliberately, in Options, early.
- **Save Project As copies the project, not the data.** The new `.aprx` still points at the
  original project's geodatabase and any layers referencing files on disk. It is not a way to
  duplicate a study area — for that you want packaging on the
  [Share tab](ribbon/share.md).
  <!-- VERIFY: confirm Save Project As does not copy the default geodatabase in 3.7.1. -->
- **Licensing changes may need a restart.** Enabling an extension does not always surface its
  tools in the current session.
  <!-- VERIFY: does enabling an extension in 3.7.1 require restarting ArcGIS Pro? -->

## Where to go next

- [Anatomy of the interface](../getting-started/interface-anatomy.md) — the other three
  layers of the UI, now that you have seen the one that is not a ribbon tab.
- [Contents pane](panes/contents.md) — the pane you will spend the most time in.
- [Catalog pane and Catalog view](panes/catalog.md) — where that default geodatabase actually
  shows up, and how to point the project somewhere else.
