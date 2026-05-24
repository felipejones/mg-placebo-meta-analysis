# Data dictionary — `mg_placebo_clean_v5.csv`

Each row is one randomized, double-blind, placebo-controlled trial of immunotherapy in generalized myasthenia gravis (gMG) included in the meta-analysis. All values are aggregate trial-level summaries extracted from the published reports, and no individual-level data are present.

Missing values are recorded as empty cells. 

## Trial identification

| Column | Type | Description |
| --- | --- | --- |
| `study_id` | string | Primary author and year (e.g., `Nowak 2025`) |
| `year` | integer | Publication year |
| `phase` | string | Trial phase (`2` or `3`) |
| `drug` | string | Investigational drug name |
| `drug_class` | string | Drug class (FcRn, complement, B-cell, IST, IVIG, etc.) |
| `route` | string | Route of administration of the investigational drug (`IV`, `SC`, `PO`) |

## Sample sizes

| Column | Type | Description |
| --- | --- | --- |
| `n_total` | integer | Total randomized participants in the trial |
| `n_placebo` | integer | Participants in the placebo arm (the analysis unit) |
| `n_active` | integer | Participants in the active arm |

## Placebo-arm population characteristics

| Column | Type | Description |
| --- | --- | --- |
| `age_mean` | numeric | Mean age in years |
| `age_sd` | numeric | Standard deviation of age |
| `female_pct` | numeric | Percentage of female participants |
| `achr_pct` | numeric | Percentage AChR-antibody positive |
| `musk_pct` | numeric | Percentage MuSK-antibody positive |
| `sero_neg_pct` | numeric | Percentage seronegative |
| `duration_mean` | numeric | Mean disease duration in years (empty where not reported) |
| `baseline_mgadl` | numeric | Mean baseline MG-ADL score |
| `baseline_mgadl_sd` | numeric | SD of baseline MG-ADL |
| `baseline_qmg` | numeric | Mean baseline QMG score |
| `baseline_qmg_sd` | numeric | SD of baseline QMG |
| `baseline_mgc` | numeric | Mean baseline MGC score |
| `baseline_mgc_sd` | numeric | SD of baseline MGC |
| `mgfa_severe_pct` | numeric | Percentage of placebo-arm participants in MGFA class III–V |

## MGFA class counts (placebo arm)

| Column | Type | Description |
| --- | --- | --- |
| `mgfa_I_n` | integer | Number in MGFA class I |
| `mgfa_II_n` | integer | Number in MGFA class II |
| `mgfa_III_n` | integer | Number in MGFA class III |
| `mgfa_IV_n` | integer | Number in MGFA class IV |
| `mgfa_V_n` | integer | Number in MGFA class V |

## Concomitant therapy (placebo arm)

| Column | Type | Description |
| --- | --- | --- |
| `pct_steroid_placebo` | numeric | Percentage on background corticosteroids |
| `pct_ist_placebo` | numeric | Percentage on background non-steroidal immunosuppressive therapy |
| `pct_achei_placebo` | numeric | Percentage on acetylcholinesterase inhibitors |
| `pct_thymectomy_placebo` | numeric | Percentage with prior thymectomy |

## Outcome timepoint (placebo arm)

| Column | Type | Description |
| --- | --- | --- |
| `tp_mgadl_raw` | string | MG-ADL endpoint timepoint as reported (free text) |
| `tp_mgadl_wk` | numeric | MG-ADL endpoint timepoint in weeks |
| `tp_qmg_raw` | string | QMG endpoint timepoint as reported |
| `tp_qmg_wk` | numeric | QMG endpoint timepoint in weeks |
| `tp_mgc_raw` | string | MGC endpoint timepoint as reported |
| `tp_mgc_wk` | numeric | MGC endpoint timepoint in weeks |

## Placebo-arm mean change from baseline and derived precision

| Column | Type | Description |
| --- | --- | --- |
| `mgadl_change` | numeric | Mean change from baseline in MG-ADL (placebo arm). Negative values denote improvement |
| `mgadl_change_sd` | numeric | SD of MG-ADL change in the placebo arm |
| `mgadl_vi` | numeric | Sampling variance of the MG-ADL mean change: `mgadl_change_sd² / n_placebo` |
| `mgadl_sei` | numeric | Standard error of the MG-ADL mean change: `mgadl_change_sd / √n_placebo` |
| `qmg_change` | numeric | Mean change from baseline in QMG (placebo arm) |
| `qmg_change_sd` | numeric | SD of QMG change in the placebo arm |
| `qmg_vi` | numeric | Sampling variance of the QMG mean change |
| `qmg_sei` | numeric | Standard error of the QMG mean change |
| `mgc_change` | numeric | Mean change from baseline in MGC (placebo arm) |
| `mgc_change_sd` | numeric | SD of MGC change in the placebo arm |
| `mgc_vi` | numeric | Sampling variance of the MGC mean change |
| `mgc_sei` | numeric | Standard error of the MGC mean change |

Where the source publication reported a standard error (SE) or 95% confidence interval (CI) rather than a standard deviation, SD was computed using SD = SE × √n or SD = √n × (upper − lower) / (2 × 1.96).

## Trial design and protocol features

| Column | Type | Description |
| --- | --- | --- |
| `era_2017` | factor | `pre_2017` if published before 2017, `2017_plus` if published in 2017 or later |
| `crossover` | logical | `TRUE` for crossover designs (Howard 2013, Tindall 1993), `FALSE` otherwise |
| `steroid_change` | factor | `Stable` if background steroid dose was protocolized to remain stable in the placebo arm, `Taper` if the protocol allowed or mandated steroid tapering |
| `steroid_change_details` | string | Free-text notes describing the steroid management protocol (taper rules, timing, etc.) |
| `rescue_therapy` | string | Whether rescue therapy was allowed per protocol |
| `rescue_type` | string | Free-text description of rescue therapy types (e.g., `IVIG, PLEX`) |
| `rescue_rate` | numeric | Proportion of placebo-arm participants who received rescue therapy (0–1 scale) |

## Notes on the dataset

- All numeric extractions are at the placebo arm level and active-arm data are not included.
- Trial-level summaries reflect the placebo-arm population at randomization. 
- Free-text fields (`steroid_change_details`, `rescue_type`, `tp_*_raw`) contain extraction notes that record how ambiguous cases were classified; downstream analyses use the structured numeric and factor columns.
