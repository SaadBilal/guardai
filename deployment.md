# Guard AI Deployment & Infrastructure Integration Guide

Guard AI is an inline, zero-trust security and compliance proxy engineered for enterprise Generative AI and Retrieval-Augmented Generation (RAG) workloads. It sits between client applications and frontier Large Language Model (LLM) APIs or vector databases to enforce dynamic PII scrubbing, tenant vector isolation, and SHA-256 audit logging in sub-15ms.

This document outlines all supported deployment models to match your enterprise security, sovereignty, and latency requirements.

---

## Deployment Options Matrix

| Deployment Model | Target Audience | Data Isolation | Latency Impact | Management Overhead |
| :--- | :--- | :--- | :--- | :--- |
| **1. Managed SaaS Proxy** | Scale-ups & B2B SaaS | Multi-Tenant Cloud / Isolated Runtime | < 15ms | Zero (Fully Managed) |
| **2. Self-Hosted VPC Container** | Enterprise & Regulated SaaS | Dedicated Private VPC (AWS/GCP/Azure) | < 5ms | Low (Helm / Kubernetes) |
| **3. Air-Gapped On-Premise** | Defense, Banking & Healthcare | 100% Isolated On-Prem Infrastructure | < 2ms | Managed by Client Operations |
| **4. Local Developer Runtime** | Testing & Development | Local Workstation (`localhost`) | < 1ms | Self-Managed (`docker run`) |

---

## Option 1: Managed SaaS Proxy

### Overview
The fastest integration method. Route your API traffic through Guard AI's managed high-availability edge nodes across European data centers (Frankfurt / Dublin). 

### Key Characteristics
* **Zero Data Retention (ZDR):** Payloads are sanitized entirely in memory (`RAM`) and never written to disk or persistent storage.
* **EU Sovereignty:** Hosted on sovereign European cloud infrastructure compliant with GDPR and the EU AI Act.
* **1-Line Integration:** No infrastructure management or code refactoring required.

### Client Integration Example (Python)
Simply update your base API URL endpoint to point to Guard AI's managed proxy gateway:

```python
import openai

# Replace default API endpoint with Guard AI Managed Proxy
client = openai.OpenAI(
    api_key="your-openai-api-key",
    base_url="https://saadbilal.github.io/v1"
)

# Standard API call - Guard AI automatically scrubs PII and logs SHA-256 hashes inline
response = client.chat.completions.create(
    model="gpt-4o",
    messages=[{"role": "user", "content": "Analyze record for John Doe, IBAN: DE89370400440532013000"}]
)
```

---

## Option 2: Self-Hosted Enterprise VPC (Recommended for Enterprise)

### Overview
Deploy Guard AI as a stateless container directly inside your cloud infrastructure (AWS EKS, GCP Cloud Run, Azure AKS, or custom Kubernetes clusters). Data never leaves your corporate perimeter.

### Key Characteristics
* **Complete Data Perimeter:** All prompt processing, Presidio NLP scrubbing, and hashing occur within your private network boundaries.
* **Sub-5ms Network Latency:** Colocate Guard AI nodes in the same region or Availability Zone (AZ) as your application microservices.
* **Auto-Scaling:** Horizontal Pod Autoscaler (HPA) scales container instances based on inbound request rates.

### Kubernetes Deployment via Helm

```yaml
# values.yaml - Guard AI Enterprise Helm Chart
replicaCount: 3

image:
  repository: registry.guardai.io/enterprise/proxy-engine
  tag: "v1.4.0"
  pullPolicy: IfNotPresent

env:
  GUARD_AI_MODE: "ENFORCE"
  PII_SCRUBBING_ENGINE: "PRESIDIO_IN_MEMORY"
  ZERO_DATA_RETENTION: "true"
  LOG_LEVEL: "INFO"
  X_TENANT_ISOLATION: "ENABLED"

resources:
  limits:
    cpu: 2000m
    memory: 4Gi
  requests:
    cpu: 500m
    memory: 1Gi

autoscaling:
  enabled: true
  minReplicas: 3
  maxReplicas: 20
  targetCPUUtilizationPercentage: 70
```

Deploying to your cluster:

```bash
helm repo add guardai https://charts.guardai.io
helm install guard-ai-proxy guardai/guard-ai-engine -f values.yaml --namespace guardai-security --create-namespace
```

---

## Option 3: Air-Gapped / On-Premise Deployment

### Overview
Designed for highly sensitive financial, healthcare, or government environments with zero internet access to third-party endpoints.

### Key Characteristics
* **Local Anonymization & Local Models:** Integrates with locally hosted LLMs (e.g., Llama 3, Mistral via vLLM / Ollama) and local vector databases (Qdrant, pgvector).
* **Cryptographic Event Auditing:** Immutable SHA-256 compliance logs are pushed directly to your internal SIEM (Splunk, Datadog, Elastic).
* **Zero External Dependencies:** Built with embedded NLP models for offline PII detection and redaction.

### Architecture Overview
```
[Client Application]
        │
        ▼ (Internal VPC/LAN Network)
[Guard AI Air-Gapped Proxy Node] ──► [Internal SIEM Log Collector]
        │ (Sanitized Prompt & X-Tenant-ID Filter)
        ▼
[Private LLM Runtime / Local Vector DB]
```

---

## Option 4: Local Developer Environment (`localhost`)

### Overview
Used by internal engineering teams for rapid prototyping, debugging, and offline integration testing.

### Quickstart via Docker

Run the proxy container locally on port `8080`:

```bash
docker run -d \
  --name guardai-local \
  -p 8080:8080 \
  -e GUARD_AI_ENV=development \
  -e ZERO_DATA_RETENTION=true \
  registry.guardai.io/public/proxy-engine:latest
```

Connect your application or playground to the local proxy runtime:

```bash
curl -X POST http://localhost:8080/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer sk-test-key" \
  -H "X-Tenant-ID: tenant_acme_corp_01" \
  -d '{
    "model": "gpt-4o",
    "messages": [{"role": "user", "content": "Test prompt with email test@company.com"}]
  }'
```

---

## Compliance & Security Warranties

Regardless of the selected deployment model, Guard AI enforces the following core security guarantees:

1. **Sub-15ms Processing Overhead:** High-throughput Rust/C++ parsing engine ensures real-time user experiences.
2. **Zero Data Retention (ZDR):** Prompts, embeddings, and response payloads exist in volatile memory (`RAM`) strictly for the duration of the request lifecycle.
3. **EU AI Act & GDPR Ready:** Built-in cryptographic event logging fulfills Article 12 compliance logging requirements and Article 10 data isolation standards.