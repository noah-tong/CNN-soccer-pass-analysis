# Data Instructions

## Included in this repository

- `../image/` (sample only): 3 PNG images for lightweight demonstration.
- `../label_annotation_sample (1).csv`: manually labeled sample file used in the notebooks.

## Files you should place locally (not tracked by git)

1. `merged_matches_plus.xlsx`
   - Put this file in the repository root.
   - The data preparation notebook expects this path by default.
   - If you still have raw match folders (`match1` to `match11` with `coordinates.csv` and `passes.csv`), you can regenerate this file in `01_data_preparation.ipynb`.

2. `graduation_thesis_test.xlsx` (if required by later analysis cells)
   - Also place it in the repository root.

## Optional raw data layout

If you want stronger reproducibility, place raw match folders under `data/raw/matches/` and update the corresponding notebook paths.
