# Recession Impact Analysis

A data portfolio project comparing how U.S. employment sectors perform during recessions. Uses FRED (Federal Reserve Economic Data) to analyze white-collar vs. blue-collar job losses across historical downturns.

## What this project answers

1. **Crossover moment:** When did white-collar jobs overtake blue-collar jobs in America?
2. **First blood:** When a recession hits, do blue-collar or white-collar workers lose jobs first?
3. **Vulnerability shift:** Are modern white-collar desk jobs as fragile as factory jobs were in the 1950s–1980s?
4. **Sub-sector bifurcation:** Why did 2008 crush construction while 2001/2020 hit tech and corporate desks?
5. **Predictive link:** If a recession hits tomorrow, which cohort gets hit harder—and how long to recover?

## Notebooks

| Notebook | What it does |
|----------|-------------|
| `01_data_collection_cleaning.ipynb` | Downloads 6 FRED series, aligns dates, engineers blue-collar/white-collar aggregates, saves master table |
| `02_eda_visualizations.ipynb` | 5 charts: macro baseline, crossover moment, first blood event study, vulnerability shift, sub-sector bifurcation |
| `03_predictive_modeling.ipynb` | Linear regression models to forecast forward 12-month job changes by cohort, plus recovery duration analysis |

## Data series used

| FRED Ticker | Column | What it measures |
|-------------|--------|-----------------|
| `USREC` | `recession_indicator` | NBER Recession Indicator (0 = expansion, 1 = recession) |
| `PAYEMS` | `total_nonfarm_payroll` | Total Nonfarm Payroll Employment (macro baseline) |
| `USCONS` | `construction_employment` | Construction employment (blue-collar) |
| `MANEMP` | `manufacturing_employment` | Manufacturing employment (blue-collar) |
| `USPBS` | `professional_business_services` | Professional & Business Services (white-collar) |
| `USINFO` | `information_sector` | Information / Tech sector (white-collar) |

## Engineered features

| Column | Formula |
|--------|---------|
| `blue_collar_jobs` | `construction_employment` + `manufacturing_employment` |
| `white_collar_jobs` | `professional_business_services` + `information_sector` |
| `core_cohort_total` | `blue_collar_jobs` + `white_collar_jobs` |
| `white_collar_pct` | `white_collar_jobs / core_cohort_total * 100` |
| `blue_collar_pct` | `blue_collar_jobs / core_cohort_total * 100` |

## Setup

1. Clone this repository
2. Install dependencies: `pip install -r requirements.txt`
3. Get a free FRED API key at https://fred.stlouisfed.org/docs/api/api_key.html
4. Add your key to the `.env` file: `FRED_API_KEY=your_key_here`
5. Run notebooks in order: `01` → `02` → `03`

## License

MIT