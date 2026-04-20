# US Flight Delay Analysis — DVA Capstone 2

**Sector:** Aviation / Transportation  
**Dataset:** US Flight Delays 2015 (Bureau of Transportation Statistics)  
**Objective:** Analyze root causes of US domestic flight delays and provide actionable recommendations to improve on-time performance.

---

## 📋 Problem Statement

US domestic airlines operated nearly **5.8 million flights** in 2015. Flight delays cost the aviation industry an estimated **$28 billion annually** in operational costs, passenger compensation, and lost productivity. This project analyzes the full 2015 flight operations dataset to identify:

1. **Which airlines and airports are most delay-prone?**
2. **What are the primary root causes of delays?**
3. **When do delays peak (by month, day, hour)?**
4. **What operational interventions can reduce delays?**

The analysis supports decision-making for airline operations managers and aviation regulators.

---

## 📂 Repository Structure

```
├── README.md                          ← You are here
├── data/
│   ├── raw/                           ← Original datasets (never edited)
│   │   ├── airlines.csv
│   │   ├── airports.csv
│   │   └── flights.csv
│   └── processed/                     ← Cleaned output from pipeline
│       ├── flights_cleaned.csv
│       ├── airlines_cleaned.csv
│       ├── airports_cleaned.csv
│       └── tableau/                   ← Aggregated datasets for Tableau
├── notebooks/
│   ├── 01_extraction.ipynb            ← Data loading & quality assessment
│   ├── 02_cleaning.ipynb              ← ETL pipeline (cleaning & transformation)
│   ├── 03_eda.ipynb                   ← Exploratory Data Analysis
│   ├── 04_statistical_analysis.ipynb  ← Hypothesis testing & regression
│   └── 05_final_load_prep.ipynb       ← Tableau-ready dataset preparation
├── scripts/
│   └── etl_pipeline.py                ← Consolidated ETL script
├── tableau/
│   ├── screenshots/                   ← Dashboard screenshots
│   └── dashboard_links.md            ← Tableau Public URL
├── reports/
│   ├── project_report.pdf            ← Final project report
│   └── presentation.pdf              ← Presentation deck
└── docs/
    └── data_dictionary.md            ← Column definitions & KPIs
```

---

## 📊 Dataset Overview

| File | Rows | Columns | Description |
|------|------|---------|-------------|
| `airlines.csv` | 14 | 2 | Airline names and IATA codes |
| `airports.csv` | 322 | 7 | Airport details with coordinates |
| `flights.csv` | 5,819,079 | 31 | Flight-level records for all 2015 US domestic flights |

**Source:** Bureau of Transportation Statistics (BTS)

---

## 🔑 Key Performance Indicators (KPIs)

| KPI | Definition |
|-----|-----------|
| On-Time Performance Rate | % of flights arriving within 15 minutes of schedule |
| Average Arrival Delay | Mean delay in minutes for non-cancelled flights |
| Cancellation Rate | % of total flights that were cancelled |
| Primary Delay Cause | Most common delay type (Airline, Weather, NAS, etc.) |

---

## 🛠 Tech Stack

| Tool | Purpose |
|------|---------|
| Python (Pandas, NumPy) | ETL pipeline, data cleaning |
| Matplotlib, Seaborn | EDA visualizations |
| SciPy, Statsmodels | Statistical analysis |
| Tableau Public | Interactive dashboard |
| GitHub | Version control & collaboration |

---

## 🚀 How to Run

### 1. Run ETL Pipeline
```bash
python scripts/etl_pipeline.py
```

### 2. Run Notebooks
Open in Jupyter Notebook or Google Colab and run in order:
```
01_extraction.ipynb → 02_cleaning.ipynb → 03_eda.ipynb → 04_statistical_analysis.ipynb → 05_final_load_prep.ipynb
```

### 3. Tableau Dashboard
- Tableau Public URL: *(to be added after publishing)*
- Screenshots available in `tableau/screenshots/`

---

## 👥 Team

| Role | Team Member | GitHub Username |
|------|------------|-----------------|
| Project Lead | | |
| Data Lead | | |
| ETL Lead | | |
| Analysis Lead | | |
| Visualization Lead | | |
| Strategy Lead | | |
| PPT & Quality Lead | | |

---

## 📄 License

This project is part of the DVA Capstone 2 program at Newton School of Technology.
