## 📌 Project Architecture & Data Flow

The platform follows a modern **Medallion Architecture** coupled with an **Multi-Agent Layer**:

1. **Bronze Layer (Raw Storage):** Connects to the Yahoo Finance API (`yfinance`) to execute hybrid extraction of both local Colombian Stock Exchange (BVC) assets (e.g., `ECOPETROL.CO`, `ISA.CO`) and major international equities (e.g., `AAPL`, `TSLA`, `NVDA`). Data is safely archived in its raw semi-structured CSV form within a persistent Google Drive Data Lake.
2. **Silver Layer (Structured Relational Store):** Utilizes **DuckDB** to build a high-performance analytical database. Raw CSV index structures are parsed, schema types are enforced, and data is normalized into an idempotent relational model (`dim_assets` and `fact_historical_prices`) using robust `INSERT OR REPLACE` transactions.
3. **Multi-Agent Layer (Intelligence Hub):** Deploys a **Gemini 2.5 Flash** Multi-agent using the modern `google-genai` SDK. Equipped with native Tool Calling (Function Calling), the Multi-agent autonomously determines when and how to generate optimized SQL queries against the DuckDB Silver Layer, analyzes short-term trends, and outputs deterministic financial decisions.
