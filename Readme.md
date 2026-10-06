# ⚡ n8n Advanced Workflows & Automation Blueprints

[![n8n.io](https://img.shields.io/badge/n8n-Workflow_Automation-FF6D5A?style=for-the-badge&logo=n8n&logoColor=white)](https://n8n.io)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.style=for-the-badge)](LICENSE)
[![JSON Blueprints](https://img.shields.io/badge/Format-n8n_JSON_v1-green?style=for-the-badge&logo=json)](https://docs.n8n.io/workflows/export-import/)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=for-the-badge)](CONTRIBUTING.md)

A production-ready repository containing optimized **n8n workflow JSON blueprints**, custom node configurations, and automated enterprise pipelines. Copy, paste, or import these blueprints directly into your n8n instance.

---

## 📌 Interactive Blueprint Catalog

Click on any category to view available workflow blueprints and their JSON file paths.

<details open>
<summary><b>🤖 AI & Agentic Pipelines (`/ai-agents`)</b></summary>

| Blueprint Name | Description | JSON Link |
| :--- | :--- | :--- |
| **RAG Knowledge Base Assistant** | Connects OpenAI, Qdrant Vector DB, and Telegram for automated Q&A. | [`ai-agents/rag-assistant.json`](./ai-agents/) |
| **Multi-Agent Orchestrator** | Uses LangChain nodes to route customer support tickets to specialized AI agents. | [`ai-agents/multi-agent-router.json`](./ai-agents/) |

</details>

<details>
<summary><b>📊 Data Analytics & ETL (`/etl-pipelines`)</b></summary>

| Blueprint Name | Description | JSON Link |
| :--- | :--- | :--- |
| **Postgres to BigQuery Sync** | Scheduled incremental batch ETL pipeline with error handling. | [`etl-pipelines/postgres-to-bigquery.json`](./etl-pipelines/) |
| **Google Sheets Webhook Sync** | Real-time webhook listener to transform and append data to Google Sheets. | [`etl-pipelines/sheets-webhook-sync.json`](./etl-pipelines/) |

</details>

<details>
<summary><b>🔔 DevOps & System Monitoring (`/devops-alerts`)</b></summary>

| Blueprint Name | Description | JSON Link |
| :--- | :--- | :--- |
| **GitHub Webhook Bot** | Listens to PR/Issue events and posts structured notifications to Slack. | [`devops-alerts/github-slack-bot.json`](./devops-alerts/) |
| **Uptime Monitor & PagerAlert** | Ping API endpoints every 60s and trigger incident alerts if HTTP status != 200. | [`devops-alerts/uptime-monitor.json`](./devops-alerts/) |

</details>

<details>
<summary><b>💼 Business & CRM Operations (`/crm-automations`)</b></summary>

| Blueprint Name | Description | JSON Link |
| :--- | :--- | :--- |
| **Stripe Invoice Automator** | Captures payment intent webhooks and generates PDF invoices in Google Drive. | [`crm-automations/stripe-invoicing.json`](./crm-automations/) |

</details>

---

## 📊 System Architecture & Import Flow

Below is the execution model showing how these JSON blueprints interact with your n8n instance and external infrastructure:

```mermaid
flowchart TD
    %% Import Phase
    subgraph 1. Repository Blueprint
        A[📄 JSON Blueprint File] -->|Copy Raw JSON or Import File| B(💻 n8n Canvas Editor)
    end

    %% Configuration
    subgraph 2. Setup & Credentials
        B --> C{🔑 Credential Binding}
        C -->|Add API Keys| D[🔐 n8n Vault / Environment Variables]
    end

    %% Execution Engine
    subgraph 3. Pipeline Execution
        D --> E[🌐 Trigger Node: Webhook / Cron / App Event]
        E --> F[🔀 Transformation & Business Logic Nodes]
        F --> G[🤖 AI / Database / API Integration Nodes]
    end

    %% Outputs
    G --> H[✅ Execution Log / Webhook Response]