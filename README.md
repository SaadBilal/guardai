# 🛡️ Guard AI (`guard-ai`)

> **Developer-First Zero-Trust API Proxy & Real-Time EU AI Act Compliance Engine**

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Python Version](https://img.shields.io/badge/python-3.11%2B-blue)](https://www.python.org/)
[![EU AI Act Compliant](https://img.shields.io/badge/EU%20AI%20Act-Art.%2012%2F17%2F50-emerald)](https://artificialintelligenceact.eu/)
[![GDPR Compliant](https://img.shields.io/badge/GDPR-Art.%205%2F17%2F32-teal)](https://gdpr.eu/)

**Guard AI** is an ultra-low-latency, zero-trust API proxy and compliance engine built for European enterprises and developers. It wraps around commercial (OpenAI, Anthropic) and self-hosted (Ollama, vLLM) LLM endpoints with **under 10 lines of code** automatically handling inline PII scrubbing, multi-tenant context isolation, and SHA-256 immutable audit logging.

---

## 🌟 Why Guard AI?

Deploying LLMs in Europe without strict compliance controls exposes businesses to statutory fines up to **€35 Million or 7% of global annual turnover** under the **EU AI Act** and **GDPR**. 

Building custom compliance pipelines takes months. Guard AI cuts this down to **10 minutes** with `< 15ms` middleware latency.

### Key Capabilities

* 🔒 **Real-Time PII Scrubbing (GDPR Art. 5 & 17):** In-memory detection and anonymization of Names, Emails, Phone Numbers, IBANs, IP Addresses, and Passports using Microsoft Presidio + spaCy.
* 🛡️ **Zero-Trust LLM Routing:** Ensures prompt payloads sent to commercial LLMs contain zero unredacted personal identifiers.
* 📜 **EU AI Act Article 12 Audit Logging:** Generates tamper-evident, SHA-256 hash-chained JSON logs tracking model parameters, latency, and PII events.
* 🏢 **Multi-Tenant Context Isolation (RAG):** Intercepts Vector DB queries (Qdrant, pgvector) to enforce strict tenant-level isolation filters.
* ⚡ **High-Performance Ingress:** Built on FastAPI & Uvicorn, engineered for asynchronous stream processing.

---
## 🚀 Quickstart

### Prerequisites

* Python 3.11 or higher
* `pip` package manager

### 1. Installation

Clone the repository and install the dependencies:

```bash
git clone [https://github.com/your-username/guard-ai.git](https://github.com/your-username/guard-ai.git)
cd guard-ai

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install required packages
pip install -r requirements.txt

# Download NLP model for PII recognition
python -m spacy download en_core_web_lg
