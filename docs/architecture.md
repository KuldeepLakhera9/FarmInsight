# System Architecture - FarmInsight

## 1. High-Level Architecture

The FarmInsight data platform follows a modern data engineering pipeline architecture:

```
[ Data Sources ]
  - IoT Sensors (Soil, Moisture, Temp)
  - Weather APIs
  - Historical Yield Reports
         │
         ▼
[ Ingestion Layer ]
  - Raw Data Landing (`data/raw/`)
         │
         ▼
[ Processing & Transformation ]
  - Data Validation & Quality Checks
  - Data Cleaning & Normalization
  - Feature Engineering & Aggregations
         │
         ▼
[ Storage & Serving Layer ]
  - Analytical Data Store / Lakehouse
         │
         ▼
[ Consumption Layer ]
  - Dashboards & Visualizations
  - Predictive Analytics & Insights
```

## 2. Layers Breakdown

1. **Ingestion Layer**:
   - Ingests raw inputs into `data/raw/` preserving original format and lineage.
2. **Validation & Quality**:
   - Ensures completeness, type conformity, and sanity checks against outlier sensor readings.
3. **Transformation Layer**:
   - Aggregates high-frequency sensor readings into hourly/daily summary metrics.
4. **Analytics Layer**:
   - Supplies analytics queries and machine learning models with curated feature sets.
