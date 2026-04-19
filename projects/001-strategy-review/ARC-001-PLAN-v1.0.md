# Project Plan: Strategy Review

> **Template Origin**: Official | **ArcKit Version**: 1.0.0 | **Command**: `$arckit-plan`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-PLAN-v1.0 |
| **Document Type** | Project Plan |
| **Project** | Strategy Review (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-04-19 |
| **Last Modified** | 2026-04-19 |
| **Review Cycle** | Quarterly |
| **Next Review Date** | 2026-05-19 |
| **Owner** | Project Manager |
| **Reviewed By** | [PENDING] |
| **Approved By** | [PENDING] |
| **Distribution** | Project Team, Architecture Team |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-04-19 | ArcKit AI | Initial creation from `$arckit-plan` command | PENDING | PENDING |

---

## Executive Summary

**Project**: Strategy Review
**Duration**: 6-12 months (Medium Complexity)
**Budget**: £[PENDING]
**Team**: [PENDING] FTE average
**Delivery Model**: Hybrid (Agile delivery within waterfall governance gates)

**Objective**: Comprehensive strategy and governance review for MODHS.

**Success Criteria**:

- Strategy alignment achieved across major stakeholders
- Clear governance gates established and approved
- Risk register mitigations actively managed
- Vendor evaluation framework defined and executed

**Key Milestones**:

- Discovery Complete: Week 6
- Alpha Complete (HLD & Vendor Selection approved): Week 16
- Beta Complete (Go-Live approved): Week 32
- Production Launch: Week 33

---

## Timeline Overview (Gantt Chart)

```mermaid
gantt
    title Strategy Review - Project Timeline
    dateFormat YYYY-MM-DD

    section Discovery
    Stakeholder Analysis          :a1, 2026-04-19, 2w
    User Research                 :a2, after a1, 2w
    Business Requirements         :a3, after a2, 2w
    Architecture Principles       :a4, after a3, 1w
    Initial Business Case         :a5, after a4, 1w
    Discovery Assessment          :milestone, m1, after a5, 0d

    section Alpha
    Detailed Requirements         :b1, after m1, 3w
    Architecture Design (HLD)     :b2, after b1, 4w
    Vendor Procurement (SOW)      :b3, after b1, 2w
    Vendor Evaluation             :b4, after b3, 3w
    Vendor Selection              :milestone, m2, after b4, 0d
    HLD Review Preparation        :b5, after b2, 1w
    HLD Review & Approval         :milestone, m3, after b5, 0d
    Security Threat Model         :b6, after b2, 2w
    Updated Business Case         :b7, after b4, 1w
    Alpha Assessment              :milestone, m4, after b7, 0d

    section Beta
    Detailed Design (DLD)         :c1, after m4, 4w
    DLD Review & Approval         :milestone, m5, after c1, 0d
    Sprint 1 - Core Services      :c2, after m5, 3w
    Sprint 2 - Integrations       :c3, after c2, 3w
    Sprint 3 - UI & Reporting     :c4, after c3, 3w
    Sprint 4 - Testing & Hardening:c5, after c4, 3w
    Security Testing (SAST/DAST)  :c6, after c5, 2w
    Performance Testing           :c7, after c6, 2w
    User Acceptance Testing (UAT) :c8, after c7, 2w
    Operational Readiness         :c9, after c8, 1w
    Beta Assessment (Go/No-Go)    :milestone, m6, after c9, 0d

    section Live
    Production Deployment         :d1, after m6, 1w
    Hypercare                     :d2, after d1, 4w
    Benefits Realization Tracking :d3, after d2, 8w
```

---

## Workflow & Gates Diagram

```mermaid
graph TB
    Start[Project Initiation] --> Discovery

    Discovery[Discovery Phase<br/>• Stakeholders<br/>• BRs<br/>• Principles<br/>• Business Case] --> DiscGate{Discovery<br/>Assessment}

    DiscGate -->|✅ Approved| Alpha
    DiscGate -->|❌ Rejected| Stop1[Stop/Pivot]

    Alpha[Alpha Phase<br/>• Detailed Requirements<br/>• HLD<br/>• Vendor Procurement<br/>• Threat Model] --> HLDGate{HLD Review}

    HLDGate -->|✅ Approved| AlphaGate{Alpha<br/>Assessment}
    HLDGate -->|❌ Rejected| RefineHLD[Refine HLD]
    RefineHLD --> HLDGate

    AlphaGate -->|✅ Approved| Beta
    AlphaGate -->|❌ Rejected| RefineAlpha[Refine Approach]
    RefineAlpha --> Alpha

    Beta[Beta Phase<br/>• DLD<br/>• Implementation<br/>• Testing<br/>• UAT] --> DLDGate{DLD Review}

    DLDGate -->|✅ Approved| Build[Implementation<br/>Sprints 1-4]
    DLDGate -->|❌ Rejected| RefineDLD[Refine DLD]
    RefineDLD --> DLDGate

    Build --> Testing[Security &<br/>Performance<br/>Testing]
    Testing --> UAT{UAT Pass?}
    UAT -->|✅ Pass| BetaGate{Beta Assessment<br/>Go/No-Go}
    UAT -->|❌ Fail| FixIssues[Fix Issues]
    FixIssues --> UAT

    BetaGate -->|✅ Go-Live| Live[Production<br/>Deployment]
    BetaGate -->|❌ No-Go| FixBlockers[Address<br/>Blockers]
    FixBlockers --> Beta

    Live --> Hypercare[Hypercare<br/>4 weeks]
    Hypercare --> BAU[Business As Usual<br/>Support]

    style DiscGate fill:#FFE4B5
    style HLDGate fill:#FFE4B5
    style AlphaGate fill:#FFE4B5
    style DLDGate fill:#FFE4B5
    style BetaGate fill:#FFE4B5
    style Stop1 fill:#FFB6C1
```

---

## Discovery Phase (Weeks 1-6)

**Objective**: Validate problem and approach

### Activities & Timeline

| Week | Activity | ArcKit Command | Deliverable |
|------|----------|----------------|-------------|
| 1-2 | Stakeholder Analysis | `$arckit-stakeholders` | Stakeholder map, drivers, goals |
| 3-4 | User Research | Manual | User needs, pain points |
| 5-6 | Business Requirements | `$arckit-requirements` | BRs with acceptance criteria |
| 7 | Architecture Principles | `$arckit-principles` | 10-15 principles |
| 8 | Initial Business Case | `$arckit-sobc` | Cost/benefit analysis |
| 8 | Initial Risk Register | `$arckit-risk` | Top 10 risks |

### Gate: Discovery Assessment (Week 8)

**Approval Criteria**:

- [ ] Problem clearly defined and validated
- [ ] User needs documented
- [ ] Business Requirements defined (15-25 BRs)
- [ ] Architecture principles agreed
- [ ] Business case shows positive ROI
- [ ] No critical risks without mitigation
- [ ] Stakeholder buy-in confirmed

**Approvers**: SRO, Architecture Board

**Possible Outcomes**:

- ✅ **Go to Alpha** - Problem validated, approach feasible
- 🔄 **Pivot** - Adjust approach based on findings
- ❌ **Stop** - Problem not worth solving or approach not feasible

---

## Alpha Phase (Weeks 9-16)

**Objective**: Design the solution and validate approach

### Activities & Timeline

| Week | Activity | ArcKit Command | Deliverable |
|------|----------|----------------|-------------|
| 9-11 | Detailed Requirements | `$arckit-requirements` | FR, NFR, INT, DR |
| 10-12 | Data Model | `$arckit-data-model` | Entity relationships |
| 11-14 | Architecture Design | `$arckit-diagram` | HLD with C4 diagrams |
| 11-13 | Generate SOW/RFP | `$arckit-sow` | Vendor procurement docs |
| 14-16 | Vendor Evaluation | `$arckit-evaluate` | Scoring matrix |
| 16 | Security Threat Model | Manual | STRIDE analysis |
| 17 | HLD Review | `$arckit-hld-review` | HLD approval |
| 18 | Updated Business Case | `$arckit-sobc` | Revised costs |

### Gate: HLD Review (Week 17)

**Approval Criteria**:

- [ ] All MUST requirements addressed in design
- [ ] Architecture principles compliant
- [ ] Security architecture defined
- [ ] Integration approach documented
- [ ] Performance approach documented
- [ ] No unmitigated high risks

**Approvers**: Architecture Board, Security Lead

### Gate: Alpha Assessment (Week 18)

**Approval Criteria**:

- [ ] HLD approved
- [ ] Vendor selected (if applicable)
- [ ] Business case updated with accurate costs
- [ ] Team and budget confirmed for Beta
- [ ] Technical feasibility demonstrated

**Approvers**: SRO, Architecture Board, Finance

**Possible Outcomes**:

- ✅ **Go to Beta** - Design validated, ready to build
- 🔄 **Iterate** - Refine design based on feedback
- ❌ **Stop** - Approach not feasible or business case negative

---

## Beta Phase (Weeks 19-32)

**Objective**: Build, test, and prepare for live

### Activities & Timeline

| Week | Activity | ArcKit Command | Deliverable |
|------|----------|----------------|-------------|
| 19-22 | Detailed Design (DLD) | Manual | DLD document |
| 23 | DLD Review | `$arckit-dld-review` | DLD approval |
| 24-26 | Sprint 1 - Core Services | Manual | Working software |
| 27-29 | Sprint 2 - Integrations | Manual | Integrated system |
| 30-32 | Sprint 3 - UI & Reporting | Manual | User interface |
| 33-35 | Sprint 4 - Hardening | Manual | Production-ready code |
| 36-37 | Security Testing | Manual | SAST/DAST results |
| 38-39 | Performance Testing | Manual | Load test results |
| 40-41 | UAT | Manual | User sign-off |
| 42 | Operational Readiness | `$arckit-operationalize` | Runbooks, DR plan |
| 42 | Quality Analysis | `$arckit-analyze` | Final quality check |

### Gate: DLD Review (Week 23)

**Approval Criteria**:

- [ ] DLD aligns with approved HLD
- [ ] All implementation details documented
- [ ] Security controls specified
- [ ] Test strategy defined
- [ ] Deployment approach documented

**Approvers**: Technical Lead, Architecture Board

### Gate: Beta Assessment / Go-Live (Week 42)

**Approval Criteria**:

- [ ] All MUST requirements implemented and tested
- [ ] Security testing passed (no critical/high vulnerabilities)
- [ ] Performance testing passed (meets NFR-P targets)
- [ ] UAT signed off by business
- [ ] Operational readiness confirmed
- [ ] DR/BCP tested
- [ ] Support team trained

**Approvers**: SRO, Architecture Board, Security Lead, Operations Lead

**Possible Outcomes**:

- ✅ **Go-Live** - Ready for production deployment
- 🔄 **Fix Issues** - Address blockers before go-live
- ❌ **No-Go** - Major issues require significant rework

---

## Live Phase (Week 43+)

**Objective**: Deploy, stabilize, and realize benefits

### Activities & Timeline

| Week | Activity | ArcKit Command | Deliverable |
|------|----------|----------------|-------------|
| 43 | Production Deployment | Manual | Live system |
| 44-47 | Hypercare | Manual | Issue resolution |
| 48+ | Benefits Tracking | `$arckit-sobc` | Benefits realization |
| Quarterly | Quality Reviews | `$arckit-analyze` | Ongoing compliance |
| Quarterly | Risk Updates | `$arckit-risk` | Updated risk register |

---

## ArcKit Commands Integration

### Discovery Phase

- Week 1-2: `$arckit-stakeholders` - Stakeholder analysis
- Week 5-6: `$arckit-requirements` - Business Requirements (BRs)
- Week 7: `$arckit-principles` - Architecture principles
- Week 8: `$arckit-sobc` - Initial business case
- Week 8: `$arckit-risk` - Initial risk register

### Alpha Phase

- Week 9-11: `$arckit-requirements` - Detailed requirements (FR, NFR, INT, DR)
- Week 10-12: `$arckit-data-model` - Data model
- Week 11-14: `$arckit-diagram` - Architecture diagrams (C4)
- Week 11-13: `$arckit-sow` - Generate SOW/RFP (if vendor needed)
- Week 14-16: `$arckit-evaluate` - Vendor evaluation (if applicable)
- Week 17: `$arckit-hld-review` - HLD approval gate
- Week 18: `$arckit-sobc` - Updated business case

### Beta Phase

- Week 23: `$arckit-dld-review` - DLD approval gate
- Week 42: `$arckit-analyze` - Quality analysis
- Week 42: `$arckit-traceability` - Verify design → code → tests
- If AI: `$arckit-ai-playbook`, `$arckit-atrs` - AI compliance

### Live Phase

- Quarterly: `$arckit-analyze` - Periodic quality reviews
- Quarterly: `$arckit-risk` - Update operational risks
- Annually: `$arckit-sobc` - Track benefits realization

---

## Resource Plan

### Team Sizing by Phase

| Phase | Duration | Team Size | Key Roles |
|-------|----------|-----------|-----------|
| Discovery | 6 weeks | [N] FTE | BA, Architect, UX Researcher |
| Alpha | 10 weeks | [N] FTE | BA, Architect, Tech Lead, Security |
| Beta | 16 weeks | [N] FTE | Full dev team, QA, DevOps |
| Live | Ongoing | [N] FTE | Support, Operations |

### Budget Summary

| Phase | Duration | Team Cost | Infrastructure | Vendor/License | Total |
|-------|----------|-----------|----------------|----------------|-------|
| Discovery | 6 weeks | £[X] | £[X] | £[X] | £[X] |
| Alpha | 10 weeks | £[X] | £[X] | £[X] | £[X] |
| Beta | 16 weeks | £[X] | £[X] | £[X] | £[X] |
| Live (Year 1) | 12 months | £[X] | £[X] | £[X] | £[X] |
| **Total** | | | | | **£[TOTAL]** |

---

## Risks & Assumptions

### Key Risks

| Risk | Impact | Likelihood | Mitigation |
|------|--------|------------|------------|
| Vendor Selection Delays | High | Medium | Start procurement early in Alpha |
| Scope Creep in Agile | Medium | High | Strict governance gates before sprint execution |
| Resource Unavailability | High | Low | Early lock-in of project team members |

### Key Assumptions

- Governance gates will be evaluated in a timely manner (within 1 week)
- Hybrid delivery approach is fully supported by external vendors
- The strategy review scope is confined to currently defined business units

### Dependencies

- Completion of existing strategy audits
- Availability of key stakeholders for interviews and reviews
- Enterprise architecture team support for HLD/DLD reviews

---

## Appendix A: Glossary

| Term | Definition |
|------|------------|
| GDS | Government Digital Service |
| HLD | High-Level Design |
| DLD | Detailed-Level Design |
| UAT | User Acceptance Testing |
| SRO | Senior Responsible Owner |
| BA | Business Analyst |
| NFR | Non-Functional Requirement |

## External References

> This section provides traceability from generated content back to source documents.
> Follow citation instructions in the project's citation reference guide.

### Document Register

| Doc ID | Filename | Type | Source Location | Description |
|--------|----------|------|-----------------|-------------|
| *None provided* | — | — | — | — |

### Citations

| Citation ID | Doc ID | Page/Section | Category | Quoted Passage |
|-------------|--------|--------------|----------|----------------|
| — | — | — | — | — |

### Unreferenced Documents

| Filename | Source Location | Reason |
|----------|-----------------|--------|
| — | — | — |

---

**Generated by**: ArcKit `$arckit-plan` command
**Generated on**: 2026-04-19 13:58 GMT
**ArcKit Version**: 1.0.0
**Project**: Strategy Review (Project 001)
**AI Model**: Gemini 3.1 Pro (High)
**Generation Context**: Initial project plan based on user prompts
