# UK COVID-19 Data Analytics ETL Pipeline
IMPORTANT DISCLAIMER: The configuration files and datasets in this repository are a representation of the project used for educational purposes. They were created to practice and demonstrate the ETL pipeline concepts and transformations required for this assignment and are not the actual production assets.

## Introduction

This project contains an Azure Data Factory (ADF) ETL pipeline designed to automate the ingestion, processing, and analysis of UK COVID-19 case data. The pipeline extracts raw CSV files from a public GitHub repository, stages them in Azure Blob Storage, and performs necessary transformations to structure the data for optimal use in Azure SQL Database. Once processed and loaded, the data serves as a reliable foundation for analysis and visualization in tools like Power BI, enabling data-driven insights into the pandemic's trends within the UK region.

The entire process is automated on a daily schedule, ensuring the analytics platform is consistently updated with the latest available information.

## Architecture & Implementation Journey
This project was built by sequentially provisioning and integrating Azure services within a single, dedicated resource group. The implementation follows a clear, layered data architecture:

### Foundation & Ingestion (The "Bronze" Layer):
The process begins with Azure Blob Storage, which was provisioned to act as the initial landing zone. A manually triggered pipeline in Azure Data Factory (ADF) was developed to ingest raw CSV files from the public GitHub repository, faithfully preserving the source data in its original state for full traceability.

### Orchestration & Transformation (The "Silver" Layer):
Using ADF's authoring tools, Linked Services were configured to securely connect the data factory to both Blob Storage and the subsequent storage layer. The core transformation logic was implemented within ADF, where data flows were designed to cleanse, structure, and prepare the raw data for analytical querying. The transformed data was then written to Azure Data Lake Gen2, serving as a curated intermediate storage layer.

### Automation & Delivery (The "Gold" Layer):
To fully automate the process, an ADF trigger was created to execute the entire ingestion and transformation pipeline on a 24-hour schedule. A separate pipeline activity was designed to efficiently load the prepared data from Data Lake Gen2 into Azure SQL Database, finalizing it into structured tables optimized for reporting.

### Analysis & Visualization:
The final step connects Power BI directly to the Azure SQL Database. This allows for the creation of dynamic reports and dashboards that visualize the now-clean, trustworthy, and regularly updated UK COVID-19 data, turning the technical pipeline into actionable business insights.

## Azure Technologies Used
Azure Resource Group: Serves as the logical container for grouping all related project resources.

- Azure Data Factory (ADF): The core orchestration service used to build, schedule, and monitor the data pipelines and transformation workflows.

- Azure Blob Storage: Used as the initial landing zone (Bronze layer) to store raw CSV files ingested from GitHub.

- Azure Data Lake Storage Gen2: Used as the primary data lake for storing transformed and curated data (Silver layer) before final loading.

- Azure SQL Database: Serves as the production data warehouse (Gold layer) for hosting structured, query-optimized tables ready for analytics.

'''
Note on Architecture: The initial design considered using Azure Databricks for advanced transformation logic and Azure HDInsight for large-scale data processing. However, these services were not utilized in the final implementation as they are not available under Azure's Free Subscription tier and were beyond the scope of this project's requirements. All transformations were successfully handled within Azure Data Factory's native data flows.
'''
