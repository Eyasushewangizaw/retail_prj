
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

<img width="1917" height="711" alt="Screenshot 2026-03-10 042303" src="https://github.com/user-attachments/assets/27eb5434-e1b5-42fc-a5bc-ec80cf12b561" />


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

# Pipeline Execution (PowerShell)

<img width="1917" height="1026" alt="Screenshot 2026-03-09 173103" src="https://github.com/user-attachments/assets/7ff37293-909c-459f-8991-be4c23ca8762" />

<img width="1159" height="303" alt="Screenshot 2026-03-09 173142" src="https://github.com/user-attachments/assets/eb4fa166-4cea-4de0-985f-c4d8906ec7b8" />

<img width="888" height="298" alt="Screenshot 2026-03-09 175100" src="https://github.com/user-attachments/assets/61f666b6-5d1c-4fd4-b4b7-cb1607a18a60" />

<img width="1915" height="832" alt="Screenshot 2026-03-10 015810" src="https://github.com/user-attachments/assets/b02577d3-e250-44ab-995c-21ff596adcd0" />

<img width="1882" height="989" alt="Screenshot 2026-03-10 015638" src="https://github.com/user-attachments/assets/c29daed4-e13d-46ec-9126-810da30957eb" />

<img width="1882" height="989" alt="Screenshot 2026-03-10 015638" src="https://github.com/user-attachments/assets/c29daed4-e13d-46ec-9126-810da30957eb" />

<img width="1918" height="981" alt="Screenshot 2026-03-10 015733" src="https://github.com/user-attachments/assets/4da4a121-72c8-42e1-9a54-a0285a6e0760" />

<img width="1909" height="987" alt="Screenshot 2026-03-10 015751" src="https://github.com/user-attachments/assets/267a6ce0-3afc-4c72-946a-959b0cb1f4b5" />


# Power Bi

## Sales by Location (Map)

* Shows order distribution across US cities

* Demonstrates geographic analytics.

<img width="1313" height="752" alt="Screenshot 2026-03-11 031758" src="https://github.com/user-attachments/assets/884ac461-3695-476f-8686-51a70a29f186" />

## Orders by Year (Trend)

* Shows trend over time

* Useful for sales forecasting or seasonality analysis.

<img width="1316" height="758" alt="Screenshot 2026-03-11 031731" src="https://github.com/user-attachments/assets/c0cbacec-5fb6-471f-98fc-78e5efb49f80" />

## Revenue by Product Category

Clear comparison of:

* Electronics (highest)

* Furniture

* Sports

* Fashion

* Grocery

<img width="1324" height="771" alt="Screenshot 2026-03-11 031658" src="https://github.com/user-attachments/assets/3f4dde5b-0b69-4d8c-88dd-985a3c950356" />













