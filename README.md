# DBT & BigQuery Analytics Project


This project demonstrates the integration of **dbt** (Data Build Tool) with **Google BigQuery** to create a simple yet powerful analytics pipeline. The purpose of this project is to explore the end-to-end process of building an ETL pipeline, incorporating version control with **Git** and **GitHub**, and applying best practices for data transformations, testing, and version tracking.


## Table of Contents

1. [Project Setup](#project-setup)
2. [BigQuery Configuration](#bigquery-configuration)
3. [DBT Configuration](#dbt-configuration)
4. [Models Overview](#models-overview)
    - [Staging Model](#staging-model-modelsstagingstg_salessql)
    - [Final Model](#final-model-modelsmartssales_finalsql)
5. [Testing](#testing)
6. [Version Control](#version-control)
7. [Next Steps](#next-steps)


## Project Setup

This project integrates dbt with Google BigQuery for data transformation and aggregation. The setup includes:

- **dbt version**: [Include version here if possible]
- **Google Cloud Platform**: BigQuery for storing and querying data
- **Version Control**: Git for tracking changes, hosted on GitHub
- **Python Environment**: Make sure you have Python 3.x installed along with necessary dependencies.



## BigQuery Configuration

I have successfully configured **dbt** to connect to **Google BigQuery**. Authentication was handled using the **Google Cloud SDK**, and I verified the connection by querying a dataset in BigQuery. A sample dataset of **1 million rows** was generated to simulate real-world data for testing and aggregation.



### Simple Macro

A macro was created to dynamically partition data based on the **date** column. The partitioning is done into two categories:

1. **Recent**
2. **Historical**

This allows for more efficient queries by segmenting the dataset based on temporal data.

## Models Overview

### Staging Model: `models/staging/stg_sales.sql`

The **staging model** is the first layer in the dbt transformation pipeline. It reads the raw sales data from BigQuery's `raw_sales` table and applies minimal transformations. This model serves as the foundation for further data aggregation and analysis.

- **Input**: `raw_sales` table in BigQuery  
- **Output**: Cleaned data for downstream consumption

### Final Model: `models/marts/sales_final.sql`

The **final model** aggregates the sales data by country and product, providing a ready-to-use table for analytics and reporting. This model takes the results from the staging model and applies further transformations.

- **Input**: Staged data from `stg_sales`  
- **Output**: Final sales data aggregated by country and product

## Testing

To ensure data quality, I have created simple tests using dbt's built-in testing capabilities. The tests check that the following columns in the final model (`sales_final`) do not contain any null values:


- `country`
- `total_orders`

These tests help ensure that the final data model is clean and consistent, providing accurate insights for decision-making.

## Version Control

This project is fully tracked with **Git** and hosted on **GitHub**. Here's how version control is integrated:

1. **Initial Commit**: The project was set up and pushed to GitHub.
2. **Commit History**: As changes were made (e.g., model creation, macro implementation, and testing), each change was tracked and pushed to the repository.
3. **Branching and Merging**: For future work, branching strategies can be introduced to maintain different development environments.

## Next Steps

- Add more data sources and models.
- Implement advanced tests (e.g., relationships, accepted values).
- Schedule dbt runs using a workflow orchestration tool (e.g., Airflow or dbt Cloud).
- Incorporate snapshots for slowly changing dimensions (SCDs).
- Explore deployment best practices.
