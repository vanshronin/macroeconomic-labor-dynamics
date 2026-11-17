# Macroeconomic Labor Dynamics (1939–2026)

An end-to-end data analysis portfolio project examining how U.S. white-collar and blue-collar employment cohorts behave across 13 NBER-defined recessions using Federal Reserve Economic Data (FRED).

## Key Findings

* **Structural Crossover:** White-collar employment overtook blue-collar employment as the dominant share of the core labor cohort in the late 20th century, fundamentally shifting U.S. recession exposure.
* **Asymmetric Shock & Recovery:** Blue-collar jobs suffer steeper immediate contractions at recession onset and take **~2.5x longer to recover** (avg. **57.5 months** vs. **23.4 months** for white-collar), failing to regain prior peaks before the next downturn in 2 historical cycles.
* **Sub-Sector Bifurcation:** Contraction severity is cycle-specific—construction and manufacturing bore the brunt of 2008, whereas information and professional services experienced sharper shocks in 2001 and 2020.
* **Predictive Limits:** Linear regression trained on pre-2020 cycles achieves moderate in-sample fit ($R^2 = 0.42$ blue-collar, $0.34$ white-collar) but fails out-of-sample ($R^2 < 0$), demonstrating that historical linear extrapolation breaks down during unprecedented black-swan shocks.

## Core Research Questions

1. **Structural Crossover:** When did white-collar employment overtake blue-collar employment in the U.S.?
2. **Shock Sensitivity:** At recession onset, which cohort contracts first and fastest?
3. **Era-by-Era Vulnerability:** How has peak-to-trough drawdown severity shifted across historical eras?
4. **Sub-Sector Bifurcation:** Why did 2008 disproportionately impact construction while 2001 and 2020 hit tech and corporate services?
5. **Predictive Outlook:** Can historical recession indicators reliably forecast forward 12-month sector job losses and recovery timelines?

## Notebooks

| Notebook | Scope |
| :--- | :--- |
| `01_data_collection_cleaning.ipynb` | Ingests 6 FRED series, aligns monthly timestamps, engineers cohort aggregates, and exports `master_table.csv` |
| `02_eda_visualizations.ipynb` | Generates 5 analytical charts covering macro baselines, structural crossover, onset event studies, era drawdowns, and sub-sector bifurcation |
| `03_predictive_modeling.ipynb` | Evaluates chronological linear regression models for forward 12-month job changes and computes historical recovery benchmarks |

## Data Dictionary & Feature Engineering

### Raw FRED Series
| Ticker | Column | Description |
| :--- | :--- | :--- |
| `USREC` | `recession_indicator` | NBER Recession Indicator (`0` = expansion, `1` = recession) |
| `PAYEMS` | `total_nonfarm_payroll` | Total Nonfarm Payroll Employment (macro baseline) |
| `USCONS` | `construction_employment` | Construction employment (blue-collar) |
| `MANEMP` | `manufacturing_employment` | Manufacturing employment (blue-collar) |
| `USPBS` | `professional_business_services` | Professional & Business Services (white-collar) |
| `USINFO` | `information_sector` | Information / Tech sector (white-collar) |

### Engineered Features
| Column | Formula |
| :--- | :--- |
| `blue_collar_jobs` | `construction_employment + manufacturing_employment` |
| `white_collar_jobs` | `professional_business_services + information_sector` |
| `core_cohort_total` | `blue_collar_jobs + white_collar_jobs` |
| `white_collar_pct` | `(white_collar_jobs / core_cohort_total) * 100` |
| `blue_collar_pct` | `(blue_collar_jobs / core_cohort_total) * 100` |

## Project Structure

```text
├── data/
│   └── processed/
│       └── master_table.csv
├── notebooks/
│   ├── 01_data_collection_cleaning.ipynb
│   ├── 02_eda_visualizations.ipynb
│   └── 03_predictive_modeling.ipynb
├── .env
├── requirements.txt
└── README.md
