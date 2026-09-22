# 🌾 FarmInsight

> **An End-to-End Agricultural Data Engineering & Analytics Platform**

[![Status](https://img.shields.io/badge/status-active-success.svg)]()
[![Data Engineering](https://img.shields.io/badge/domain-Data%20Engineering-blue.svg)]()
[![Python](https://img.shields.io/badge/python-3.10%2B-blue.svg)]()
[![License](https://img.shields.io/badge/license-MIT-green.svg)]()

---

## 📌 Table of Contents

- [Overview](#-overview)
- [System Architecture & Pipeline](#-system-architecture--pipeline)
- [Project Structure](#-project-structure)
- [Datasets Overview](#-datasets-overview)
- [Documentation](#-documentation)
- [Getting Started](#-getting-started)
- [Data Pipeline Roadmap](#-data-pipeline-roadmap)
- [Contributing](#-contributing)
- [License](#-license)

---

## 🚜 Overview

**FarmInsight** is a data engineering and analytics project built to ingest, clean, model, and analyze agricultural data. By consolidating disparate data streams—including farmer demographics, crop cultivation cycles, localized weather telemetry, and historical harvest yields—FarmInsight provides actionable insights to improve crop productivity, optimize resource allocation (fertilizer and pesticide usage), and mitigate climate risks.

### Key Objectives
- **Centralized Data Lake**: Ingest and structure heterogeneous agricultural datasets into a unified repository.
- **Data Quality & Validation**: Enforce schema consistency, handle missing observations, and detect anomalies in telemetry readings.
- **Relational Data Modeling**: Connect farmer profiles, crop lifecycles, and regional weather patterns with final crop yields for downstream analytics.
- **Actionable Insights**: Enable predictive yield forecasting, resource optimization, and seasonal performance benchmarking.

---

## 🏗 System Architecture & Pipeline

FarmInsight adheres to a multi-tiered data engineering pipeline:

```
┌──────────────────┐     ┌──────────────────┐     ┌──────────────────┐     ┌──────────────────┐
│   Data Sources   │ ──> │ Ingestion Layer  │ ──> │ Transformation   │ ──> │ Analytics & BI   │
│                  │     │   (Raw Zone)     │     │   & Modeling     │     │   (Consumption)  │
└──────────────────┘     └──────────────────┘     └──────────────────┘     └──────────────────┘
 • Farmer Profiles        • data/raw/              • Data Cleaning          • Yield Dashboards
 • Crop Cycles            • Schema Validation      • Deduplication          • Weather Impact
 • Weather Telemetry      • Checksums & Audit      • Entity Joins           • Resource ROI
 • Harvest Yields                                  • Feature Engineering
```

For comprehensive details on architectural design, data layers, and pipeline specifications, refer to [architecture.md](docs/architecture.md).

---

## 📂 Project Structure

```text
FarmInsight/
│
├── data/
│   ├── raw/                        # Untouched, raw agricultural source datasets
│   │   ├── crops.csv               # Crop cultivation records, sowing/harvest dates, inputs
│   │   ├── farmers.csv             # Farmer profiles, landholding, soil & irrigation types
│   │   ├── weather.csv             # District-level weather and climate telemetry
│   │   └── yield.csv               # Historical harvest yields per crop and farmer
│   │
│   └── sample/                     # Minified sample datasets for testing and CI/CD
│
├── docs/                           # Project specifications and technical documentation
│   ├── architecture.md             # End-to-end system design & pipeline architecture
│   ├── data_dictionary.md          # Schema definitions, data types, and field descriptions
│   └── requirements.md             # Functional and non-functional requirements
│
├── .gitignore                      # Git ignore file for artifacts and environments
└── README.md                       # Main project documentation
```

---

## 📊 Datasets Overview

The raw data layer contains four primary entities located in `data/raw/`:

| Dataset | Records | Description | Primary / Key Fields |
| :--- | :--- | :--- | :--- |
| **[`farmers.csv`](data/raw/farmers.csv)** | 800+ | Farmer demographics, regional location, land size, and soil/irrigation methods. | `farmer_id`, `district`, `taluka`, `village`, `land_area_acres`, `soil_type`, `irrigation_type` |
| **[`crops.csv`](data/raw/crops.csv)** | 1,300+ | Crop cultivation cycles, seasons (Kharif, Rabi, Adsali, Perennial), and chemical inputs. | `crop_id`, `farmer_id`, `crop`, `season`, `sowing_date`, `harvest_date`, `fertilizer_used_kg`, `pesticide_used_l` |
| **[`weather.csv`](data/raw/weather.csv)** | 1,000+ | Daily weather readings across agricultural districts. | `weather_id`, `date`, `district`, `temperature_c`, `humidity_percent`, `rainfall_mm` |
| **[`yield.csv`](data/raw/yield.csv)** | 1,300+ | Recorded harvest outputs mapped to individual crops and farmers. | `yield_id`, `farmer_id`, `crop_id`, `harvest_year`, `total_yield_tons` |

> Detailed column-level definitions and constraints can be reviewed in [data_dictionary.md](docs/data_dictionary.md).

---

## 📖 Documentation

Detailed engineering documentation is maintained in the [`docs/`](docs/) directory:

- 📋 [**Requirements Specification**](docs/requirements.md): Details business use cases, functional ingestion/transformation requirements, and non-functional performance benchmarks.
- 📐 [**System Architecture**](docs/architecture.md): Illustrates the end-to-end data pipeline, data flow across storage zones, and processing layers.
- 📚 [**Data Dictionary**](docs/data_dictionary.md): Documents data schemas, types, nullability rules, and descriptive metadata for all tables.

---

## 🚀 Getting Started

### Prerequisites
- [Git](https://git-scm.com/) installed on your machine
- [Python 3.10+](https://www.python.org/) recommended

### 1. Clone the Repository
```bash
git clone https://github.com/KuldeepLakhera9/FarmInsight.git
cd FarmInsight
```

### 2. Set Up Virtual Environment
```bash
# Create a virtual environment
python -m venv venv

# Activate on Windows (PowerShell):
.\venv\Scripts\Activate.ps1

# Activate on Linux/macOS:
source venv/bin/activate
```

### 3. Explore the Datasets
You can inspect the raw datasets in `data/raw/` or run exploratory analysis using Python:
```python
import pandas as pd

farmers_df = pd.read_csv("data/raw/farmers.csv")
crops_df = pd.read_csv("data/raw/crops.csv")
weather_df = pd.read_csv("data/raw/weather.csv")
yield_df = pd.read_csv("data/raw/yield.csv")

print(f"Farmers: {len(farmers_df)}, Crops: {len(crops_df)}, Weather Records: {len(weather_df)}, Yield Records: {len(yield_df)}")
```

---

## 🗺 Data Pipeline Roadmap

- [x] **Repository Scaffolding**: Structured project directories and documentation baseline.
- [x] **Raw Datasets Ingestion**: Sourced farmers, crops, weather, and yield datasets.
- [ ] **Data Cleaning & Validation**: Implement automated schema checks, null handling, and outlier detection.
- [ ] **Transformation & Modeling**: Develop dimensional models (star/snowflake schema) linking crops, weather conditions, and yields.
- [ ] **Automated Orchestration**: Build automated pipeline DAGs (e.g., using Apache Airflow, Prefect, or Mage).
- [ ] **Analytics & Dashboarding**: Build interactive visualizations for yield trends, soil-crop compatibility, and weather impacts.

---

## 🤝 Contributing

Contributions are welcome! If you'd like to improve the data pipelines, documentation, or analytics models:
1. Fork the repository
2. Create your feature branch (`git checkout -b feature/new-transformation`)
3. Commit your changes (`git commit -m 'Add new transformation pipeline'`)
4. Push to the branch (`git push origin feature/new-transformation`)
5. Open a Pull Request

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
