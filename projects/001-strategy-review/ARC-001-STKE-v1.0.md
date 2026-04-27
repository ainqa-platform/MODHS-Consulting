# Stakeholder Drivers Analysis: Integration Strategy & SMILE CDR Migration

> **Template Origin**: Official | **ArcKit Version**: 1.0.0 | **Command**: `/arckit.stakeholders`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-STKE-v1.0 |
| **Document Type** | Stakeholder Drivers Analysis |
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
| **Distribution** | Project Board, Steering Committee |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-04-27 | ArcKit AI | Initial creation based on project scope expansion (v1.2) | PENDING | PENDING |

---

## 1. Stakeholder Identification & Mapping

### 1.1 Power-Interest Grid

```text
       High ^
            |
            |   Keep Satisfied             Manage Closely
            |   ----------------           ----------------
            |   - CIO (MODHS)              - Medical Director
     P      |   - CDO (MODHS)              - IT Director (PSMMC)
     O      |                              - National Interop Board
     W      |
     E      |   Monitor (Minimum Effort)   Keep Informed
     R      |   ----------------           ----------------
            |   - External Vendors         - Dept. Heads (Lab/Rad)
            |   - Legacy HIS Support       - Clinical Staff
            |
            +---------------------------------------------------->
                                 INTEREST                    High
```

### 1.2 Stakeholder Register

| Stakeholder | Role | Power | Interest | Quadrant | Engagement Strategy |
|-------------|------|-------|----------|----------|---------------------|
| Medical Director | Clinical SRO | High | High | Manage Closely | Weekly briefings, clinical validation |
| CDO (MODHS) | Data Owner | High | High | Manage Closely | Bi-weekly data governance boards |
| IT Director (PSMMC) | Technical Lead | High | High | Manage Closely | Daily standups, technical design reviews |
| CIO (MODHS) | Strategic Lead | High | Medium | Keep Satisfied | Monthly steering committee |
| Dept. Heads | Service Owners | Medium| Medium | Keep Informed | Monthly workshops |
| National Interop Board| Regulator | High | Medium | Manage Closely | Formal compliance reviews (NPHIES/NHIC) |

---

## 2. Stakeholder Drivers

### 2.1 Medical Director (Clinical SRO)
- **DRIVER**: Unified Longitudinal Patient Record.
- **Context**: PSMMC clinical staff currently move between systems (Cerner, Legacy HIS) causing fragmented care and safety risks.
- **Intensity**: CRITICAL
- **Enablers**: SMILE CDR consolidation, EMPI matching.
- **Blockers**: Incomplete data migration, legacy system downtime.

### 2.2 Chief Data Officer (CDO)
- **DRIVER**: Data Quality & National Compliance.
- **Context**: KSA NHIC requires accurate patient identity. CDO is accountable for EMPI integrity and PDPL data residency.
- **Intensity**: HIGH
- **Enablers**: NHIC Patient Registry API, robust MDM layer.
- **Blockers**: Duplicate records in legacy systems, lack of national ID in older datasets.

### 2.3 IT Director (PSMMC)
- **DRIVER**: Technical Debt Reduction & Platform Stability.
- **Context**: Maintaining multiple legacy HIS systems is costly and risky. Modernizing via FHIR reduces long-term maintenance.
- **Intensity**: HIGH
- **Enablers**: Rhapsody normalization, SMILE CDR scalability.
- **Blockers**: Integration resource shortages, vendor lock-in of legacy systems.

---

## 3. Goals & Outcomes Mapping

| Stakeholder | Driver | Goal (SMART) | Measurable Outcome |
|-------------|--------|--------------|--------------------|
| Medical Dir | Unified Record | Consolidate 100% of available clinical data from 5+ sources by Q4 2026. | Zero need for clinicians to access legacy HIS for patient history. |
| CDO | Data Quality | Achieve 99.9% EMPI match accuracy for the 2.5M patient base. | NHIC sync error rate < 0.1%. |
| IT Director | Stability | Achieve 99.9% availability for the Integration Hub. | < 4 hours total unplanned downtime per year. |
| Regulator | Compliance | 100% conformance to FHIR R4 KSA profiles for NPHIES reporting. | GDS/National Service assessment pass (first attempt). |

---

## 4. Governance (RACI)

| Key Decision | Medical Dir | CDO | IT Director | CIO | Regulator |
|--------------|-------------|-----|-------------|-----|-----------|
| Data Consolidation Scope | **A** | **C** | **R** | **I** | **I** |
| EMPI Matching Rules | **I** | **A** | **R** | **C** | **C** |
| Cloud Hosting (KSA) | **I** | **C** | **R** | **A** | **I** |
| Compliance Sign-off | **R** | **C** | **R** | **A** | **C** |

*R = Responsible, A = Accountable, C = Consulted, I = Informed*

---

## 5. Conflict Analysis & Resolution

| Conflict | Synergies | Resolution Strategy |
|----------|-----------|---------------------|
| **Speed vs. Safety**: Medical Dir wants fast consolidation; CDO wants careful data cleansing. | Both want high-quality data for patient safety. | Phased ingestion: Start with high-confidence records, use MDM dashboard for manual verification of outliers. |
| **On-prem vs. Cloud**: IT Director prefers local control; CIO mandates Cloud First (PRIN-1). | Both want scalability and resilience. | Hybrid Model: Keep EMR on-prem, place Integration Hub and CDR in KSA Cloud (PDPL compliant). |

---

**Generated by**: ArcKit `$arckit-stakeholders` command
**Generated on**: 2026-04-27
**ArcKit Version**: 1.0.0
**Project**: Integration Strategy & SMILE CDR Migration (Project 001)
**AI Model**: Gemini 3.1 Pro (High)
