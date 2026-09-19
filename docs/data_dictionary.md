# Data Dictionary - FarmInsight

This document defines the schema, field types, and descriptions for datasets used across the FarmInsight project.

## 1. Overview of Datasets
- **Raw Data (`data/raw/`)**: Source files in their original format as received from IoT sensors, external APIs, and manual uploads.
- **Sample Data (`data/sample/`)**: Representative subsets of raw or processed data used for local development, testing, and CI/CD validation.

---

## 2. Core Entities & Schemas

### 2.1 Farm & Field Metadata
| Field Name | Data Type | Nullable | Description |
| :--- | :--- | :--- | :--- |
| `farm_id` | STRING / UUID | No | Unique identifier for the farm |
| `field_id` | STRING / UUID | No | Unique identifier for a field/plot |
| `crop_type` | STRING | No | Name of crop cultivated (e.g., Wheat, Rice, Corn) |
| `area_acres` | FLOAT | No | Field area in acres |
| `soil_type` | STRING | Yes | Classification of soil (e.g., Loamy, Sandy, Clay) |

### 2.2 Soil & Weather Sensor Telemetry
| Field Name | Data Type | Nullable | Description |
| :--- | :--- | :--- | :--- |
| `record_id` | STRING / UUID | No | Unique identifier for sensor reading |
| `field_id` | STRING / UUID | No | Foreign key linking to the field |
| `timestamp` | TIMESTAMP | No | Timestamp of reading (UTC) |
| `soil_moisture_pct` | FLOAT | Yes | Soil moisture percentage (0-100%) |
| `soil_temperature_c` | FLOAT | Yes | Soil temperature in Celsius |
| `ambient_temp_c` | FLOAT | Yes | Ambient air temperature in Celsius |
| `humidity_pct` | FLOAT | Yes | Relative humidity percentage |
| `rainfall_mm` | FLOAT | Yes | Precipitation measured in millimeters |
