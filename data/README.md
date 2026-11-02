# Palmer Penguins Dataset Provenance

## Overview
This directory contains the original raw dataset `penguins.csv` (344 rows, 8 columns) collected by Dr. Kristen Gorman and the Palmer Station Long Term Ecological Research (LTER) program.

## Dataset Details
- **File**: `data/penguins.csv`
- **Rows**: 344 observations
- **Target Outcome**: `body_mass_g` (integer/float, body mass in grams)
- **Categorical Factors**:
  - `species`: Adelie, Chinstrap, Gentoo (3 levels)
  - `sex`: male, female (2 levels; capitalized as Male/Female during data preparation)
- **Additional Variables**: `island`, `bill_length_mm`, `bill_depth_mm`, `flipper_length_mm`, `year`
- **Data Filtering for Analysis**:
  - Raw records: 344
  - Missing `body_mass_g` or `sex`: 11 records removed (2 with missing mass and sex, 9 with missing sex only)
  - Complete cases analyzed: 333 records

## Scientific Source & Citations
1. **Primary Research Study**:
   Gorman KB, Williams TD, Fraser WR (2014) Ecological Sexual Dimorphism and Environmental Variability within a Community of Antarctic Penguins (Genus *Pygoscelis*). *PLoS ONE* 9(3): e90081. doi:[10.1371/journal.pone.0090081](https://doi.org/10.1371/journal.pone.0090081)

2. **R / Python Package**:
   Horst AM, Hill AP, Gorman KB (2020). palmerpenguins: Palmer Archipelago (Antarctica) penguin data. R package version 0.1.0. doi:[10.5281/zenodo.3960218](https://doi.org/10.5281/zenodo.3960218)

## License
Creative Commons Zero v1.0 Universal (CC0 1.0) Public Domain Dedication.
Data are published with no copyright restrictions.
