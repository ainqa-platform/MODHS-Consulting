# High-Level Design (HLD) Review: Integration Strategy & SMILE CDR Migration

> **Template Origin**: Official | **ArcKit Version**: 1.0.0 | **Command**: `/arckit.hld-review`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-HLDR-v1.0 |
| **Document Type** | High-Level Design Review |
| **Project** | Integration Strategy & SMILE CDR Migration (Project 001) |
| **Classification** | OFFICIAL-SENSITIVE |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-04-27 |
| **Last Modified** | 2026-04-27 |
| **Review Cycle** | On-Demand |
| **Next Review Date** | 2026-05-27 |
| **Owner** | Lead Enterprise Architect |
| **Reviewed By** | PENDING |
| **Approved By** | PENDING |
| **Distribution** | Project Team, Architecture Team, MODHS CDO |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-04-27 | ArcKit AI | Initial review of Level 1-4 diagrams and Data Model (v1.2 scope) | PENDING | PENDING |

---

## 1. Review Overview

### 1.1 Purpose

This document evaluates the proposed architecture for Project 001 (Consolidation & Migration) against the MODHS Enterprise Architecture Principles (v1.1) and Project Requirements (v1.2).

### 1.2 HLD Document Under Review

**Document**: Diagrams [DIAG-003/006] and Data Model [DATA-v1.0]
**ArcKit Version**: 1.0.0
**Submitted By**: Internal Architecture Team
**Submission Date**: 2026-04-27

### 1.3 Review Participants

| Name | Role | Organization | Review Focus |
|------|------|--------------|--------------|
| ArcKit AI | Lead Reviewer | Enterprise Architecture | Overall alignment and traceabilty |
| PENDING | Security Architect | Security | KSA Cloud Residency & Zero Trust |
| PENDING | Data Architect | Data Governance | EMPI & NHIC Synchronization |

---

## 2. Executive Summary

### 2.1 Overall Assessment

**Status**: **APPROVED WITH CONDITIONS**

**Summary**: 
The proposed High-Level Design (HLD), represented by the Level 1-4 C4 diagrams and the comprehensive Data Model, demonstrates a robust and compliant approach to clinical data consolidation. The move from a "Cerner-only" scope to a "Multi-system MODHS Consolidation" effectively addresses previous gaps identified in the SMILE CDR strategy.

The architecture leverages a hybrid cloud model that correctly isolates the internal EMR (Cerner) while providing a scalable, FHIR-native layer in KSA-based cloud regions for national interoperability. However, while the design is conceptually sound, several operational and disaster recovery details must be formalized before proceeding to the Detailed Design (DLD) phase.

### 2.2 Key Strengths

- **Sovereignty Compliance**: Explicit use of KSA cloud regions (Oracle/Google) and the inclusion of the NHIC registry for identity verification aligns with Saudi PDPL and health mandates.
- **Security by Design**: The two-tier Rhapsody (DMZ/Internal) bridge correctly implements Zero Trust principles for national HIE connectivity.
- **Standardization**: Full alignment with FHIR R4 (KSA Profile) for the central repository ensures future-proof integration with NPHIES and Mawid.

### 2.3 Key Concerns

- **DR Failover Runbook**: The deployment diagram identifies a multi-region/AZ topology, but the automated failover mechanisms and RTO/RPO validation are not yet documented.
- **Operational SLOs**: While metrics are mentioned, specific Service Level Objectives (SLOs) for message processing latency (Rhapsody) and API response times (SMILE CDR) are undefined.
- **Legacy Ingestion Complexity**: The batch extraction from legacy HIS systems [E-002] remains a high-risk area for data quality.

### 2.4 Conditions for Approval

**MUST Address Before Detailed Design**:

1. [BLOCKING-01]: Define the automated failover runbook for the KSA Cloud region to meet NFR-A-1 targets.
2. [BLOCKING-02]: Formalize the Data Quality Dashboard implementation plan for the MDM/EMPI layer to ensure 99.9% match accuracy.

**SHOULD Address During Detailed Design**:

1. [ADVISORY-01]: Define SLI/SLO targets for the SMILE CDR FHIR API.
2. [ADVISORY-02]: Detail the specific HL7 v2 to FHIR R4 mapping complexity for legacy HIS sources.

### 2.5 Recommendation

- [ ] **APPROVED**
- [x] **APPROVED WITH CONDITIONS**: Proceed after addressing blocking items listed above
- [ ] **REJECTED**

---

## 3. Architecture Principles Compliance

| Principle ID | Principle Name | Status | Comments |
|--------------|----------------|--------|----------|
| **PRIN-1** | Cloud First & Scalability | ✅ Compliant | SMILE CDR deployed in KSA Cloud (OCI/GCP). |
| **PRIN-2** | Zero Trust Security | ✅ Compliant | External Rhapsody gateway provides DMZ isolation and WAF. |
| **PRIN-8** | Data Sovereignty | ✅ Compliant | KSA-only data residency for health records and audit logs. |
| **PRIN-14** | Audit & Observability | ⚠️ Partial | Audit Log [E-006] is defined, but alerting logic is missing. |
| **PRIN-15** | FHIR-Native Strategy | ✅ Compliant | All internal storage and external exchange use FHIR R4 KSA. |

---

## 4. Requirements Coverage Analysis

### 4.1 Functional Requirements Coverage

| Requirement ID | Requirement Summary | Addressed in HLD | Design Element | Assessment |
|----------------|---------------------|------------------|----------------|------------|
| BR-5 | MODHS Consolidation | ✅ Yes | DIAG-003, DIAG-005 | Adequate |
| BR-6 | MDM for Patient EMPI| ✅ Yes | DATA-E-001, DIAG-004| Adequate |
| INT-3 | NHIC Sync | ✅ Yes | DIAG-004, DATA-E-001| Adequate |
| FR-1 | FHIR R4 KSA | ✅ Yes | DATA-E-004 | Adequate |

### 4.2 Non-Functional Requirements Coverage

| NFR ID | Requirement | Target | HLD Approach | Assessment |
|--------|-------------|--------|--------------|------------|
| NFR-A-1 | Availability | 99.9% | Hybrid Multi-AZ | ✅ |
| NFR-SEC-3| Data Residency | KSA Only | OCI/GCP Riyadh | ✅ |
| NFR-SEC-2| PDPL Audit | 7 Years | Audit Log [E-006] | ✅ |

---

## 6. Security Architecture Review

### 6.1 Threat Model Assessment
- **External Breach**: Mitigated by External Rhapsody DMZ and mTLS.
- **Data Leakage**: Mitigated by PDPL-compliant KSA cloud residency and encryption at rest.
- **Identity Sprawl**: Mitigated by the central MDM layer and NHIC synchronization.

### 6.2 Security Controls
- **Authentication**: mTLS 1.3 for all national HIE connections.
- **Authorization**: RBAC enforced at the FHIR repository level.
- **Encryption**: AES-256 for clinical data volumes and audit stores.

---

## 11. Issues and Recommendations

### 11.1 Critical Issues (BLOCKING)

| ID | Issue | Impact | Recommendation | Owner | Target Date |
|----|-------|--------|----------------|-------|-------------|
| BLOCKING-01 | Missing DR Failover Runbook | HIGH | Document the multi-region failover sequence and RTO validation. | Infra Arch | 2026-05-10 |
| BLOCKING-02 | Data Quality Monitoring | MEDIUM | Specify the DQ dashboard architecture for monitoring EMPI match rates. | Data Arch | 2026-05-10 |

---

## 12. Review Decision

**Status**: **APPROVED WITH CONDITIONS**

**Effective Date**: 2026-04-27

**Conditions**:
1. Resolve [BLOCKING-01] and [BLOCKING-02] within the next 14 days.
2. Ensure DLD phase includes detailed mapping for legacy HIS data types.

---

**Generated by**: ArcKit `/arckit.hld-review` command
**Generated on**: 2026-04-27 11:15 GMT
**ArcKit Version**: 1.0.0
**Project**: Integration Strategy & SMILE CDR Migration (Project 001)
**AI Model**: Gemini 3.1 Pro (High)
**Generation Context**: Review of DIAG-003/006 and DATA-v1.0 against PRIN-v1.1 and REQ-v1.2
