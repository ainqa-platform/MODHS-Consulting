# Project Requirements: Integration Strategy & SMILE CDR Migration

> **Template Origin**: Official | **ArcKit Version**: 1.0.0 | **Command**: `$arckit-requirements`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-REQ-v1.2 |
| **Document Type** | Business and Technical Requirements |
| **Project** | Integration Strategy & SMILE CDR Migration (Project 001) |
| **Classification** | OFFICIAL-SENSITIVE |
| **Status** | DRAFT |
| **Version** | 1.2 |
| **Created Date** | 2026-04-19 |
| **Last Modified** | 2026-04-27 |
| **Review Cycle** | Quarterly |
| **Next Review Date** | 2026-05-27 |
| **Owner** | Project Manager |
| **Reviewed By** | [PENDING] |
| **Approved By** | [PENDING] |
| **Distribution** | Project Team, Architecture Team, PSMMC Stakeholders |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-04-19 | ArcKit AI | Initial creation from `$arckit-requirements` command | [PENDING] | [PENDING] |
| 1.1 | 2026-04-20 | ArcKit AI | Refreshed to incorporate global architecture principles (ARC-000-PRIN-v1.0) | [PENDING] | [PENDING] |
| 1.2 | 2026-04-27 | ArcKit AI | Updated to align with ARC-000-PRIN-v1.1; added MDM/NHIC and multi-system consolidation scope | [PENDING] | [PENDING] |

## Document Purpose

This document outlines the business, functional, non-functional, integration, and data requirements for the Mawid/NPHIES integrations via Rhapsody and the deployment/migration of SMILE CDR for PSMMC, expanding to a broader MODHS context.

---

## Executive Summary

### Business Context

PSMMC relies on Rhapsody as the core integration middleware to connect its legacy systems and Cerner (Millenium, Oracle DB v11) with national healthcare systems such as NPHIES and Mawid. While parts of the integration have been completed, critical flows like the Mawid Practitioner lookup and NPHIES Clinical Documents remain unresolved. Concurrently, the organization is moving toward a modernized clinical data repository using SMILE CDR. Recent feedback indicates a need to move beyond a Cerner-centric approach to consolidate all available MODHS systems and implement a robust Master Data Management (MDM) strategy for Patient EMPI that aligns with the KSA NHIC patient registry [REQ-C5].

### Objectives

- Complete the Mawid and NPHIES integrations via Rhapsody.
- Resolve the Practitioner fetch issue in the Mawid integration.
- Establish SMILE CDR as the active clinical data repository and achieve NPHIES conformance.
- Successfully migrate clinical data from the Legacy HIS/EMR to SMILE CDR.
- **New**: Consolidate all available MODHS systems into the SMILE CDR platform [REQ-C5].
- **New**: Implement a Master Data Management (MDM) strategy for Patient EMPI considering KSA NHIC patient registry [REQ-C5].
- Ensure alignment with global architecture principles including Cloud First, Privacy by Design (PDPL), and Interoperability (FHIR R4 KSA).

### Expected Outcomes

- **Full Interoperability**: 100% of defined Mawid and NPHIES use cases active in production.
- **Data Modernization**: Legacy HIS and other MODHS systems' data accessible via SMILE CDR FHIR endpoints.
- **Single Source of Truth**: Authorized Patient EMPI synchronized with KSA NHIC registry.
- **Compliance**: Passing NPHIES QNR conformance and adhering to Saudi PDPL and health data residency mandates.

### Project Scope

**In Scope**:
- Fixing the Mawid Practitioner fetching issue.
- Completing NPHIES Clinical Docs, Rad Image Manifest, CDA requests.
- Deploying SMILE CDR aligned with Cloud First and Zero Trust principles.
- Migrating legacy HIS/EMR data to SMILE CDR.
- Consolidating other MODHS system data into SMILE CDR.
- Implementing MDM/EMPI with NHIC integration.

**Out of Scope**:
- Upgrading Cerner Millenium to a newer version.
- Replacing the Rhapsody integration engine.

---

## Stakeholders

| Stakeholder | Role | Organization | Involvement Level |
|-------------|------|--------------|-------------------|
| Ayman | Primary Contact | PSMMC | Decision maker |
| Asma | Secondary Contact | PSMMC | Requirements definition |
| Fawaz / Hanan | Project Team | PSMMC | Technical review |
| Ashique | Integration Lead | Project Team | NPHIES/Cerner integration |
| Julnishar / Aman | Integration Lead | Project Team | Mawid integration |
| Rehman | Lean Representative | Lean | External integration validation |

---

## Business Requirements

### BR-1: Complete Mawid Integration
**Description**: The system must fully support the Mawid integration use cases, specifically resolving the Practitioner lookup failure.
**Rationale**: Mawid integration (via Lean) is critical for MOD-specific (Eatizaz) appointment and clinic management.
**Priority**: MUST_HAVE
**Stakeholder**: Julnishar, Aman, Rehman

### BR-2: Complete NPHIES Integration
**Description**: The system must finalize the remaining NPHIES integration workflows, including Clinical Documents and Rad Image Manifests.
**Rationale**: To meet national healthcare interoperability standards, the hospital must provide comprehensive clinical and radiological data to NPHIES.
**Priority**: MUST_HAVE
**Stakeholder**: Ashique

### BR-3: Deploy and Conform SMILE CDR
**Description**: The organization must deploy SMILE CDR and use it to achieve NPHIES QNR conformance.
**Rationale**: SMILE CDR will serve as the modernized FHIR-native repository enabling robust national integrations.
**Priority**: MUST_HAVE
**Stakeholder**: Ayman, Asma

### BR-4: Legacy Data Migration
**Description**: Clinical data from the legacy HIS/EMR must be fully migrated to the new SMILE CDR environment.
**Rationale**: Decommissioning the legacy systems requires safely porting historical clinical data to the new FHIR-based repository.
**Priority**: MUST_HAVE
**Stakeholder**: Fawaz, Hanan

### BR-5: MODHS System Consolidation
**Description**: The platform MUST expand its focus beyond Cerner to consolidate data from all available systems within the MODHS ecosystem [REQ-C5].
**Rationale**: Achieving a true Enterprise Health Record requires data from across the medical city, not just the core EMR.
**Priority**: MUST_HAVE
**Stakeholder**: Ayman, Asma

### BR-6: MDM for Patient EMPI
**Description**: Implement a Master Data Management strategy for Patient Enterprise Master Patient Index (EMPI) that incorporates the KSA NHIC patient registry [REQ-C5].
**Rationale**: Accurate patient identification is foundational to clinical safety and national health exchange.
**Priority**: MUST_HAVE
**Stakeholder**: Julnishar

---

## Functional Requirements

### Use Cases

#### UC-1: Mawid Practitioner Lookup
**Actor**: Mawid System (External)
**Main Flow**:
1. Mawid sends a Practitioner fetch request (FHIR R4 KSA).
2. Rhapsody translates request to Cerner-compatible HL7.
3. Cerner responds with Practitioner details.
4. Rhapsody translates response back to FHIR R4 KSA.
**Priority**: CRITICAL

#### UC-2: NHIC Patient Registry Sync (New)
**Actor**: SMILE CDR / MDM Layer
**Main Flow**:
1. System receives a patient registration/update request.
2. MDM layer checks internal index and queries KSA NHIC Patient Registry.
3. System reconciles data and updates the Single Source of Truth (SSOT).
**Priority**: HIGH

### Functional Requirements Detail

#### FR-1: FHIR R4 KSA Translation
**Description**: Rhapsody must accurately translate HL7 messages from Cerner to FHIR R4 KSA profiles for Mawid.
**Relates To**: BR-1, ARC-000-PRIN-v1.1 (Principle 9)
**Priority**: MUST_HAVE

#### FR-2: CDA Document Retrieval
**Description**: Support the request and retrieval of CDA documents for NPHIES.
**Relates To**: BR-2
**Priority**: MUST_HAVE

#### FR-3: Multi-Source Data Ingestion
**Description**: SMILE CDR must support ingestion of clinical data from non-Cerner MODHS systems via HL7 v2 or FHIR.
**Relates To**: BR-5
**Priority**: MUST_HAVE

---

## Non-Functional Requirements (NFRs)

### Performance Requirements

#### NFR-P-1: Integration Throughput
**Requirement**: End-to-end (Cerner to Mawid/NPHIES) translation latency: < 500ms.
**Priority**: HIGH

### Security and Privacy Requirements (aligned with ARC-000-PRIN-v1.1)

#### NFR-SEC-1: Zero Trust Architecture
**Requirement**: Implement defense-in-depth security with identity-based access and mutual TLS for all service-to-service communication.
**Alignment**: Security by Design (Zero Trust) - Principle 11
**Priority**: CRITICAL

#### NFR-SEC-2: Privacy Integral (PDPL Compliance)
**Requirement**: All processing of health data must comply with Saudi PDPL, including data minimization and explicit consent management where required.
**Alignment**: Privacy Integral - Principle 6
**Priority**: CRITICAL

#### NFR-SEC-3: Health Data Residency
**Requirement**: All Personal Health Information (PHI) MUST reside within the Kingdom of Saudi Arabia (KSA).
**Alignment**: Data Sovereignty - Principle 8
**Priority**: CRITICAL

### Architecture and Cloud Requirements

#### NFR-A-1: Cloud First and Scalability
**Requirement**: The SMILE CDR deployment must be architected for horizontal scalability, utilizing cloud infrastructure where residency laws permit.
**Alignment**: Cloud First - Principle 1
**Priority**: HIGH

---

## Integration Requirements

### External System Integrations

#### INT-1: Mawid (Lean/Eatizaz)
**Pattern**: Cerner -> Rhapsody -> Mawid (FHIR R4 KSA)
**Priority**: CRITICAL

#### INT-2: NPHIES
**Pattern**: Cerner -> Rhapsody -> NPHIES (XDS/FHIR)
**Priority**: CRITICAL

#### INT-3: KSA NHIC Patient Registry (New)
**Purpose**: Authoritative patient identity verification.
**Integration Type**: Real-time API
**Alignment**: Single Source of Truth - Principle 7
**Priority**: MUST_HAVE

---

## Data Requirements

### Data Migration Requirements
**Scope**: Clinical data from Legacy HIS/EMR and other MODHS systems.
**Alignment**: Single Source of Truth - Principle 7
**Priority**: CRITICAL

### MDM Requirements (New)
**Description**: Implement deduplication and cross-referencing logic between Cerner, Legacy HIS, and NHIC identifiers.
**Priority**: MUST_HAVE

---

## Requirement Conflicts & Resolutions

- **Conflict**: Cloud First (NFR-A-1) vs. Data Residency (NFR-SEC-3).
- **Resolution**: Use KSA-based cloud regions (e.g., Oracle Cloud Riyadh, Google Cloud Dammam) to satisfy both principles.

---

## External References

### Document Register

| Doc ID | Filename | Type | Source Location | Description |
|--------|----------|------|-----------------|-------------|
| EXT-01 | cerner | Note | `external/cerner` | Cerner context, Rhapsody status |
| EXT-02 | initial_discussion | Note | `external/initial_discussion` | Mawid/NPHIES scope |
| EXT-03 | mawid_integration | Note | `external/mawid_integration` | Mawid use cases |
| EXT-04 | NPHIES_QNR | Note | `external/NPHIES_QNR` | NPHIES conformance |
| EXT-05 | SMILE_CDR_Current_Status | Note | `external/SMILE_CDR_Current_Status` | MDM/NHIC and multi-system needs |
| PRIN-01| ARC-000-PRIN-v1.1 | Doc | `000-global/ARC-000-PRIN-v1.1.md` | Global EA Principles v1.1 |

### Citations

| Citation ID | Doc ID | Category | Quoted Passage |
|-------------|--------|----------|----------------|
| [REQ-C1] | EXT-03 | Issue | "Practitioners - Fetch doctor -- not working" |
| [REQ-C5] | EXT-05 | Scope | "Currently I see they are only focusing on Cerner... MDM for Patient EMPI... NHIC patient registry" |

---

**Generated by**: ArcKit `$arckit-requirements` command
**Generated on**: 2026-04-27 11:00 GMT
**ArcKit Version**: 1.0.0
**Project**: Integration Strategy & SMILE CDR Migration (Project 001)
**AI Model**: Gemini 3.1 Pro (High)
**Generation Context**: Updated to align with EA Principles v1.1 and incorporate MDM/NHIC context from external/SMILE_CDR_Current_Status
