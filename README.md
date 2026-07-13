# Customer Churn Analysis

An end-to-end exploratory data analysis of customer churn — from raw, messy multi-table data to a cleaned dataset, churn metrics, and visualizations.

## Overview

This project pulls customer, subscription, and support data out of a SQLite database, cleans and merges it into a single analysis-ready table, engineers churn-related features, and explores the drivers of churn through summary statistics, Matplotlib/Seaborn visualizations, and pivot tables.

## Project Structure

```
Churn-Analysis/
├── Churn_Analysis.ipynb          # Main analysis notebook
├── data/
│   ├── customer_churn.db         # Raw SQLite database (customer, subscription, support tables)
│   ├── customer_churn_data_raw.xlsx  # Raw data (Excel source)
│   └── Churn_data.csv            # Cleaned, merged dataset produced by the notebook
├── requirements.txt
└── README.md
```

## Data

The raw data lives in `customer_churn.db`, a SQLite database with three tables:

- **customer** — demographics (name, gender, date of birth, country, state, etc.)
- **subscription** — plan type, contract type, subscription/renewal/cancellation dates, monthly charges, CLTV, churn score
- **support** — complaint dates, escalations, CSAT scores

`Churn_data.csv` is the cleaned output: the three tables merged on `customerid`, with engineered features such as `churn_flag`, `tenure_days`, `churn_risk`, and `complaint_count`.

## What the Notebook Does

1. **Data loading** — reads all tables from the SQLite database into pandas DataFrames.
2. **Cleaning** — per-table cleaning:
   - Customer: drops unused columns, standardizes gender values, parses dates, fills missing country from state.
   - Subscription: parses subscription/renewal/cancellation dates.
   - Support: drops unused columns, parses complaint dates, deduplicates to one row per customer while keeping a complaint count.
3. **Feature engineering** — creates `churn_flag` (1 if cancelled), `complaint_count`, and merges all three tables into one dataset.
4. **Analysis** — computes churn rate, retention rate, churn by plan/subscription type/state, revenue loss from churned customers, average revenue per user, average tenure, escalation rate, and a `churn_risk` bucket (low/med/high) from the churn score.
5. **Visualization**
   - Matplotlib: churn trend over time, churn rate by plan type, churn rate by state, churn split by gender.
   - Seaborn: correlation heatmap, pairplot, and categorical plots of charges by plan/gender/churn risk.
6. **Pivot tables** — churn rate by plan type, and a multi-metric pivot (monthly charges, unique customers, churn rate) by plan type.

## Getting Started

### Prerequisites
- Python 3.9+
- Jupyter Notebook or JupyterLab

### Installation
```bash
git clone <your-repo-url>
cd Churn-Analysis
pip install -r requirements.txt
```

### Run
```bash
jupyter notebook Churn_Analysis.ipynb
```

## Key Metrics Produced
- Overall churn rate & retention rate
- Churn rate by plan type, subscription type, and state
- Revenue loss attributable to churned customers
- Average revenue per user (ARPU)
- Average customer tenure
- Escalation rate
- Churn risk segmentation (low / medium / high)

## License

Add a license of your choice (e.g., MIT) here.
