# MODHS Enterprise Architecture Principles

> **Template Origin**: Official | **ArcKit Version**: 1.0 | **Command**: `$arckit-principles`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-000-PRIN-v1.1 |
| **Document Type** | Enterprise Architecture Principles |
| **Project** | MODHS Global (Project 000) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.1 |
| **Created Date** | 2026-04-20 |
| **Last Modified** | 2026-04-27 |
| **Review Cycle** | Annual |
| **Next Review Date** | 2027-04-20 |
| **Owner** | Enterprise Architecture Review Board |
| **Reviewed By** | AI Assistant (2026-04-27) |
| **Approved By** | PENDING |
| **Distribution** | Enterprise Architects, Development Teams, PSMMC Stakeholders |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-04-20 | ArcKit AI | Initial creation from `$arckit-principles` command | AI Assistant | 2026-04-20 |
| 1.1 | 2026-04-27 | ArcKit AI | Expanded to full template structure; added healthcare-specific (FHIR/PDPL) and operational principles | PENDING | PENDING |

---

## Executive Summary

This document establishes the immutable principles governing all technology architecture decisions at MODHS. These principles ensure consistency, security, scalability, and alignment with business strategy across all projects and initiatives, specifically aligning with TCoP (Technology Code of Practice), Saudi PDPL (Personal Data Protection Law), and international healthcare standards (FHIR/HL7).

**Scope**: All technology projects, systems, and initiatives within MODHS and its medical cities (e.g., PSMMC).
**Authority**: Enterprise Architecture Review Board.
**Compliance**: Mandatory unless exception approved by CTO/CIO.

**Philosophy**: These principles are **technology-agnostic** - they describe WHAT qualities the architecture must have, not HOW to implement them with specific products. Technology selection happens during research and design phases guided by these principles.

---

## I. Strategic Principles

### 1. Cloud First and Scalability

**Principle Statement**:
All new systems MUST be designed for cloud deployment and horizontal scalability, defaulting to public cloud infrastructure unless security, data residency, or regulatory constraints mandate otherwise.

**Rationale**:
Cloud-first aligns with TCoP guidelines and provides the elastic capacity required to handle variable healthcare data demands and national integration loads (e.g., NPHIES/Mawid).

**Implications**:
- Design for stateless components that can be replicated.
- Avoid hard-coded limits or fixed capacity assumptions.
- Utilize cloud-native patterns (containers, serverless) where feasible.
- Plan for distributed deployment across multiple availability zones.

**Validation Gates**:
- [ ] System can scale horizontally without manual reconfiguration.
- [ ] No single points of failure limiting scale.
- [ ] Cloud-native architecture used as the default option.
- [ ] Scaling metrics and triggers defined.

---

### 2. Open Source Default

**Principle Statement**:
Projects SHOULD evaluate and utilize open-source software and standards over proprietary alternatives whenever they meet the required security, supportability, and capability thresholds.

**Rationale**:
Open source prevents vendor lock-in, reduces licensing costs, and promotes interoperability. It aligns with the "Open Source" pillar of the MODHS strategy.

**Implications**:
- Perform "build vs buy vs open source" analysis during discovery.
- Ensure open-source components have active communities and security support.
- Contribute back to the community where appropriate.

**Validation Gates**:
- [ ] Open-source options evaluated during research.
- [ ] License compliance verified (e.g., no restrictive Copyleft for internal apps).
- [ ] Support model for open-source components defined.

---

### 3. Sustainability By Design

**Principle Statement**:
Architectures MUST optimize resource utilization to minimize the carbon footprint and energy consumption of IT operations.

**Rationale**:
Efficient architectures are both environmentally and economically responsible. This aligns with TCoP sustainability goals.

**Implications**:
- Use auto-scaling to match capacity to demand exactly.
- Optimize data storage and retention to avoid "dark data" accumulation.
- Choose energy-efficient regions or providers where possible.

**Validation Gates**:
- [ ] Resource allocation matches demand metrics.
- [ ] Decommissioning plan for old resources exists.
- [ ] Efficient data processing patterns (e.g., event-driven) used.

---

### 4. Resilience and Fault Tolerance

**Principle Statement**:
All systems MUST gracefully degrade when dependencies fail and recover automatically without data loss or manual intervention.

**Rationale**:
Failures are inevitable in complex integrations like Cerner, Rhapsody, and NPHIES. The architecture must assume failures and design for continuity.

**Implications**:
- Implement circuit breakers and retries for external APIs.
- Use bulkhead isolation to prevent cascading failures.
- Automated health checks and self-healing.

**Validation Gates**:
- [ ] Failure modes identified and mitigated (FMEA).
- [ ] RTO (Recovery Time Objective) and RPO (Recovery Point Objective) defined.
- [ ] Automated failover tested.

---

### 5. Observability and Operational Excellence

**Principle Statement**:
All systems MUST emit structured telemetry (logs, metrics, traces) enabling real-time monitoring, troubleshooting, and capacity planning.

**Rationale**:
Operational visibility is critical for managing patient-critical integrations. We cannot operate what we cannot observe.

**Implications**:
- Use correlation IDs across service boundaries (Cerner -> Rhapsody -> External).
- Define Service Level Indicators (SLIs) for key patient journeys.
- Structured logging (JSON) for easy analysis.

**Validation Gates**:
- [ ] Centralized logging and monitoring configured.
- [ ] Alerts mapped to actionable runbooks.
- [ ] Dashboard exists for system health.

---

## II. Data and Privacy Principles

### 6. Privacy Integral (Privacy By Design)

**Principle Statement**:
Privacy controls and data minimization MUST be embedded into the design phase of all applications, not added as an afterthought.

**Rationale**:
Healthcare systems handle sensitive Personal Health Information (PHI). Compliance with Saudi PDPL and international standards is non-negotiable.

**Implications**:
- Mask or pseudonymize PHI where full visibility is not required.
- Implement least-privilege access for all users and services.
- Data protection impact assessments (DPIA) performed early.

**Validation Gates**:
- [ ] PDPL compliance verified.
- [ ] Data minimization principles applied.
- [ ] Encryption at rest and in transit implemented.

---

### 7. Single Source of Truth

**Principle Statement**:
Every data domain MUST have a single authoritative source. Derived copies must be clearly labeled and synchronized.

**Rationale**:
Multiple authoritative sources create inconsistency, reconciliation overhead, and data integrity issues. For clinical data, the EMR/CDR is the truth.

**Implications**:
- Identify the system of record (e.g., SMILE CDR for clinical objects).
- Synchronize derived caches via event-driven updates.
- Prohibit bidirectional sync without master conflict resolution.

**Validation Gates**:
- [ ] System of record identified for each data entity.
- [ ] Synchronization strategy documented.
- [ ] No split-brain scenarios in data flow.

---

### 8. Data Sovereignty and Residency

**Principle Statement**:
All Personal Health Information (PHI) MUST reside within the Kingdom of Saudi Arabia (KSA) unless explicit regulatory approval is obtained.

**Rationale**:
Compliance with local data residency laws (NDMO, PDPL) is mandatory for healthcare data.

**Implications**:
- Use local cloud regions or on-premise infrastructure.
- Cross-border data transfers require legal and regulatory basis.
- Audit trails for data access must be maintained locally.

**Validation Gates**:
- [ ] Data residency verified.
- [ ] Access logs stored and audited.
- [ ] Regulatory approval for any external processing.

---

## III. Integration Principles

### 9. Interoperability and Standard Interfaces

**Principle Statement**:
Systems MUST expose functionality through well-defined, versioned interfaces using industry-standard protocols. Healthcare integrations MUST prioritize HL7 FHIR R4 (KSA Profiles).

**Rationale**:
Loose coupling through standard interfaces enables independent evolution and seamless national integration (Mawid, NPHIES).

**Implications**:
- Use RESTful APIs with FHIR standards for all clinical data exchange.
- Direct database access across system boundaries is prohibited.
- Version all APIs to support backward compatibility.

**Validation Gates**:
- [ ] API specifications published (e.g., OpenAPI, FHIR profiles).
- [ ] Versioning strategy defined.
- [ ] No direct DB coupling.

---

### 10. Asynchronous Communication

**Principle Statement**:
Systems SHOULD use asynchronous communication for non-real-time interactions to improve resilience and decoupling.

**Rationale**:
Asynchronous patterns reduce temporal coupling and improve fault tolerance, especially when integrating with external systems like NPHIES.

**Implications**:
- Use message queues or event streams for notifications and batch updates.
- Implement idempotency on all event consumers.
- Dead-letter queues (DLQ) for failed message processing.

**Validation Gates**:
- [ ] Async patterns used for non-critical path flows.
- [ ] Idempotency handles retries correctly.
- [ ] Message durability and monitoring in place.

---

## IV. Quality and Security Attributes

### 11. Security by Design (Zero Trust)

**Principle Statement**:
All architectures MUST implement defense-in-depth security with zero-trust principles. Security is a foundational requirement, not a feature.

**Rationale**:
Healthcare architectures are high-value targets. Security must be foundational to protect against breaches and ensure patient safety.

**Implications**:
- No network-based trust; every request must be authenticated.
- Service-to-service authentication (e.g., mTLS).
- Secrets management via secure vaults (no hardcoded keys).

**Validation Gates**:
- [ ] Threat model completed.
- [ ] Multi-factor authentication (MFA) for administrative access.
- [ ] Secrets stored in managed vaults.

---

### 12. Performance and Efficiency

**Principle Statement**:
All systems MUST meet defined performance targets (latency, throughput) under expected load with efficient resource use.

**Rationale**:
Patient care depends on responsive systems. Latency in clinical integrations (e.g., Practitioner fetch) can impact operations.

**Implications**:
- Performance requirements defined in discovery.
- Load testing performed before production deployment.
- Hot paths identified and optimized.

**Validation Gates**:
- [ ] Performance SLAs defined and met.
- [ ] Scalability tests validated.
- [ ] Resource efficiency (CPU/Mem) within targets.

---

### 13. Maintainability and Evolvability

**Principle Statement**:
All systems MUST be designed for change, with clear separation of concerns, modular architecture, and comprehensive documentation.

**Rationale**:
Healthcare systems have long lifecycles. Design decisions should optimize for long-term understandability.

**Implications**:
- Modular architecture with clear boundaries (e.g., Domain-Driven Design).
- Separation of business logic from infrastructure/integration logic.
- Use of ADRs (Architecture Decision Records) to document choices.

**Validation Gates**:
- [ ] Architecture documentation current.
- [ ] ADRs created for significant decisions.
- [ ] Modular code structure verified.

---

## V. Development Practices

### 14. Infrastructure as Code (IaC)

**Principle Statement**:
All infrastructure MUST be defined as code, version-controlled, and deployed through automated pipelines.

**Rationale**:
Manual infrastructure changes create drift and inconsistency. IaC enables repeatability and rapid disaster recovery.

**Implications**:
- No manual changes to production environments ("No-Ops").
- Infrastructure code follows the same review process as application code.
- Environments are reproducible from source.

**Validation Gates**:
- [ ] Infrastructure defined in code (Terraform, CloudFormation, etc.).
- [ ] CI/CD pipeline deploys infrastructure.
- [ ] No drift between code and live state.

---

### 15. Automated Testing

**Principle Statement**:
All code and configuration changes MUST be validated through automated testing before deployment to production.

**Rationale**:
Ensures quality and prevents regressions in critical clinical flows.

**Implications**:
- Implement unit, integration, and end-to-end tests.
- Security scanning (SAST/DAST) included in pipeline.
- Test coverage targets defined and monitored.

**Validation Gates**:
- [ ] Automated tests pass in CI.
- [ ] Coverage meets project thresholds.
- [ ] Critical patient journeys covered by E2E tests.

---

### 16. Continuous Integration and Deployment (CI/CD)

**Principle Statement**:
All changes MUST go through automated build, test, and deployment pipelines with quality gates at each stage.

**Rationale**:
Reduces deployment risk and improves the speed of delivering updates to clinical staff.

**Implications**:
- Automated rollbacks for failed deployments.
- Quality gates (security, performance, testing) enforced.
- Frequent, small releases favored over large, risky ones.

**Validation Gates**:
- [ ] CI/CD pipeline operational.
- [ ] Quality gates configured.
- [ ] Deployment success metrics tracked.

---

## VI. Exception Process

Principles are mandatory unless a documented exception is approved.

1. **Submit**: Provide business/technical rationale for the deviation.
2. **Review**: Architecture Board evaluates risk and duration.
3. **Approve**: CTO/CIO sign-off for major deviations.
4. **Log**: Document in project artifacts and review quarterly.

---

**Generated by**: ArcKit `$arckit-principles` command
**Generated on**: 2026-04-27
**ArcKit Version**: 1.0
**Project**: MODHS Global (Project 000)
**AI Model**: Gemini 3.1 Pro (High)
