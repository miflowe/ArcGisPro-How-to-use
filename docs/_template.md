# TEMPLATE — do not publish this page

Copy this for every Python script page. Keep it short. If a section has nothing worth saying,
delete the section — do not pad it.

**Target length: one screen, plus the parameter table.** The reader came to run the script,
not to read about it.

## Where the script file lives

Put the `.py` file at `docs/wildfire/scripts/files/<name>.py` and link to it relatively:

```markdown
[Download `clip_fuels.py`](files/clip_fuels.py)
```

MkDocs copies non-markdown files in `docs/` into the built site, so the link works as a
download. Because the file is inside `docs/`, `mkdocs build --strict` also verifies the link
resolves — a script page whose download link is broken will fail CI rather than ship dead.

## What to leave out

- **A line-by-line walkthrough of the code.** The reader can open it. Say what it does and
  what it assumes.
- **Anything the reader would do unprompted.**
- **Fire science they do not need to act on.** Cite it, do not teach it.

The page earns its keep on: **what it does**, **what it needs**, **how to run it**, and **what
it does not account for**.

---

# <Script name, as a verb phrase: "Clip fuel rasters to a study area">

<One sentence: what the script produces.>

**Use this when:** <the concrete situation.>

[Download `<name>.py`](files/<name>.py)

## What it does

<Two or three sentences. The steps it performs, in order, in plain language.>

## What you need

- **Inputs:** <files and the form they must be in — projection, cell size, extent.>
- **ArcGIS Pro:** <version, and any extension such as Spatial Analyst.>
- **Python packages:** <anything beyond what arcpy ships with. Note that the default
  environment is read-only and must be cloned first.>
  <!-- VERIFY: confirm cloning is still required in 3.7.1 before adding packages. -->

## How to run it

1. <Where to run it from — the Python window in ArcGIS Pro, or a standalone prompt using the
   Pro environment. Say which, because they behave differently.>
2. <How parameters are supplied: edited at the top of the file, or passed as arguments.>

| Parameter | What it is | Example |
|---|---|---|
| <name> | <what it controls> | <a realistic value> |

## What you get

<The outputs, where they are written, and their format.>

## Gotchas

- <Something that silently gives wrong results. Mismatched cell sizes, unprojected inputs,
  and fuel codes the simulator does not recognise are the recurring ones here.>

## Limitations

<Required. What the script and the model behind it do not account for. These are research
tools; the site must not read as though the outputs are ground truth. Be specific — "does not
model spotting" beats "has limitations".>

=== "United States"
    <If the script is fuel-model specific, say which classification it assumes. Never let a
    reader point it at the wrong country's fuel data without warning.>

=== "Canada"
    <Same.>
