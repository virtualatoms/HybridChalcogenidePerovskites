# Hybrid Chalcogenide Perovskites

Data, analysis scripts, and crystal structures accompanying the publication:

> **On the possibility of hybrid chalcogenide perovskite photovoltaics**
> *Faraday Discussions* (2025)

## Overview

This repository contains the scripts used to analyse and plot results for four hydrazinium (HZ) chalcogenide perovskites: HZZrS₃, HZZrSe₃, HZHfS₃, and HZHfSe₃. The raw calculation data (DFT relaxations, machine-learning force field molecular dynamics, and optical spectra) is archived on NOMAD (link to be added).

## Repository structure

```
notebooks/        Jupyter notebooks for analysis and figure generation
data/             Extracted data files used by the plotting notebooks
plots/            Output figures (PDF)
relaxed-cifs/     DFT-relaxed crystal structures (CIF format)
thermal-cifs/     Structures with anisotropic displacement parameters from MD (CIF format)
```

## Scripts

| Notebook | Description |
|---|---|
| `01-extract-md.ipynb` | Extracts octahedral tilt angles and unit cell volumes from MD trajectories using [PDynA](https://github.com/WMD-group/PDynA); outputs `data/tilt_data.json` and `data/volume_data.json` |
| `02-thermal-elipsoids.ipynb` | Computes anisotropic displacement parameters from MD trajectories and writes averaged CIF structures to `thermal-cifs/` |
| `03-plot-md.ipynb` | Plots tilt angle distributions and volume statistics; produces `plots/md_summary.pdf` |
| `04-plot-optics.ipynb` | Plots optical absorption spectra, band gaps, and spectroscopic limited maximum efficiency (SLME); produces `plots/optics_summary.pdf` |
| `05-tolerance-factor.ipynb` | Calculates Goldschmidt tolerance factors and octahedral factors for candidate hybrid chalcogenide perovskites |
| `06-crystal-structure.ipynb` | Renders crystal structure visualisations using [hofmann](https://github.com/utf/hofmann) |

## Raw data

The raw calculation data (DFT relaxations, MLFF molecular dynamics, and optical spectra) is archived on NOMAD (DOI: to be added). The scripts expect the calculation directories to be present in the root of this repository, alongside `notebooks/` and `data/`.

To download and extract the dataset via the command line, run:

```bash
curl -X POST "https://nomad-lab.eu/prod/v1/api/v1/entries/raw/query" \
  -H "Content-Type: application/json" \
  -d '{"query": {"datasets.doi": "<DOI>"}}' \
  -o nomad-data.zip
unzip nomad-data.zip -d .
```

Replace `<DOI>` with the dataset DOI above.

## Crystal structures

DFT-relaxed structures are provided in `relaxed-cifs/`. Structures with thermal ellipsoids derived from 300 K MLFF-MD trajectories are in `thermal-cifs/`.

## Requirements

- [pymatgen](https://pymatgen.org)
- [PDynA](https://github.com/WMD-group/PDynA)
- [hofmann](https://github.com/utf/hofmann) (for crystal structure visualisation)
- Standard scientific Python stack (numpy, matplotlib, pandas)
