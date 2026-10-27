# MADS Philly Bikeshare

Milestone II project: forecast hourly Indego departures at each station, and group stations by how they are used.

Trip files come from [Indego](https://www.rideindego.com/about/data/). Weather, station status, sports, and rebalancing context come from [DisPatch70](https://huggingface.co/datasets/hulnegy/DisPatch70).

## Notebooks

Run these from this folder, in order:

1. `01_data_joining.ipynb` builds `data/processed/` from the Indego and DisPatch70 downloads.
2. `02_shared_analysis_prep.ipynb` prepares the analysis files and writes `data/shared/shared_manifest.json`.
3. `03_eda.ipynb` checks the joined station-hour panel and writes `figures/eda/`.
4. `04_unsupervised_model_training.ipynb` clusters trips and stations.
5. `05_supervised_model_training.ipynb` compares forecast models and writes `results/supervised/`.

Notebooks 04 and 05 also read `data/shared/shared_manifest.json`.

Training is January 2024 through December 2025. Validation is January–March 2026. The held-out test is April–June 2026. Dates live in `project_settings.json`.

## Setup

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

## What is not in git

`data/` is ignored. Notebook 01 downloads raw files into `data/raw/` and writes the modeling tables to `data/processed/`. The station-hour table is about 116MB, which is above GitHub's 100MB file limit. Notebook 01 reuses a raw file when it is already on disk.
