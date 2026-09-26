<!-- GUARD AI PROPRIETARY HEADER -->
<div align="center">

# 🛡️ Guard AI
### Enterprise Zero-Trust AI Proxy & EU Compliance Engine

**Designed & Built by [Saad Bilal](https://saadbilal.vercel.app/)**

[![License: Proprietary](https://img.shields.io/badge/License-Proprietary_Commercial-red.svg)](https://github.com/saadbilal/guardai/blob/main/LICENSE)
[![Status: Active Development](https://img.shields.io/badge/Status-Phase_2_Active-sky.svg)](#)
[![Compliance: EU AI Act](https://img.shields.io/badge/EU_AI_Act-Article_10_%26_12_Compliant-teal.svg)](#)

---

### 🔒 PROPRIETARY SOFTWARE NOTICE

> **Notice to all users and visitors:**  
> **Guard AI** is proprietary software owned exclusively by **Saad Bilal**.  
> The source code, architecture, design assets, and documentation contained in this repository are **NOT open-source**. Unauthorised copying, modification, distribution, reverse engineering, or commercial deployment of this codebase—in whole or in part—without express written permission from the copyright owner is strictly prohibited.
>
> 🌐 **Public Live Demo & Documentation:** [https://saadbilal.github.io/guardai/](https://saadbilal.github.io/guardai/)  
> ✉️ **Commercial Licensing & Inquiries:** Contact Saad Bilal via [LinkedIn](https://www.linkedin.com/in/saadbilal/) or [Portfolio](https://saadbilal.vercel.app/)

---

</div>

> **Developer-First Zero-Trust API Proxy & Real-Time EU AI Act Compliance Engine**

## 💡 What is Guard AI?

**Guard AI** is an ultra-low-latency, zero-trust API proxy and compliance engine built for European enterprises, SaaS companies, and developers. It wraps around commercial (OpenAI, Anthropic) and self-hosted (Ollama, vLLM) LLM endpoints with **under 10 lines of code** automatically handling inline PII scrubbing, multi-tenant context isolation, and SHA-256 immutable audit logging.

Deploying Generative AI applications in Europe without strict compliance controls exposes businesses to statutory fines up to **€35 million or 7% of global annual turnover** under the **EU AI Act** and **GDPR**.

Building custom compliance pipelines takes months of legal and engineering work. Guard AI reduces this to a **10-minute integration** with `< 15ms` middleware latency overhead.

## 🌟 Key Features

* 🔒 **Real-Time Inline PII Scrubbing (GDPR Art. 5 & 17):** In-memory detection and anonymization of Names, Email addresses, Phone numbers, IBANs, IP Addresses, and Passports using Microsoft Presidio and spaCy models.

* 🛡️ **Zero-Trust LLM Routing:** Ensures prompt payloads sent to commercial or external LLM backends contain zero unredacted personal identifiers.

* 📜 **EU AI Act Article 12 Audit Logging:** Generates tamper-evident, SHA-256 hash-chained JSON logs tracking model parameters, execution latency, and anonymized PII events.

* 🏢 **Multi-Tenant Context Isolation (RAG Security):** Intercepts Vector DB queries (Qdrant, PostgreSQL `pgvector`) to enforce strict tenant-level metadata isolation filters.

* ⚡ **High-Performance Ingress:** Built on Python 3.11+, FastAPI, and Uvicorn, engineered for high-concurrency asynchronous stream processing.

* 🇪🇺 **Sovereign Cloud Native:** Pre-configured for EU-based routing (e.g., AWS Frankfurt / Azure West Europe) under Zero Data Retention (ZDR) enterprise policies.


## 🛡️ Regulatory Compliance & EU Legal Alignment

Guard AI is built from the ground up to address the strict compliance requirements enforced by European Union regulations for enterprise Generative AI deployments.

### 🇪🇺 EU AI Act Compliance

| EU AI Act Provision | Regulatory Requirement | Guard AI Technical Enforcement |
| :--- | :--- | :--- |
| **Article 12** <br>*(Record-Keeping & Traceability)* | High-risk AI systems must automatically record event logs throughout their lifecycle to guarantee traceability. | **Cryptographic Audit Pipeline:** Every incoming prompt and sanitized output generates an immutable, tamper-evident SHA-256 event log in real-time. |
| **Article 10** <br>*(Data & Data Governance)* | Mandates strict data management, privacy protection, and bias mitigation for data used during inference and training. | **In-Memory PII Scrubbing:** Presidio + spaCy NLP engines strip sensitive entities (Names, IBANs, Emails, Credentials) before payloads reach LLMs. |
| **Article 15** <br>*(Cybersecurity & Data Leakage)* | Requires systems to resist unauthorized data leakage, prompt injection, and cross-tenant context bleeding. | **Multi-Tenant Vector Isolation:** Injected metadata filtering guarantees strict client isolation across RAG vector database queries. |

### 🔒 GDPR (General Data Protection Regulation)

| GDPR Provision | Legal Mandate | How Guard AI Safeguards Your Enterprise |
| :--- | :--- | :--- |
| **Article 5(1)(c)** <br>*(Data Minimization)* | Personal data must be limited strictly to what is necessary for processing. | **Dynamic Anonymization:** Redacts personal identifiers instantly so downstream frontier models receive only anonymized contextual tokens. |
| **Article 32** <br>*(Security of Processing)* | Implement technical measures to maintain data confidentiality and prevent unauthorized access. | **Zero-Trust Reverse Proxy:** Operates on Zero Data Retention (ZDR) routing, acting as an enterprise firewall. |

---


## 🏗️ Architecture Diagram

```
[ Client Application / Web Backend ]
                 │
                 ▼ (REST API / OpenAI Format)
┌─────────────────────────────────────────────────────────────┐
│                       GUARD AI PROXY                        │
│                                                             │
│   ┌────────────────────────┐    ┌────────────────────────┐  │
│   │ In-Memory PII Scrubber │───>│ Multi-Tenant Isolator  │  │
│   │ (Presidio + spaCy)     │    │ (Vector DB Metadata)   │  │
│   └───────────┬────────────┘    └───────────┬────────────┘  │
│               │                             │               │
│               ▼                             ▼               │
│   ┌─────────────────────────────────────────────────────┐   │
│   │        EU AI Act Article 12 Audit Engine            │   │
│   │        (SHA-256 Immutable Hash Chained Logs)        │   │
│   └─────────────────────────────────────────────────────┘   │
└──────────────────────────────┬──────────────────────────────┘
                               │ (Zero Data Retention Route)
                               ▼
            [ Sovereign EU LLM / Enterprise Endpoint ]

```

## 🚀 Quickstart Guide

### Prerequisites

* **Python:** 3.11 or higher

* **Package Manager:** `pip`

### 1. Installation

Clone the repository and set up your Python environment:

```
git clone https://github.com/your-username/guard-ai.git
cd guard-ai

# Create virtual environment
python3 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install required packages
pip install fastapi uvicorn presidio-analyzer presidio-anonymizer pydantic spacy

# Download spaCy language model for PII entity recognition
python3 -m spacy download en_core_web_lg

```

### 2. Run the Gateway

Start the Guard AI proxy server locally:

```
python3 main.py

```

The server will initialize on `http://localhost:8000`.

## 💻 Usage & Verification

Send an OpenAI-compatible payload containing sensitive PII data to Guard AI:

```
curl -X POST "http://localhost:8000/v1/chat/completions" \
  -H "Content-Type: application/json" \
  -H "X-Guard-API-Key: test_secret_key_123" \
  -d '{
    "model": "gpt-4o",
    "messages": [
      {
        "role": "user",
        "content": "Hello, my name is Saad Bilal and my email is saad.bilal@example.com. Please check my invoice balance."
      }
    ]
  }'

```

### Server Output & Audit Event

Guard AI scrubbed the PII in-memory before downstream routing and generated an audit record:

```
{
  "timestamp": "2026-09-24T15:20:00.123456+00:00",
  "event_type": "INFERENCE_REQUEST_PROCESSED",
  "compliance_standards": ["EU_AI_ACT_ART_12", "GDPR_ART_5", "GDPR_ART_17"],
  "tenant_id": "tenant_a1b2c3d4",
  "status_code": 200,
  "performance": {
    "execution_latency_ms": 11.45
  },
  "privacy": {
    "pii_detected": true,
    "entities_scrubbed": ["PERSON", "EMAIL_ADDRESS"],
    "prompt_sha256": "8f921a413d2e4b8a9a91e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b"
  },
  "sovereignty": {
    "routing_region": "eu-central-1 (Frankfurt)",
    "zero_data_retention_active": true
  }
}

```

## 📊 EU AI Act & GDPR Compliance Matrix

| **Regulation** | **Article** | **Requirement** | **How Guard AI Fulfills It** | 
| **GDPR** | Article 5(1)(c) | Data Minimization | Redacts all detected personal identifiers prior to external routing. | 
| **GDPR** | Article 17 | Right to Erasure | Zero persistence of raw user text in logs; vector tenant mapping. | 
| **EU AI Act** | Article 12 | Record-Keeping & Auditability | Automated SHA-256 hashed audit events logging latency, models, and privacy stats. | 
| **EU AI Act** | Article 50 | Transparency Obligations | Appends standardized metadata notifications indicating AI generation. | 

## 🛠️ Tech Stack

* **Language:** Python 3.11+

* **Framework:** FastAPI, Uvicorn

* **PII Engine:** Microsoft Presidio Analyzer & Anonymizer, spaCy (`en_core_web_lg`)

* **Validation:** Pydantic v2

* **Audit & Hashing:** Cryptographic SHA-256 hash chaining

## 🛣️ Development Roadmap

* \[x\] **Phase 1: Core Proxy & PII Engine**

  * Async FastAPI reverse proxy

  * Presidio inline anonymizer middleware

  * SHA-256 compliance audit logging

* \[ \] **Phase 2: Vector Security & Context Isolation**

  * Metadata filtering middleware for Qdrant & PostgreSQL `pgvector`

  * Deletion triggers for RAG pipelines (GDPR Art. 17)

* \[ \] **Phase 3: Dashboard & Automated DPIA Reports**

  * Next.js executive portal for real-time traffic & compliance metrics

  * Single-click Data Protection Impact Assessment (DPIA) PDF exports

* \[ \] **Phase 4: Open-Source SDKs**

  * Python SDK (`pip install guard-ai-python`)

  * Node.js/TypeScript SDK (`npm install @guard-ai/sdk`)


  
### 🚀 Phase 2 Roadmap: Deep Database Integration

Guard AI is currently advancing to **Phase 2**, shifting from prompt-level protection to enterprise database-layer security:

* **Tenant-Based Vector DB Middleware:** Native middleware adapters for **Qdrant**, **pgvector**, and **ChromaDB** that automatically inject `X-Tenant-ID` metadata filters to eliminate cross-tenant data leaks in multi-tenant RAG architectures.
* **Tamper-Proof Audit Vault:** Expanding SHA-256 local logging into an append-only, immutable audit ledger for external compliance verification.
  

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the project repository.

2. Create your feature branch (`git checkout -b feature/NewFeature`).

3. Commit your changes (`git commit -m 'Add NewFeature'`).

4. Push to the branch (`git push origin feature/NewFeature`).

5. Open a Pull Request.

## 📜 License

Distributed under the MIT License. See `LICENSE` for details.
