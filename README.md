# OptimalPrint Automation Registry

> Central documentation hub for OptimalPrint's custom automation systems, workflows, and integrations.

---

## Repository Structure

```
optimalprint-automation/
├── README.md                    # This file - System Registry
├── context/
│   └── technical-context.md     # Technical environment documentation
├── specifications/
│   ├── analytics/               # Analytics & tracking specs
│   ├── feeds/                   # Product feed specs
│   └── content/                 # Content automation specs
├── templates/
│   ├── problem-definition.md    # Template for new projects
│   └── technical-specification.md
├── workflows/                   # Exported n8n workflow JSONs
└── decisions/                   # Architecture Decision Records
```

---

## Active Systems

### Analytics & Tracking

| System | Purpose | Location | Spec | Status | Last Updated |
|--------|---------|----------|------|--------|--------------|
| Card Category Tracking | Categorize card pages in Amplitude via derived properties | Amplitude | [Pending] | Active | 2025-01 |

### Product Feeds

| System | Purpose | Location | Spec | Status | Last Updated |
|--------|---------|----------|------|--------|--------------|
| Blueshift Apparel Feed | Best-seller recommendations for apparel | n8n Workflow #[ID] | [Pending] | Active | 2025-01 |

### Content Automation

| System | Purpose | Location | Spec | Status | Last Updated |
|--------|---------|----------|------|--------|--------------|
| Landing Page Generator | AI-assisted Contentful page creation | n8n Workflow #[ID] | [Pending] | In Development | 2024-12 |

---

## Deprecated Systems

| System | Reason | Deprecated Date | Replacement |
|--------|--------|-----------------|-------------|
| *None yet* | | | |

---

## Pending Development

| System | Problem Definition | Priority | Target Date |
|--------|-------------------|----------|-------------|
| *Add new projects here* | [Link] | | |

---

## Quick Links

### Documentation
- [Technical Context](context/technical-context.md) — Environment, stack, constraints

### Templates
- [Problem Definition Template](templates/problem-definition.md) — Use for new projects
- [Technical Specification Template](templates/technical-specification.md) — Use for system design

### Claude Projects
- **Strategy & Research** — Problem definition and research
- **System Architecture** — Technical specification
- **Analytics Pipeline** — Analytics implementation
- **Product Feed Automation** — Feed implementation

---

## How to Use This Repository

### Starting a New Project
1. Copy `templates/problem-definition.md` to `specifications/[category]/[project-name]-problem.md`
2. Work through the Problem Definition in the Strategy & Research Claude project
3. Once approved, copy `templates/technical-specification.md` to `specifications/[category]/[project-name]-spec.md`
4. Work through the Technical Specification in the System Architecture Claude project
5. Build modules in the appropriate Implementation Claude project
6. Export completed workflows to `workflows/`
7. Update this README with the new system

### Updating Existing Systems
1. Find the specification in `specifications/`
2. Update the spec with changes
3. Update the "Last Updated" date in this README
4. If architecture changes significantly, create an ADR in `decisions/`

---

## Maintenance

**Repository Owner:** Ed (Product Manager)

**Update Frequency:** Update this README whenever a system is added, modified, or deprecated.

**Last Full Review:** [Date]
