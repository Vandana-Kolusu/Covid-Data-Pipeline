Overview

This project is an end-to-end ETL (Extract, Transform, Load) pipeline using Azure Data Factory (ADF), Azure Databricks, and ADF Mapping Data Flows. The pipeline extracts data from two different sources—Azure Blob Storage (CSV files) and HTTP API (JSON data)—and loads the raw data into Azure Data Lake Storage (ADLS). The data is then processed and stored in a separate folder in ADLS before being ingested into Azure SQL Database for analytics.
