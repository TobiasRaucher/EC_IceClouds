# EC_IceClouds

Bachelor's thesis research at KNMI (Tobias Raucher) studying the spatial distribution and physical characteristics of ice clouds using the EarthCARE satellite (ATLID lidar, CPR radar). Data period: January 2025 – February 2026.

## Research Question

> How does EarthCARE characterise the global distribution and physical properties of ice clouds in December 2025, and how consistent are these observations with the CALIPSO record?

### Sub-questions
**Distribution**
- What is the spatial distribution of ice clouds detected by EarthCARE between January 2025 and February 2026?

**Physical Characterisation** (December 2025)
- In what thermal environment do EarthCARE-detected ice clouds occur?
- What microphysical characteristics (IWC, effective radius) do EarthCARE-detected ice clouds exhibit?
- What optical characteristics (lidar ratio, linear depolarization ratio) do EarthCARE-detected ice clouds exhibit?

**Evaluation**
- How do EarthCARE's ice cloud spatial distribution and frequency compare to a similar El Niño/La Niña cycle year from CALIPSO in December?
- How do EarthCARE's ice cloud thermal, microphysical, and optical characteristics compare to published values from CALIPSO?

---

## Data Products

| Product | Content | Ice classification |
|---------|---------|----------|
| `ATL_TC__2A` | ATLID target classification + temperature | code 3 |
| `AC__TC__2B` | Synergetic (ATLID + CPR) classification | codes 3, 13, 14, 15, 19, 21 |
| `ATL_EBD_2A` | Extinction, backscatter, depolarization ratio | masked via ATL_TC |
| `ATL_ICE_2A` | Effective radius, ice water content | masked via ATL_TC |

Raw data: EarthCARE L2 HDF5 files (not tracked in this repo).

---

## Notebooks

### `notebooks/processing/`
Data ingestion and gridding notebooks. Run on the KNMI work PC against remote L2 data. Versioned by suffix:

| Folder | Contents |
|--------|----------|
| `v0/` | Initial exploration notebooks |
| `v1/` | Full-period batch processing (Jan 2025–Feb 2026) |
| `v1.5/` | ATL_TC__2A occurrence processing (updated QC/exclusion logic) |

Key notebooks:
- `v1/ATL_TC__2A_processing_1.ipynb` — ice occurrence + temperature (ATL_TC)
- `v1/AC_TC_2B_processing_1.1.ipynb` — synergetic ice occurrence (AC_TC)
- `v1/ATL_EBD_2A_processing_1.ipynb` — optical properties (extinction, backscatter, depol ratio, lidar ratio)
- `v1/ATL_ICE_2A_processing_1.ipynb` — microphysics (IWC, effective radius)
- `v1/AC_TC_2B_processing_monthly.ipynb` — month-by-month AC_TC occurrence (Jan 2025–Feb 2026)
- `v1.5/ATL_TC__2A_processing_monthly.ipynb` — month-by-month ATL_TC occurrence (Jan 2025–Feb 2026)

### `notebooks/plotting/`
- `All_Data_Plots.ipynb` — all analysis figures: lat×height cross-sections, latitudinal profiles, scatter plots, world maps

### `notebooks/heatmap/`
Earlier exploratory heatmap experiments.

---

## Grid Settings
- Horizontal resolution: 1.0° (standard), 0.5° (temperature map)
- Height: 0–20 km, 100 m spacing (201 levels)
- Min samples per cell: 10
- Quality filter: `quality_status` ≤ 1 (Good + Likely Good)

---

## Output File Naming
```
{PRODUCT}_{RESOLUTION}deg_{START}_{END}_{FORMAT}.nc
```
Formats: `_3d` (lat×lon×height), `_latheight` (lat×height zonal mean), `_latlon` (lat×lon height-collapsed).

Output files are not tracked in this repository.
