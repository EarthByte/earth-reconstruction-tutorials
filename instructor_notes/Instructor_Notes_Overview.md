# Instructor Notes — Earth Evolution: Spatio-Temporal Data and Model Analysis

Working notes for running the module: what each session needs, exact data dependencies,
timing, licensing, and setup. This is the practical companion to the top-level `README.md`.

## Setup, once, before term starts

```
conda env create -f environment.yml
conda activate gplately-pygmt
jupyter lab
```

Every notebook depends only on what's in `environment.yml`. These are real GPlates/pyGMT
research workflows, not lightweight examples — expect the environment build itself to take a
few minutes, and expect `plate_model_manager` to download and cache each plate-reconstruction
model the first time a notebook asks for it (a one-off cost per model, cached under
`data/pmm_cache/` afterward, not re-downloaded on subsequent runs).

## The companion data archive (Sessions 6 and 8 — read this before teaching either)

Some of the source tutorial suite's notebooks depend on raster/grid data too large for GitHub,
distributed instead via a companion Zenodo archive (DOI: 10.5281/zenodo.21836196). Every
notebook that needs it checks for it in its first code cell and raises a clear
`FileNotFoundError` naming exactly what's missing if it isn't there — so a missing download
surfaces immediately, not partway through a class.

**Download and extract the archive once, before term, as a folder named `zenodo_data/` at the
top level of this repository** (a sibling of `data/` and the `session*/` folders — never merged
into `data/`). The archive is organized into per-dataset subfolders; you only need the ones
below:

| Needed by | `zenodo_data/` subfolder |
|---|---|
| `session03_minerals_tectonic_setting/Detrital_Zircons_Reconstructed.ipynb`, `Detrital_Zircon_Distance_to_Subduction.ipynb` | `zircon_geochronology_Wu2023/` |
| `session04_mantle_dynamics/DT_History_Clustering.ipynb`, `DT_vs_Sediment_Flux.ipynb` | `dynamic_topography_Dhungana/` (~570 MB) |
| `session04_mantle_dynamics/Dynamic_Topo_Mantle_to_Plate_Frame_Conversion.ipynb` | `dynamic_topography_Young2022/` |
| `session05_paleogeography_thermochronology/Thermochron_Central_Asia.ipynb` (one panel only — see below) | `paleoDEM_ScoteseWright2018/` |
| `session06_sedimentary_basins/Sedimentary_Basins.ipynb`, `Crustal_Stretching_Beta_Factor.ipynb`, `Individual_Rift_Basin_Analysis.ipynb` | `sediment_thickness_BirdMooney/`, `crustal_thickness_Afonso/` |
| `session08_paleoclimate/pySCION_Phanerozoic_Biogeochemistry.ipynb` | `pySCION_biogeochemistry_model/`, `paleoDEM_ScoteseWright2018/` |
| `session08_paleoclimate/Cenozoic_Ocean_Gateways.ipynb` | `gateway_reconstruction_Straume2020/` |

**Sessions 6 and 8 are the two sessions where this matters for every core notebook** — every
notebook in `session06_sedimentary_basins/` needs at least one of these subfolders, and two of
`session08_paleoclimate/`'s three notebooks do (`Boucot_Climate_Sensitive_Lithologies.ipynb`
does not — it only needs the small, already-bundled `data/Zahirovic2022_with_gpmdb_frame.rot`).
Plan a one-time download well before those two classes; a laptop with no prior download will
fail on the first cell, by design, rather than midway through the session.

A per-dataset environment-variable override (e.g. `ZENODO_SANTOSH_DIR`) is available in each
notebook's configuration cell for anyone keeping the archive at a non-default location.

## Session-by-session data and timing

| # | Session | Notebooks (in `session0N_.../`) | Data |
|---|---|---|---|
| 1 | Orientation | `Hello_Deep_Time`, `GPlates_Web_Service_Python`, `Projection_Cookbook`, `Plate_Model_Comparison`, `Rotation_Model_Comparison` | Self-contained — plate models auto-fetched, no local files needed |
| 2 | Plate kinematics | `Paleobathymetry_Profile`, `Rift_Obliquity`, `Kinematic_Feature_Extraction`, `Subducted_Slab_Flux_Inventory` | Self-contained except `Rift_Obliquity` (`data/rift_obliquity/`, bundled) |
| 3 | Minerals → tectonic setting | `Detrital_Zircons_Reconstructed`, `Detrital_Zircon_Distance_to_Subduction`, `Hf_Nd_Terrane_Mapping` | First two need the Zenodo archive; `Hf_Nd_Terrane_Mapping` is self-contained (`data/hf_nd_isotopes/`, bundled) |
| 4 | Mantle dynamics | `REVEAL_Tomography_Slices`, `DT_History_Clustering`, `DT_vs_Sediment_Flux`, `Dynamic_Topo_Mantle_to_Plate_Frame_Conversion` | `REVEAL_Tomography_Slices` is self-contained (`data/reveal_tomography/`, bundled); the other three need the Zenodo archive |
| 5 | Paleogeography, paleotopography, thermochronology | `Geochem_Corrected_Paleo_Elevation`, `Macrostrat_Lithology_Styled_Paleomaps`, `Thermochron_Central_Asia`, `Ophiolite_Emplacement_PaleoMap` | Self-contained (`data/paleotopo_scotese/`, `data/thermochronology_central_asia/`, `data/ophiolites/`, all bundled; Macrostrat is a live API call), **except** one panel of `Thermochron_Central_Asia` that needs the Zenodo `paleoDEM_ScoteseWright2018/` subfolder |
| 6 | Sedimentary basins | `Sedimentary_Basins`, `Crustal_Stretching_Beta_Factor`, `Individual_Rift_Basin_Analysis` | All three need the Zenodo archive (see table above); the basin-polygon shapefile itself is bundled (`data/evenick_2021_basins/`) |
| 7 | Paleobiogeography | `Reef_Builders_Paleolatitude`, `Kimmeridgian_Dinosaurs`, `Cenozoic_Foraminifera_Paleo_Latitude`, `Bioregionalization_H3_Hierarchical` | Self-contained (`data/paleoclimate/`, `data/foraminifera_cenozoic/`, bundled) |
| 8 | Paleoclimate | `Boucot_Climate_Sensitive_Lithologies`, `pySCION_Phanerozoic_Biogeochemistry`, `Cenozoic_Ocean_Gateways` | `Boucot_Climate_Sensitive_Lithologies` is self-contained (`data/Zahirovic2022_with_gpmdb_frame.rot`, bundled); the other two need the Zenodo archive |
| 9 | Resource exploration | `SW_Pacific_Porphyry_Prospectivity`, `Seafloor_Anomalies_Porphyry_Cu`, `Craton_Boundary_Framework` | Self-contained (`data/mineral_exploration/`, `data/seafloor_anomalies_mather/`, `data/craton_boundary_framework/`, all bundled) |
| 10 | Capstone | (student's own choice of an extension notebook) | Depends on which extension notebook is chosen — check its data needs before approving a student's pick |

Suggested assessment: a lightweight participation/lab-notebook mark across Sessions 1–9 (e.g.
40%), plus the Session 10 mini-project and a short presentation (e.g. 60%). Check your specific
unit-of-study outline for the exact weightings used this year.

## Extension notebooks (independent follow-up work, including the capstone)

Each session's core notebooks above are drawn from a much larger tutorial suite (see
`README.md` > *Where these notebooks come from*). Students working ahead, or choosing a Session
10 capstone notebook, can draw on any further notebook from the same suite
([EarthByte/GPlately-pyGMT-tutorials](https://github.com/EarthByte/GPlately-pyGMT-tutorials)) —
check that notebook's own data requirements (the suite's `Notebooks/README.md` documents this
per-notebook) before a student commits to one, since several of the suite's extension notebooks
depend on parts of the Zenodo archive not listed in the table above.

## Licensing and attribution

- **Notebooks and data (`session*/`, `data/`)** — copied and adapted, with permission, from
  [EarthByte/GPlately-pyGMT-tutorials](https://github.com/EarthByte/GPlately-pyGMT-tutorials),
  R.D. Müller, S.E. Williams, A. Merdith, J. Leonard, S.C. Boone, J. Zhou, B.R. Mather and
  colleagues' own published tutorial suite. BSD-3-Clause; the original notice is reproduced in
  full in `LICENSE-NOTEBOOKS`. Each `data/` subfolder carries its own `README.md`, copied
  unchanged from the source suite, with that dataset's specific citation and license (several
  datasets — e.g. the Evenick (2021) basin polygons — carry their own more restrictive terms;
  read the relevant `README.md` before redistributing any individual dataset separately from
  this repository).
- **This file, the top-level `README.md`, and any other newly written framing text** — original
  material for this module, MIT-licensed (`LICENSE`).
- **Macrostrat** (`session05_paleogeography_thermochronology/Macrostrat_Lithology_Styled_Paleomaps.ipynb`)
  queries the public Macrostrat API live at run time — no local data, no separate license
  concern, but does need network access in class.

## A note on the source material

Unlike a from-scratch teaching module, every notebook here is a real, published research
workflow, complete with the occasional rough edge (a stray empty cell, a leftover unused
variable) that a from-scratch notebook wouldn't have. That's intentional — the whole point of
building this module from the source suite rather than rewriting it is that students are
looking at the same code a working researcher actually runs, not a sanitized teaching version
of it.
