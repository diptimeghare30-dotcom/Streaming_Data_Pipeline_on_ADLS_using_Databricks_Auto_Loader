# 🚀 ADLS + Databricks Auto Loader Medallion Architecture for Ecommerce Analytics

## 📌 Project Overview
This project demonstrates a **real-time and batch data ingestion pipeline** using **Azure Data Lake Storage (ADLS), Azure Databricks, PySpark, and Auto Loader** following the **Medallion Architecture (Bronze, Silver, Gold)**.

The pipeline ingests **dimension and fact data** from ADLS, processes it using both **batch and streaming**, and produces **analytics-ready datasets**.

---

## 🏗️ Architecture Overview

### 🔹 Domain
Ecommerce

### 🔹 Data Sources
- Azure Data Lake Storage (ADLS Gen2)
- File formats: CSV
- Data Types:
  - Dimension Data (Products, Customers)
  - Fact Data (Orders, Returns)

---

## 🥉 Bronze Layer (Raw Data)

### 📥 Batch Ingestion (Dimensions)
- Products and Customers loaded from ADLS using batch processing
- Adds metadata:
  - `_source_file`
  - `ingested_at`

Tables:
- `bronze.products`
- `bronze.customers`

---

### ⚡ Streaming Ingestion (Facts using Auto Loader)

- Uses **Databricks Auto Loader (cloudFiles)**
- Incremental ingestion from ADLS
- Handles schema inference and evolution
- Uses checkpointing for fault tolerance

Tables:
- `bronze.orders`
- `bronze.returns`

---

## 🥈 Silver Layer (Cleansed & Transformed)

### 🧹 Dimension Processing
- Trim and clean text fields
- Remove special characters
- Handle null values
- Standardize categories
- Validate numeric fields

Tables:
- `silver.products`
- `silver.customers`

---

### 🔄 Streaming Fact Processing
- Data type casting
- Date formatting
- Null filtering
- Data standardization

Tables:
- `silver.orders`
- `silver.returns`

---

## 🥇 Gold Layer (Business Insights)

### 📊 Aggregated Tables

#### 1️⃣ Daily Sales
- `gold.fact_daily_sales`
  - Daily revenue
  - Units sold
  - Order count

#### 2️⃣ Product Performance
- `gold.fact_product_performance`
  - Total units sold
  - Total revenue
  - Refund amount
  - Refund rate

#### 3️⃣ Category Revenue
- `gold.category_revenue`

#### 4️⃣ Top Customers
- `gold.top_customers`

---

## ⚙️ Key Features

- ✅ Medallion Architecture (Bronze → Silver → Gold)
- ✅ Real-time ingestion using Auto Loader
- ✅ Batch + Streaming hybrid pipeline
- ✅ Schema enforcement and evolution
- ✅ Data quality checks (nulls, formats)
- ✅ Scalable Delta Lake storage
- ✅ Checkpointing for fault tolerance

---

## 🛠️ Tech Stack

- Azure Data Lake Storage (ADLS Gen2)
- Azure Databricks
- PySpark
- Delta Lake
- Databricks Auto Loader
- Structured Streaming

---

## 🔁 Data Pipeline Flow

1. Load dimension data (Products, Customers) → Bronze (Batch)
2. Load fact data (Orders, Returns) → Bronze (Streaming via Auto Loader)
3. Clean and transform data → Silver
4. Perform aggregations → Gold
5. Generate analytics tables for reporting

---

## ▶️ How to Run

### 1️⃣ Setup Azure Resources
- Create Storage Account (ADLS Gen2)
- Create Container and upload CSV files
- Create Azure Databricks workspace

---

### 2️⃣ Create Catalog & Schemas
CREATE SCHEMA bronze;
CREATE SCHEMA silver;
CREATE SCHEMA gold;

## 3️⃣ Run Dimension Pipelines
Execute:
- `dim_bronze.py`
- `dim_silver.py`
- `dim_gold.py`

---

## 4️⃣ Run Streaming Pipelines
Execute:
- `fact_bronze_autoloader.py`
- `fact_silver_stream.py`

---

## 5️⃣ Create Gold Tables
Run SQL script:
- `fact_gold.sql`

---

## 📊 Sample Output

### 📅 Daily Sales
- Revenue per day  
- Total orders  
- Units sold  

### 📦 Product Performance
- Sales vs refunds  
- Revenue insights  
- Refund rate analysis  

---

## 🚧 Data Quality Handling
- Null handling and imputation  
- Data type validation  
- Standardization of categories  
- Removal of invalid records  

---

## 📈 Future Enhancements
- Integrate with Power BI dashboards  
- Add orchestration (ADF / Fabric Pipelines)  
- Implement CDC for real-time updates  
- Add monitoring & alerting  
- Optimize using Z-Ordering & Partitioning  
