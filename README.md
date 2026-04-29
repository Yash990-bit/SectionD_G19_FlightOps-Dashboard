# ✈️ US Aviation Performance Analysis (2015)
[![Python](https://img.shields.io/badge/Python-3.12-blue?logo=python)](https://www.python.org/)
[![Pandas](https://img.shields.io/badge/Data-Pandas-150458?logo=pandas)](https://pandas.pydata.org/)
[![Tableau](https://img.shields.io/badge/Visuals-Tableau-E97627?logo=tableau)](https://public.tableau.com/)

## 📝 Executive Summary
**Project Objective:** Can we predict and reduce US flight delays through systemic data engineering?  
This repository hosts a high-fidelity **Aviation ETL Pipeline** and **Strategic Ops Dashboard**. By analyzing 5.8M rows of Bureau of Transportation Statistics (BTS) data, we identify carrier bottlenecks, seasonal delay profiles, and operational interventions to improve on-time performance.

---

## 🏗 Industrial Data Architecture
The pipeline is designed for horizontal scalability and reproducibility.

```mermaid
graph LR
    A[Raw Data] --> B[ETL Script]
    B --> C[Processed Data]
    C --> D[Statistical Validation]
    D --> E[Tableau Prep]
    E --> F[Visual Dashboard]
```

---

## 📂 Detailed Repository Structure

```text
├── notebooks/
│   ├── 01_extraction.ipynb         # Data ingestion and raw schema assessment
│   ├── 02_cleaning.ipynb           # Main ETL pipeline: formatting, imputation, and outlier audit
│   ├── 03_eda.ipynb                # Strategic analysis of delay trends and carrier benchmarks
│   ├── 04_statistical_analysis.ipynb # Hypothesis testing and statistical validation of insights
│   └── 05_final_load_prep.ipynb    # Final joins and denormalization for BI usage
├── scripts/
│   ├── etl_pipeline.py             # Automates the extraction and cleaning process (Production)
│   ├── sample_dataset.py           # Downsamples 5.8M rows to 100k for performance/IDE stability
│   └── tableau_prep.py             # Generates pre-aggregated CSVs for fast Tableau loading
├── data/
│   ├── raw/                        # Original Source Data (Airlines, Airports, 100k Flight Sample)
│   ├── processed/                  # Validated outputs from the cleaning pipeline
│   └── processed/tableau/          # High-performance aggregates ready for Dashboard import
├── docs/
│   └── data_dictionary.md          # Visual data lineage and detailed column definitions
├── tableau/
│   └── dashboard_links.md          # Storage for live project URLs and dashboard screenshots
└── README.md                       # This executive summary
```

---

## 🚀 Quick Start (One-Click Pipeline)
1.  **Clone the Repo**: `git clone https://github.com/adamyatiwari12/SectionD_G19_FlightOps-Dashboard.git`
2.  **Run ETL**: `python3 scripts/etl_pipeline.py` (Converts raw CSVs to cleaned assets).
3.  **Prepare for BI**: `python3 scripts/tableau_prep.py` (Generates aggregated Tableau CSVs).

---

## 📊 Standard KPI Framework
*   **OTP (On-Time Performance)**: Arrival Delay ≤ 15 minutes.
*   **D-Delay & A-Delay**: Variance between departure and arrival timelines.
*   **Cancellation Tiers**: Root-cause categorization (Carrier, Weather, NAS, Security).

---

## 👤 Team Group-19 (Section D)

| Role                 | Member             |
|----------------------|--------------------|
| **Project Lead**     | Adamya Tiwari      |
| **ETL Engineer**     | Agnik Misra        |
| **Data Scientist**   | Yash Raghubanshi   |
| **BI Developer**     | Prateek            |
| **Strategy Lead**    | Rahul              |
| **Analysis Lead**    | Ram                |

---
**Institutional Sponsor:** Newton School of Technology  
**Program:** DVA Capstone 2 Simulation
