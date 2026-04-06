# Protoj AI Mesh Spec

## Background
Personally, I am a big advocate for small, specialized language models. This spec I created in Oct. 2025 based on blending the concept of small language models and agents communicating on a peer-to-peer network. The result turned out to be a mashing of peer-to-peer and IoT Mesh Network concpets. 

> **"Mesh AI: The Infrastructure Layer for Secure, Collaborative Intelligence."**

This repository contains the functional specification for the **Protoj AI Mesh** — an orchestration platform that enables small, specialized language models (SLMs) to reason together privately, explainably, and at scale.

---

## Overview

Traditional LLM pipelines rely on a single large model with broad permissions and no verifiable audit trail. The AI Mesh replaces this with a **governed network of specialized SLMs**, where every task is:

- **Scoped** by cryptographically signed capability tokens
- **Policy-enforced** per tenant and jurisdiction (HIPAA, SOC 2, GDPR)
- **Safety-evaluated** before any output is released
- **Provenance-signed** with an immutable, tamper-proof audit record
- **Self-healing** — automatically re-routed when a violation is detected

---

## Spec Document

The full functional specification is in [Ai-Mesh-Spec.md](Ai-Mesh-Spec.md).

**Version:** 1.0  
**Date:** October 25, 2025

---

## Core Architecture

| Component | Role |
|---|---|
| **Orchestration Engine** | Receives, classifies, and routes tasks across SLM nodes |
| **Policy Engine** | Evaluates compliance, issues capability tokens, adapts thresholds |
| **Capability Token Service** | Issues cryptographically bound, scoped execution permits |
| **SLM Nodes** | Specialized models (Summarizer, Refactorer, Safety, Validator, etc.) |
| **Safety Co-Processor** | Independently evaluates outputs for risk, PII leakage, hallucination |
| **Provenance Signer** | C2PA-compliant SHA-256 signing of all task records |
| **Audit Ledger** | Append-only, hash-chained, cross-region replicated audit trail |
| **Tool Sandbox** | Isolated execution environment for all file/API tool access |
| **Adaptive Policy Engine** | Tightens or relaxes governance based on live telemetry |
| **Federated Policy Engine** | Merges policies across tenants/regions for collaboration and global rollouts |

---

## Use Cases

| ID | Title | Key Capabilities |
|---|---|---|
| [UC-MESH-01](#uc-mesh-01) | Safe and Governed Task Routing | Dynamic routing, token issuance, PII redaction, safety scoring, provenance |
| [UC-MESH-02](#uc-mesh-02) | Self-Healing Re-Routing After Policy Violation | Violation detection, automatic token revocation, re-route under stricter constraints |
| [UC-MESH-03](#uc-mesh-03) | Multi-Tenant Isolation | Zero cross-tenant visibility, per-tenant capability tokens, partitioned audit ledgers |
| [UC-MESH-04](#uc-mesh-04) | Cross-Tenant Federated Collaboration | Joint capability tokens, dual-signed provenance, federated policy merging |
| [UC-MESH-05](#uc-mesh-05) | Autonomous Safety Arbitration (Quorum) | Multi-SLM consensus voting before output release |
| [UC-MESH-06](#uc-mesh-06) | Governed Tool Invocation & Sandboxed Execution | Token-scoped file/API access, sandboxed subprocess execution |
| [UC-MESH-07](#uc-mesh-07) | Provenance & Immutable Audit Trail Replication | Cross-region hash replication, 3-of-3 quorum verification, attestation certificates |
| [UC-MESH-08](#uc-mesh-08) | Intelligent Policy Adaptation | Telemetry-driven threshold tuning, versioned policy evolution, rollback |
| [UC-MESH-09](#uc-mesh-09) | Federated Risk Sharing & Global Compliance Rollout | Global risk signals, cross-jurisdiction policy propagation, per-region override layers |
| [UC-MESH-10](#uc-mesh-10) | Autonomous Node Governance & Peer Reputation | Decentralized trust scoring, automatic quarantine/promotion, peer vote consensus |

---

## Key Concepts

### Capability Tokens
Every task execution is gated by a signed capability token that encodes:
- Permitted SLM models
- Budget ceiling and TTL
- Tool access permissions (file read, network access, etc.)
- Tenant ID and jurisdiction
- Policy version reference

Tokens are non-transferrable and cryptographically bound to a single tenant and execution context.

### Self-Healing
When a safety score falls below threshold or a policy violation is detected, the orchestration engine automatically:
1. Revokes the current capability token
2. Issues a tightened replacement token (stricter redaction, reduced TTL, added safety models)
3. Re-processes the task under the new constraints
4. Logs the entire remediation sequence in the audit ledger

### Multi-Tenant Isolation
Each tenant operates in a fully isolated execution lane:
- Separate capability tokens signed with per-tenant private keys
- SLM nodes tagged with tenant scope — mismatched tokens are rejected at the routing layer
- Distinct audit ledger partitions with separate hash chains
- Cross-tenant access attempts return `403 Forbidden` and are logged

### Federated Collaboration
Two or more tenants can collaborate under a temporary joint policy:
- Federated Policy Engine merges individual tenant policies into a combined ruleset
- Joint capability tokens carry dual signatures from both tenants and the federation authority
- Results are dual-signed and replicated to both tenants' ledgers
- Federation expires automatically after TTL; no residual data retained

### Safety Arbitration Quorum
Before any output is released, a quorum of independent Safety SLMs evaluates it in parallel:
- Each evaluator uses a distinct rule set (PII leakage, insecure API calls, hallucination risk, license compliance)
- A configurable threshold of passes (e.g., 2-of-3) is required for release
- Failed quorum triggers the self-healing re-route mechanism

### Provenance & Audit Integrity
Every task record is:
- Hashed with SHA-256 and signed via Ed25519 (C2PA-compliant)
- Replicated to regional ledger nodes with quorum verification
- Append-only — modifications require a new block, preserving the full chain
- Queryable via attestation certificate API

---

## Real-World Scenarios

**Multinational Bank:** GDPR-compliant SLMs per region, local knowledge bases, offline distilled models for traders, automatic routing to a Legal Specialist SLM when uncertain — with full audit trail.

**National Health System (200 hospitals):** HIPAA-compliant clinical query SLMs, Medicaid prior-auth generation SLMs, offline tablet models in rural clinics, clinical decision support routing with radiology cross-reference — 100% HIPAA audit pass rate.

---

## Traceability Matrix (Patent Claims)

The spec includes a full traceability matrix mapping all 10 use cases to 22 patent claims. Summary:

| Claim | Coverage |
|---|---|
| 1 — Dynamic SLM orchestration and routing | UC-01, 02, 03, 04, 05, 06, 07, 08, 09, 10 |
| 2 — Capability tokens | UC-01, 02, 03, 04, 06 |
| 3 — Tenant-scoped isolation | UC-03 |
| 4 — Sandboxed tool invocation | UC-06 |
| 5 — Jurisdiction/tenant policy enforcement | UC-01, 02, 03, 04, 06 |
| 6 — Safety co-processor | UC-01, 02, 05 |
| 7 — Provenance signing and audit logging | UC-01, 04, 06, 07, 08 |
| 8 — Self-healing re-routing | UC-02, 05, 08 |
| 9 — Multi-layer policy enforcement | UC-01, 03, 04, 06, 07 |
| 10 — Federated collaboration | UC-04, 09 |
| 11 — Distributed ledger replication | UC-07, 09 |
| 12 — Peer reputation and node self-governance | UC-10 |
| 13 — Tool access mediation | UC-06 |
| 14 — Adaptive governance | UC-02, 06, 08 |
| 15 — Multi-SLM consensus safety arbitration | UC-05 |
| 16 — Tamper-proof hash-chained audit | UC-07 |
| 17 — Telemetry-driven policy adaptation | UC-02, 05, 08 |
| 18 — Multi-tenant trust scoring | UC-10 |
| 19 — Federated ledger sync | UC-07, 09, 10 |
| 20 — Role-based cryptographic isolation | UC-03, 04 |
| 21 — Global compliance propagation | UC-04, 09 |
| 22 — Overall self-healing, self-regulating mesh | All use cases |

---

## Design Constraints Summary

| Aspect | Specification |
|---|---|
| SLM hop latency | ≤ 2.5 seconds |
| Self-healing round-trip overhead | ≤ 1.0 second average |
| Safety arbitration overhead | ≤ 1.8 seconds average |
| Global policy propagation | ≤ 3 minutes |
| Ledger replication interval | Every 15 minutes or 50 entries |
| Minimum consensus quorum | 2-of-3 (configurable) |
| Cryptographic signing | Ed25519 signatures, SHA-256/SHA-512 hashing |
| Provenance standard | C2PA-compliant |
| Audit retention | Configurable per jurisdiction (e.g., 7 years HIPAA) |
| Policy update cadence | Minimum 4 hours between automatic revisions |
| Federation TTL | Default 6 hours, configurable |
| Trust decay | 0.01 per 72 hours of node inactivity |

---

## Compliance Coverage

- **HIPAA** — PHI redaction, jurisdiction-scoped routing, 7-year audit retention
- **GDPR** — Local data residency enforcement, data TTL, Art. 28 processor compliance
- **SOC 2** — Policy audit trails, access control, breach detection
- **ISO 27001** — Audit logging and access governance
- **HIMSS / C2PA** — Signed provenance for clinical and content integrity