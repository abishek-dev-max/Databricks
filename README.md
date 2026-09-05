# 🚲 Bike Rental Analytics — Databricks & Power BI 
An end-to-end Bike Rental Analytics platform built using Databricks and Power BI, following a Medallion Architecture to transform raw rental data into analytics-ready dimensional and fact datasets and ultimately deliver business KPIs through an interactive Power BI dashboard.
The project demonstrates a complete modern data analytics workflow:

Raw Data
   │
   ▼
Databricks
   │
   ├── Bronze Layer
   │
   ├── Silver Layer
   │
   └── Gold Layer
          │
          ▼
    Dimensional Model
          │
          ▼
    Unity Catalog
          │
          ▼
Power BI Semantic Model
          │
          ▼
Power BI Report / Dashboard
# 📌 Project Overview

The objective of this project is to build a complete analytics solution for a bike rental business, starting from raw rental data and progressing through data engineering, dimensional modeling, KPI creation, and business intelligence reporting.
The solution uses Databricks as the primary data engineering and data storage platform and Power BI as the visualization and analytics layer. The processed data is governed and managed through Databricks Unity Catalog, while Power BI connects to the Databricks data layer using the Databricks Power BI OIDC connector. The project is designed to demonstrate how a modern analytics platform can transform operational data into actionable business insights.

# 🏗️ Architecture

The project follows the Medallion Architecture pattern.

                         ┌─────────────────────┐
                         │     Raw Sources     │
                         │                     │
                         │  Bike Rental Data   │
                         └──────────┬──────────┘
                                    │
                                    ▼
                         ┌─────────────────────┐
                         │   BRONZE LAYER      │
                         │                     │
                         │ Raw / Ingested Data │
                         └──────────┬──────────┘
                                    │
                             Transformation
                                    │
                                    ▼
                         ┌─────────────────────┐
                         │    SILVER LAYER     │
                         │                     │
                         │ Cleaned & Validated │
                         │       Data          │
                         └──────────┬──────────┘
                                    │
                             Transformation
                                    │
                                    ▼
                         ┌─────────────────────┐
                         │     GOLD LAYER      │
                         │                     │
                         │ Business-Ready Data │
                         │ Dimensional Model   │
                         └──────────┬──────────┘
                                    │
                                    ▼
                         ┌─────────────────────┐
                         │   UNITY CATALOG     │
                         │                     │
                         │ Governed Tables     │
                         └──────────┬──────────┘
                                    │
                             OIDC Connector
                                    │
                                    ▼
                         ┌─────────────────────┐
                         │ POWER BI SEMANTIC   │
                         │       MODEL         │
                         └──────────┬──────────┘
                                    │
                                    ▼
                         ┌─────────────────────┐
                         │    POWER BI REPORT  │
                         │                     │
                         │ KPIs & Analytics    │
                         └─────────────────────┘
# ⭐ Dimensional Model

The Gold layer follows a star-schema-oriented design.
Conceptually:

                         dim_date
                            │
                            │ 1
                            │
                            ▼ *
                       fact_rental
                            ▲
                            │ *
                            │
                         dim_bike

Additional dimensions can be connected to the central fact table depending on the analytical requirements.
The dimensional model provides:
Better reporting performance
Clear business semantics
Easier DAX development
Reusable dimensions
Consistent filtering
Simplified Power BI relationships

# 🔐 Unity Catalog

The Gold-layer analytical tables are stored and governed using Databricks Unity Catalog. Unity Catalog provides a centralized governance layer for the data assets used by the project.
The overall structure follows:

Catalog
   │
   └── Schema
          │
          ├── fact_rental
          ├── dim_date
          ├── dim_bike
          └── other dimensions

This creates a controlled data layer between the Databricks processing environment and downstream BI consumers.

# 🔗 Power BI Connectivity

Power BI is connected to the Databricks data platform using the Databricks Power BI OIDC connector.
The architecture is:

Databricks Unity Catalog
          │
          │
          ▼
Power BI Databricks OIDC Connector
          │
          ▼
Power BI Semantic Model
          │
          ▼
Power BI Report
The OIDC-based connection provides an authentication mechanism between Power BI and Databricks without requiring the project to expose raw credentials directly in the BI workflow. The Power BI semantic model acts as the analytical layer between the Gold data and the final report.
