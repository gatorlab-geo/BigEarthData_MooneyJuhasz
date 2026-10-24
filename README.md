# Reproducibility Package — Scientometric Analysis of *Big Earth Data* (2017–2026)

> Companion reproducibility package for the scientometric analysis in:  
> **Mooney, P. & Juhász, L.** *"A mixed-methods retrospective and reflective analysis of the Big Earth Data journal"*, *Big Earth Data* (10-Year Retrospective Special Issue).

## Overview

This repository contains the self-contained Jupyter notebooks, anonymized aggregated datasets, figures, and summary tables for the scientometric evaluation of the *Big Earth Data* journal over its first decade (2017–August 30, 2026).

The analytical workflow adapts the scientometric framework of [Juhász (2024)](https://doi.org/10.1080/13658816.2024.2347306), expanded to include all **339 citable publications** (`Research Articles`, `Review Articles`, and `Data / Technical / Perspective Notes`) across publication volume, geographic footprint, institutional presence, and international co-authorship analyses.

## Repository Structure

```text
BigEarthData_MooneyJuhasz/
├── README.md                            ← Package documentation
├── 01_collect_and_process.ipynb         ← Self-contained Scopus API collection & aggregation pipeline
├── 02_manuscript_figures_tables.ipynb   ← Self-contained notebook reproducing all figures, tables & stats
├── environment.yml                      ← Conda environment specification (recommended for Cartopy/GEOS)
├── requirements.txt                     ← Pip package list
├── .env.example                         ← Template for user-supplied Scopus API credentials
├── CITATION.cff                         ← Citation metadata
├── .zenodo.json                         ← Zenodo archival metadata
├── LICENSE                              ← MIT (code) & CC BY 4.0 (aggregated data/figures)
├── data/
│   ├── corpus_index.csv                 ← Frozen 356-record index (scopus_id, doi, year, subtype, citable)
│   ├── metrics_summary.csv              ← Annual publication & international collaboration metrics (2017–2026)
│   ├── SUBTYPE_YEAR.csv                 ← Annual publication counts by Scopus document subtype
│   ├── COUNTRIES.csv                    ← Country-level publication counts (full-score counting, N = 339)
│   ├── COUNTRIES_YEAR.csv               ← Country × year publication counts (N = 339)
│   ├── AFFILIATIONS.csv                 ← Year × institution affiliation occurrences (N = 339)
│   ├── CITIES.csv                       ← Country × city affiliation occurrences (N = 339)
│   ├── CITIES_GEOCODED.csv              ← Pre-geocoded city coordinates (WGS84) for offline reproduction
│   ├── COLLAB.csv                       ← Bilateral country co-authorship pair frequencies (N = 339)
│   ├── ranking_scores.csv               ← Longitudinal journal impact indicators (2017–2025)
│   └── ne_10m_admin_0_countries.zip     ← Public-domain Natural Earth 1:10m country boundaries
├── figures/                             ← Generated 300 dpi figures (fig_01–fig_07, fig_A1–fig_A3)
└── tables/                              ← Generated summary tables (.md and .tex)
```

## Quick Start

### 1. Reproduce All Manuscript Figures, Tables, and Statistics (No API Key Required)

All aggregated CSVs, pre-geocoded city coordinates, and public-domain Natural Earth boundary data are included in `data/`, so `02_manuscript_figures_tables.ipynb` runs completely offline:

```bash
conda env create -f environment.yml
conda activate bed-scientometrics
jupyter lab 02_manuscript_figures_tables.ipynb
```

Running all cells regenerates every figure in `figures/` (`fig_01_volume.png`–`fig_07_journal_impact.png` and `fig_A1_impact_appendix.png`–`fig_A3_cities_map.png`), every summary table in `tables/`, and prints a verification summary matching all quantitative claims in the manuscript.

### 2. Re-collect Raw Metadata from the Scopus API (Optional)

In compliance with Elsevier's API Terms of Service, raw Scopus API JSON responses and personal API credentials are not redistributed in this archive. Instead, `data/corpus_index.csv` records the exact frozen corpus (`356` Scopus IDs and DOIs retrieved on August 30, 2026), and `01_collect_and_process.ipynb` provides the complete, self-contained collection, CAS institutional consolidation, geocoding, and CSV aggregation pipeline.

To re-run collection with your own institutional Scopus API credentials:

```bash
cp .env.example .env
# Edit .env and insert your SCOPUS_API_KEY_1
jupyter lab 01_collect_and_process.ipynb
```

## Corpus Summary (Retrieved August 30, 2026)

- **Query**: `SRCTITLE("Big Earth Data") AND (PUBYEAR > 2016)`
- **Total indexed records**: `356` (`339` citable + `17` non-citable)
- **Counting method**: Full-score attribution (each unique country affiliated with a citable item receives one count)

| Journal Article Type | Scopus Subtype(s) | Citable | Count |
|---|---|:---:|---:|
| Research Article | `Article` | Yes | 276 |
| Review Article | `Review` | Yes | 12 |
| Data / Technical / Perspective Note | `Data Paper` (2018–2024); `Note` (2025–2026) | Yes | 51 |
| **Subtotal (citable corpus)** | | | **339** |
| Editorial | `Editorial` | No | 15 |
| Erratum | `Erratum` | No | 2 |
| **Total indexed** | | | **356** |

> **Note on Scopus Subtypes**: Beginning in 2025, Scopus reclassified *Big Earth Data* Data Notes from `Data Paper` (`38` items, 2018–2024) to `Note` (`13` items, 2025–2026). Both subtypes represent the journal's Notes formats and are combined (`51` items) throughout the analysis.

## Methodological Reference

Juhász, L. (2024). Assessing publication trends in selected GIScience journals. *International Journal of Geographical Information Science*, 38(8), 1443–1467. https://doi.org/10.1080/13658816.2024.2347306

## License

Code and notebooks are released under the **MIT License**; aggregated data tables and figures are released under **CC BY 4.0** (see [`LICENSE`](LICENSE)). Natural Earth vector map data (`data/ne_10m_admin_0_countries.zip`) are in the public domain (**CC0**).
