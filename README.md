# ❄️ From Notebook to Pipeline: Hands-On Data Engineering with Python

[![PyData Boston 2025](https://img.shields.io/badge/PyData-Boston%202025-blue)](https://pydata.org/)
[![Snowflake](https://img.shields.io/badge/Powered%20by-Snowflake-29B5E8)](https://www.snowflake.com/)
[![Python 3.10+](https://img.shields.io/badge/Python-3.10+-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

> **Author:** Renan Peres  
> **Event:** PyData Boston 2025

---

## 📋 Table of Contents

- [Overview](#-overview)
- [What You'll Learn](#-what-youll-learn)
- [Prerequisites](#-prerequisites)
- [Quick Start](#-quick-start)
- [Project Structure](#-project-structure)
- [Pipeline Architecture](#-pipeline-architecture)
- [Resources](#-resources)

---

## 🎯 Overview

This repository contains the companion notebook for the **"From Notebook to Pipeline: Hands-On Data Engineering with Python"** tutorial at PyData Boston 2025.

Build a complete, production-ready data pipeline using Python and Snowflake—transforming raw CSV data into actionable business insights with automated incremental refreshes.

### 🔗 Quick Links

| Resource | Link |
|----------|------|
| 📓 GitHub Repository | [Snowflake-Labs/pydata_boston_2025_notebook_to_pipeline](https://github.com/Snowflake-Labs/pydata_boston_2025_notebook_to_pipeline) |
| ☁️ Snowflake Free Trial (120 days) | [Sign Up Here](https://signup.snowflake.com/?trial=student&cloud=aws&region=us-west-2) |
| 🎥 Workshop Tutorial: Hands-On Data Engineering with Python  | [Youtube Video](https://www.youtube.com/watch?v=Rj4_atYG3MY&list=PLGVZCDnMOq0rhHGZp727T3aRoUYwXXxQJ&index=6) |
| 🎥 Tutorial: Create External Users in Snowflake | [Youtube Video](https://www.youtube.com/watch?v=TqDXlVwoz1c) |

---

## 📚 What You'll Learn

By completing this tutorial, you will be able to:

- ✅ **Ingest data** from CSV files stored in cloud storage (AWS S3) into Snowflake tables
- ✅ **Transform raw data** using both Python (Snowpark) and SQL approaches
- ✅ **Build a 3-tier automated pipeline** using Snowflake Dynamic Tables
- ✅ **Leverage incremental refresh** to process only changed data efficiently
- ✅ **Monitor pipeline performance** through refresh history and metrics
- ✅ **Create AI-powered insights** using semantic models and Snowflake Intelligence *(optional)*

---

## 🛠 Prerequisites

| Requirement | Details |
|-------------|---------|
| **Python** | Version 3.10.x or higher |
| **Package Manager** | pip or conda |
| **IDE** | VS Code with Jupyter extension (recommended) |
| **Snowflake Account** | [Free 120-day trial](https://tinyurl.com/pydata2025) |
| **Internet Connection** | Required for Snowflake connectivity |

### Required Python Packages

```bash
snowflake-snowpark-python>=1.11.0
snowflake-core>=0.6.0
pandas>=1.5.0
python-dotenv>=1.0.0  # for loading .env into the notebook
```

---

## 🚀 Quick Start

### Option A: Local Development (Intermediate/Advanced)

#### Using pip (classic)
```bash
# 1. Clone the repository
git clone https://github.com/Snowflake-Labs/pydata_boston_2025_notebook_to_pipeline.git
cd pydata_boston_2025_notebook_to_pipeline

# 2. Create and activate virtual environment
python3 -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate

# 3. Install dependencies
pip install --upgrade pip
pip install -r requirements.txt

# 4. Verify installation
python -c "from snowflake.snowpark import Session; from snowflake.core import Root; print('✅ Installation successful!')"

# 5. Open the notebook in VS Code and start coding!
```

#### Using uv (fast Python package manager)
```bash
# 0. Install uv (Linux/macOS)
curl -LsSf https://astral.sh/uv/install.sh | sh
# Windows users: see https://docs.astral.sh/uv/installing/ for options

# 1. Clone the repository
git clone https://github.com/Snowflake-Labs/pydata_boston_2025_notebook_to_pipeline.git
cd pydata_boston_2025_notebook_to_pipeline

# 2. Create a virtual environment with uv
uv venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate

# 3. Install dependencies (reads requirements.txt)
uv pip install -r requirements.txt

# 4. Verify installation (without activating, you can also do: `uv run ...`)
python -c "from snowflake.snowpark import Session; from snowflake.core import Root; print('✅ Installation successful!')"
# Or
uv run -c "from snowflake.snowpark import Session; from snowflake.core import Root; print('✅ Installation successful!')"

# 5. Open the notebook in VS Code and start coding!
```

### Option B: Snowflake Notebooks (Beginner-Friendly)

1. Log into your [Snowflake account](https://app.snowflake.com/)
2. Navigate to **Projects** → **Notebooks**
3. Click **+ Notebook** → **Import .ipynb file**
4. Configure: Database: `SNOWFLAKE_LEARNING_DB`, Schema: `PUBLIC`, Runtime: `Run on warehouse`
5. Install packages via the **Packages** dropdown: `snowflake`, `snowflake-snowpark-python`

---

## 📁 Project Structure

```
data_engineering_snowflake_pipeline/
├── 📓 cloud_data_pipeline.ipynb    # Main tutorial notebook
├── 📄 README.md                    # This file
├── 📋 requirements.txt             # Python dependencies
├── 📂 data/                        # Sample data files (if any)
├── 📂 img/                         # Documentation images
└── .env                            # Local-only credentials (not committed)
```

> Tip: Add `.env` to your `.gitignore` to avoid committing secrets.

---

## 🔐 Environment Variables (.env)

Create a local `.env` file to avoid hardcoding Snowflake credentials:

```ini
SNOWFLAKE_ACCOUNT=your_account
SNOWFLAKE_USER=your_username
SNOWFLAKE_PASSWORD=your_password
SNOWFLAKE_ROLE=ACCOUNTADMIN
SNOWFLAKE_WAREHOUSE=COMPUTE_WH
```

Use `python-dotenv` in the notebook to load these values:

```python
from dotenv import load_dotenv
import os

load_dotenv()
connection_parameters = {
    "account": os.getenv("SNOWFLAKE_ACCOUNT"),
    "user": os.getenv("SNOWFLAKE_USER"),
    "password": os.getenv("SNOWFLAKE_PASSWORD"),
    "role": os.getenv("SNOWFLAKE_ROLE"),
    "warehouse": os.getenv("SNOWFLAKE_WAREHOUSE"),
}
```

---

## 🏗 Pipeline Architecture

You'll build a pipeline for **Tasty Bytes**, a global food truck company that needs fresh, daily business metrics.

### Data Flow Diagram

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                              DATA PIPELINE                                   │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  ╔═══════════════╗                                                          │
│  ║   RAW ZONE    ║  ← CSV files from AWS S3                                 │
│  ╠═══════════════╣                                                          │
│  ║ order_header  ║  ~248M rows                                              │
│  ║ order_detail  ║  ~618M rows                                              │
│  ║ menu          ║  ~287 rows                                               │
│  ╚═══════╤═══════╝                                                          │
│          │                                                                  │
│          ▼                                                                  │
│  ╔═══════════════════════════════════════╗                                  │
│  ║           TIER 1: ENRICHMENT          ║  ← 12-hour lag                   │
│  ╠═══════════════════════════════════════╣                                  │
│  ║ orders_enriched      │ Temporal dims, │                                  │
│  ║                      │ discount flags │                                  │
│  ║───────────────────────────────────────║                                  │
│  ║ order_items_enriched │ Product info,  │                                  │
│  ║                      │ profit calcs   │                                  │
│  ╚═══════════════╤═══════════════════════╝                                  │
│                  │                                                          │
│                  ▼                                                          │
│  ╔═══════════════════════════════════════╗                                  │
│  ║         TIER 2: FACT TABLE            ║  ← Downstream lag                │
│  ╠═══════════════════════════════════════╣                                  │
│  ║ order_fact           │ Unified view   │                                  │
│  ║                      │ of all orders  │                                  │
│  ╚═══════════════╤═══════════════════════╝                                  │
│                  │                                                          │
│                  ▼                                                          │
│  ╔═══════════════════════════════════════╗                                  │
│  ║      TIER 3: AGGREGATED METRICS       ║  ← Downstream lag                │
│  ╠═══════════════════════════════════════╣                                  │
│  ║ daily_business_metrics │ Revenue,     │                                  │
│  ║                        │ orders, etc. │                                  │
│  ║────────────────────────────────────────║                                  │
│  ║ product_performance    │ Sales,       │                                  │
│  ║ _metrics               │ profit/item  │                                  │
│  ╚═══════════════════════════════════════╝                                  │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Pipeline Tiers Explained

| Tier | Purpose | Tables | Refresh Strategy |
|------|---------|--------|------------------|
| **Raw** | Land source data | `order_header`, `order_detail`, `menu` | Manual/Batch |
| **Tier 1** | Enrich & clean | `orders_enriched`, `order_items_enriched` | 12-hour lag |
| **Tier 2** | Join & unify | `order_fact` | Downstream |
| **Tier 3** | Aggregate | `daily_business_metrics`, `product_performance_metrics` | Downstream |

---

## 📖 Resources

### Documentation
- [Snowflake Dynamic Tables](https://docs.snowflake.com/en/user-guide/dynamic-tables-intro)
- [Snowpark Python Developer Guide](https://docs.snowflake.com/en/developer-guide/snowpark/python/index)
- [Snowflake Python API Reference](https://docs.snowflake.com/developer-guide/snowflake-python-api/reference/latest/index)
- [Snowflake Intelligence](https://docs.snowflake.com/en/user-guide/snowflake-cortex/snowflake-intelligence)

### Learning
- [Coursera: Snowflake Data Engineering Professional Certificate](https://www.coursera.org/professional-certificates/snowflake-data-engineering)
- [Snowflake Developers YouTube Channel](https://www.youtube.com/channel/UCxgY7r-o_ql8ADIdyiQr3Zw)
- [Snowflake Developer Hub](https://developers.snowflake.com)

### Community
- [Snowflake-Labs GitHub](https://github.com/Snowflake-Labs)