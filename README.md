# Placebo-arm responses in generalized myasthenia gravis immunotherapy trials

Code and data for the systematic review and meta-analysis of placebo-arm responses in randomized, double-blind, placebo-controlled trials of immunotherapy in generalized myasthenia gravis (gMG).

## Citation

If you use this code or data, please cite:

> Jones FJS, Iaali H, Prokop LJ, Skolka M, Naddaf E. Placebo-arm responses in generalized myasthenia gravis immunotherapy trials: a systematic review and meta-analysis. *[Journal]* (in submission).

Protocol registered with PROSPERO: CRD420251074417.

## Repository contents

| File | Description |
| --- | --- |
| `Meta_analysis_code.Rmd` | Full analysis pipeline: pooling, subgroup and sensitivity analyses, meta-regression, conditional predictions, MCID probabilities |
| `mg_placebo_clean_v5.csv` | Extracted trial-level dataset (28 trials, 57 variables) |
| `data_dictionary.md` | Column-by-column description of the dataset |
| `mg-placebo-meta-analysis.Rproj` | RStudio project file (sets the working directory automatically) |
| `LICENSE` | MIT License |

## Reproducing the analysis

### Requirements

- R (≥ 4.1)
- R packages: `metafor`, `dplyr`, `ggplot2`, `tibble`, `ggrepel`, `scales`

Install missing packages:

```r
install.packages(c("metafor", "dplyr", "ggplot2", "tibble", "ggrepel", "scales"))
```

### Steps

1. Clone or download this repository.
2. Open `mg-placebo-meta-analysis.Rproj` in RStudio. This sets the working directory to the repository root, so relative paths resolve correctly.
3. Open `Meta_analysis_code.Rmd`.
4. Run all chunks (`Run > Run All`) or knit the document.

The pipeline reads `mg_placebo_clean_v5.csv` and writes result CSVs and PDF figures to the repository root.

### Outputs produced

CSV files (results tables):

- `results_primary_summary.csv` — primary pooled estimates with 95% CI, PI, *I²*, *τ²*
- `results_subgroup_summary.csv` — pooled estimates across all 5 subgroups (primary, contemporary, stable steroids, phase 3, excluding crossover)
- `results_metaregression.csv` — univariable meta-regression results with β, SE, *p*, R²
- `results_conditional_pi.csv` — conditional predictions from baseline-severity meta-regression (all trials)
- `results_conditional_pi_contemporary.csv` — conditional predictions, contemporary subset
- `results_joint_conditional_pi.csv` — joint predictions conditioning on baseline severity and assessment timepoint
- `results_mcid.csv` — minimal clinically important difference probabilities (all trials and subgroups)
- `results_mcid_contemporary.csv` — MCID probabilities, contemporary subset
- `results_within_trial_sd.csv` — descriptive summary of within-trial SD of placebo-arm change

PDF figures: primary forest plots, subgroup forest plots (contemporary, stable, phase 3, excluding crossover), leave-one-out sensitivity plots, and meta-regression bubble plots for baseline severity and assessment timepoint.

## Methods summary

Random-effects models were fit using restricted maximum likelihood (REML) with the Knapp–Hartung adjustment. Ninety-five percent prediction intervals were computed for every model as

> μ̂ ± *t*₁₋ₐ/₂, *k*−2 × √(τ̂² + SE(μ̂)²)

Per-trial estimates of placebo-arm mean change were extracted as reported in each publication, with SE or 95% CI converted to SD where necessary using SD = SE × √n or SD = √n × (upper − lower) / (2 × 1.96). Sampling variance per trial is `vi = SD² / n` and standard error per trial is `sei = SD / √n`, both computed at extraction.

For full methods see the manuscript.

## License

Code is released under the MIT License (see `LICENSE`).

Data (`mg_placebo_clean_v5.csv`) is released under [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/) and consists of aggregate trial-level summaries extracted from previously published trial reports. No individual-level data are included. When using or redistributing the dataset, please cite the original trial publications (listed in the manuscript) as well as this repository.

## Contact

Felipe J. S. Jones — corresponding author (see manuscript).
