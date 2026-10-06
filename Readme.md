# ⚡ n8n Advanced Workflows & Automation Blueprints

<div align="center">

![n8n.io](https://img.shields.io/badge/n8n-Workflow_Automation-FF6D5A?style=for-the-badge&logo=n8n&logoColor=white)
![Format](https://img.shields.io/badge/Format-n8n_JSON_v1-000000?style=for-the-badge&logo=json&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)
![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=for-the-badge)

**A production-ready repository containing enterprise-grade n8n JSON blueprints, custom node pipelines, and modular automation architectures.**

[Import Guide](#-how-to-import-blueprints-into-n8n) • [Blueprint Catalog](#-interactive-blueprint-catalog) • [Architecture](#-system-architecture) • [Troubleshooting](#-troubleshooting--faq)

</div>

---

## 📌 Interactive Blueprint Catalog

Select a domain to view available JSON blueprints, descriptions, and structural dependencies:

<details open>
<summary><b>🤖 AI & Agentic Pipelines (<code>/ai-agents</code>)</b></summary>
<br>

| Blueprint | Description | Core Nodes | JSON Link |
| :--- | :--- | :--- | :--- |
| **RAG Knowledge Base Assistant** | Hybrid vector search with LangChain, OpenAI embeddings, and Telegram interface. | `OpenAI`, `Qdrant`, `Telegram` | [`ai-agents/rag-assistant.json`](./ai-agents/) |
| **Multi-Agent Router** | Autonomous router assigning incoming support queries to specialized agent sub-graphs. | `LangChain`, `AI Agent`, `Switch` | [`ai-agents/multi-agent-router.json`](./ai-agents/) |
| **Document Summarizer & Extractor** | Parses uploaded PDFs, extracts structured JSON fields using GPT-4, and emails reports. | `PDF Parser`, `OpenAI`, `Gmail` | [`ai-agents/doc-summarizer.json`](./ai-agents/) |

</details>

<details>
<summary><b>📊 Data Analytics & ETL (<code>/etl-pipelines</code>)</b></summary>
<br>

| Blueprint | Description | Core Nodes | JSON Link |
| :--- | :--- | :--- | :--- |
| **Postgres to BigQuery Sync** | Incremental batch extraction with dead-letter queue handling. | `PostgreSQL`, `BigQuery`, `Cron` | [`etl-pipelines/postgres-to-bigquery.json`](./etl-pipelines/) |
| **Google Sheets Webhook Sync** | Real-time webhook listener to validate, transform, and insert clean data rows. | `Webhook`, `Code (JS)`, `GSheets` | [`etl-pipelines/sheets-webhook-sync.json`](./etl-pipelines/) |
| **MySQL to Redis Cache Invalidation** | Listens for database updates and invalidates corresponding Redis key caches. | `MySQL`, `Redis`, `Function` | [`etl-pipelines/mysql-redis-cache.json`](./etl-pipelines/) |

</details>

<details>
<summary><b>🔔 DevOps & System Monitoring (<code>/devops-alerts</code>)</b></summary>
<br>

| Blueprint | Description | Core Nodes | JSON Link |
| :--- | :--- | :--- | :--- |
| **GitHub Webhook Bot** | Filters pull request/issue events and constructs formatted Slack cards. | `GitHub`, `Slack`, `Filter` | [`devops-alerts/github-slack-bot.json`](./devops-alerts/) |
| **Uptime Monitor & Alerting** | Executes periodic API health checks and dispatches PagerDuty incidents on failure. | `Schedule`, `HTTP Request`, `PagerDuty` | [`devops-alerts/uptime-monitor.json`](./devops-alerts/) |

</details>

<details>
<summary><b>💼 Business Operations & CRM (<code>/crm-automations</code>)</b></summary>
<br>

| Blueprint | Description | Core Nodes | JSON Link |
| :--- | :--- | :--- | :--- |
| **Stripe Invoice Automator** | Captures payment events, compiles HTML-to-PDF invoices, and uploads to Google Drive. | `Stripe`, `HTML-to-PDF`, `GDrive` | [`crm-automations/stripe-invoicing.json`](./crm-automations/) |
| **HubSpot Lead Enrichment** | Enriches new contacts using Clearbit API before sending a summary to sales reps. | `HubSpot`, `HTTP Request`, `SendGrid` | [`crm-automations/hubspot-enrichment.json`](./crm-automations/) |

</details>

---

## 📊 System Architecture

The high-level data flow and processing topology across self-hosted and cloud n8n instances:

```mermaid
flowchart TD
    %% Source Ingestion
    subgraph Ingestion Layer
        A1[🌐 Webhook Triggers] 
        A2[⏰ Schedule / Cron Triggers]
        A3[📥 Polling Triggers]
    end

    %% n8n Orchestration Core
    subgraph n8n Workflow Engine
        B1{🔀 Input Router}
        B2[⚡ Data Transformation Nodes]
        B3[🛡️ Error Handler / Retry Loop]
    end

    %% Execution Targets
    subgraph Processing & Integration
        C1[🤖 AI Models / Vector DBs]
        C2[💾 Databases & Warehouses]
        C3[💬 Chat Platforms & Email]
    end

    A1 --> B1
    A2 --> B1
    A3 --> B1
    
    B1 --> B2
    B2 -->|Success| C1
    B2 -->|Success| C2
    B2 -->|Success| C3
    
    B2 -.->|On Failure| B3
    B3 -.->|Alert| C3