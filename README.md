# 🧠 Mackintosh Risk

### **Next-Generation FinTech Risk Intelligence**
Built by **Kayleighy Mackintosh – Mackintosh Enterprises**

![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)
![License: Apache-2.0](https://img.shields.io/badge/License-Apache--2.0-green.svg)
![R](https://img.shields.io/badge/Made%20with-R-276DC3.svg)
![CI](https://github.com/MackintoshEnterprises/mackintosh-risk/actions/workflows/ci.yml/badge.svg)

---

## 🧩 Overview

**Mackintosh Risk** is an advanced, auditable FinTech analytics framework that unifies **credit risk scoring** and **fraud flagging** within one reproducible R ecosystem.

It blends **machine learning**, **real-time streaming analytics**, and **cloud-native data pipelines** to provide CTO-level confidence in financial decision systems.

Key capabilities:
- 🚀 **Credit risk modeling** — XGBoost-powered PD (probability of default) scoring  
- ⚡ **Streaming fraud detection** — Kafka-based transaction scoring with Snowflake persistence  
- ☁️ **Cloud storage and governance** — AWS S3 Parquet event logs + Snowflake audit tables  
- 🔍 **Explainability** — SHAP-based `/explain` API endpoint  
- 📊 **Observability** — Prometheus metrics and model performance dashboards  
- 🧱 **Compliance-ready architecture** — deterministic builds, schema validation, PII redaction  

---

## 🧠 Architecture

```mermaid
flowchart LR
    subgraph DataLayer["📦 Data Layer"]
      S3[(AWS S3 Parquet Logs)]
      SF[(Snowflake - RISK Schema)]
      K[Kafka REST Proxy]
    end

    subgraph ModelLayer["🧮 Model Layer"]
      M1[XGBoost - Credit PD Model]
      M2[XGBoost - Fraud Detection Model]
    end

    subgraph AppLayer["⚙️ Application Layer"]
      API[Plumber API /health /predict /fraud /explain /metrics]
      WORKER[Fraud Streaming Worker]
    end

    K -->|Transactions| WORKER --> M2
    WORKER -->|Flags + Alerts| SF
    M1 -->|Credit Scoring| API
    API -->|Audit + Decisions| SF
    API -->|Logs| S3
