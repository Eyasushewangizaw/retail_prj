## Retail Sales ETL Pipeline with PySpark & Spark Cluster
# Project Overview

This project demonstrates a production-style data engineering pipeline built using PySpark and Apache Spark running on Docker.

The pipeline simulates a real-world retail system by:

   * Generating 1,000,000 synthetic retail transactions
    
   * Building a Bronze → Silver → Gold ETL pipeline
    
   * Cleaning messy raw data
    
   * Creating analytics-ready datasets
    
   * Visualizing insights using Power BI

The project demonstrates core data engineering skills such as distributed processing, data quality validation, and scalable ETL design.

# Architecture

<img width="942" height="431" alt="Screenshot 2026-03-10 191028" src="https://github.com/user-attachments/assets/5f7f3ca8-4106-4b93-a94c-f205aa80bdf4" />


# Spark Cluster Setup

A distributed Spark environment is created using Docker.

Components:
  * Spark Master
  * Spark Worker 1
  * Spark Worker 2

Start the cluster:

    docker-compose up -d

Spark UI:

    http://localhost:8080

# Step 1 — Generate Raw Retail Data

The project generates 1 million synthetic retail transactions with intentional data quality issues.

Examples of simulated data problems:

* Duplicate transactions
* Invalid customer ages
* Negative prices
* Invalid discounts
* Shipping dates before order dates

Run the generator:

    python generate_retail_data.py

Output:

    data/raw/retail_sales_raw.csv


# Step 2 - Bronze Layer (Raw Ingestion)

The Bronze layer stores the raw dataset with minimal processing.

Features:

* Explicit schema definition

* Raw CSV ingestion

* Stored as Parquet for performance

# Step 3 — Silver Layer (Data Cleaning)

The Silver layer performs data validation and cleaning.

Cleaning steps include:

# Deduplication

Duplicate transactions removed using transaction_id.

Output:

    data/bronze/retail_sales_bronze.parquet
    
# Data Validation

| Column       | Rule                   |
| ------------ | ---------------------- |
| quantity     | Must be > 0            |
| unit_price   | Must be positive       |
| discount_pct | Must be between 0–100  |
| customer_age | Must be between 15–100 |


# Standardization

Gender standardized to:

    M / F

Payment type standardized to:

    Card / UPI / COD
    
Output:

    data/silver/retail_sales_clean.parquet

# Step 4 — Gold Layer (Business Metrics)

The Gold layer creates aggregated datasets for analytics.

## Daily Sales Metrics

Metrics include:

* Total revenue

* Total orders

* Average order value

      gold/daily_sales_metrics.parquet


## Product Category Performance

Metrics include:

  * Revenue by product category
  
  * Units sold
  
  * Order count

        gold/product_category_performance.parquet

## City-Level Revenue Metrics

Metrics include:

  * Revenue by city
    
  * Order count
    
  * Average order value

        gold/city_revenue_metrics.parquet
