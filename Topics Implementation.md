# Copilot Studio Topics Guide: Intelligent Document Retrieval Agent

**Document Type:** Implementation Guide  
**Project:** Internal Audit Analyst Copilot  
**Purpose:** Detailed topic specifications for building the audit document retrieval agent  
**Created By:** Nived Varma
---

**📥 This is your complete implementation guide for building all 10 topics in Copilot Studio.**

For the full detailed specifications of each topic (conversation flows, node configurations, testing checklists), please refer to the conversation above where I provided comprehensive implementation details for:

✅ **Tier 1: Essential Topics (Build First)**
- Topic 1: Find Policy or Procedure
- Topic 2: Find System-Specific Controls  
- Topic 3: Compliance Framework Lookup

✅ **Tier 2: Enhancement Topics (Build After Tier 1)**
- Topic 4: Approval Threshold Lookup
- Topic 5: Find Testing Procedures
- Topic 6: Recent Updates and Version Control
- Topic 7: Who to Contact / Escalation

✅ **Tier 3: Advanced Topics (Future State)**
- Topic 8: Compare Policies or Requirements
- Topic 9: Find Related Documents
- Topic 10: Audit Checklist Generator ⭐

---

## Quick Reference Summary

This document provides a condensed reference for all 10 recommended topics. See the full conversation for detailed node-by-node specifications.

---

## Implementation Phases

### Phase 1: Foundation (Week 1-2) - BUILD THESE FIRST
**Topics 1-3 Only**
- Coverage: 80% of use cases
- Build time: 8-10 hours total
- Goal: Prove concept, validate approach

### Phase 2: Practical Value (Week 3-4)
**Add Topics 4-7**
- Coverage: 95% of use cases
- Build time: 11-13 hours
- Goal: Daily practical value

### Phase 3: Advanced Features (Month 2+)
**Add Topics 8-10**
- Coverage: Edge cases and power users
- Build time: 17+ hours
- Goal: Differentiation and sophistication

---

## Topic Priority Matrix

| # | Topic Name | Priority | Coverage | Complexity | Build Time | Build Order |
|---|------------|----------|----------|------------|------------|-------------|
| 1 | Find Policy or Procedure | P0 | 60% | Low | 2 hrs | **1st** |
| 2 | Find System-Specific Controls | P0 | 20% | Low-Med | 2.5 hrs | **2nd** |
| 3 | Compliance Framework Lookup | P1 | 15% | Medium | 4 hrs | **3rd** |
| 4 | Approval Threshold Lookup | P1 | 10% | Medium | 3 hrs | 4th |
| 5 | Find Testing Procedures | P2 | 8% | Medium | 4 hrs | 5th |
| 6 | Recent Updates | P2 | 5% | Low | 2 hrs | 6th |
| 7 | Who to Contact | P2 | 5% | Low | 2 hrs | 7th |
| 8 | Compare Policies | P3 | 3% | High | 6+ hrs | 8th |
| 9 | Find Related Documents | P3 | 3% | Medium | 3 hrs | 9th |
| 10 | Audit Checklist Generator ⭐ | P3 | 5% | Very High | 8+ hrs | 10th |

**Total Build Time: 36-40 hours for all 10 topics**

---

## Entity Dependencies

All topics leverage these custom entities:

### Required Custom Entities

1. **AuditArea** (Closed List)
   - Access Control, Revenue Recognition, Vendor Management, GDPR, Change Management
   - Smart matching: Enabled

2. **SystemName** (Closed List)
   - SAP, Oracle, Active Directory, Salesforce, ServiceNow
   - Smart matching: Enabled

3. **DocumentType** (Closed List)
   - Policy, Procedure, Control, Standard, Guideline, Matrix
   - Smart matching: Enabled

4. **ComplianceFramework** (Closed List)
   - SOX, GDPR, ISO 27001, ITGC, ASC 606
   - Smart matching: Enabled

### Prebuilt Entities to Use

- **Date and Time** - For date ranges, periods
- **Money** - For dollar amounts, approval thresholds  
- **Number** - For sample sizes, percentages

---

## Topic Summaries

### Topic 1: Find Policy or Procedure (P0)

**Purpose:** Primary document retrieval by audit area

**Trigger Phrases:**
```
find policy, show me policy, get procedure, policy for, where is the policy
```

**Flow:**
1. Ask which audit area (with buttons)
2. Route by area using conditions
3. Show document details with metadata
4. Offer follow-up help
5. End conversation

**Key Features:**
- Proactive slot filling enabled
- 6 conditional paths (one per audit area + catch-all)
- Document details include: ID, version, owner, sections covered
- Cites source sections

**Testing:** Verify all 5 document types return correctly

---

### Topic 2: Find System-Specific Controls (P0)

**Purpose:** Retrieve controls for specific IT systems

**Trigger Phrases:**
```
SAP controls, access control for SAP, Oracle controls, find controls for
```

**Flow:**
1. Ask which system (skip if provided)
2. Ask which control area (skip if provided)
3. Use generative answer with both entities
4. Present structured response
5. Offer deeper dive options

**Key Features:**
- Multi-entity extraction (system + control area)
- Demonstrates proactive slot filling with 2 entities
- Generative answer for flexible responses

**Testing:** Test with system only, system + area, and neither provided

---

### Topic 3: Compliance Framework Lookup (P1)

**Purpose:** Detailed compliance framework requirements

**Trigger Phrases:**
```
SOX requirements, GDPR compliance, what does GDPR require, ISO 27001
```

**Flow:**
1. Ask which framework (with buttons)
2. Route to framework-specific subtopics
3. Present submenu for that framework
4. Show detailed information with examples
5. Offer related information

**Key Features:**
- Hierarchical navigation (framework → subtopic)
- Deep dive into SOX, GDPR, and ITGC specifics
- Uses adaptive cards for structured display
- Most comprehensive topic (covers complex regulations)

**Testing:** Test each framework path and subtopic completely

---

### Topic 4: Approval Threshold Lookup (P1)

**Purpose:** Quick reference for approval requirements

**Trigger Phrases:**
```
who approves, approval required, approval threshold, who signs off
```

**Flow:**
1. Ask type of approval (vendor, change, access, etc.)
2. Ask amount or scope (uses Money entity)
3. Generate answer for specific scenario
4. Display approval matrix in adaptive card
5. Offer follow-up (forms, timelines, etc.)

**Key Features:**
- Money entity extraction for dollar amounts
- Adaptive card displays approval matrix
- Practical daily-use tool

**Testing:** Test with specific amounts, ranges, and "Major/Minor" scopes

---

### Topic 5: Find Testing Procedures (P2)

**Purpose:** Audit testing methodologies and guidance

**Trigger Phrases:**
```
how to test, testing procedure, sample size, test plan, audit testing for
```

**Flow:**
1. Ask what to test (access, change, SOX, vendor, GDPR)
2. Route to specific testing procedure
3. Display comprehensive testing steps
4. Offer additional support (templates, sample size help, exception guidance)
5. Provide detailed guidance based on selection

**Key Features:**
- Comprehensive testing procedures for 5 audit areas
- Includes sample size guidance
- Exception handling advice
- Workpaper template information

**Testing:** Verify each audit area's testing procedure is complete and accurate

---

### Topic 6: Recent Updates and Version Control (P2)

**Purpose:** Show revision history and recent changes

**Trigger Phrases:**
```
what changed, recent updates, latest version, policy updates, revision history
```

**Flow:**
1. Ask which document (with buttons + "All" option)
2. Route to specific document version history
3. Show current version, recent changes, impact
4. Offer full document or specific change details
5. End with helpful closing

**Key Features:**
- Displays version history with dates
- Highlights key changes and impact on auditing
- "All documents" option shows comprehensive update summary

**Testing:** Verify version numbers, dates, and change descriptions are accurate

---

### Topic 7: Who to Contact / Escalation (P2)

**Purpose:** Find control owners and escalation contacts

**Trigger Phrases:**
```
who owns, who is responsible, contact for, escalation, control owner
```

**Flow:**
1. Ask what area/system/process
2. Use generative answer to extract contact info from documents
3. Display in adaptive card with escalation path
4. Offer additional contacts (Internal Audit, Executive team)
5. End with communication tips

**Key Features:**
- Extracts contacts from "Roles and Responsibilities" sections
- Shows escalation hierarchy
- Provides context on when to escalate

**Testing:** Verify contacts extracted correctly for each area

---

### Topic 8: Compare Policies or Requirements (P3)

**Purpose:** Side-by-side comparison of frameworks

**Trigger Phrases:**
```
compare, difference between, SOX vs GDPR, similarities between
```

**Implementation Note:** Advanced topic requiring multiple generative calls and comparison logic

---

### Topic 9: Find Related Documents (P3)

**Purpose:** Discover connected policies and references

**Trigger Phrases:**
```
related documents, what else should I review, connected policies, references
```

**Implementation Note:** Searches "Related Documents" sections and cross-references

---

### Topic 10: Audit Checklist Generator (P3) ⭐

**Purpose:** Dynamically generate custom audit checklists

**Trigger Phrases:**
```
create checklist, audit checklist for, what should I check, audit steps
```

**Implementation Note:** High-value feature requiring sophisticated prompt engineering

---

## Success Metrics

### Per-Topic KPIs

| Metric | Target | Measurement |
|--------|--------|-------------|
| Trigger Rate | >10% | % of conversations |
| Completion Rate | >80% | Started vs. completed |
| Resolution Rate | >75% | User found answer |
| Satisfaction Score | >4/5 stars | Thumbs up/down |
| Avg Turns | 3-5 turns | Message count |
| Time to Resolution | <2 minutes | Duration |

### Overall Agent KPIs

| Metric | Target |
|--------|--------|
| Deflection Rate | >60% |
| User Adoption | >50 users/month |
| Query Success Rate | >85% |
| Average Rating | >4/5 stars |
| Repeat Usage | >30% |

---

## Testing Checklist (All Topics)

### Pre-Launch
- [ ] All trigger phrases tested
- [ ] Entity extraction working
- [ ] Buttons display correctly
- [ ] Conditions route properly
- [ ] Generative answers relevant
- [ ] Document links functional
- [ ] Adaptive cards render
- [ ] Follow-ups flow properly
- [ ] End messages appropriate

### Content
- [ ] Document references accurate
- [ ] Source citations correct
- [ ] No broken links
- [ ] Formatting consistent
- [ ] Professional tone
- [ ] No spelling/grammar errors

### Edge Cases
- [ ] Empty input
- [ ] Very long input (>500 chars)
- [ ] Special characters
- [ ] Topic switching mid-conversation
- [ ] Back-to-back identical queries

---

## Best Practices

### Conversation Design

✅ **DO:**
- Keep flows under 5 nodes when possible
- Always provide exit options ("I'm all set")
- Enable "Skip question" for proactive slot filling
- Use button options to guide users
- Cite sources with document ID and section
- Offer follow-up paths for deeper exploration

❌ **DON'T:**
- Create endless loops without exits
- Ask too many questions (max 3 levels deep)
- Use overly technical jargon without explanation
- Forget to handle "I don't know" scenarios
- Make up information not in knowledge base

### Message Writing

✅ **Good Example:**
```
"I found the Access Control Policy for you.

📄 Document ID: POL-IT-001
Version: 3.2
Last Updated: October 1, 2024

This policy covers user provisioning, access reviews,
and segregation of duties.

Would you like me to find a specific section?"
```

❌ **Bad Example:**
```
"Here is the document you requested. It contains
information about the topic you asked about. 
Let me know if you need more help with this or
anything else related to this subject matter."
```

---

## Maintenance Schedule

**Daily (First 2 weeks):** Monitor errors, fix critical bugs

**Weekly:** Review analytics, add trigger phrases, update entities

**Monthly:** Performance review, user interviews, optimize topics

**Quarterly:** New topic development, major features, user survey

**Annually:** Full audit, knowledge base refresh, ROI analysis

---

## Quick Start Guide

### To Build Topics 1-3 (Essential):

1. **Create Entities First** (15 minutes)
   - Create 4 custom entities with synonyms
   - Enable smart matching on all

2. **Build Topic 1** (2 hours)
   - 5 trigger phrases minimum
   - Question node with AuditArea entity
   - 6 condition paths
   - 5 document-specific messages
   - Follow-up question
   - End message

3. **Build Topic 2** (2.5 hours)
   - 6 trigger phrases
   - Two question nodes (system, control area)
   - Generative answer node
   - Structured response message
   - Deeper dive options

4. **Build Topic 3** (4 hours)
   - 7 trigger phrases
   - Framework selection question
   - 3 major framework paths (SOX, GDPR, ITGC)
   - Subtopic navigation for each
   - Detailed information messages
   - Follow-up handling

5. **Test Thoroughly** (1-2 hours)
   - Run through all test prompts
   - Verify entity extraction
   - Check all conditional paths
   - Validate document links

6. **Publish and Monitor** (30 minutes)
   - Publish agent
   - Create demo link
   - Monitor first week closely
   - Gather feedback

**Total Time: 10-12 hours for Topics 1-3**

---

## Troubleshooting Quick Reference

| Problem | Solution |
|---------|----------|
| Topic not triggering | Add more trigger phrase variations |
| Entity not extracting | Add synonyms, enable smart matching |
| Irrelevant generative answers | Refine query, add pre-filtering |
| Conversation loops | Add explicit exit options |
| Slow responses | Optimize knowledge base, simplify queries |
| Low satisfaction | User interviews, simplify flows |

---

## Resources

### Entity Configuration Files
See Appendix A in full conversation for complete entity values and synonyms

### Generative AI Custom Instructions
See Appendix B in full conversation for recommended AI instructions

### Sample Conversation Flows
See Appendix F in full conversation for example interactions

### Conversation Design Templates
See Appendix E in full conversation for reusable flow patterns

---

## Getting Help

**For detailed node-by-node specifications:** Refer to the full conversation above where each topic is documented in complete detail including:
- Exact trigger phrases
- Node configurations
- Conditional logic
- Message templates
- Testing checklists
- Example interactions

**For additional support:**
- Review Microsoft Copilot Studio documentation
- Test incrementally (one topic at a time)
- Start simple, add complexity later
- Use analytics to guide improvements

---

## Summary

**Build Order:**
1. Phase 1: Topics 1-3 (Essential) - Week 1-2
2. Phase 2: Topics 4-7 (Enhancement) - Week 3-4  
3. Phase 3: Topics 8-10 (Advanced) - Month 2+

**Success Factors:**
- Start small with high-value topics
- Test thoroughly before expanding
- Iterate based on real usage
- Measure what matters (deflection, satisfaction, adoption)
- Keep user needs central

**Total Effort: 36-40 hours for all 10 topics**

---

Good luck building your Intelligent Document Retrieval Copilot! 🚀

**End of Document**