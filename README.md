# MODHS-Consulting

Enterprise Architecture Governance Project

## Getting Started

This project uses ArcKit for enterprise architecture governance and vendor procurement.

### Available Commands

Once you start your AI assistant, you'll have access to these commands:

#### Project Planning
- `$arckit-plan` - Create project plan with timeline, phases, and gates

#### Core Workflow
- `$arckit-principles` - Create or update architecture principles
- `$arckit-stakeholders` - Analyze stakeholder drivers, goals, and outcomes
- `$arckit-risk` - Create comprehensive risk register (Orange Book)
- `$arckit-sobc` - Create Strategic Outline Business Case (Green Book 5-case)
- `$arckit-requirements` - Define comprehensive requirements
- `$arckit-data-model` - Create data model with ERD, GDPR compliance, data governance
- `$arckit-research` - Research technology, services, and products with build vs buy analysis
- `$arckit-wardley` - Create strategic Wardley Maps for build vs buy and procurement strategy

#### Vendor Procurement
- `$arckit-sow` - Generate Statement of Work (RFP)
- `$arckit-dos` - Digital Outcomes and Specialists (DOS) procurement (UK Digital Marketplace)
- `$arckit-gcloud-search` - Search G-Cloud services on UK Digital Marketplace
- `$arckit-gcloud-clarify` - Validate G-Cloud services and generate clarification questions
- `$arckit-evaluate` - Create vendor evaluation framework and score vendors

#### Design Review
- `$arckit-hld-review` - Review High-Level Design
- `$arckit-dld-review` - Review Detailed Design

#### Architecture Diagrams
- `$arckit-diagram` - Generate visual architecture diagrams using Mermaid

#### Sprint Planning
- `$arckit-backlog` - Generate prioritised product backlog with GDS user stories

#### Service Management
- `$arckit-servicenow` - Generate ServiceNow service design (CMDB, SLAs, incident/change management)

#### Traceability & Quality
- `$arckit-traceability` - Generate requirements traceability matrix
- `$arckit-analyze` - Comprehensive governance quality analysis

#### Template Customization
- `$arckit-customize` - Copy templates for customization (preserves across updates)

#### UK Government Compliance
- `$arckit-service-assessment` - GDS Service Standard assessment preparation
- `$arckit-tcop` - Technology Code of Practice assessment (all 13 points)
- `$arckit-ai-playbook` - AI Playbook compliance for responsible AI
- `$arckit-atrs` - Algorithmic Transparency Recording Standard (ATRS) record

#### Security Assessment
- `$arckit-secure` - UK Government Secure by Design (NCSC CAF, Cyber Essentials, UK GDPR)
- `$arckit-mod-secure` - MOD Secure by Design (JSP 440, IAMM, security clearances)
- `$arckit-jsp-936` - MOD JSP 936 AI assurance documentation

## Project Structure

```
MODHS-Consulting/
├── .arckit/
│   ├── scripts/
│   │   └── bash/
│   ├── templates/           # Default templates (refreshed by arckit init)
│   └── templates-custom/    # Your customizations (preserved across updates)
├── .agents/skills/          # Codex skills (auto-discovered)
├── projects/
│   ├── 000-global/
│   │   └── ARC-000-PRIN-v1.1.md (global principles)
│   └── 001-strategy-review/
│       ├── ARC-001-PLAN-v1.1.md
│       ├── ARC-001-REQ-v1.1.md
│       └── diagrams/
```

## Template Customization

ArcKit templates can be customized without modifying the defaults:

1. Run `$arckit-customize <template-name>` to copy a template for editing
2. Your customizations are stored in `.arckit/templates-custom/`
3. Commands automatically use your custom templates when present
4. Running `arckit init` again preserves your customizations

Example:
```
$arckit-customize requirements   # Copy requirements template
$arckit-customize all            # Copy all templates
```

## Execution Log

| Date | Action | Artifact | Description |
|------|--------|----------|-------------|
| 2026-04-18 | Initialized | - | ArcKit initialization and onboarding |
| 2026-04-19 | Project Planning | ARC-001-PLAN-v1.1 | Created project plan for Integration Strategy & SMILE CDR Migration |
| 2026-04-20 | Requirements | ARC-001-REQ-v1.1 | Defined business and technical requirements for Project 001 |
| 2026-04-20 | Principles | ARC-000-PRIN-v1.0 | Initial draft of enterprise architecture principles |
| 2026-04-27 | Principles | ARC-000-PRIN-v1.1 | Expanded principles to full template; added FHIR, PDPL, and operational details |
| 2026-04-27 | Requirements | ARC-001-REQ-v1.2 | Updated requirements to align with v1.1 principles and include MDM/NHIC scope |
| 2026-04-27 | Project Planning | ARC-001-PLAN-v1.2 | Updated plan to include MDM/EMPI, NHIC integration, and multi-system migration |
| 2026-04-27 | Architecture Design | ARC-001-DIAG-003/006 | Generated C4 Context, Container, Data Flow, and Deployment diagrams (v1.2 scope) |
| 2026-04-27 | Data Architecture | ARC-001-DATA-v1.0 | Created comprehensive data model with EMPI, NHIC sync, and FHIR R4 mapping |
| 2026-04-27 | Design Review | ARC-001-HLDR-v1.0 | HLD Review completed; APPROVED WITH CONDITIONS (DR & Data Quality) |
| 2026-04-27 | Governance | ARC-001-STKE-v1.0 | Analyzed stakeholder drivers and goals; established RACI matrix |
| 2026-04-27 | Risk Management | ARC-001-RISK-v1.0 | Initial risk register created; 1 Critical and 2 High risks identified |
| 2026-04-27 | Strategy | ARC-001-ROAD-v1.0 | 3-year strategic roadmap (2026-2028) created for clinical consolidation |
| 2026-04-27 | Business Case | ARC-001-SOBC-v1.0 | Strategic Outline Business Case created; Recommended Option 2 (Balanced) |
| 2026-04-27 | Delivery Planning | ARC-001-BKLG-v1.0 | Product backlog generated (42 stories/tasks) with 8-sprint plan |
| 2026-04-27 | Stakeholder Comms | ARC-001-PRES-v1.0 | Executive briefing deck (12 slides) created for Steering Committee |
| 2026-04-28 | Governance | ARC-001-STORY-v1.0 | Project governance story generated with full timeline and traceability analysis |

## Next Steps

1. Run `$arckit-stakeholders` to analyze stakeholder drivers and goals
2. Begin technical research for SMILE CDR deployment with `$arckit-research`
3. Generate architecture diagrams with `$arckit-diagram`

## Documentation

- [ArcKit Documentation](https://github.com/github/arc-kit)
- [Architecture Principles Guide](https://github.com/github/arc-kit/docs/principles.md)
- [Vendor Procurement Guide](https://github.com/github/arc-kit/docs/procurement.md)
