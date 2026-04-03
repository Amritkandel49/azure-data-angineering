# Azure End-to-End Data Engineering Project

This repository contains an end-to-end data engineering project built on Microsoft Azure, covering the complete data lifecycle from ingestion to analytics using the **Medallion Architecture**.

## Project Architecture (Medallion Approach)
The project organizes data logically in a data lake into three distinct layers:
- **Bronze (Raw/Ingestion Layer):** Unprocessed, raw data ingested directly from source systems.
- **Silver (Transformed/Cleansed Layer):** Filtered, cleaned, and augmented data, converted to efficient formats like Parquet.
- **Gold (Presentation/Serving Layer):** Business-ready, aggregated data optimized for analytics and reporting.

## Tech Stack & Tools Used
- **Azure Data Factory (ADF):** Primary orchestration tool for dynamic data pipelines.
- **Azure Data Lake Storage Gen2 (ADLS Gen2):** Scalable cloud storage for all medallion layers.
- **Azure Databricks:** Spark-based analytics platform for large-scale data transformation.
- **Azure Synapse Analytics:** Unified platform for data warehousing and distributed SQL querying.
- **Power BI:** Data visualization and dashboarding.
- **PySpark & SQL:** Core programming languages for transformations and querying.

## Project Phases

### Phase 1: Data Ingestion (Bronze Layer)
- Configured Linked Services and Datasets within **Azure Data Factory** to connect to source structures.
- Built a highly dynamic and parameterized pipeline utilizing `ForEach` and `Lookup` activities to recursively pull multiple files (Sales, Customers, Products, etc.) instead of manual one-by-one ingestion.
- Successfully landed the raw data securely into the ADLS Gen2 Bronze container.

### Phase 2: Data Transformation (Silver Layer)
- Provisioned and configured an **Azure Databricks** compute cluster.
- Established secure authentication via **Azure Service Principals**.
- Authored **PySpark** code (`silver_layer.ipynb`) to read the raw data, apply necessary business transformations, clean up nulls, and format columns.
- Wrote the transformed datasets back to the ADLS Gen2 Silver container in optimized `Parquet` format.

### Phase 3: Data Warehousing & Analytics (Gold Layer)
- Leveraged **Azure Synapse Analytics** utilizing SQL pools.
- Used the `OPENROWSET()` function to directly query transformed Parquet files from the Data Lake without moving data.
- Built **External Tables** and Views (`Create External Table.sql`, `Create Views Gold.sql`) to serve as a logical data warehouse.
- Connected the Gold layer structures seamlessly to **Power BI** to deliver interactive executive dashboards.