# Technical Specification: [Project Name]

> **Status**: Draft / Under Review / Approved / In Development / Complete
> **Created**: YYYY-MM-DD
> **Author**: Ed
> **Problem Definition**: [Link to Problem Definition Document]

---

## 1. Overview

**System Purpose:**
[One paragraph describing what this system does and why]

**Success Criteria Reference:**
[Copy or link the success criteria from the Problem Definition]

---

## 2. System Architecture

### High-Level Diagram

```
[ASCII diagram or description of how components connect]

Example:
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│  Trigger    │────▶│  Module A   │────▶│  Module B   │
│  (Webhook)  │     │  (Process)  │     │  (Output)   │
└─────────────┘     └─────────────┘     └─────────────┘
                           │
                           ▼
                    ┌─────────────┐
                    │  Module C   │
                    │  (Store)    │
                    └─────────────┘
```

### Data Flow Summary
1. [Step 1]: [What happens]
2. [Step 2]: [What happens]
3. [Step 3]: [What happens]

---

## 3. Module Specifications

### Module 1: [Name]

**Purpose:** [One sentence describing what this module does]

**Implementation:** [n8n workflow / JavaScript / Supabase / etc.]

#### Inputs
| Name | Type | Source | Required | Description |
|------|------|--------|----------|-------------|
| [input1] | [type] | [where from] | Yes/No | [description] |
| [input2] | [type] | [where from] | Yes/No | [description] |

#### Outputs
| Name | Type | Destination | Description |
|------|------|-------------|-------------|
| [output1] | [type] | [where to] | [description] |
| [output2] | [type] | [where to] | [description] |

#### Processing Logic
1. [Step 1]
2. [Step 2]
3. [Step 3]

#### Error Handling
| Error Condition | Behavior |
|-----------------|----------|
| [Condition 1] | [What happens] |
| [Condition 2] | [What happens] |

#### Acceptance Criteria
- [ ] Given [input], produces [expected output]
- [ ] When [error condition], [expected behavior]
- [ ] Handles [edge case] by [behavior]
- [ ] Performance: [constraint if any]

#### Dependencies
- **Requires:** [Other modules or systems this needs]
- **Provides to:** [Other modules that depend on this]

---

### Module 2: [Name]

**Purpose:** [One sentence]

**Implementation:** [Type]

#### Inputs
| Name | Type | Source | Required | Description |
|------|------|--------|----------|-------------|
| | | | | |

#### Outputs
| Name | Type | Destination | Description |
|------|------|-------------|-------------|
| | | | |

#### Processing Logic
1. 
2. 
3. 

#### Error Handling
| Error Condition | Behavior |
|-----------------|----------|
| | |

#### Acceptance Criteria
- [ ] 
- [ ] 
- [ ] 

#### Dependencies
- **Requires:** 
- **Provides to:** 

---

### Module 3: [Name]

[Same structure as above - copy for each module]

---

## 4. Data Contracts

### [Data Object 1 Name]

**Used By:** Module A → Module B

**Schema:**
```json
{
  "field1": "string — description, constraints",
  "field2": "number — description, valid range",
  "field3": {
    "nestedField": "string — description"
  },
  "field4": ["array of string — description"]
}
```

**Example:**
```json
{
  "field1": "example value",
  "field2": 42,
  "field3": {
    "nestedField": "example"
  },
  "field4": ["item1", "item2"]
}
```

**Validation Rules:**
- field1: Required, max 255 characters
- field2: Required, positive integer, range 1-1000
- field3: Optional, defaults to null
- field4: Required, minimum 1 item

---

### [Data Object 2 Name]

**Used By:** [Source] → [Destination]

**Schema:**
```json
{
  
}
```

**Example:**
```json
{
  
}
```

**Validation Rules:**
- 

---

## 5. Integration Points

### Triggers
| Trigger | Type | Source | Frequency |
|---------|------|--------|-----------|
| [Trigger 1] | Webhook/Schedule/Manual/Event | [Source] | [How often] |

### External APIs
| API | Purpose | Auth Method | Rate Limits |
|-----|---------|-------------|-------------|
| [API 1] | [What for] | [API Key/OAuth/etc.] | [If known] |

### Data Stores
| Store | Purpose | Access Pattern |
|-------|---------|----------------|
| [Supabase table X] | [What for] | [Read/Write/Both] |
| [Google Sheet Y] | [What for] | [Read/Write/Both] |

### Credentials Required
| Credential | System | n8n Credential Name |
|------------|--------|---------------------|
| [Cred 1] | [System] | [Name in n8n] |

---

## 6. Build Sequence

Build modules in this order:

| Order | Module | Reason | Estimated Effort |
|-------|--------|--------|------------------|
| 1 | [Module X] | No dependencies | [Hours/complexity] |
| 2 | [Module Y] | Depends on X | [Hours/complexity] |
| 3 | [Module Z] | Depends on X and Y | [Hours/complexity] |

---

## 7. Testing Strategy

### Unit Testing (per module)
- Each module tested against its acceptance criteria
- Test with representative sample data
- Verify error handling with invalid inputs

### Integration Testing
- [ ] Test full data flow from trigger to final output
- [ ] Verify data contracts are respected between modules
- [ ] Test with production-like data volumes

### Acceptance Testing
- [ ] Verify all Problem Definition success criteria are met
- [ ] Test in staging environment before production
- [ ] Document any deviations or limitations

---

## 8. Deployment Plan

### Pre-Deployment
- [ ] All modules pass acceptance criteria
- [ ] Integration testing complete
- [ ] Documentation updated
- [ ] Credentials configured

### Deployment Steps
1. [Step 1]
2. [Step 2]
3. [Step 3]

### Rollback Plan
- [How to revert if something goes wrong]

### Post-Deployment Verification
- [ ] [Check 1]
- [ ] [Check 2]

---

## 9. Monitoring & Maintenance

### Monitoring
- [What to watch for normal operation]
- [Alerts to set up]

### Maintenance Tasks
| Task | Frequency | Responsible |
|------|-----------|-------------|
| [Task 1] | [Weekly/Monthly/etc.] | [Who] |

### Known Limitations
- [Limitation 1]
- [Limitation 2]

---

## 10. Open Questions / TBD

- [ ] [Question 1] — Blocked by: [What]
- [ ] [Question 2] — Blocked by: [What]

---

## 11. Revision History

| Date | Version | Change | Author |
|------|---------|--------|--------|
| YYYY-MM-DD | 0.1 | Initial specification | Ed |
| | | | |

---

## 12. Implementation Log

*Updated during build phase*

| Module | Status | Location | Notes |
|--------|--------|----------|-------|
| [Module 1] | Not Started / In Progress / Complete | [n8n ID, file path] | |
| [Module 2] | | | |
| [Module 3] | | | |
