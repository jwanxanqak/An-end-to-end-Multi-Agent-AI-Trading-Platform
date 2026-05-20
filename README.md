# Trading Multi-Agent (v1)

An end-to-end Multi-Agent AI Trading Platform designed to extract financial market data, build a structured relational data store using DuckDB, and deploy an intelligent, autonomous AI Multi-Agent powered by Gemini 2.5 Flash to perform technical analysis, query data via tool use (function calling), and generate structured quantitative trading recommendations.

## 📌 Project Architecture & Data Flow

The platform follows a modern **Medallion Architecture** coupled with an **Multi-Agent Layer**:

1. **Bronze Layer (Raw Storage):** Connects to the Yahoo Finance API (`yfinance`) to execute hybrid extraction of both local Colombian Stock Exchange (BVC) assets (e.g., `ECOPETROL.CO`, `ISA.CO`) and major international equities (e.g., `AAPL`, `TSLA`, `NVDA`). Data is safely archived in its raw semi-structured CSV form within a persistent Google Drive Data Lake.
2. **Silver Layer (Structured Relational Store):** Utilizes **DuckDB** to build a high-performance analytical database. Raw CSV index structures are parsed, schema types are enforced, and data is normalized into an idempotent relational model (`dim_assets` and `fact_historical_prices`) using robust `INSERT OR REPLACE` transactions.
3. **Multi-Agent Layer (Intelligence Hub):** Deploys a **Gemini 2.5 Flash** Multi-agent using the modern `google-genai` SDK. Equipped with native Tool Calling (Function Calling), the Multi-agent autonomously determines when and how to generate optimized SQL queries against the DuckDB Silver Layer, analyzes short-term trends, and outputs deterministic financial decisions.

---

## 🛠️ Tech Stack

* **Core AI Engine:** Google GenAI SDK (`google-genai`), `gemini-2.5-flash` (with strict JSON response schemas and system instruction constraints).
* **Database & Analytical Engine:** DuckDB (OLAP-optimized, fast vectorized execution engine, embedded persistence).
* **Data Processing & Engineering:** Pandas, NumPy, Python 3.12.
* **Financial Extraction:** Yahoo Finance API (`yfinance`).
* **Storage / Environment:** Google Colab, Google Drive (Persistent Data Lake Storage).
* **Visualization:** Matplotlib, Seaborn.

---

## 📂 Project Structure & Database Schema

### Relational Model Design

#### 1. `dim_assets` (Dimension Table)
Stores descriptive metadata for all monitored financial tokens.
* `ticker` (VARCHAR, Primary Key) - Cleaned ticker handle.
* `asset_name` (VARCHAR) - Full name of the company or equity.
* `market` (VARCHAR) - Market categorization (`BVC` for Colombian market, `GLOBAL` for international equities).
* `currency` (VARCHAR) - Trading currency (`COP`, `USD`).

#### 2. `fact_historical_prices` (Fact Table)
Stores structured granular pricing history.
* `ticker` (VARCHAR, Primary Key / Foreign Key)
* `date` (DATE, Primary Key) - Trading date calendar indicator.
* `open` (DOUBLE) - Opening price.
* `high` (DOUBLE) - Daily session high.
* `low` (DOUBLE) - Daily session low.
* `close` (DOUBLE) - Final session close price.
* `adj_close` (DOUBLE) - Adjusted close price for dividends/splits.
* `volume` (BIGINT) - Volume of shares traded.
* `ingestion_timestamp` (TIMESTAMP) - Audit tracking indicator for incremental loads.

---

## 🚀 Step-by-Step Setup Guide

### 1. Persistent Storage Setup
Ensure your Google Drive is mounted within Google Colab to preserve extracted raw data and the DuckDB analytical binary file:
```python
from google.colab import drive
import os

drive.mount('/content/drive')
BASE_PATH = "/content/drive/MyDrive/Trading_Agent_POCv1"
os.makedirs(os.path.join(BASE_PATH, "data", "raw"), exist_ok=True)
os.makedirs(os.path.join(BASE_PATH, "db"), exist_ok=True))

