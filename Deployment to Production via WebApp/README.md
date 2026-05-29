# ☁️ Phase 5: WebApp Architecture & Prototypical Deployment

This section covers the implementation of a decoupled microservices architecture designed to serve the Multi-Agent Trading System. The system features a **FastAPI Asynchronous Backend Engine** and a **Streamlit Interactive Dashboard Frontend**, integrated dynamically within a Google Colab ecosystem and securely exposed via a reverse-proxy tunnel (`localtunnel`).

```                 ┌──────────────────────────────────────────────┐
                    │               Google Drive                   │
                    │         (Persistent Data Lake)               │
                    │           └─ agent_cache.json                │
                    └──────────────────────┬───────────────────────┘
                                           │ Read-Only (Poll)
                                           ▼
┌──────────────────────┐        ┌──────────────────────┐        ┌──────────────────────┐
│  Localtunnel Proxy   │        │  FastAPI Core API    │        │ Streamlit UI Engine  │
│  (Public Gateway)    │◄──────►│     (Port 8000)      │◄──────►│     (Port 8501)      │
│                   )  │  HTTP  │  - Signal Endpoints  │  HTTP  │  - Asset Monitor     │
│  [Secured via IP]    │        │  - Conversational LLM│        │  - Risk Management   │
└──────────────────────┘        └──────────────────────┘        └──────────────────────┘

---

## 5.1 Environment Setup & Core Dependencies

To construct the decoupled application layer and bridge local network stacks out of the virtualized environment, we provision Python framework constraints alongside Node.js-based routing networks.

## 5.2 Backend Service Infrastructure (`main.py`)

The backend layer is architected via **FastAPI** to expose high-performance RESTful APIs. It implements strict data validation schemas using `pydantic` and acts as the execution layer for parsing, combining, and orchestrating downstream agent consensus policies.

### Architectural Logic Highlights:
* **Payload Sanitation & Parsing Engine:** Automatically extracts, formats, and sanitizes raw JSON block text (stripping markdown syntax wraps like ` ```json `) cached by previous execution cycles in the Google Drive Data Lake.
* **Agent Consensus & Conflict Resolution Algorithm:** Integrates deterministic logic evaluating the outputs of the **Basic AI Agent** and **Advanced AI Agent**. If an analytical divergence is flagged, the **Portfolio Manager Agent** triggers an override pipeline, favoring the deeper mathematical metrics processed via the DuckDB indexing system.
* **Resilience & Fallback Matrix:** Implements a structured graceful degradation fallback mechanism (`has_data: False`) to catch cache misses or unindexed tickers without throwing breaking HTTP 500 runtime faults.

## 5.3 Interactive Frontend User Interface (`app.py`)

The presentation layer is developed in **Streamlit**, offering an analytical cockpit for algorithmic execution tracking. The view layout uses modern UI modules organized across distinct, componentized tabs.

### Module Configuration:
1. **Dynamic Control Sidebar:** Includes a batch asset processing array containing 30 global and local stock market symbols (`AVAILABLE_ASSETS`). It features a global state macro checkbox (`Select all 30 assets`) that dynamically handles massive lookups without raising race conditions or execution bugs.
2. **Multi-Agent Asset Monitor Tab:** Uses explicit state containers (`st.expander`) and clean async HTTP queries to visually contrast agent reasoning side-by-side using unified `st.metric` indicators and conditional rendering markers (`st.success`, `st.error`, `st.warning`).
3. **Portfolio Monitoring & Risk Rules Tab:** Maps real-time data checkpoints, maximum drawdowns, and structural protection alerts managed down-stream via DuckDB.
4. **Conversational Interactive Console Tab:** Simulates asynchronous agent-to-user chat interaction with stateful history maintenance preserved inside `st.session_state`.

## 5.4 Asynchronous Infrastructure Execution & Network Tunneling

Because Google Colab operates within ephemeral, isolated virtual machines, running network daemons directly requires decoupling standard interactive shell blockades. We handle this via `nohup` (No Hang Up) sub-processes and expose internal ports via a reverse-proxy topology.
