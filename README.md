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
