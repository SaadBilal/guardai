# Guard AI: Enterprise Sovereign AI Governance & Zero-Trust Middleware Framework

> **A Cryptographic & Regulatory Compliance Architecture for EU AI Act, GDPR, PECA, and PDPB Enforcement**

[![Target Standards](https://img.shields.io/badge/Compliance-EU%20AI%20Act%20%7C%20GDPR%20%7C%20PECA%20%7C%20PDPB-0284c7?style=flat-svg)](https://github.com/saadbilal/guardai)
[![Latency](https://img.shields.io/badge/Latency-%3C%2015ms%20Enforced-10b981?style=flat-svg)](#4-key-performance-benchmarks)
[![Security Architecture](https://img.shields.io/badge/Architecture-Zero--Trust%20Proxy-6366f1?style=flat-svg)](#2-technical-system-architecture)

---

## Executive Summary

The rapid integration of Generative AI (GenAI) and Large Language Models (LLMs) into enterprise workflows has created a major regulatory and security liability. Organizations processing customer, financial, and public sector data face three core attack surfaces:

1. **Unintentional PII/PHI Data Exfiltration:** Plaintext queries routed to foreign cloud providers violate cross-border data transfer laws.
2. **Adversarial Exploitation:** Direct prompt injections, indirect jailbreaks, and system prompt overrides compromise enterprise logic.
3. **Regulatory Non-Compliance:** Stiff statutory penalties under the **European Union Artificial Intelligence Act (EU AI Act)**, **GDPR**, Pakistan's **Prevention of Electronic Crimes Act (PECA 2016/2025)**, and the **Personal Data Protection Bill (PDPB)**.

**Guard AI** is a zero-trust proxy middleware engineered to operate at the ingress/egress boundaries of enterprise applications. Operating at **sub-15ms processing latency**, Guard AI redacts Personally Identifiable Information (PII), blocks adversarial prompts, guarantees sovereign data residency, and maintains SHA-256 hash-chained immutable audit logs for regulatory accountability.

---

## 1. Statutory & Regulatory Alignment Matrix

Guard AI converts regulatory statutes into deterministic code constraints across European Union and Pakistani legal frameworks.

| Jurisdiction | Statute / Legal Article | Regulatory Requirement | Guard AI Technical Enforcement Mechanism |
| :--- | :--- | :--- | :--- |
| **European Union** | **EU AI Act (Art. 9, 10 & 14)** | Risk management, data governance, and continuous human oversight for High-Risk AI Systems. | Dynamic risk scoring on input vectors, automated context bounding, and execution of deterministic fallback mechanisms for anomalous queries. |
| **European Union** | **GDPR (Art. 5, 32 & 44)** | Data minimization, protection against unauthorized processing, and strict cross-border transfer limits. | On-premise / sovereign cloud zero-trust proxying with zero-persistence PII sanitization prior to external API dispatch. |
| **Pakistan** | **PECA (Sec. 14, 16 & 21)** | Strict penalties for identity fraud, unauthorized access, and illegal data interception. | Real-time Regex & Named Entity Recognition (NER) tokenization for 13-digit CNIC codes, phone numbers, and banking credentials. |
| **Pakistan** | **PDPB (Art. 8, 11 & 14)** | Consent-based processing, mandatory cross-border isolation, and protection against automated profiling. | Enforces strict PII masking before foreign model dispatch, ensuring non-sovereign LLMs only receive contextually sanitized tokens. |
| **Pakistan** | **National AI Policy 2025** | Verifiable governance, ethical alignment, and sovereign deployment across public sector IT systems. | Cryptographic SHA-256 hash-chaining of every prompt-response payload for immutable audit trails and 100% local deployment capability. |

---

## 2. Technical System Architecture

Guard AI operates as an asynchronous, high-throughput gateway stationed between client applications (e.g., mobile apps, web backends, agentic workflows) and external upstream LLM providers (e.g., OpenAI, Anthropic, Bedrock, or self-hosted models).