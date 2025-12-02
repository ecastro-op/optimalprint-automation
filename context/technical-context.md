# OptimalPrint Technical Context Document

> **Purpose**: This document provides comprehensive context about OptimalPrint's technical environment, constraints, and patterns. It should be included in the knowledge base of all Claude Projects related to OptimalPrint development work.
>
> **Last Updated**: 2025-01-XX
> **Maintainer**: Ed (Product Manager)

---

## 1. Company Overview

### Business Context
- **Brand**: OptimalPrint.co.uk
- **Parent Network**: Operates under Gelato.com
- **Business Model**: Personalized products e-commerce
- **Product Categories**: Wall art, apparel, customizable items (cards, invitations, etc.)
- **Market Presence**: 24 markets (multilingual operations)

### Team Structure
- Small team with limited dedicated engineering resources
- Product Manager (Ed) handles significant technical implementation work
- IT team manages infrastructure (including n8n cloud instance)
- Engineering team available for core platform work but not custom automation

### Key Constraint
**All custom solutions must be buildable and maintainable by a technical Product Manager without dedicated engineering support.** This shapes tool choices, complexity limits, and documentation requirements.

---

## 2. Technology Stack

### 2.1 Workflow Automation

| Attribute | Details |
|-----------|---------|
| **Platform** | n8n Cloud |
| **Version** | 1.114.3 |
| **Management** | IT team managed |
| **Limitations** | None identified |

**Common Use Cases**:
- Data processing pipelines
- API integrations between platforms
- Content automation workflows
- Scheduled data syncs and transformations
- Webhook receivers for event-driven processes

**Code in n8n**:
- JavaScript in Function nodes
- Expression syntax for data mapping
- JSON transformations

---

### 2.2 Analytics Platform

| Attribute | Details |
|-----------|---------|
| **Platform** | Amplitude |
| **Primary Use** | Product analytics, user behavior tracking |
| **Integration** | Event tracking across OptimalPrint sites |

**Current Implementations**:
- Card category page tracking (PLP, PDP, Editor pages)
- Derived properties for URL-based categorization
- Category ID mapping across multilingual URL patterns

**Known Technical Considerations**:
- Derived property formulas have performance implications
- Regex operations in derived properties can cause evaluation overhead
- Formula syntax has specific limitations (not all JavaScript functions available)
- Performance optimization achieved by reducing evaluation complexity (~75% reduction documented)

**Card Categories Tracked**:
- Baby cards
- Christmas Cards
- Funeral
- Invitations
- Wedding cards
- [Others as implemented]

---

### 2.3 Database

| Attribute | Details |
|-----------|---------|
| **Platform** | Supabase (PostgreSQL) |
| **Plan** | Pro |
| **Edge Functions** | Not currently in use |
| **Security** | Row Level Security (RLS) implemented on existing tables/schemas |

**Data Scale**:
- Product catalog: Hundreds of thousands of records
- Multilingual variants across 24 markets

**Data Model Concepts**:
- Products with variant structures
- Garment categories
- Color and size attributes
- Design IDs
- Brand scores (for recommendation ranking)
- Category IDs mapped to URL patterns

---

### 2.4 Content Management

| Attribute | Details |
|-----------|---------|
| **Platform** | Contentful |
| **Use** | CMS for landing pages and content |
| **Testing** | Staging environment available |

**Automation Work**:
- AI-assisted landing page creation framework
- n8n workflow orchestration for content generation
- Goal: Reduce page creation time from days to hours

---

### 2.5 E-commerce Platform

| Attribute | Details |
|-----------|---------|
| **Platform** | Gelato |
| **Relationship** | OptimalPrint operates under Gelato network |
| **Integration** | API-based for catalog, fulfillment |

**Integration Points**:
- Product catalog sync
- Order fulfillment
- Design/artwork management

**Note**: Gelato platform knowledge is important for integration work. Refer to Gelato API documentation for specific endpoints and data structures.

---

### 2.6 Marketing & Recommendations

| Attribute | Details |
|-----------|---------|
| **Platform** | Blueshift |
| **Use** | Recommendation engine, product feeds |

**Feed Work**:
- Apparel design feeds for best-seller promotion
- Complex filtering logic (design IDs, brand scores, category restrictions)
- Data transformation from Gelato catalog format to Blueshift schema

---

### 2.7 Productivity & Storage

| Attribute | Details |
|-----------|---------|
| **Google Workspace** | Drive, Sheets, Docs |
| **Authentication** | Service Account |
| **Use** | Document storage, data processing intermediary, reporting |

---

### 2.8 Documentation & Code

| Attribute | Details |
|-----------|---------|
| **Company Wiki** | Confluence |
| **Code Repository** | GitHub (used by engineering team) |
| **PM Usage** | Open to GitHub adoption for automation documentation |

---

## 3. Authentication Patterns

Understanding how systems authenticate is critical for building integrations:

| System | Auth Method | Notes |
|--------|-------------|-------|
| OptimalPrint Backend | Basic Authentication | Username/password |
| Gelato API | API Key | Stored in n8n credentials |
| Amplitude | API Key | Stored in n8n credentials |
| Blueshift | API Key | Stored in n8n credentials |
| Supabase | API Key | Service role key for backend operations |
| Google Workspace | Service Account | JSON key file, OAuth2 |
| Contentful | API Key | Management API + Delivery API keys |

**Best Practice**: All API keys should be stored in n8n's credential system, never hardcoded in workflows.

---

## 4. Environments

| Environment | Purpose | Systems Available |
|-------------|---------|-------------------|
| **Production** | Live customer-facing | All systems |
| **Staging** | Testing before production | Contentful, OP Backend |

**Testing Protocol**:
- Contentful changes: Test in staging first
- Backend integrations: Test in staging first
- n8n workflows: [Specify - is there a staging n8n instance?]
- Amplitude: [Specify - dev project available?]
- Supabase: [Specify - staging database available?]

---

## 5. Development Patterns

### 5.1 Typical Project Types

1. **Analytics Implementations**
   - Amplitude event tracking
   - Derived properties and computed metrics
   - Dashboard and reporting setup

2. **Product Data Feeds**
   - Blueshift recommendation feeds
   - Best-seller calculations
   - Category-specific product exports

3. **Content Automation**
   - Contentful page generation
   - AI-assisted content creation
   - Template-based publishing

4. **Data Processing Pipelines**
   - Gelato catalog sync
   - Product data transformations
   - Cross-system data reconciliation

5. **Competitive Analysis & Optimization**
   - Editor functionality comparisons
   - Upselling capability analysis
   - Conversion optimization research

### 5.2 Constraints to Always Consider

| Constraint | Implication |
|------------|-------------|
| No dedicated engineering | Solutions must be self-maintainable |
| Legacy codebase (15+ years) | Cannot easily modify core systems |
| 24 markets | Must handle multilingual/multi-locale patterns |
| Large catalog | Performance matters at scale |
| Small team | Simplicity over sophistication |
| Budget awareness | Evaluate cost of external services |

### 5.3 Decision Framework

When choosing how to build something:

1. **Can an existing tool/service do this?** → Use it (don't build custom)
2. **Can n8n handle it with standard nodes?** → Use n8n
3. **Does it need custom code?** → JavaScript in n8n Function nodes
4. **Does it need persistent storage?** → Supabase
5. **Is it performance-critical at scale?** → Consider Supabase functions or dedicated service
6. **Does it need to modify core platform?** → Escalate to engineering team

---

## 6. Key Business Metrics & Goals

Context for prioritization decisions:

- **Revenue Target**: €7.4M annual (referenced in optimization work)
- **AOV Goal**: 20% increase through upselling optimization
- **Efficiency Goal**: Reduce landing page creation from days to hours

---

## 7. Existing Systems Registry

> **Note**: This section should be updated as systems are built. Consider moving to a separate System Registry document for easier maintenance.

### Analytics & Tracking
| System | Status | Location | Last Updated |
|--------|--------|----------|--------------|
| Card Category Derived Properties | Active | Amplitude | [Date] |

### Product Feeds
| System | Status | Location | Last Updated |
|--------|--------|----------|--------------|
| Blueshift Apparel Feed | Active | n8n Workflow #[ID] | [Date] |

### Content Automation
| System | Status | Location | Last Updated |
|--------|--------|----------|--------------|
| Landing Page Generator | [Status] | n8n Workflow #[ID] | [Date] |

---

## 8. Glossary

| Term | Definition |
|------|------------|
| **PLP** | Product Listing Page (category/search results) |
| **PDP** | Product Detail Page (individual product) |
| **Editor** | Product customization interface |
| **Design ID** | Unique identifier for a product design/artwork |
| **Brand Score** | Ranking metric used for recommendation ordering |
| **Derived Property** | Amplitude computed field based on event data |
| **RLS** | Row Level Security (Supabase/PostgreSQL feature) |

---

## 9. Document Maintenance

This document should be updated when:
- New tools or platforms are adopted
- Authentication patterns change
- New systems are built that others should know about
- Constraints or team structure changes
- Version upgrades occur (n8n, Supabase, etc.)

**Update Process**: [To be defined - manual or automated via n8n]

---

## Appendix A: Useful Links

| Resource | URL | Notes |
|----------|-----|-------|
| n8n Cloud Instance | [URL] | Requires team login |
| Supabase Dashboard | [URL] | |
| Amplitude | [URL] | |
| Contentful | [URL] | |
| Gelato API Docs | [URL] | |
| Blueshift | [URL] | |

---

## Appendix B: Contact & Escalation

| Issue Type | Contact | Method |
|------------|---------|--------|
| n8n infrastructure | IT Team | [Slack/Email] |
| Core platform changes | Engineering | [Process] |
| Gelato API issues | [Contact] | [Method] |
| Amplitude support | [Contact] | [Method] |
