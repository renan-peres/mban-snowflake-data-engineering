### pydata_boston_2025_notebook_to_pipeline


# From Notebook to Pipeline: Hands-On Data Engineering with Python
#### PyData Boston 2025
##### By: Renan Peres
- Github Repository: [https://github.com/Snowflake-Labs/pydata_boston_2025_notebook_to_pipeline](https://github.com/Snowflake-Labs/pydata_boston_2025_notebook_to_pipeline)
- Snowflake 120-day free Account: [https://signup.snowflake.com/?trial=student&cloud=aws&region=us-west-2](https://signup.snowflake.com/?trial=student&cloud=aws&region=us-west-2)
## Lab Overview

This repo contains the companion notebook for the **From Notebook to Pipeline: Hands-On Data Engineering with Python** tutorial at PyData Boston 2025. It contains two files:

* **python_data_pipeline.ipynb** – Jupyter Notebook where we will build an end-to-end data pipeline in Python.
  
* **requirements.txt** – Required packages to build the pipeline **if** you are building in your local notebook environment.

In this notebook, you'll build an end-to-end data pipeline using Python. You'll learn how to:

- Ingest data from CSV files in cloud storage and land it as data in tables
- Transform raw data using a combination of Python and SQL
- Build a 3-tier, automated data transformation pipeline
- Use incremental refresh capabilities to serve fresh, up-to-date data
- Monitor pipeline performance
- **Optional (but recommended)**: Interact with the final data product using AI and semantic models

### Lab Setup

To complete this lab using this Notebook, you will need the following:
- Ability to run Jupyter Notebooks – this lab uses VS Code which has built-in Jupyter Notebook support
- Python 3.10.x (run `python` in your terminal to see which version you have installed)
- pip (or conda)
- Python packages: `snowflake` and `snowflake-snowpark-python`
- A free 120-day Snowflake trial account: [https://tinyurl.com/pydata2025](https://tinyurl.com/pydata2025)
- An Internet connection

## Scenario & Pipeline Architecture

You're a data engineer that works for a global food truck company called Tasty Bytes. Data analysts on your team report on business metrics and product performance on a daily basis, and require fresh, up-to-date data for their reports. To assist them, you'll build a pipeline with the following 3-tier architecture:

**Raw Data: Orders and order details**
- Land raw data from CSVs cloud storage into tables

**Tier 1: Raw Data Enrichment**
- Enrich raw data (order headers) with temporal dimensions
- Enrich raw data (order items) with product details and profit calculations

**Tier 2: Fact Table**
- Join enriched orders data from Tier 1 with enriched items into a unified fact table

**Tier 3: Aggregated Metrics**
- Build table with aggregated daily business metrics (revenue, orders, customers)
- Build table with aggregated product performance metrics (sales, profit by product)

**Extension: AI-assisted report generation**
- Generate semantic model for AI-assisted queries and report generation