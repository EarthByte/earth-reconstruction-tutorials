# Earth Evolution — Spatio-Temporal Data and Model Analysis

[![Environment](https://img.shields.io/badge/environment-conda--forge-44A833?logo=anaconda&logoColor=white)](environment.yml)
[![Python](https://img.shields.io/badge/python-3.10%2B-3776AB?logo=python&logoColor=white)](environment.yml)
[![License: MIT](https://img.shields.io/badge/license%20(new%20material)-MIT-blue.svg)](LICENSE)
[![License: BSD-3-Clause](https://img.shields.io/badge/license%20(notebooks%20%26%20data)-BSD--3--Clause-blue.svg)](LICENSE-NOTEBOOKS)

A standalone Honours (4th-year) module. 3 credit points (approximately 25 contact hours), 10
sessions. You build and interrogate real plate-tectonic reconstructions with
[GPlately](https://github.com/GPlates/gplately) and [pyGMT](https://www.pygmt.org/), working
from a curated set of real, published research notebooks rather than toy examples.

> **Quick start:** `conda env create -f environment.yml && conda activate gplately-pygmt && jupyter lab`
> — see **Running the notebooks** below for details and a `mamba` alternative.

Every notebook follows the same pattern: a **`# === USER CONFIGURATION ===`** cell near the top
marks the handful of things you're meant to change (a model, a time, a region, a threshold),
followed by cells that run correctly without needing to be understood line-by-line on first
read. You are never handed a blank cell — every session asks you to run real, working code,
then deliberately change something specific in it and see what happens.

## Session map

| # | Folder | Theme |
|---|---|---|
| 1 | `session01_orientation` | Orientation — building a paleo-map: the GPlately + pyGMT plumbing, and why "the model" is really "a model" |
| 2 | `session02_plate_kinematics` | Plate kinematics through time — quantifying motion and its consequences at a plate boundary |
| 3 | `session03_minerals_tectonic_setting` | From minerals to tectonic setting — a mineral grain as a tectonic-setting proxy |
| 4 | `session04_mantle_dynamics` | Mantle dynamics and dynamic topography — surface expressions of deep-mantle processes |
| 5 | `session05_paleogeography_thermochronology` | Paleogeography, paleotopography, and thermochronology |
| 6 | `session06_sedimentary_basins` | Sedimentary basins as the subsidence archive |
| 7 | `session07_paleobiogeography` | Paleobiogeography — reconstructed plate positions as the coordinate system for evolutionary biogeography |
| 8 | `session08_paleoclimate` | Paleoclimate and Earth-system evolution |
| 9 | `session09_resource_exploration` | Reconstruction-driven resource exploration |
| 10 | `session10_capstone` | Capstone — independent adaptation of one extension notebook |

Each session folder holds that session's notebooks under descriptive filenames (no numbering
tied to any external source — see **Where these notebooks come from**, below). Session 10 has
no fixed notebook of its own: it's a independent mini-project adapting one extension notebook
from an earlier session (see `instructor_notes/`).

`instructor_notes/` has the full session-by-session timing plan, the exact data each notebook
needs and where to get it, and licensing/attribution. `data/` holds the real, small
(git-trackable) datasets used in-class; two sessions additionally require a companion data
archive too large for GitHub — see **Data**, below, before running those sessions.

## Where these notebooks come from

These notebooks are a curated, in-class subset of a much larger tutorial suite,
[EarthByte/GPlately-pyGMT-tutorials](https://github.com/EarthByte/GPlately-pyGMT-tutorials) (80
notebooks in total, BSD-3-Clause). This module's ten sessions select 33 of those as core,
in-class material; each session's instructor notes point to further "extension" notebooks from
the same suite for independent follow-up work, including the Session 10 capstone.

Filenames here are **descriptive only, with no number prefix** — the original suite numbers its
notebooks against a companion paper's figure/table numbering, which is expected to change after
that paper's review is complete. Dropping the numbering here means this module's structure
doesn't move when that happens. The session map above is the authoritative ordering.

## Running the notebooks

Unlike a pure-Python/scikit-learn module, this one depends on
[GPlates](https://www.gplates.org/)/pyGPlates-based geospatial libraries that are **not
pip/Colab-installable** — they're distributed via conda-forge. There is no "just click Open in
Colab" option here.

**Recommended: conda/mamba, once, at the start of term:**
```
conda env create -f environment.yml
conda activate gplately-pygmt
jupyter lab
```
(`mamba env create -f environment.yml` is a faster drop-in if you have mamba installed.)
Every notebook only needs what's in `environment.yml` — GPlately, pyGMT, JupyterLab, and the
standard scientific Python stack. No GPU is required.

## Data

Every notebook reads real, published data. Most of it is small enough to git-track directly —
it's already in `data/` in this repository. Read `instructor_notes/` for the exact per-notebook
manifest, but in short:

- **Most sessions need nothing beyond what's already here.** Plate-reconstruction models
  themselves (rotation files, plate polygons) are fetched and cached automatically on first use
  via `plate_model_manager` — expect a one-off download the first time each session runs, not a
  manual step.
- **Sessions 6 and 8 need a companion data archive** (rasters and grids too large for GitHub —
  sediment/crustal-thickness grids, a Zenodo-only rotation file, dynamic-topography model
  output) from the source suite's Zenodo record. **Download and extract this once, before
  teaching those two sessions** — see `instructor_notes/` for the exact archive, the expected
  `zenodo_data/` folder layout, and which notebooks in Sessions 4 and 5 also need a subset of
  it. Every notebook that needs this data checks for it on its first cell and fails immediately,
  with a clear message, if it isn't there — so a missing download shows up right away, not
  partway through class.

## Attribution

These notebooks and their data are copied and adapted, with permission, from
[EarthByte/GPlately-pyGMT-tutorials](https://github.com/EarthByte/GPlately-pyGMT-tutorials) —
R.D. Müller and colleagues' own published, BSD-3-Clause-licensed tutorial suite — and remain
under that license; the original notice is reproduced in `LICENSE-NOTEBOOKS`. Newly written
material in this repository (this README, the instructor notes, and any session-specific
framing text) is released under the [MIT License](LICENSE). Full attribution and per-dataset
citations are in `instructor_notes/`.

## License

New material in this repository is released under the [MIT License](LICENSE). Notebooks and
data copied from the source tutorial suite remain under the original
[BSD-3-Clause license](LICENSE-NOTEBOOKS).
