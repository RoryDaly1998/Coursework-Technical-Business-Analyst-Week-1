# Self-Service Automation Candidates

This document identifies process steps suitable for automation or customer self-service based on four suitability criteria, and prioritizes top candidates for Phase 1 implementation.

## Self-Service Suitability Framework

### High-Volume Steps
Steps that occur frequently across the delinquent account base, where even small efficiency gains multiply significantly.

- **Check whether the money has been paid in the legacy database** — Every arrangement requires fulfillment tracking; currently manual and error-prone.
- **Log contact attempt** — Every customer interaction triggers a manual logging step across multiple systems.
- **Flag account or move on worklist** — Every account requires disposition after each contact attempt.
- **Update tracker and legacy database** — Required for every resolved case; currently 3-4 manual entries per resolution.
- **Returns customer contact history** — Repeated lookup across spreadsheet and email.

---

### Repeatable Steps
Steps that follow consistent, predictable workflows with little variation between cases.

- **Delinquency report created** — Triggered automatically when account enters queue; consistent logic.
- **Returns customer details** — Lookup of customer data from legacy database; structured query with fixed output.
- **Returns customer contact history** — Extraction of communication log; consistent data retrieval pattern.
- **Customer identity checked** — Verification against customer record; rules-based validation.
- **Flag account or move on worklist** — Disposition logic based on outcome (paid/not paid/arrangement set); rules-driven.
- **Update tracker and legacy database** — Record update logic based on payment confirmation; repeatable steps.
- **Check whether the money has been paid** — Query against payment systems; repeatable lookup.

---

### Rules-Driven Steps
Steps that follow clear decision logic without requiring judgment or negotiation.

- **Delinquency report created** — Automatic report generation based on account status.
- **Check whether the money has been paid** — Query result is binary (paid/not paid); no interpretation required.
- **Customer identity checked** — Rules-based verification (name, DOB, account number match).
- **Flag account or move on worklist** — Decision tree: if arrangement set → flag; if paid → close; if no response → escalate.
- **Update tracker and legacy database** — Status transitions follow clear rules based on payment outcome.
- **Returns customer details** — Data lookup; no decision logic.
- **Returns customer contact history** — Data retrieval; no decision logic.

---

### Lower-Risk Steps
Steps where automation errors are unlikely to trigger compliance risk, customer dissatisfaction, or financial loss.

- **Returns customer contact history** — Read-only data retrieval; no financial or compliance exposure.
- **Returns customer details** — Read-only lookup; no account modifications.
- **Delinquency report created** — System-to-system data transfer; compliance risk exists but is data quality issue, not automation risk.
- **Flag account or move on worklist** — Logical disposition; low risk if rules are correct.
- **Check whether the money has been paid** — Query against authoritative payment data; minimal risk if payment system is source of truth.

---

## Top Automation Candidates for Phase 1

### Candidate 1: Payment Fulfillment Check & Account Status

**Process Steps:**
- Check whether the money has been paid in the legacy database
- Flag account or move on worklist

**Self-Service Criteria Met:** High-volume, Repeatable, Rules-driven, Lower-risk

**Associated Pain Points:**
- **Pain Point 4: No System-Driven Arrangement Fulfillment Check** — Reps must rely on memory or manual checking; system should automatically prompt and verify.
- **Pain Point 5: Poor Visibility of Promise-to-Pay Fulfillment** — No way to track promised dates or auto-verify on due date.

**Jobs-to-be-Done (JTBD):**
- **JTBD-04:** *"When a case is awaiting a promised callback, I want to record and track the promised date, so that the callback is completed on time and the case does not remain stalled."*

**Automation Approach:**
- Scheduled daily batch process queries payment systems (bank, card processor) for all outstanding arrangements.
- Automatically flags accounts where promised payment has cleared.
- Updates tracker with status and closes case if payment meets original obligation.
- Alerts reps to accounts where promise is overdue.
- Single system of record replaces spreadsheet + email tracking.

**Impact:**
- Eliminates manual checking.
- Prevents re-contact on already-paid accounts.
- Resolves Pain Point 4 (automatic fulfillment check) and Pain Point 5 (payment visibility).
- Supports Pain Point 1 (single system of record) by centralizing arrangement tracking.

---

### Candidate 2: Contact History Retrieval & Duplicate Prevention

**Process Steps:**
- Returns customer contact history (from spreadsheet)
- Returns customer contact history (from email)

**Self-Service Criteria Met:** High-volume, Repeatable, Rules-driven, Lower-risk

**Associated Pain Points:**
- **Pain Point 1: Multi-Source Update Discrepancies** — Contact history scattered across spreadsheet, email, and phone logs; reps waste time cross-checking.

**Jobs-to-be-Done (JTBD):**
- **JTBD-04:** *"When a case is awaiting a promised callback, I want to record and track the promised date, so that the callback is completed on time and the case does not remain stalled."*

**Automation Approach:**
- Unified contact history dashboard pulls from phone system, email, and legacy database.
- Shows all contact attempts, outcomes, and promised follow-up dates in chronological order.
- Flags accounts where a prior promise or arrangement exists and is still pending.
- Alerts rep if they are about to re-contact an account with an active arrangement.
- Integrates with outbound call system to block re-contact on flagged arrangements.

**Impact:**
- Eliminates manual cross-checking per account per contact.
- Prevents duplicate contact attempts (reduces compliance risk and customer complaints).
- Resolves Pain Point 1 (single source of truth for contact history).
- Supports Candidate 1 by providing input to arrangement fulfillment check.

---

### Candidate 3: Automated Record Logging & System Synchronization

**Process Steps:**
- Log contact attempt (in database and spreadsheet/email)
- Create internal email-as-record-keeping
- Update tracker and legacy database (when payment received)

**Self-Service Criteria Met:** High-volume, Repeatable, Rules-driven, Lower-risk

**Associated Pain Points:**
- **Pain Point 1: Multi-Source Update Discrepancies** — Updates must be entered in 3-4 places; discrepancies between systems are common.
- **Pain Point 2: Manual Record Update and Discrepancies** — Time-consuming manual entry across multiple locations.

**Jobs-to-be-Done (JTBD):**
- **JTBD-05:** *"When a compliance review requires reconstructing what happened to a case, I want to rely on a complete record of its activity across systems, so that I can verify the case history without searching fragmented records."*

**Automation Approach:**
- When rep logs outcome in primary system (call result, arrangement details, payment received), it automatically:
  - Records in legacy database.
  - Updates all tracking spreadsheets.
  - Creates audit trail entry (replacing email-as-record-keeping).
  - Triggers follow-up date in scheduling system.
- Single data entry point replaces manual logging to 3-4 systems.
- Audit trail is system-generated, timestamped, and immutable (compliance requirement).

**Impact:**
- Reduces per-contact administrative time.
- Eliminates data discrepancies between systems (single entry point).
- Provides reliable audit trail for compliance.
- Resolves Pain Point 1 (no more multi-source updates) and Pain Point 2 (no more manual discrepancies).

---

### Candidate 4: Automated Case Triage and Complexity Classification

**Process Steps:**
- Check account legacy status
- Customer identity checked

**Self-Service Criteria Met:** Repeatable, Rules-driven, Lower-risk

**Jobs-to-be-Done (JTBD):**
- **JTBD-02:** *"When a collections case needs attention, I want to identify whether it is straightforward or requires specialist handling, so that it receives the appropriate level of support."*

**Automation Approach:**
- Scoring algorithm evaluates case complexity based on:
  - Account type (credit card vs. loan vs. overdraft).
  - Customer circumstances flagged in data (hardship marker, vulnerability indicator, previous dispute).
  - Account status (early delinquency vs. late).
  - Payment history (chronic non-payer vs. first default).
  - Whether account has been escalated or transferred previously.
- Assigns case to one of three tracks: **Routine** (suitable for rep or self-service), **Complex** (requires experienced rep), or **Specialist** (hardship, vulnerability, legal, regulatory).
- Flags accounts with hardship, vulnerability, or regulatory hold for human review before automation is attempted.
- Routes routine cases to standard contact strategies; escalates complex and specialist cases immediately.

**Impact:**
- Ensures simple cases move quickly without bottleneck from complex work.
- Protects vulnerable customers by identifying them upfront and routing to appropriate handling.
- Enables reliable reporting: managers can now distinguish routine from specialist work and report on each separately.
- Reduces misrouted cases and rework from inappropriate handling.
- Resolves Pain Point 2 by providing clear classification.

---

### Candidate 5: Intelligent Case Prioritization and Contact Sequencing

**Process Steps:**
- Receive the worklist
- Contact the customer (sequencing of outreach)

**Self-Service Criteria Met:** Repeatable, Rules-driven, Lower-risk

**Jobs-to-be-Done (JTBD):**
- **JTBD-03:** *"When multiple customer accounts need contact, I want to sequence outreach strategically, so that customers are contacted at an appropriate time and recovery effort is focused."*

**Automation Approach:**
- Scoring algorithm ranks cases in worklist by:
  - Time-sensitivity (cases with imminent promise-to-pay dates, overdue arrangements, or legal deadlines ranked first).
  - Customer readiness (accounts with recent contact, prior engagement, or high payment probability ranked higher).
  - Time-of-contact optimization (avoid calling at times customer is unlikely to answer; flag preferred contact windows).
  - Strategic timing (cases suitable for early-week contact ranked higher than Friday escalations).
  - Reprioritize daily based on: previous contact attempts that day, shift handoff timing, escalation rules.
- Prevents same customer being called multiple times in same day or by multiple reps.
- Recommends contact method (phone at time X, SMS at time Y, email) based on customer history and account type.

**Impact:**
- Increases contact success rate by calling at optimal times and sequencing.
- Prevents wasted contact attempts on customers already engaged or awaiting callback.
- Improves recovery rate: customers reached at right time are more likely to commit to payment.
- Reduces rep frustration: removes randomness from worklist allocation.
- Resolves Pain Point 3 by preventing re-contact and Pain Point 1 by ensuring coordinated strategy.

---

## Representative-Led Steps (Should Remain High-Touch)

The following steps require human judgment, negotiation, customer empathy, or complex decision-making and should **not** be automated or pushed to self-service:

### HIGH-RISK / JUDGMENT-REQUIRED:

**Negotiate payment options with customer**
- *Reason:* Requires judgment about customer hardship, ability to pay, and negotiation of arrangement terms. Regulatory requirement for compliance with affordability rules. High financial impact if wrong decision made. Risk of treating vulnerable customers unfairly.

**Recontact customer, attempt new arrangement**
- *Reason:* Requires judgment about customer's changed circumstances, potential hardship, and willingness to engage. Second or third contact attempts are high-risk for compliance (contact frequency rules, vulnerable customer protection). Needs experienced rep judgment.

**Escalate to manager**
- *Reason:* Escalation decision requires judgment: Is this a complex case? Is customer in hardship? Does it require specialist handling or legal action? Managers must make these calls based on customer circumstances.
