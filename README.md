# Innovation-Credit-System
# Replication Materials
## Quantitative Evaluation and Signaling: The Impact of the Innovation Credit System on Patent Grants by Manufacturing Firms

Author: Xinyue Rao
Contact: xinyue.rao@student.uq.edu.au

This repository contains the Stata do-file and the manually-compiled
policy treatment list used to produce all tables and figures in the
paper. It does NOT contain the underlying firm-level financial,
governance, and patent data, which are proprietary and commercially
licensed (see "Data" below).

## Contents

- `ICS_main_analysis.do` — master do-file. Runs the descriptive
  statistics (Table 1), baseline regression (Table 3), parallel trends
  test (Figure 1), all robustness checks (Table 4 + Figures 2),
  mechanism test (Table 5), and heterogeneity analysis (Tables 6-8).
- `policy_pilot_list.xlsx` — city-level Innovation Credit System pilot
  start dates, extracted directly from the panel data used to construct
  the treatment variable (Score). One row per treated city (CityCode)
  with its earliest pilot year.

## Data (not included — must be obtained independently)

This study uses three types of data that are not included in this
repository due to licensing restrictions:

1. **Firm-level financial, governance, and credit rating data** —
   licensed from CSMAR (https://www.gtarsc.com).
2. **Patent application and grant data** — licensed from incoPat
   (https://www.incopat.com).
3. **Green total factor productivity / green transformation index** —
   from the CNPD database.

Readers with their own valid licenses to these databases can obtain
the raw data directly. This do-file assumes a merged panel dataset
named `基础面板_v2.dta`, placed at:

    data/processed/基础面板_v2.dta

with (at minimum) the following variables: firm identifier (`stkcd`),
year, listing board, city code, patent grants/applications, the
treatment variables (`treat_points`, `treat_post_points`,
`policytime_points`), the control variables described in the paper
(Size, Lev, ROE, FirmAge, SOE, Board, Indep, Top1, TobinQ), and the
mechanism/heterogeneity variables described in Section 3.2 of the
manuscript (credit rating, supply chain risk, customer concentration,
Boone indicator, R&D intensity, high-tech status).

## Software requirements

- Stata 17 or later (for `xporegress`, used in the supplementary Lasso
  DML validation)
- User-written packages (install via `ssc install <name>`):
  `reghdfe`, `csdid`, `bacondecomp`, `winsor2`, `estout`, `ddml`,
  `pystacked`
- Python 3 with scikit-learn, configured for `pystacked`, is required
  ONLY for the random forest DML step (Table 4 Column 5). This step is
  wrapped in a `capture noisily` block and will be skipped gracefully
  (falling back to the validated hardcoded coefficient) if Python is
  not configured — see the comments in the do-file.

## How to run

1. Place the raw panel dataset (see "Data" above) at
   `data/processed/基础面板_v2.dta`, and the auxiliary raw files
   referenced in the do-file (firm life cycle, green TFP, green
   transformation index) under `data/raw/`.
2. Update the hardcoded file paths at the top of each section in
   `ICS_main_analysis.do` if your folder structure differs.
3. Run the do-file top to bottom. Each section can also be run
   independently, since every section reloads the base panel.
4. Output tables (.rtf) and figures (.png) are written to
   `output/tables/` and `output/figures/`.

## Citation

If you use this code or the policy pilot list, please cite:

Rao, X. (2026). Quantitative Evaluation and Signaling: The Impact of
the Innovation Credit System on Patent Grants by Manufacturing Firms.
