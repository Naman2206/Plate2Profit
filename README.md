# 🍽️ Plate2Profit – Restaurant Sales Analytics Platform

An **end-to-end cloud-native restaurant sales analytics project** built on **Snowflake** using a **Metadata‑Driven Medallion Architecture (Bronze → Silver → Gold)**. The platform ingests raw sales data from AWS S3, processes it through reusable data pipelines, and serves analytics-ready data to **Power BI** for business insights.

---

## 📌 Project Objective

The goal of **Plate2Profit** is to:

* Build a **scalable and reusable data pipeline** for restaurant sales data
* Implement **full load and incremental load** using metadata-driven logic
* Apply **Medallion Architecture** best practices in Snowflake
* Enable **fast, reliable BI reporting** for restaurant performance

---

## 🏗️ High-Level Architecture

![Plate2Profit Architecture](images/plate2profit_architecture.png)

**Data Flow Overview**:

1. **AWS S3** – Raw restaurant sales data landing zone
2. **Snowflake (SRC DB)** – Source layer storing raw ingested tables
3. **Metadata Table** – Controls active tables, load type (Full/Incremental)
4. **Data Prep Layer** – Transformation & cleansing logic
5. **Views Layer** – Standardized reusable views
6. **DWH Destination DB** – Final curated tables (Gold Layer)
7. **Power BI** – Reporting & visualization

---

## 🥉🥈🥇 Medallion Architecture Implementation

### 🥉 Bronze Layer (Raw Data)

* Raw data ingested from **AWS S3** into Snowflake
* Minimal transformations
* Maintains historical data
* Acts as the **source of truth**

**Examples**:

* `raw_orders`
* `raw_order_items`
* `raw_payments`

---

### 🥈 Silver Layer (Cleaned & Prepared Data)

* Data cleansing and standardization
* Data type corrections
* Null handling & deduplication
* Business-friendly column naming

**Examples**:

* `clean_orders`
* `clean_customers`
* `clean_products`

---

### 🥇 Gold Layer (Analytics / DWH)

* Aggregated and analytics-ready tables
* Business KPIs & metrics
* Optimized for BI tools

**Examples**:

* `daily_sales_summary`
* `restaurant_performance`
* `top_selling_items`

---

## 🧠 Metadata-Driven Design

A central **METADATA table** controls the pipeline execution:

| Column Name      | Description                            |
| ---------------- | -------------------------------------- |
| table_name       | Source table name                      |
| load_type        | FULL / INCREMENTAL                     |
| is_active        | Whether table participates in pipeline |
| primary_key      | Used for change detection              |
| watermark_column | Used for incremental load              |

**Benefits**:

* No hardcoding of tables
* Easy onboarding of new datasets
* Pipeline controlled via data, not code

---

## 🔄 Load Strategy

### 🔁 Full Load (R)

* Truncate & reload destination table
* Used for small or reference tables
* Steps:

  1. Data Prep
  2. Load into View
  3. Reload destination table

---

### ➕ Incremental Load (I)

* Detects only changed/new records
* Uses watermark or primary key
* Steps:

  1. Data Prep
  2. Load into View
  3. Detect changes
  4. Merge into destination table

---

## 🧩 Transformation Layer

Transformations include:

* Revenue calculation
* Order-level aggregations
* Date & time normalization
* Restaurant & product mapping

Reusable **Snowflake Views** act as a semantic layer between raw data and DWH tables.

---

## 📊 BI & Reporting (Power BI)

![Restaurant Sales Dashboard](images/plate2profit_dashboard.png)

Power BI connects directly to **Gold Layer tables** to provide:

* Daily & monthly sales trends
* Total revenue & order volume
* Top-selling menu items
* Cuisine-wise sales contribution
* Peak ordering hours & day-wise performance

**Why Power BI?**

* Fast refresh from Snowflake
* Scalable semantic modeling
* Business-friendly dashboards

---

## 🛠️ Tech Stack

* **Cloud Storage**: AWS S3
* **Data Warehouse**: Snowflake
* **Architecture**: Medallion (Bronze/Silver/Gold)
* **ETL/ELT**: SQL-based transformations
* **Metadata Control**: Snowflake Tables
* **Visualization**: Power BI

---

## 📁 Project Structure

```
Plate2Profit/
│
├── metadata/
│   └── table_metadata.sql
│
├── bronze/
│   └── raw_load.sql
│
├── silver/
│   └── data_prep_views.sql
│
├── gold/
│   └── dwh_tables.sql
│
├── powerbi/
│   └── RestaurantSalesDashboard.pbix
│
└── README.md
```

---

## 🚀 Key Highlights (Interview Ready)

* Metadata-driven Snowflake pipeline
* Supports **Full & Incremental loads**
* Implements **industry-standard Medallion Architecture**
* Optimized for BI consumption
* Easily extensible for new restaurant datasets

---

## 📈 Future Enhancements

* Add Snowflake Streams & Tasks
* Implement CDC using Snowflake Streams
* Orchestrate using Airflow / ADF
* Add data quality checks
* Real-time ingestion support


