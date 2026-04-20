# Project Requirements: Integration Strategy & SMILE CDR Migration

> **Template Origin**: Official | **ArcKit Version**: 1.0.0 | **Command**: `$arckit-requirements`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-REQ-v1.1 |
| **Document Type** | Business and Technical Requirements |
| **Project** | Integration Strategy & SMILE CDR Migration (Project 001) |
| **Classification** | OFFICIAL-SENSITIVE |
| **Status** | DRAFT |
| **Version** | 1.1 |
| **Created Date** | 2026-04-19 |
| **Last Modified** | 2026-04-20 |
| **Review Cycle** | Quarterly |
| **Next Review Date** | 2026-05-20 |
| **Owner** | Project Manager |
| **Reviewed By** | [PENDING] |
| **Approved By** | [PENDING] |
| **Distribution** | Project Team, Architecture Team, PSMMC Stakeholders |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-04-19 | ArcKit AI | Initial creation from `$arckit-requirements` command | [PENDING] | [PENDING] |
| 1.1 | 2026-04-20 | ArcKit AI | Refreshed to incorporate global architecture principles (ARC-000-PRIN-v1.0) | [PENDING] | [PENDING] |

## Document Purpose

This document outlines the business, functional, non-functional, integration, and data requirements for the Mawid/NPHIES integrations via Rhapsody and the deployment/migration of SMILE CDR for PSMMC.

---

## Executive Summary

### Business Context

PSMMC relies on Rhapsody as the core integration middleware to connect its legacy systems and Cerner (Millenium, Oracle DB v11) with national healthcare systems such as NPHIES and Mawid. While parts of the integration have been completed, critical flows like the Mawid Practitioner lookup and NPHIES Clinical Documents remain unresolved. Concurrently, the organization is moving toward a modernized clinical data repository using SMILE CDR, which necessitates achieving NPHIES QNR conformance and migrating data from the legacy HIS/EMR.

### Objectives

- Complete the Mawid and NPHIES integrations via Rhapsody.
- Resolve the Practitioner fetch issue in the Mawid integration.
- Establish SMILE CDR as the active clinical data repository and achieve NPHIES conformance.
- Successfully migrate clinical data from the Legacy HIS/EMR to SMILE CDR.
- Ensure alignment with global architecture principles including Cloud First, Privacy by Design, and Interoperability.

### Expected Outcomes

- **Full Interoperability**: 100% of defined Mawid and NPHIES use cases active in production.
- **Data Modernization**: Legacy HIS data accessible via SMILE CDR FHIR endpoints.
- **Compliance**: Passing the NPHIES QNR conformance testing and adhering to privacy and security mandates.

### Project Scope

**In Scope**:
- Fixing the Mawid Practitioner fetching issue.
- Completing NPHIES Clinical Docs, Rad Image Manifest, CDA requests.
- Deploying SMILE CDR aligned with Cloud First principles.
- Migrating legacy HIS/EMR data to SMILE CDR.

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
**Success Criteria**:
- Practitioner fetching works seamlessly between Cerner, Rhapsody, and Mawid.
- Clinic Retrieval, Slot Booking, and Appointment Update flows are validated.
**Priority**: MUST_HAVE
**Stakeholder**: Julnishar, Aman, Rehman

---

### BR-2: Complete NPHIES Integration

**Description**: The system must finalize the remaining NPHIES integration workflows, including Clinical Documents and Rad Image Manifests.
**Rationale**: To meet national healthcare interoperability standards, the hospital must provide comprehensive clinical and radiological data to NPHIES.
**Success Criteria**:
- Clinical Documents, Rad Image Manifest, CDA document request, and CDA document retrieve flows are completed and tested.
**Priority**: MUST_HAVE
**Stakeholder**: Ashique

---

### BR-3: Deploy and Conform SMILE CDR

**Description**: The organization must deploy SMILE CDR and use it to achieve NPHIES QNR conformance.
**Rationale**: SMILE CDR will serve as the modernized FHIR-native repository enabling robust national integrations and future-proofing the architecture.
**Success Criteria**:
- SMILE CDR is active in the environment.
- NPHIES QNR conformance certification is achieved.
**Priority**: MUST_HAVE
**Stakeholder**: Ayman, Asma

---

### BR-4: Legacy Data Migration

**Description**: Clinical data from the legacy HIS/EMR must be fully migrated to the new SMILE CDR environment.
**Rationale**: Decommissioning the legacy systems requires safely porting historical clinical data to the new FHIR-based repository without loss of fidelity.
**Success Criteria**:
- 100% of targeted legacy data is mapped and migrated to SMILE CDR.
- Zero data loss during migration.
**Priority**: MUST_HAVE
**Stakeholder**: Fawaz, Hanan

---

## Functional Requirements

### Use Cases

#### UC-1: Mawid Practitioner Lookup
**Actor**: Mawid System (External)
**Preconditions**: External Rhapsody is online, Cerner is available.
**Main Flow**:
1. Mawid sends a Practitioner fetch request (FHIR R4 KSA).
2. Rhapsody (External DMZ) receives and authenticates the request.
3. Rhapsody translates the request to Cerner-compatible HL7.
4. Cerner responds with Practitioner details.
5. Rhapsody translates the response back to FHIR R4 KSA.
6. Mawid receives the correct Practitioner details.
**Postconditions**: Practitioner is successfully fetched.
**Exception Flows**: If Cerner times out, Rhapsody returns a standard FHIR OperationOutcome error.
**Priority**: CRITICAL

---

### Functional Requirements Detail

#### FR-1: FHIR R4 KSA Translation
**Description**: Rhapsody must accurately translate HL7 messages from Cerner to FHIR R4 KSA profiles for Mawid.
**Relates To**: BR-1, UC-1
**Acceptance Criteria**:
- [ ] Translation handles Practitioner mapping correctly.
- [ ] Translation handles Appointment scheduling mapping correctly.
**Priority**: MUST_HAVE

#### FR-2: CDA Document Retrieval
**Description**: The integration pathway must support the request and retrieval of CDA documents for NPHIES.
**Relates To**: BR-2
**Acceptance Criteria**:
- [ ] XDS to CDA workflows are fully mapped in Rhapsody.
**Priority**: MUST_HAVE

---

## Non-Functional Requirements (NFRs)

### Performance Requirements

#### NFR-P-1: Integration Throughput
**Requirement**: Rhapsody message translation must introduce minimal latency.
- Internal Rhapsody to External Rhapsody latency: < 50ms
- End-to-end (Cerner to Mawid/NPHIES) translation latency: < 500ms
**Priority**: HIGH

### Security and Privacy Requirements (aligned with ARC-000-PRIN-v1.0)

#### NFR-SEC-1: DMZ Isolation (Zero Trust)
**Requirement**: The two-tier Rhapsody architecture must strictly control traffic flow.
- External Rhapsody must only communicate with allowed national endpoints (Ayenati, Sehhatek, NPHIES, Mawid/Lean).
- Internal Rhapsody must validate all traffic before forwarding to Cerner.
**Alignment**: Security by Design (Zero Trust)
**Priority**: CRITICAL

#### NFR-SEC-2: Privacy Integral (Privacy By Design)
**Requirement**: All data in transit and at rest within the SMILE CDR platform and Rhapsody integration layer must be encrypted and subject to least-privilege access.
**Alignment**: Privacy Integral principle
**Priority**: CRITICAL

### Architecture and Cloud Requirements

#### NFR-A-1: Cloud First and Scalability
**Requirement**: The SMILE CDR deployment must be architected for horizontal scalability, ideally utilizing cloud infrastructure unless local residency laws strictly prohibit it.
**Alignment**: Cloud First and Scalability principle
**Priority**: HIGH

#### NFR-A-2: Sustainability
**Requirement**: Resource allocation for the integration engine and SMILE CDR should support automatic scaling to avoid over-provisioning and reduce energy consumption.
**Alignment**: Sustainability By Design principle
**Priority**: MEDIUM

### Compliance and Regulatory Requirements

#### NFR-C-1: NPHIES QNR Conformance
**Requirement**: The SMILE CDR implementation must pass all required testing for NPHIES QNR conformance.
**Applicable Regulations**: Saudi Ministry of Health / NPHIES Standards
**Priority**: CRITICAL

---

## Integration Requirements

### External System Integrations

#### INT-1: Mawid (Lean/Eatizaz)
**Purpose**: Patient appointment and clinic management.
**Integration Type**: Real-time API
**Data Exchanged**: Clinic Retrieval, Practitioners, Slots, Booking Notifications, Document Uploads.
**Integration Pattern**: Cerner -> Internal Rhapsody -> External Rhapsody -> Mawid (aligned with Asynchronous Communication where applicable)
**Priority**: CRITICAL

#### INT-2: NPHIES
**Purpose**: National health information exchange and insurance services.
**Integration Type**: Real-time API
**Data Exchanged**: ADT, Lab Orders/Reports, Rad Orders/Reports, Clinical Docs, CDA.
**Integration Pattern**: Cerner -> Rhapsody -> NPHIES (via XDS/FHIR)
**Priority**: CRITICAL

---

## Data Requirements

### Data Migration Requirements

**Migration Scope**: All relevant clinical, demographic, and historical data from the Legacy HIS/EMR to SMILE CDR.
**Migration Strategy**: ETL process translating legacy schemas to FHIR resources.
**Data Transformation**: Legacy tables must be mapped to valid FHIR R4 resources.
**Data Validation**: Pre and post-migration record counts and checksums.
**Alignment**: Single Source of Truth principle
**Priority**: CRITICAL

---

## Requirement Conflicts & Resolutions

*No major conflicts identified in the provided external context. Scope constraints are driven by NPHIES and Mawid external API requirements. Cloud First deployment for SMILE CDR may require balancing with specific data residency regulations.*

---

## External References

### Document Register

| Doc ID | Filename | Type | Source Location | Description |
|--------|----------|------|-----------------|-------------|
| EXT-01 | cerner | Note | `external/cerner` | Cerner context, Rhapsody usage, NPHIES status |
| EXT-02 | initial_discussion | Note | `external/initial_discussion` | Mawid/NPHIES scope and SMILE CDR migration |
| EXT-03 | mawid_integration | Note | `external/mawid_integration` | Mawid use cases and Practitioner issue |
| EXT-04 | NPHIES_QNR | Note | `external/NPHIES_QNR` | SMILE CDR and NPHIES conformance |
| PRIN-01| ARC-000-PRIN-v1.0 | Doc | `000-global/ARC-000-PRIN-v1.0.md` | Global Enterprise Architecture Principles |

### Citations

| Citation ID | Doc ID | Category | Quoted Passage |
|-------------|--------|----------|----------------|
| [REQ-C1] | EXT-03 | Issue | "Practitioners - Fetch doctor -- not working" |
| [REQ-C2] | EXT-01 | Scope | "Clinical Documents -- WIP", "CDA document request -- ??" |
| [REQ-C3] | EXT-04 | Compliance| "When we have smile CDR active... create a conformance" |
| [REQ-C4] | EXT-02 | Scope | "Data Migration from Legacy HIS/EMR to SMILE CDR" |

---

**Generated by**: ArcKit `$arckit-requirements` command
**Generated on**: 2026-04-20 10:45 GMT
**ArcKit Version**: 1.0.0
**Project**: Integration Strategy & SMILE CDR Migration (Project 001)
**AI Model**: Gemini 3.1 Pro (High)
**Generation Context**: Refreshed to incorporate global architecture principles from ARC-000-PRIN-v1.0
