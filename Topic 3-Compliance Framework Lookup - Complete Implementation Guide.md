# Topic 3: Compliance Framework Lookup - Complete Implementation Guide

**Document Type:** Step-by-Step Implementation Guide  
**Topic Priority:** P1 (Build Third)  
**Complexity:** Medium  
**Value:** ⭐⭐⭐⭐ (High Impact)
**Created By:** Nived Varma
---

## 📖 Table of Contents

1. [Overview](#overview)
2. [What You'll Build](#what-youll-build)
3. [Prerequisites](#prerequisites)
4. [Implementation Steps](#implementation-steps)
5. [Testing Guide](#testing-guide)
6. [Troubleshooting](#troubleshooting)
7. [Example Interactions](#example-interactions)

---

## Overview

### What is Compliance Framework Lookup?

A **hierarchical navigation topic** that provides detailed information on compliance frameworks including SOX, GDPR, ITGC, and ISO 27001. Users can drill down into specific requirements, timelines, and implementation guidance.

### Real-Time Example

**Without This Topic:**
```
Auditor: "What are GDPR breach notification requirements?"
→ Opens policy document
→ Searches for "breach notification"
→ Reads through 10+ pages
→ May miss key details (72-hour rule)
→ Takes 15-20 minutes
```

**With This Topic:**
```
Auditor: "GDPR breach notification requirements"
→ Bot: "I can help with GDPR. What aspect?"
→ [Shows buttons: Data subject rights, Breach notification, etc.]
→ User clicks "Breach notification"
→ Bot shows complete timeline with specifics:
   - Discovery → InfoSec: Immediately
   - InfoSec → DPO: Within 2 hours
   - DPO → Supervisory Authority: Within 72 hours
   - DPO → Individuals: Without undue delay (if high risk)
→ Takes 30 seconds
→ No ambiguity
```

---

## What You'll Build

### Complete Conversation Flow

```
User: "SOX requirements" or "GDPR compliance"
    ↓
[Q] Which compliance framework?
    ├─ SOX (Sarbanes-Oxley)
    ├─ GDPR (Data Privacy)
    ├─ ITGC (IT General Controls)
    ├─ ISO 27001
    └─ Other framework
    ↓
[Condition: Route by framework selected]
    ↓
━━━ SOX PATH ━━━
[M] "I can help with SOX 404. What would you like to know?"
    ↓
[Q] Select SOX topic:
    ├─ Financial controls and testing
    ├─ Control narratives and RCMM
    ├─ Management assertions
    ├─ Control deficiencies
    └─ Specific control
    ↓
[Generative Answer] → Provides detailed SOX information
    ↓
[Adaptive Card] → Structured display with document details
    ↓
━━━ GDPR PATH ━━━
[M] "I can help with GDPR. What aspect are you interested in?"
    ↓
[Q] Select GDPR topic:
    ├─ Data subject rights (access, erasure, portability)
    ├─ Data breach notification (72-hour rule)
    ├─ Data retention and disposal
    ├─ International data transfers
    ├─ DPIA requirements
    └─ Legal bases for processing
    ↓
[Condition: Route by GDPR subtopic]
    ↓
[Message] → Detailed information with timelines, requirements
    ↓
━━━ ITGC PATH ━━━
[Similar structure for IT General Controls]
    ↓
[Q] "Additional help?"
    ├─ Yes, another question
    ├─ Show related documents
    └─ I'm all set
    ↓
[End Conversation]
```

### Key Features

🎯 **Hierarchical Navigation**
- Framework selection → Subtopic selection → Detailed information
- Three levels deep for major frameworks (SOX, GDPR, ITGC)

📊 **Framework-Specific Content**
- **SOX:** Control testing, RCMM, management assertions
- **GDPR:** Data subject rights, breach notification, DPIAs
- **ITGC:** Change management, access controls, operations

⏱️ **Timeline Information**
- GDPR: 72-hour breach notification rule
- Data subject rights: 1-month response deadlines
- SOX: Quarterly testing cycles

📝 **Structured Display**
- Adaptive cards for key information
- Formatted messages with examples
- Clear section headers and bullet points

🔗 **Cross-References**
- Links to related policies
- References to specific document sections
- Compliance mapping across frameworks

---

## Prerequisites

### Before You Start

✅ **Completed Topics 1-2**
- Find Policy or Procedure (basic retrieval)
- System-Specific Controls

✅ **Knowledge Base Ready**
- All 5 sample documents uploaded and indexed:
  - access_control_policy.md
  - sox_revenue_recognition.md
  - vendor_management_policy.md
  - data_privacy_gdpr_policy.md
  - itgc_change_management.md

✅ **Entities Created**
- `ComplianceFramework` entity with values:
  - SOX, GDPR, ISO 27001, ITGC, ASC 606

✅ **Generative Answers Enabled**
- Working knowledge base search
- Tested with previous topics

### Recommended Experience

- Understanding of conditional logic
- Comfortable with multi-level conversation flows
- Basic knowledge of compliance frameworks (helpful but not required)

---

## Implementation Steps

---

## STEP 1: Create the Topic

### 1.1 Navigate to Topics

1. Open your copilot in **Copilot Studio**
2. Click **"Topics"** in left navigation
3. Click **"+ New topic"** or **"+ Add"**
4. Select **"From blank"**

### 1.2 Configure Topic Settings

**Topic Name (Internal):**
```
ComplianceFrameworkLookup
```

**Display Name (User-Facing):**
```
Compliance Framework Information
```

**Description:**
```
Provides detailed information on compliance frameworks including SOX, GDPR, 
ITGC, and ISO 27001. Includes requirements, timelines, and implementation guidance.
```

### 1.3 Add Trigger Phrases

Add these 20+ trigger phrases:

```
SOX requirements
GDPR compliance
what does GDPR require
SOX controls
ISO 27001
compliance requirements for
regulatory requirements
GDPR breach notification
data subject rights
what are SOX controls
help with GDPR
SOX 404 controls
data protection requirements
IT general controls
ITGC requirements
compliance framework
what is required for SOX
GDPR data retention
breach notification timeline
data privacy requirements
```

**How to Add:**
1. In the topic canvas, find **"Add phrases"** section at top
2. Type each phrase and press Enter
3. Add all 20+ phrases
4. Click **"Save"**

---

## STEP 2: Build Question Node 1 - Framework Selection

### 2.1 Add Question Node

1. Click **"+"** button below trigger section
2. Select **"Ask a question"**

### 2.2 Configure the Question

**Question Text:**
```
Which compliance framework are you asking about?
```

**Identify:**
- Click dropdown → Select **`ComplianceFramework`** entity

**Save response as:**
```
varFramework
```

**Add Options for User (Buttons):**

Click **"+ Add"** under "Options for user" for each:

```
SOX (Sarbanes-Oxley)
GDPR (Data Privacy)
IT General Controls (ITGC)
ISO 27001
ASC 606 (Revenue Recognition)
Other framework
```

**Enable Proactive Slot Filling:**
1. Click **"..."** menu on the question node
2. Select **"Properties"**
3. Toggle **"Skip question"** to **Enabled**

### 2.3 Visual Verification

Your node should show:
- Question text clearly visible
- 6 button options
- Entity: ComplianceFramework
- Variable: varFramework
- Skip question: Enabled

---

## STEP 3: Build Condition Node - Route by Framework

### 3.1 Add Condition Node

1. Click **"+"** below Node 1
2. Select **"Add a condition"**

### 3.2 Configure Conditions

**Condition 1: SOX**
- Variable: `varFramework`
- Operator: **contains**
- Value: `"SOX"`

**Condition 2: GDPR**
- Click **"+ New condition"**
- Variable: `varFramework`
- Operator: **contains**
- Value: `"GDPR"`

**Condition 3: ITGC**
- Click **"+ New condition"**
- Variable: `varFramework`
- Operator: **contains**
- Value: `"ITGC"`
OR
- Variable: `varFramework`
- Operator: **contains**
- Value: `"IT General"`

**Condition 4: ISO**
- Click **"+ New condition"**
- Variable: `varFramework`
- Operator: **contains**
- Value: `"ISO"`

**Condition 5: All Others**
- Leave as **"All other conditions"**

### 3.3 Why Use "contains" Instead of "is equal to"?

Using **"contains"** is more flexible:
- Matches "SOX", "SOX 404", "Sarbanes-Oxley"
- Matches "GDPR", "GDPR compliance", "General Data Protection"
- More forgiving of user variations

---

## STEP 4: Build SOX Branch (Condition 1)

### 4.1 SOX Introduction Message

**Under SOX condition, add:**

1. Click **"+"** in SOX branch
2. Select **"Send a message"**

**Message Text:**
```
I can help with SOX 404 compliance requirements.

📊 **SOX 404 Overview:**
Our SOX program covers internal controls over financial reporting, 
particularly for revenue recognition.

**What would you like to know about?**
```

### 4.2 SOX Subtopic Question

1. Click **"+"** after introduction message
2. Select **"Ask a question"**

**Question Text:**
```
Select a SOX topic:
```

**Identify:**
- Select **"User's entire response"**

**Save response as:**
```
varSOXTopic
```

**Add Options (Buttons):**
```
Financial controls and testing results
Control narratives and RCMM
Management assertions and sign-offs
Control deficiencies and remediation
Specific control (e.g., revenue recognition)
```

### 4.3 SOX Generative Answer

1. Click **"+"** after SOX question
2. Select **"Advanced"** → **"Generative answers"**

**Configuration:**

**Input variable:** `Activity.Text` (default)

**Data sources:** Click "Edit"
- Check: ☑ sox_revenue_recognition.md
- Check: ☑ vendor_management_policy.md (for vendor-related controls)
- Enable **"Customize input"** checkbox

**Custom input:**
```
You are a SOX compliance expert. The user asked about: {varSOXTopic}

Provide detailed information from the SOX 404 Control Documentation for Revenue Recognition (Document ID: SOX-FIN-REV-001).

Include:
- Specific control descriptions with control IDs
- Testing procedures and methodologies
- Q3 2024 testing results (if asked about testing)
- Management assertions (if asked about assertions)
- Control deficiencies and remediation plans (if asked about deficiencies)
- Expected results and acceptance criteria

Format your response professionally with:
- Clear headings
- Bullet points for lists
- Specific references to document sections
- Control IDs and version numbers

Be comprehensive but focus on what the user specifically asked about: {varSOXTopic}
```

**Content moderation:** Medium

**Save the node**

### 4.4 SOX Follow-up Question

1. Click **"+"** after Generative Answer
2. Select **"Ask a question"**

**Question Text:**
```
Is there anything else I can help you with regarding SOX compliance?
```

**Options (Buttons):**
```
Yes, I have another question
Show me related documents
No, I'm all set
```

**Save as:** `varSOXFollowUp`

### 4.5 SOX End Branch

1. Add **Condition node** to check `varSOXFollowUp`
2. If "another question" → Redirect to SOX subtopic question
3. If "related documents" → Show document list
4. If "all set" → End conversation with survey

---

## STEP 5: Build GDPR Branch (Condition 2)

### 5.1 GDPR Introduction Message

**Under GDPR condition, add:**

1. Click **"+"** in GDPR branch
2. Select **"Send a message"**

**Message Text:**
```
I can help with GDPR (General Data Protection Regulation) requirements.

🔒 **GDPR Compliance Areas:**

Our GDPR policy covers all aspects of data protection for EEA/UK personal data.

**What aspect are you interested in?**
```

### 5.2 GDPR Subtopic Question

1. Click **"+"** after introduction message
2. Select **"Ask a question"**

**Question Text:**
```
Select a GDPR topic:
```

**Identify:** "User's entire response"

**Save response as:** `varGDPRTopic`

**Add Options (Buttons):**
```
Data subject rights (access, erasure, portability)
Data breach notification (72-hour rule)
Data retention and disposal schedules
International data transfers and SCCs
DPIA (Data Protection Impact Assessment) requirements
Legal bases for processing
```

### 5.3 GDPR Condition Node - Route by Subtopic

1. Click **"+"** after GDPR subtopic question
2. Select **"Add a condition"**

**Configure 6 conditions:**

**Condition 1:** `varGDPRTopic` contains `"data subject rights"`
**Condition 2:** `varGDPRTopic` contains `"breach"`
**Condition 3:** `varGDPRTopic` contains `"retention"`
**Condition 4:** `varGDPRTopic` contains `"transfer"`
**Condition 5:** `varGDPRTopic` contains `"DPIA"`
**Condition 6:** `varGDPRTopic` contains `"legal bases"`

### 5.4 GDPR Data Subject Rights Branch (Detailed)

**Under Condition 1 (data subject rights), add Message:**

```
📋 **GDPR Data Subject Rights Overview**

Under GDPR, individuals have the following rights:

**1️⃣ Right of Access (Subject Access Request - SAR)**
- **Response deadline:** 1 month (extendable by 2 months if complex)
- **Process:** 
  • Identity verification required
  • Data compilation from all systems
  • Provide copy of personal data + processing information
- **What to include:** Data categories, purposes, recipients, retention period, source

**2️⃣ Right to Rectification**
- **Response deadline:** 1 month
- **Process:** Correct inaccurate or incomplete personal data
- **Action:** Update data in all systems, notify third parties

**3️⃣ Right to Erasure ("Right to be Forgotten")**
- **Valid grounds:**
  • Data no longer necessary for original purpose
  • Consent withdrawn (and no other legal basis)
  • Objection to processing
  • Data processed unlawfully
- **Exceptions:** Legal obligations, legal claims, public health
- **Process:** Delete from all systems including backups (within backup cycle)

**4️⃣ Right to Restriction**
- **Triggers:** Accuracy contested, unlawful processing, legal claims
- **Action:** Mark as "restricted" - retain but not process

**5️⃣ Right to Data Portability**
- **Applies to:** Processing based on consent or contract, automated processing
- **Format:** Structured, machine-readable (CSV, JSON, XML)
- **Can transmit:** Directly to new controller if technically feasible

**6️⃣ Right to Object**
- **Direct Marketing:** Absolute right, must cease immediately
- **Legitimate Interests:** May continue if compelling grounds override

**📅 Response Deadlines:**
- First request: Free, within 1 month
- Excessive/repetitive: Reasonable fee allowed, or refuse
- Extension: +2 months if complex (must notify within 1 month)

**Source:** Data Privacy and GDPR Compliance Policy (POL-SEC-GDPR-001), Section 5

Would you like detailed procedures for handling any specific rights request?
```

### 5.5 GDPR Breach Notification Branch

**Under Condition 2 (breach), add Message:**

```
🚨 **GDPR Data Breach Notification Requirements**

**CRITICAL TIMELINE - 72 HOURS:**

**Internal Notification:**
- Discovery → InfoSec: **Immediately**
- InfoSec → DPO: **Within 2 hours**
- DPO → Executive Team: **Within 4 hours** (if likely breach)

**External Notification:**
- DPO → Supervisory Authority: **Within 72 hours** ⏰
- DPO → Affected Individuals: **Without undue delay** (if high risk)

**When Notification Required:**

✅ **Notify Regulator IF:**
- Risk to individuals' rights and freedoms
- Examples: Financial loss, discrimination, damage to reputation, identity theft

✅ **Notify Individuals IF:**
- High risk to rights and freedoms
- Examples: Special category data, unencrypted data, large volume, vulnerable groups

**Risk Assessment Factors:**
- Type and sensitivity of data (special category = higher risk)
- Volume of affected individuals
- Ease of identifying individuals
- Severity of consequences
- Ability of individuals to mitigate harm

**Example Scenarios:**

| Scenario | Notify Regulator? | Notify Individuals? |
|----------|------------------|---------------------|
| Encrypted laptop stolen (strong encryption) | No | No |
| Unencrypted USB with 10K customer emails lost | Yes | Yes |
| Health records accessed by unauthorized employee | Yes | Yes |
| Marketing email sent to wrong recipient (BCC error) | Assess case-by-case | Possibly |

**Breach Documentation Required:**
- Date and time of breach discovery
- Nature of breach
- Categories and number of individuals affected
- Categories and volume of records affected
- Consequences (actual and potential)
- Remedial actions taken
- Notification decisions and rationale

**⏰ Key Reminder:** The 72-hour clock starts when you become AWARE of the breach, not when the breach occurred.

**Source:** Data Privacy and GDPR Compliance Policy (POL-SEC-GDPR-001), Section 10

Need help with breach assessment or notification templates?
```

### 5.6 GDPR Retention Branch

**Under Condition 3 (retention), add Message:**

```
📅 **GDPR Data Retention and Disposal Requirements**

**Core Principle:** Retain data only as long as necessary for stated purpose (GDPR Article 5(1)(e))

**Common Retention Periods:**

| Data Category | Retention Period | Legal Basis | Disposal Method |
|--------------|-----------------|-------------|-----------------|
| Active customer records | Relationship + 3 years | Contract, Legal | Secure deletion |
| Transactional data | 7 years | Legal (tax) | Secure deletion |
| Marketing consent | Consent valid + 3 years | Accountability | Secure deletion |
| Employee personnel files | Termination + 7 years | Legal (employment law) | Secure destruction |
| Payroll records | 7 years | Legal (tax) | Secure destruction |
| Recruitment (unsuccessful) | 6 months | Legitimate interests | Secure deletion |
| GDPR documentation (DPIAs, ROPA) | Processing + 3 years | Accountability | Archive |
| Privacy notices | Superseded + 3 years | Accountability | Archive |
| Data breach records | Incident + 5 years | Accountability | Archive |

**Disposal Methods:**

**Electronic Data:**
✓ Cryptographic erasure (encryption key destruction)
✓ Secure deletion software (DOD 5220.22-M standard)
✓ Physical destruction of storage media (degaussing, shredding)

**Paper Records:**
✓ Cross-cut shredding (P-4 standard or higher)
✓ Certified destruction service for bulk disposal
✓ Certificate of destruction retained

**Backup Data:**
- Data purged from backups within normal backup cycle (90 days)
- Document if retention obligations exceed backup cycle
- Cannot rely on "it's in backup" to avoid deletion obligations

**Key Requirements:**
☐ Define retention periods for ALL data categories
☐ Implement automated deletion/archival processes
☐ Review and purge data at end of retention period
☐ Document legal or regulatory retention requirements
☐ Balance retention needs vs. data minimization principle

**Source:** Data Privacy and GDPR Compliance Policy (POL-SEC-GDPR-001), Section 8

Would you like the complete retention schedule or disposal procedures?
```

### 5.7 GDPR International Transfers Branch

**Under Condition 4 (transfer), add Message:**

```
🌍 **GDPR International Data Transfer Requirements**

Transfers outside EEA/UK require approved safeguards:

**Transfer Mechanisms:**

**1️⃣ Adequacy Decision (Easiest)**
- EU-recognized countries with adequate protection
- Currently adequate countries:
  ✓ UK, Switzerland, Canada, Japan, South Korea
  ✓ Israel, New Zealand, Argentina, Uruguay
  ✓ Andorra, Faroe Islands, Guernsey, Jersey, Isle of Man
- No additional safeguards needed

**2️⃣ Standard Contractual Clauses (SCCs) (Most Common)**
- EU-approved model contracts
- Updated SCCs effective 2021 (must use new version)
- Must conduct Transfer Impact Assessment (TIA)
- Implementation: Execute SCC addendum with vendor

**SCC Modules:**
- Module 1: Controller to Controller
- Module 2: Controller to Processor (most common)
- Module 3: Processor to Processor
- Module 4: Processor to Controller

**3️⃣ Binding Corporate Rules (BCRs)**
- Internal policies for multinational groups
- Requires supervisory authority approval
- Our BCRs approved by Irish DPA (lead authority)

**4️⃣ Derogations (Limited Use Only)**
- Explicit consent for specific transfer
- Necessary for contract performance
- Important public interest reasons
- ⚠️ NOT viable for routine/repetitive transfers

**US Data Transfers - Post-Schrems II:**

**EU-US Data Privacy Framework (DPF):**
- Successor to Privacy Shield (invalidated in Schrems II)
- US companies self-certify to DPF
- Must verify vendor certification annually
- Check status: https://www.dataprivacyframework.gov/list

**Transfer Impact Assessment (TIA) Required:**
For transfers to non-adequate countries:
1. Assess laws of destination country (government access, surveillance)
2. Evaluate supplementary measures needed beyond SCCs
3. Document assessment and decision
4. Re-assess if circumstances change

**Action Items for Compliance:**
☐ Identify all international data transfers
☐ Verify transfer mechanism in place (adequacy, SCCs, BCRs)
☐ Ensure SCCs are 2021 version (not old Privacy Shield-era)
☐ Complete TIA for high-risk transfers
☐ Verify US vendors have valid DPF certification
☐ Document all transfers and safeguards

**Source:** Data Privacy and GDPR Compliance Policy (POL-SEC-GDPR-001), Section 7

Need help assessing a specific data transfer?
```

### 5.8 GDPR DPIA Branch

**Under Condition 5 (DPIA), add Message:**

```
📋 **Data Protection Impact Assessment (DPIA) Requirements**

**When DPIA Required (Mandatory):**
✅ Systematic and extensive profiling with significant effects
✅ Large-scale processing of special category data
✅ Systematic monitoring of publicly accessible areas (CCTV at scale)
✅ New technologies with high privacy risk
✅ Automated decision-making with legal or similar significant effects
✅ Processing children's data at scale
✅ Cross-border data transfers outside EEA

**DPIA Threshold Screening:**
Complete screening questionnaire for all new projects/systems involving personal data.
If 2+ criteria met → DPIA required

**DPIA Process - 6 Steps:**

**Step 1: Describe Processing**
- Nature, scope, context, purposes of processing
- Types of personal data and data subjects
- Data flows and system architecture
- Data lifecycle (collection → storage → deletion)

**Step 2: Assess Necessity and Proportionality**
- Is processing necessary for stated purpose?
- Are less intrusive alternatives available?
- Is data minimization applied?
- Is purpose limitation respected?

**Step 3: Identify and Assess Risks**
Evaluate risks to individuals' rights and freedoms:
- Unauthorized access or disclosure
- Accidental loss or destruction
- Discrimination or identity theft
- Reputational damage
- Loss of confidentiality
- Physical, material, or non-material damage

**Risk Rating:** Likelihood × Impact = Risk Score
- Low: Minor inconvenience
- Medium: Significant impact (financial loss, distress)
- High: Severe impact (discrimination, identity theft, physical harm)

**Step 4: Identify Mitigation Measures**

**Technical Controls:**
- Encryption (at rest and in transit)
- Pseudonymization or anonymization
- Access controls (RBAC, least privilege)
- Security monitoring and logging
- Data loss prevention (DLP)

**Organizational Measures:**
- Privacy policies and procedures
- Staff training on data protection
- Data processing agreements with vendors
- Privacy by design approach
- Regular audits and reviews

**Step 5: DPO Review and Approval**
- DPO reviews DPIA for completeness
- DPO assesses residual risk after mitigations
- If high residual risk remains → Consult supervisory authority before proceeding
- DPO sign-off required before project launch

**Step 6: Monitor and Review**
- Reassess DPIA if significant changes to processing
- Annual review for high-risk processing
- Update risk assessments based on incidents
- Track implementation of mitigation measures

**DPIA Template:**
Available on Privacy SharePoint site (FORM-GDPR-DPIA)

**Consultation with Supervisory Authority:**
Required BEFORE processing if:
- High residual risk remains after mitigations
- DPO recommends consultation
- Novel or complex processing activity

**DPIA Documentation Retention:**
- Keep for life of processing + 3 years
- Make available to supervisory authority upon request

**Source:** Data Privacy and GDPR Compliance Policy (POL-SEC-GDPR-001), Section 6

Would you like help completing a DPIA for your project?
```

### 5.9 GDPR Legal Bases Branch

**Under Condition 6 (legal bases), add Message:**

```
⚖️ **GDPR Legal Bases for Processing Personal Data**

All processing MUST have at least one lawful basis (GDPR Article 6):

**1. Consent** 🤝
**Definition:** Freely given, specific, informed, unambiguous indication of agreement
**Requirements:**
- Must be explicit opt-in (pre-ticked boxes INVALID)
- Separate consent for different purposes
- Easy to withdraw (as easy as to give)
- Documented with timestamp and consent text
- Children (under 16): Parental consent required
**Use for:** Marketing communications, optional data sharing, non-essential cookies
**Not for:** Employee data (power imbalance), critical services

**2. Contract** 📄
**Definition:** Processing necessary to perform contract with data subject
**Examples:**
- Order fulfillment and delivery
- Payment processing
- Account management and customer support
- Employment contracts (payroll, benefits)
**Cannot use for:** Processing beyond what's strictly necessary for contract

**3. Legal Obligation** ⚖️
**Definition:** Processing required to comply with legal obligation
**Examples:**
- Tax reporting and accounting records (7 years)
- Employment law compliance (wage records, discrimination prevention)
- Health and safety regulations
- Anti-money laundering (AML) checks
- Court orders and legal process
**Note:** Must be specific legal requirement, not just "good practice"

**4. Vital Interests** 🚑
**Definition:** Processing necessary to protect someone's life
**Examples:**
- Medical emergencies
- Disaster response
- Child protection
**Note:** Rarely applicable in commercial contexts, true life-or-death only

**5. Public Task** 🏛️
**Definition:** Processing necessary for public interest or official authority
**Applicability:** Primarily government and public sector
**Examples:** Law enforcement, public health, education
**Not for:** Private sector except specific statutory functions

**6. Legitimate Interests** ⚙️
**Definition:** Processing necessary for legitimate interests of controller or third party (unless overridden by data subject's interests)

**Requires:** Legitimate Interests Assessment (LIA) - three-part test:
1. Purpose test: Is there a legitimate interest?
2. Necessity test: Is processing necessary for that interest?
3. Balancing test: Do individual's interests override?

**Can use for:**
✓ Fraud prevention and network security
✓ Internal administrative purposes (HR management)
✓ Direct marketing to existing customers (B2B)
✓ Sharing data within corporate group
✓ Physical security (CCTV)
✓ Debt collection

**Cannot use for:**
✗ Special category (sensitive) data
✗ Children's data
✗ Intrusive profiling or surveillance
✗ Unexpected or privacy-invasive processing

**Before Processing - Legal Basis Assessment:**
1. Identify purpose of processing
2. Select most appropriate lawful basis
3. Document rationale and assessment
4. Update privacy notice to reflect legal basis
5. Store assessment in data protection records

**Changing Legal Basis:**
- Generally not allowed after processing started
- Exception: Compatible purpose + original basis remains valid
- Must update privacy notice and notify individuals

**Special Category Data:**
Requires BOTH:
1. Article 6 basis (above) AND
2. Article 9 condition (explicit consent, employment law, vital interests, etc.)

**Source:** Data Privacy and GDPR Compliance Policy (POL-SEC-GDPR-001), Section 4

Need help determining appropriate legal basis for your processing activity?
```

### 5.10 GDPR Follow-up

After all GDPR subtopic branches, add:

1. **Question node:** "Is there anything else I can help you with regarding GDPR?"
2. **Options:** Another question / Show related documents / I'm all set
3. **Route accordingly** (loop back or end)

---

## STEP 6: Build ITGC Branch (Condition 3)

### 6.1 ITGC Introduction Message

**Under ITGC condition, add:**

1. Click **"+"** in ITGC branch
2. Select **"Send a message"**

**Message Text:**
```
I can help with IT General Controls (ITGC) requirements.

🖥️ **ITGC Areas Covered:**

Our ITGC documentation focuses on:
- Change Management
- Access Controls
- Computer Operations
- Program Development

**What would you like to know about?**
```

### 6.2 ITGC Subtopic Question

1. Click **"+"** after introduction
2. Select **"Ask a question"**

**Question Text:** "Select an ITGC topic:"

**Save as:** `varITGCTopic`

**Add Options:**
```
Change management process and CAB approval
Segregation of duties (developers vs. deployers)
Emergency change procedures
Testing and UAT requirements
Production access controls
Change management metrics and KPIs
```

### 6.3 ITGC Generative Answer

1. Click **"+"** after question
2. Select **"Advanced"** → **"Generative answers"**

**Data sources:** itgc_change_management.md

**Custom input:**
```
Provide detailed information about {varITGCTopic} from the IT General Controls - Change Management documentation (ITGC-CHG-001).

Include:
- Specific procedures and workflows
- Approval requirements and matrices
- Control activities and responsibilities
- Examples and best practices
- References to policy sections

Format professionally with clear headings and bullet points.
```

### 6.4 ITGC Follow-up

Similar to SOX and GDPR, add follow-up question and routing.

---

## STEP 7: Build "Other Frameworks" Branch (Condition 5)

### 7.1 Message for Other Frameworks

**Under "All other conditions", add:**

```
I currently have detailed documentation for these frameworks:

✅ **SOX 404** - Financial controls and revenue recognition
✅ **GDPR** - Data privacy and protection requirements
✅ **ITGC** - IT general controls (change management focus)
✅ **ASC 606** - Revenue recognition standard (within SOX docs)

**If you need information about another framework** (ISO 27001, HIPAA, PCI DSS, etc.), please let me know and I'll help with what's available or guide you to the right resource.

Would you like to:
- Go back and select a different framework
- Search for a specific policy or document
- I'm all set
```

Add question node with routing options.

---

## STEP 8: Add Final Follow-up and End

### 8.1 Universal Follow-up Question

At the end of each framework path, ensure you have:

**Question node:**
```
"Is there anything else I can help you with regarding {varFramework} compliance?"
```

**Options:**
- Yes, I have another question
- Show me related documents
- No, I'm all set

### 8.2 Conditional Routing

**If "another question":**
- Redirect back to framework-specific subtopic question
- Or use generative answer for free-form question

**If "related documents":**
- Message with list of related policies
- Include document IDs and links

**If "all set":**
- End with survey

### 8.3 End Message

```
Great! If you need any compliance or audit documentation in the future, just ask.

💡 **Quick tip:** You can also ask me to:
- Find specific policies
- Generate audit checklists
- Look up approval requirements

Happy auditing! ✅
```

Add **End conversation** node with survey.

---

## STEP 9: Save and Publish

### 9.1 Save Your Work

1. Click **"Save"** (top right)
2. Review your flow visually
3. Check all paths are complete

### 9.2 Publish

1. Click **"Publish"**
2. Review changes
3. Confirm publish
4. Wait for success message

---

## Testing Guide

### Test Scenario 1: SOX Controls

**Input:**
```
User: "SOX requirements"
```

**Expected Flow:**
```
Bot: "Which compliance framework?"
User: [Clicks "SOX (Sarbanes-Oxley)"]
Bot: "I can help with SOX 404. What would you like to know?"
     [Shows 5 SOX topics as buttons]
User: [Clicks "Financial controls and testing results"]
Bot: [Generative answer with SOX control details from document]
     [Shows Q3 2024 testing results]
     [References SOX-FIN-REV-001]
Bot: "Anything else about SOX?"
```

**Validation:**
- [ ] Trigger phrase activated topic
- [ ] Framework selection worked
- [ ] SOX subtopics displayed
- [ ] Generative answer returned relevant info
- [ ] Referenced correct document (SOX-FIN-REV-001)
- [ ] Included specific details (control IDs, testing results)
- [ ] Follow-up question appeared

### Test Scenario 2: GDPR Breach Notification

**Input:**
```
User: "GDPR breach notification"
```

**Expected Flow:**
```
Bot: [Skips framework question - detected "GDPR"]
     "I can help with GDPR. What aspect?"
     [Shows 6 GDPR topics]
User: [Clicks "Data breach notification (72-hour rule)"]
Bot: [Shows detailed breach notification message]
     - Internal timeline (Immediately, 2 hours, 4 hours)
     - External timeline (72 hours to authority, without delay to individuals)
     - Risk assessment factors
     - Example scenarios table
     - Documentation requirements
Bot: "Anything else about GDPR?"
```

**Validation:**
- [ ] Proactive slot filling worked (skipped framework question)
- [ ] GDPR subtopics appeared
- [ ] Breach notification content detailed and accurate
- [ ] Timelines clearly specified (72 hours, etc.)
- [ ] Table formatted correctly
- [ ] Examples included
- [ ] Referenced POL-SEC-GDPR-001

### Test Scenario 3: ITGC Change Management

**Input:**
```
User: "What are change management requirements?"
```

**Expected Flow:**
```
Bot: "Which compliance framework?"
User: [Types "ITGC" or "change management"]
Bot: "I can help with ITGC. What would you like to know?"
User: [Clicks "Change management process and CAB approval"]
Bot: [Generative answer with]:
     - CAB meeting schedule (Tuesdays 2 PM)
     - Change categories (Standard, Normal, Major, Emergency)
     - Approval requirements by category
     - Referenced ITGC-CHG-001
```

**Validation:**
- [ ] Framework detected
- [ ] ITGC subtopics shown
- [ ] Generative answer specific to change management
- [ ] Referenced correct document
- [ ] Included specific details from policy

### Test Scenario 4: Multiple Framework Queries

**Input:**
```
User: "Tell me about SOX"
[Complete SOX interaction]
Bot: "Anything else?"
User: "Yes, now tell me about GDPR"
```

**Expected:**
- [ ] Bot returns to framework selection
- [ ] Can handle second framework smoothly
- [ ] Variables don't conflict
- [ ] Context switches properly

### Test Scenario 5: Edge Cases

**Test A: Unknown Framework**
```
User: "HIPAA requirements"
Bot: "Which compliance framework?"
User: [Types "HIPAA"]
Bot: [Routes to "Other frameworks" message]
     "I currently have SOX, GDPR, ITGC, ASC 606..."
```

**Test B: Very Specific Query**
```
User: "GDPR data portability requirements for SaaS customers"
Bot: [Detects GDPR, shows subtopics]
User: [Clicks "Data subject rights"]
Bot: [Shows all 6 rights including data portability]
     [Specific format requirements: CSV, JSON, XML]
```

**Test C: Abbreviations**
```
User: "SOX 404"
Expected: Recognizes SOX

User: "DPR" (Data Protection Regulation)
Expected: May not recognize - user needs to clarify
```

---

## Troubleshooting

### Problem: Framework Not Detected from Trigger

**Symptoms:**
- User says "GDPR requirements"
- Bot asks "Which framework?" instead of skipping

**Solution:**
1. **Check entity extraction:**
   - Verify `ComplianceFramework` entity has "GDPR" as value
   - Add synonyms: "GDPR", "Data Protection", "Privacy Regulation"

2. **Check "Skip question" setting:**
   - Must be enabled on framework question node
   - Test with specific trigger: "Tell me about GDPR"

3. **Add more trigger phrases:**
   - Include framework-specific phrases
   - "GDPR compliance", "SOX requirements", "ITGC controls"

### Problem: Subtopic Buttons Not Showing

**Symptoms:**
- Framework selected but no subtopic options appear

**Solution:**
1. **Check condition routing:**
   - Verify condition uses "contains" not "is equal to"
   - Check spelling: `"SOX"` not `"Sox"`

2. **Check message + question sequence:**
   - Introduction message first
   - Question node with buttons second
   - Must be in correct branch after condition

3. **Check button text:**
   - Must have actual text in button options
   - Not just empty buttons

### Problem: Generative Answer Too Generic

**Symptoms:**
- Response doesn't reference specific documents
- Lacks detail from knowledge base

**Solution:**
1. **Verify data sources:**
   - Correct documents selected for that framework
   - SOX branch should use sox_revenue_recognition.md
   - GDPR branch should use data_privacy_gdpr_policy.md

2. **Enhance custom prompt:**
   - Add "Reference specific document sections"
   - Include "Cite document IDs and version numbers"
   - Request "Include specific examples from the policy"

3. **Test knowledge base:**
   - In test chat, ask "What's in SOX-FIN-REV-001?"
   - If no answer, knowledge base not indexed properly

### Problem: Messages Too Long / Not Formatted Well

**Symptoms:**
- Wall of text, hard to read
- No structure or sections

**Solution:**
1. **Add formatting:**
   - Use **bold** for headers
   - Use ✓ ✗ symbols for lists
   - Add section dividers with ━━━
   - Use tables for complex info

2. **Break into multiple messages:**
   - Introduction message
   - Detailed content message
   - Summary/next steps message

3. **Use adaptive cards (optional):**
   - More structured display
   - Better for tables and lists
   - (Requires additional configuration)

### Problem: User Can't Get Back to Framework Selection

**Symptoms:**
- User stuck in SOX subtopics
- Wants to switch to GDPR

**Solution:**
1. **Add "Go back" option:**
   - In follow-up question, add button: "Select different framework"
   - Routes back to framework selection

2. **Add "Start over" option:**
   - Redirects to beginning of topic

3. **Allow natural language:**
   - If user says "Actually, tell me about GDPR instead"
   - Topic should re-trigger or use fallback

---

## Example Interactions

### Example 1: Quick SOX Query

```
User: "What are SOX controls for revenue?"

Bot: I can help with SOX 404 compliance requirements.

📊 SOX 404 Overview:
Our SOX program covers internal controls over financial reporting,
particularly for revenue recognition.

What would you like to know about?

[Financial controls and testing results]
[Control narratives and RCMM]
[Management assertions and sign-offs]
[Control deficiencies and remediation]
[Specific control]

User: [Clicks "Financial controls and testing results"]

Bot: Here's information about SOX 404 Financial Controls for Revenue Recognition:

**Key Controls Tested (Q3 2024):**

**Control REV-C01: Contract Review and Approval**
- All contracts >$100K require Revenue Team review before execution
- Testing: 25 contracts sampled
- Results: No exceptions noted
- Effectiveness: ✓ Effective

**Control REV-C02: System-Enforced Revenue Recognition**
- SAP RAR automatically calculates revenue based on approved contract terms
- Testing: 30 contracts tested for accurate SSP allocation
- Results: No exceptions noted
- Effectiveness: ✓ Effective

**Control REV-C03: Monthly Revenue Reconciliation**
- Senior Revenue Accountant reconciles subledger to GL monthly
- Testing: July, August, September 2024 reconciliations reviewed
- Results: No exceptions noted
- Effectiveness: ✓ Effective

**Control REV-C04: Revenue Cut-off Testing**
- Revenue Accounting Manager performs quarterly cut-off testing
- Testing: Q3 2024 (Sept 30) tested with 40 transactions
- Results: 1 immaterial exception ($75K, corrected in Q4)
- Effectiveness: ✓ Effective

**Control REV-C05: Manual Revenue Journal Entry Review**
- All manual revenue JEs require dual approval
- Testing: 18 manual JEs in Q3 tested (100% of population)
- Results: No exceptions noted
- Effectiveness: ✓ Effective

**Overall Assessment:**
Internal controls over revenue recognition are operating effectively
with no material weaknesses or significant deficiencies identified.

**Source:** SOX 404 Control Documentation - Revenue Recognition (SOX-FIN-REV-001)

Is there anything else I can help you with regarding SOX compliance?

[Yes, I have another question]
[Show me related documents]
[No, I'm all set]

User: [Clicks "No, I'm all set"]

Bot: Great! If you need any compliance or audit documentation in the future, just ask.

💡 Quick tip: You can also ask me to:
- Find specific policies
- Generate audit checklists  
- Look up approval requirements

Happy auditing! ✅

[End conversation with survey]
```

### Example 2: Detailed GDPR Investigation

```
User: "I need to understand GDPR breach notification"

Bot: [Skips framework question - detected GDPR]

I can help with GDPR (General Data Protection Regulation) requirements.

🔒 GDPR Compliance Areas:

Our GDPR policy covers all aspects of data protection for EEA/UK personal data.

What aspect are you interested in?

[Data subject rights (access, erasure, portability)]
[Data breach notification (72-hour rule)]
[Data retention and disposal schedules]
[International data transfers and SCCs]
[DPIA requirements]
[Legal bases for processing]

User: [Clicks "Data breach notification (72-hour rule)"]

Bot: 🚨 GDPR Data Breach Notification Requirements

CRITICAL TIMELINE - 72 HOURS:

Internal Notification:
- Discovery → InfoSec: Immediately
- InfoSec → DPO: Within 2 hours
- DPO → Executive Team: Within 4 hours (if likely breach)

External Notification:
- DPO → Supervisory Authority: Within 72 hours ⏰
- DPO → Affected Individuals: Without undue delay (if high risk)

[... full breach notification content ...]

Need help with breach assessment or notification templates?

User: "Yes, how do I assess if it's high risk?"

Bot: Great question! Here's how to assess breach risk:

**Risk Assessment Factors:**

1. **Type and Sensitivity of Data:**
   - Special category data (health, racial origin) = HIGH risk
   - Financial data (bank accounts, credit cards) = HIGH risk
   - Contact information only (email, phone) = LOWER risk

2. **Volume of Affected Individuals:**
   - <100 people = Lower risk
   - 100-10,000 = Medium risk
   - >10,000 = Higher risk

3. **Ease of Identifying Individuals:**
   - Data includes names, IDs = Easy identification = HIGHER risk
   - Pseudonymized/coded data = Harder identification = LOWER risk

4. **Consequences to Individuals:**
   - Could lead to identity theft = HIGH risk
   - Could cause discrimination = HIGH risk
   - Minor inconvenience only = LOWER risk

5. **Special Characteristics:**
   - Children's data = HIGHER risk
   - Vulnerable groups = HIGHER risk
   - General population = Standard risk

**Risk Matrix:**
HIGH risk = Must notify individuals + authority
MEDIUM risk = Must notify authority, assess individual notification
LOW risk = May not need to notify

**Example Assessment:**
Breach: Laptop with 500 customer records stolen
- ✓ Encrypted with strong encryption
- Assessment: LOW risk (data protected by encryption)
- Action: NO notification required

Breach: USB with 5,000 unencrypted employee health records lost
- ✗ Unencrypted
- ✓ Special category data (health)
- ✓ Large volume
- Assessment: HIGH risk
- Action: Notify authority AND individuals

Need help assessing your specific situation?

[... continues ...]
```

---

## Summary

### What You Built

✅ **Hierarchical Topic** with 3 levels of navigation:
- Framework selection
- Subtopic selection  
- Detailed information

✅ **Three Major Framework Paths:**
- SOX: 5 subtopics, testing results, control details
- GDPR: 6 subtopics, timelines, requirements, examples
- ITGC: 6 subtopics, change management focus

✅ **Rich Content:**
- Timelines (72-hour breach rule)
- Tables (risk scenarios, retention periods)
- Examples (breach assessments)
- Checklists (DPIA process)
- References (document IDs, sections)

✅ **Smart Navigation:**
- Proactive framework detection
- Loop back for multiple queries
- Related documents
- Graceful exits

### Key Success Metrics

- **Trigger Rate:** Should be >15% of conversations
- **Completion Rate:** >80% (users find what they need)
- **Follow-up Rate:** 30-40% ask additional questions
- **Satisfaction:** >4.5/5 stars

### Time Investment

- **Setup & Framework Selection:** 30 minutes
- **SOX Branch:** 45 minutes
- **GDPR Branch (6 subtopics):** 90 minutes
- **ITGC Branch:** 30 minutes
- **Testing & Refinement:** 45 minutes
- **Total:** ~4 hours

---

**You now have a comprehensive Compliance Framework Lookup topic that provides detailed, structured information on SOX, GDPR, and ITGC!** 🎉

This topic showcases:
- Conditional logic
- Hierarchical navigation
- Rich content delivery
- Multiple paths and branches
- Professional formatting

**Well done! This is a complex, high-value topic.** 🚀

---

**End of Implementation Guide**