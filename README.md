# Azure Data Factory - End-to-End ETL Pipeline with Databricks and Dataflows

## Overview
This project is an end-to-end ETL (Extract, Transform, Load) pipeline using Azure Data Factory (ADF), Azure Databricks, and ADF Mapping Data Flows. The pipeline extracts data from two different sources—Azure Blob Storage (CSV files) and HTTP API (JSON data)—and loads the raw data into Azure Data Lake Storage (ADLS). The data is then processed and stored in a separate folder in ADLS before being ingested into Azure SQL Database for analytics.

---

## Architecture
### Workflow Summary
1. Extract (Data Ingestion)  
   - Source 1: CSV files from Azure Blob Storage → Ingested into Raw folder in Azure Data Lake.
   - Source 2: JSON data from HTTP API → Ingested into Raw folder in Azure Data Lake.
  
2. Transform (Data Processing)  
   - Azure Databricks transforms CSV data and writes cleaned data to Processed folder in ADLS.
   - ADF Mapping Data Flows process JSON data and write the cleaned data to Processed folder in ADLS.

3. Load (Final Data Storage)  
   - The processed data from ADLS is ingested into Azure SQL Database for further analysis.
   - The pipeline is scheduled using triggers and monitored using ADF and Azure Monitor.

---

## Technology Stack
- Azure Data Factory (ADF) – Orchestration of the ETL process.
- Azure Blob Storage – Stores initial CSV data before ingestion.
- Azure Data Lake Storage (ADLS) – Stores raw and processed data.
- HTTP API Connector – Fetches JSON data dynamically.
- Azure Databricks – Performs complex transformations on CSV data.
- ADF Mapping Data Flows – Handles JSON data transformations.
- Azure SQL Database – Stores the final processed data.
- Azure Monitor – Tracks execution and alerts failures.
- GitHub – Version control for ADF pipelines.

---

## Pipeline Workflow
### 1️⃣ Data Ingestion (Raw Data Storage)
- Source 1: Azure Blob Storage (CSV files)  
  - ADF Copy Activity moves raw CSV files from Blob Storage to Raw folder in ADLS.
  
- Source 2: HTTP API (JSON data)  
  - ADF HTTP Connector extracts real-time JSON data and writes it into Raw folder in ADLS.

💾 Data Flow in ADLS After Ingestion
```
💽 Azure Data Lake Storage (ADLS)
│—— 📂 raw_data/              # Stores raw unprocessed data
│    ├── csv_files/          # Raw CSV data from Blob Storage
│    └── json_files/         # Raw JSON data from HTTP API
```

---

### 2️⃣ Data Transformation (Processed Data Storage)
#### Azure Blob Storage Data (CSV) – Processed using Databricks
- ADF triggers a Databricks notebook to process raw CSV data.
- Transformations performed in Databricks:
  - Handling missing values, duplicate records, and data cleansing.
  - Aggregations and data type conversions.
  - Writing cleaned CSV data to Processed folder in ADLS.

#### HTTP API Data (JSON) – Processed using ADF Mapping Data Flows
- JSON data from the Raw folder in ADLS is processed using ADF Mapping Data Flows:
  - Standardizing data formats.
  - Filtering and handling missing/null values.
  - Writing cleaned JSON data to Processed folder in ADLS.

💾 Data Flow in ADLS After Processing
```
💽 Azure Data Lake Storage (ADLS)
│—— 📂 raw_data/               # Raw unprocessed data
│    ├── csv_files/           # Raw CSV data from Blob Storage
│    └── json_files/          # Raw JSON data from HTTP API
│
│—— 📂 processed_data/         # Stores cleaned and transformed data
│    ├── transformed_csv/     # Processed CSV files from Databricks
│    └── transformed_json/    # Processed JSON files from Dataflows
```

---

### 3️⃣ Data Loading (Final Storage in SQL)
- Processed data from ADLS (Processed folder) is ingested into Azure SQL Database.
- Data is structured and optimized for analytical queries.
- Triggers automate the pipeline execution at scheduled intervals.

---

## Monitoring & Error Handling
- ADF Monitoring Panel – View pipeline execution history.
- Azure Log Analytics – Capture logs and track failures.
- Databricks Logging – Review logs from the Databricks notebook execution.
- Alerts & Notifications – Email alerts for pipeline failures using Logic Apps.

---

 



