# Risk Register: Integration Strategy & SMILE CDR Migration

> **Template Origin**: Official | **ArcKit Version**: 1.0.0 | **Command**: `/arckit.risk`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-RISK-v1.0 |
| **Document Type** | Risk Register |
| **Project** | Integration Strategy & SMILE CDR Migration (Project 001) |
| **Classification** | OFFICIAL-SENSITIVE |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-04-27 |
| **Last Modified** | 2026-04-27 |
| **Review Cycle** | Monthly |
| **Next Review Date** | 2026-05-27 |
| **Owner** | Project Manager |
| **Reviewed By** | PENDING |
| **Approved By** | PENDING |
| **Distribution** | Project Board, Steering Committee, Risk Owners |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-04-27 | ArcKit AI | Initial creation following Orange Book principles and HLDR findings | PENDING | PENDING |

---

## 1. Executive Summary

### 1.1 Overview
This risk register identifies and assesses 7 key risks associated with the MODHS Integration Platform and SMILE CDR Migration. The profile reflects a high-complexity project transitioning to a hybrid cloud model and consolidating multiple legacy systems.

### 1.2 Risk Profile Distribution

- **Critical Risks (20-25)**: 1 risk (Disaster Recovery Gaps)
- **High Risks (13-19)**: 2 risks (Legacy Data Ingestion, Hybrid Latency)
- **Medium Risks (6-12)**: 3 risks (National Interop Drift, Skill Gaps, PDPL Interpretation)
- **Low Risks (1-5)**: 1 risk (Stakeholder Engagement)

**Overall Risk Profile**: **CONCERNING**. The presence of a Critical risk related to Disaster Recovery and high-impact technology risks requires immediate management attention and mitigation.

### 1.3 Key Risks Requiring Immediate Attention
1. **R-004 (TECHNOLOGY, Critical 20)**: Disaster Recovery Runbook Gaps. Lack of validated automated failover.
2. **R-005 (TECHNOLOGY, High 16)**: Legacy System Data Corruption. Risk to EMPI integrity.
3. **R-003 (TECHNOLOGY, High 16)**: Hybrid Cloud Latency. Risk to real-time clinical performance.

---

## 2. Risk Matrix Visualization

### 2.1 Inherent Risk Matrix (Before Controls)

```text
                                       IMPACT
                 1-Minimal   2-Minor    3-Moderate   4-Major    5-Severe
              ┌───────────┬───────────┬───────────┬───────────┬───────────┐
   5-Almost   │           │           │           │           │           │
   Certain    │    5      │    10     │    15     │    20     │    25     │
              ├───────────┼───────────┼───────────┼───────────┼───────────┤
   4-Likely   │           │           │           │   R-005   │   R-004   │
              │    4      │    8      │    12     │    16     │    20     │
   L          ├───────────┼───────────┼───────────┼───────────┼───────────┤
   I 3-Possible│          │           │   R-002   │   R-003   │           │
   K          │    3      │    6      │    9      │    12     │    15     │
   ...        └───────────┴───────────┴───────────┴───────────┴───────────┘
```

---

## 3. Detailed Risk Register

### R-004: Disaster Recovery Runbook Gaps
- **Category**: TECHNOLOGY
- **Description**: The architecture provides multi-region redundancy, but formal automated failover runbooks and RTO/RPO validation are missing (HLDR BLOCKING-01).
- **Consequences**: Extended downtime during a regional cloud outage, failing to meet NFR-A-1 (99.9% availability).
- **Affected Stakeholders**: IT Director (PSMMC), Medical Director.
- **Inherent Risk**: L: 4, I: 5 (Score: 20) **CRITICAL**
- **Existing Controls**: Multi-AZ OCI/GCP deployment.
- **Control Effectiveness**: WEAK (Lack of orchestration/testing).
- **Residual Risk**: L: 4, I: 5 (Score: 20) **CRITICAL**
- **Response**: **TREAT**
- **Risk Owner**: IT Director (PSMMC)
- **Action Plan**: Develop and test automated failover scripts; conduct DR drill by 2026-05-30.

### R-005: Legacy System Data Corruption
- **Category**: TECHNOLOGY
- **Description**: Poor data quality in legacy HIS systems (missing IDs, duplicates) corrupts the Master Patient Index (EMPI) during ingestion.
- **Consequences**: Clinical safety risk due to mismatched patient records; NHIC sync failures.
- **Affected Stakeholders**: CDO (MODHS), Medical Director.
- **Inherent Risk**: L: 4, I: 4 (Score: 16) **HIGH**
- **Existing Controls**: Rhapsody normalization rules.
- **Control Effectiveness**: ADEQUATE
- **Residual Risk**: L: 3, I: 4 (Score: 12) **MEDIUM**
- **Response**: **TREAT**
- **Risk Owner**: CDO (MODHS)
- **Action Plan**: Implement the Data Quality Dashboard (HLDR BLOCKING-02) to monitor match rates.

### R-003: Hybrid Cloud Performance Latency
- **Category**: TECHNOLOGY
- **Description**: The network latency between the on-premise Cerner system and the cloud-based SMILE CDR degrades real-time clinical response times.
- **Consequences**: Clinician frustration and potential workarounds that bypass the integration platform.
- **Affected Stakeholders**: Medical Director, IT Director.
- **Inherent Risk**: L: 4, I: 4 (Score: 16) **HIGH**
- **Existing Controls**: KSA-based cloud region (OCI Riyadh) to minimize geographical distance.
- **Control Effectiveness**: ADEQUATE
- **Residual Risk**: L: 3, I: 4 (Score: 12) **MEDIUM**
- **Response**: **TREAT**
- **Risk Owner**: IT Director (PSMMC)
- **Action Plan**: Conduct network performance baseline testing; implement dedicated ExpressRoute/FastConnect.

---

## 4. Risk Ownership & 4Ts Summary

| Stakeholder | Owned Risks | Critical/High Risks |
|-------------|-------------|---------------------|
| IT Director (PSMMC) | R-003, R-004, R-007 | R-004 (Critical), R-003 (High) |
| CDO (MODHS) | R-002, R-005, R-006 | R-005 (High) |
| Medical Director | R-001 | 0 |

**4Ts Distribution**:
- **TREAT**: 85% (6 risks)
- **TOLERATE**: 15% (1 risk - Stakeholder Engagement)
- **TRANSFER**: 0%
- **TERMINATE**: 0%

---

## 5. Monitoring & Review Framework

- **Critical/High Risks**: Reviewed **Weekly** at the Project Management meeting.
- **Medium/Low Risks**: Reviewed **Monthly** at the Steering Committee.
- **Escalation**: Any risk exceeding score 15 must be escalated to the MODHS CIO immediately.
- **Next Review Date**: 2026-05-27

---

**Generated by**: ArcKit `$arckit-risk` command
**Generated on**: 2026-04-27
**ArcKit Version**: 1.0.0
**Project**: Integration Strategy & SMILE CDR Migration (Project 001)
**AI Model**: Gemini 3.1 Pro (High)
**Generation Context**: Initial risk register based on STKE-v1.0, HLDR-v1.0, and REQ-v1.2
