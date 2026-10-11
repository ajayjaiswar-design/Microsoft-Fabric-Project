# Sales Data Pipeline Using Microsoft Fabric

## Project Overview

This project demonstrates an end-to-end data analytics solution using Microsoft Fabric. It ingests sales data from GitHub, processes it through the Bronze, Silver, and Gold layers, and loads the final dimension and fact tables into a Warehouse. A semantic model and Power BI report are then created to analyse sales data through interactive visuals.

## Technologies Used

Microsoft Fabric – Data processing and analytics platform.
Data Pipeline – Ingests CSV data from GitHub.
Lakehouse – Stores raw and processed data.
PySpark – Cleans, transforms, and aggregates data.
Delta Tables – Store data in Bronze, Silver, and Gold layers.
Fabric Warehouse – Stores dimension and fact tables.
Semantic Model – Defines relationships, measures, and RLS.
Power BI – Creates interactive reports using Direct Lake.

## Project Workflow

GitHub (sales_data.csv)
          ↓
Pipeline: pl_ingest_sales
          ↓
Lakehouse Files (Raw Data)
          ↓
Notebook 1: nb_load_to_Delta
          ↓
Bronze: bronze_sales
          ↓
Notebook 2: nb_transform_bronze_to_silver
          ↓
Silver: silver_sales
          ↓
Notebook 3: nb_build_gold_layer
          ↓
Gold: gold_sales_summary
          ↓
Notebook 4: nb_build_tables
          ↓
Dimension and Fact Tables
          ↓
Warehouse: wh_sales
          ↓
Semantic Model: Sales Semantic
          ↓
Power BI Report: Sales Report
          ↓
Interactive Sales Analysis

## 1. Data Ingestion

The pipeline pl_ingest_sales uses the CopyRawSalesCSV activity to copy sales_data.csv from GitHub into the Lakehouse Files section using HTTP.

Output: Raw CSV file stored in the Lakehouse.

## 2. Bronze Layer

The notebook nb_load_to_Delta reads the raw CSV file and loads the data into the bronze_sales Delta table.

Purpose: Store raw data in a structured format for further processing.

## 3. Silver Layer

The notebook nb_transform_bronze_to_silver cleans the Bronze data, renames columns, standardises formats, and applies the correct data types.
The transformed data is stored in silver_sales.

Purpose: Improve data quality and prepare the data for analysis.

## 4. Gold Layer

The notebook nb_build_gold_layer creates monthly revenue summaries by region and product category, along with other required aggregations.
The results are stored in gold_sales_summary.

Purpose: Prepare aggregated data for business reporting and analysis.

## 5. Dimension and Fact Tables

The notebook nb_build_tables creates the following tables and assigns surrogate keys to the dimension records:

dim_product – Stores product details.
dim_customer – Stores customer details.
dim_region – Stores region details.
fact_sales – Stores sales data and related dimension keys.

Purpose: Organise sales data into a dimensional model for reporting.

## 6. Date Dimension

A Warehouse named wh_sales was created, and the dim_date table was created using SQL with a surrogate key for each date record.

Purpose: Support date-based analysis, including monthly, quarterly, and yearly reporting.

## 7. Loading Data into the Warehouse

The dimension and fact tables were copied into wh_sales, bringing the final analytical tables together in one place.

The Warehouse contains:

Table	
dim_product	 → Product information
dim_customer → Customer information
dim_region   → Region information
dim_date     → Calendar information
fact_sales   → Sales measures and dimension keys

These tables form the foundation of a star schema for reporting and analysis.

## 8. Creating the Semantic Model

A semantic model named Sales Semantic was created and connected to the wh_sales Warehouse to access the dimension and fact tables.
The model defines the relationships between tables, creates measures for business calculations, and applies row-level security (RLS) where required.

Purpose: Provide a consistent data model for reporting and control access to data where needed.

## 9. Creating the Power BI Report

A Power BI report named Sales Report was created using the Sales Semantic model.
The report uses Direct Lake to access data through the semantic model and display sales information in interactive visuals.
These visuals help users analyse revenue, sales trends, product categories, and regional performance.

Purpose: Present sales insights in an interactive format to support business analysis and decision-making.

## Medallion Architecture

Layer	Table	            Purpose

Bronze	bronze_sales	    Stores raw data
Silver	silver_sales	    Stores cleaned data
Gold	gold_sales_summary	Stores aggregated sales data

## Final Outcome

The project builds a complete analytics solution in Microsoft Fabric, from raw CSV ingestion to interactive Power BI reporting. It combines pipelines, PySpark notebooks, Lakehouse tables, a Warehouse, a semantic model, and a Power BI report.

## Conclusion

This project demonstrates how Microsoft Fabric can be used to ingest, clean, transform, model, and visualise sales data. The final solution provides structured data and interactive reports for exploring sales performance and supporting business decisions.
