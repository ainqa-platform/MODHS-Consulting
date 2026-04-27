# Strategic Outline Business Case (SOBC): MODHS Integration Platform

> **Template Origin**: Official | **ArcKit Version**: 1.0.0 | **Command**: `/arckit.sobc`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-SOBC-v1.0 |
| **Document Type** | Strategic Outline Business Case (SOBC) |
| **Project** | Integration Strategy & SMILE CDR Migration (Project 001) |
| **Classification** | OFFICIAL-SENSITIVE |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-04-27 |
| **Last Modified** | 2026-04-27 |
| **Owner** | Chief Data Officer (MODHS) |
| **Reviewed By** | PENDING |
| **Approved By** | PENDING |

## Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2026-04-27 | ArcKit AI | Initial strategic case for clinical data consolidation and migration |

---

## 1. Executive Summary

This Strategic Outline Business Case (SOBC) proposes the establishment of the MODHS Integration Platform, powered by SMILE CDR and a central Master Patient Index (EMPI). The project addresses the critical fragmentation of patient data across PSMMC's legacy HIS systems and the Cerner EMR, while ensuring compliance with KSA national health mandates (NPHIES, Mawid, NHIC) and the Saudi Personal Data Protection Law (PDPL).

**Recommended Option**: Option 2 (Balanced - Consolidated SMILE CDR + KSA Cloud).
**Estimated Investment**: £15.2M (SAR 72.5M) over 3 years.
**Benefit-Cost Ratio (BCR)**: 2.8:1 (Estimated).
**Payback Period**: 22 months.

---

## 2. Strategic Case

### 2.1 Problem Statement
MODHS currently operates 5+ legacy HIS systems alongside the Cerner EMR at PSMMC. This fragmentation results in:
- **Patient Safety Risk**: Clinicians lack a unified longitudinal view of patient history, allergy, and medication data.
- **Compliance Gaps**: Difficulty in scaling national reporting (NPHIES) and identity verification (NHIC).
- **Technical Debt**: High operational costs for maintaining unsupported legacy hardware and databases.

### 2.2 Strategic Alignment
- **Vision 2030 (Health Sector Transformation)**: Modernizing digital health infrastructure and enhancing interoperability.
- **MODHS Principles**: Aligning with "FHIR First" (PRIN-12) and "Data Sovereignty" (PRIN-8).

### 2.3 Spending Objectives
1. **Consolidate** 100% of available clinical data into a single FHIR R4 repository by Q4 2027.
2. **Synchronize** 2.5M patient identities with the National NHIC Patient Registry.
3. **Decommission** 5+ legacy HIS systems to reduce annual IT maintenance costs by 40%.
4. **Achieve** 100% national compliance for NPHIES and Mawid integration.

---

## 3. Economic Case (Options Appraisal)

| Feature | Option 0: Do Nothing | Option 1: Minimal (Cerner Only) | Option 2: Balanced (Recommended) | Option 3: Comprehensive (HIE) |
|---------|-----------------------|----------------------------------|-----------------------------------|-------------------------------|
| **Scope** | Maintain existing silos | SMILE CDR for Cerner data only | Consolidated CDR + EMPI + Cloud | Full MOD-wide HIE (KSA) |
| **Strategic Fit**| Poor | Low | **High** | Very High |
| **Benefits** | Zero | 30% | **85%** | 100% |
| **Complexity** | N/A | Low | **Medium** | High |
| **ROM Cost** | £0 (Direct) | £4.5M | **£15.2M** | £45.0M+ |
| **BCR** | 1:1 (Negative) | 1.8:1 | **2.8:1** | 2.1:1 |

**Rationale for Recommended Option**: Option 2 provides the highest ROI by consolidating all available MODHS systems (not just Cerner) into a single hub, enabling the decommissioning of expensive legacy debt while keeping the scope manageable and focused on PSMMC.

---

## 4. Commercial Case

### 4.1 Procurement Strategy
- **SMILE CDR**: Enterprise license procurement via KSA-authorized partner.
- **Cloud Hosting**: Leveraging existing MODHS/Government framework agreements for Oracle Cloud Riyadh or Google Cloud Dammam.
- **Rhapsody**: Expansion of existing license and support.

---

## 5. Financial Case

### 5.1 Budget Requirement (3-Year Forecast)

| Category | Year 1 (Foundation) | Year 2 (Integration) | Year 3 (Transformation) | Total |
|----------|---------------------|----------------------|-------------------------|-------|
| Licensing | £3.2M | £1.5M | £1.5M | £6.2M |
| Cloud Ops | £0.8M | £1.2M | £1.4M | £3.4M |
| Pro Services| £2.5M | £1.5M | £1.0M | £5.0M |
| Training | £0.2M | £0.2M | £0.2M | £0.6M |
| **Total** | **£6.7M** | **£4.4M** | **£4.1M** | **£15.2M** |

**Affordability**: To be confirmed via MODHS Finance Department based on proposed legacy HIS cost savings (Est. £3M annually).

---

## 6. Management Case

### 6.1 Governance & Resource
- **SRO**: Medical Director (MODHS).
- **Project Manager**: To be assigned from PMO.
- **Architecture Lead**: ArcKit / Enterprise Architecture Team.

### 6.2 Key Risks (from ARC-001-RISK-v1.0)
1. **R-004 (Critical)**: Disaster Recovery Runbook Gaps. Mitigation: Automated failover development.
2. **R-005 (High)**: Legacy Data Corruption. Mitigation: Data Quality Dashboard for EMPI matching.
3. **R-003 (High)**: Hybrid Cloud Latency. Mitigation: KSA-based region and network baseline testing.

---

**Generated by**: ArcKit `$arckit-sobc` command
**Generated on**: 2026-04-27 12:30 GMT
**ArcKit Version**: 1.0.0
**Project**: Integration Strategy & SMILE CDR Migration (Project 001)
**AI Model**: Gemini 3.1 Pro (High)
**Generation Context**: Initial business case based on ROAD-v1.0, STKE-v1.0, and RISK-v1.0
