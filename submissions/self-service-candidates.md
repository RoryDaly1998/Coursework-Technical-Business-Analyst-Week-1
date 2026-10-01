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

### Candidate 2: Automatic Case Assignment with Pre-Loaded Customer Details

**Process Steps:**
- Receive next case from worklist
- Returns customer details (from legacy database)
- Returns customer contact history (unified from all sources)

**Self-Service Criteria Met:** High-volume, Repeatable, Rules-driven, Lower-risk

**Associated Pain Points:**
- **Pain Point 1: Multi-Source Update Discrepancies** — Contact history scattered across spreadsheet, email, and phone logs; reps waste time cross-checking.
- **Pain Point 6: Time-Consuming Customer Contact Attempts** — Reps spend time looking up customer details before each call.

**Jobs-to-be-Done (JTBD):**
- **JTBD-04:** *"When a case is awaiting a promised callback, I want to record and track the promised date, so that the callback is completed on time and the case does not remain stalled."*

**Automation Approach:**
- When rep is ready for next case, system automatically assigns the highest-priority case from the sequenced worklist and simultaneously loads:
  - Customer demographics (name, address, DOB, contact details).
  - Account details (balance, type, delinquency status, arrangement history).
  - Complete contact history (all prior calls, emails, promises, outcomes) in chronological order.
  - Vulnerability or hardship flags.
  - Recommended contact method and optimal calling window.
- All information pre-loaded and displayed in single dashboard view.
- Rep can immediately begin call without lookup overhead.
- Prevents reps from choosing their own cases (ensures sequencing compliance).

**Impact:**
- Eliminates lookup time per account.
- Ensures cases are worked in optimal sequence (prevents cherry-picking).
- Reduces context-switching and improves contact quality.
- Resolves Pain Point 1 (unified customer view) and Pain Point 6 (faster contact initiation).

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

### Candidate 4: Automated Case Classification and Complexity Triage

**Process Steps:**
- Check account legacy status
- Customer identity checked

**Self-Service Criteria Met:** Repeatable, Rules-driven, Lower-risk

**Associated Pain Points:**
- **Pain Point 2: Manual Record Update and Discrepancies** — Manual routing without system guidance leads to inconsistent handling.

**Jobs-to-be-Done (JTBD):**
- **JTBD-02:** *"When a collections case needs attention, I want to identify whether it is straightforward or requires specialist handling, so that it receives the appropriate level of support."*

**Automation Approach:**
- Evaluates case complexity based on: account type, customer circumstances flags (hardship, vulnerability, disputes), account status, payment history, escalation history.
- Assigns case to: **Routine** (standard contact), **Complex** (experienced rep required), or **Specialist** (hardship, vulnerability, legal/regulatory).
- Protects vulnerable customers by flagging for human review before automation.
- Enables routing to appropriate skill level.
- Classification feeds into prioritization algorithm (Candidate 5) to ensure specialist cases are not cherry-picked or underhandled.

**Impact:**
- Routes cases to appropriate handling level based on complexity.
- Protects vulnerable customers through automated identification and escalation.
- Enables managers to distinguish and report on routine vs. specialist work.
- Prevents misrouted cases and rework from inappropriate handling.
- Resolves Pain Point 2 through systematic case evaluation.

---

### Candidate 5: Intelligent Case Prioritization and Contact Sequencing

**Process Steps:**
- Receive the worklist
- Contact the customer (sequencing of outreach)

**Self-Service Criteria Met:** Repeatable, Rules-driven, Lower-risk

**Associated Pain Points:**
- **Pain Point 3: Broken Arrangements and Re-Contact on Already-Promised Accounts** — Uncoordinated sequencing causes duplicate contacts.

**Jobs-to-be-Done (JTBD):**
- **JTBD-03:** *"When multiple customer accounts need contact, I want to sequence outreach strategically, so that customers are contacted at an appropriate time and recovery effort is focused."*

**Automation Approach:**
- Ranks all active cases in worklist by:
  - Time-sensitivity (imminent promise-to-pay dates, overdue arrangements, legal deadlines ranked first).
  - Customer readiness (recent contact, prior engagement, high payment probability ranked higher).
  - Time-of-contact optimization (recommended call windows based on customer profile and historical answer rates).
  - Strategic timing (early-week calls ranked higher than Friday escalations).
- Respects case classification from Candidate 4: ensures specialist cases receive appropriate priority and are routed accordingly.
- Reprioritizes daily based on: contact attempts that day, shift handoffs, escalation rules.
- Prevents same customer being called multiple times same day or by multiple reps.
- Recommends contact method (phone at time X, SMS at time Y, email) based on customer history.

**Impact:**
- Ensures cases are worked in optimal sequence, maximizing contact success rates.
- Prevents duplicate contacts and re-contact on active arrangements.
- Increases recovery rate by calling customers at optimal times.
- Eliminates worklist randomness and rep cherry-picking.
- Resolves Pain Point 3 through coordinated sequencing.

---

### Candidate 6: Automated Recontact Flagging and Follow-Up Scheduling

**Process Steps:**
- Log contact attempt outcome
- Flag account or move on worklist
- Create scheduled callback reminder

**Self-Service Criteria Met:** High-volume, Repeatable, Rules-driven, Lower-risk

**Associated Pain Points:**
- **Pain Point 5: Poor Visibility of Promise-to-Pay Fulfillment** — Reps must manually track who to recontact and when; system provides no reminders.
- **Pain Point 4: No System-Driven Arrangement Fulfillment Check** — Manual tracking leads to missed follow-ups.

**Jobs-to-be-Done (JTBD):**
- **JTBD-04:** *"When a case is awaiting a promised callback, I want to record and track the promised date, so that the callback is completed on time and the case does not remain stalled."*

**Automation Approach:**
- When rep logs contact outcome (no answer, voicemail, promised callback, agreed arrangement with callback date), system automatically:
  - Flags account for recontact with classification: **Today** (same day follow-up), **Tomorrow** (next business day), **Week** (within 7 days), **Scheduled** (specific date logged by rep).
  - Creates scheduler entry with due date and time window (based on customer preference or historical contact success patterns).
  - Alerts rep when approaching due date (notification before scheduled time).
  - Prevents system from assigning other reps to same account until recontact flag is cleared or escalated.
  - Tracks recontact compliance: how many promised callbacks were completed on time vs. missed.
- Eliminates need for reps to manually track who to call back (replaces informal "sticky note" tracking).
- No data entry required from rep beyond normal outcome logging.

**Impact:**
- Ensures promised follow-ups are not forgotten or delayed.
- Reduces recontact compliance risk (demonstrable proof that promised dates were attempted).
- Eliminates manual recontact tracking burden on reps.
- Provides visibility to managers on follow-up adherence.
- Prevents customers from being re-contacted unnecessarily (separate tracking prevents duplicate calls).
- Resolves Pain Points 4 and 5 through automated, system-driven follow-up management.

---

### Candidate 6: Automated Recontact Flagging and Follow-Up Scheduling

**Process Steps:**
- Log contact attempt outcome
- Flag account or move on worklist
- Create scheduled callback reminder

**Self-Service Criteria Met:** High-volume, Repeatable, Rules-driven, Lower-risk

**Associated Pain Points:**
- **Pain Point 5: Poor Visibility of Promise-to-Pay Fulfillment** — Reps must manually track who to recontact and when; system provides no reminders.
- **Pain Point 4: No System-Driven Arrangement Fulfillment Check** — Manual tracking leads to missed follow-ups.

**Jobs-to-be-Done (JTBD):**
- **JTBD-04:** *"When a case is awaiting a promised callback, I want to record and track the promised date, so that the callback is completed on time and the case does not remain stalled."*

**Automation Approach:**
- When rep logs contact outcome (no answer, voicemail, promised callback, agreed arrangement with callback date), system automatically:
  - Flags account for recontact with classification: **Today** (same day follow-up), **Tomorrow** (next business day), **Week** (within 7 days), **Scheduled** (specific date logged by rep).
  - Creates scheduler entry with due date and time window (based on customer preference or historical contact success patterns).
  - Alerts rep when approaching due date (notification before scheduled time).
  - Prevents system from assigning other reps to same account until recontact flag is cleared or escalated.
  - Tracks recontact compliance: how many promised callbacks were completed on time vs. missed.
- Eliminates need for reps to manually track who to call back (replaces informal "sticky note" tracking).
- No data entry required from rep beyond normal outcome logging.

**Impact:**
- Ensures promised follow-ups are not forgotten or delayed.
- Reduces recontact compliance risk (demonstrable proof that promised dates were attempted).
- Eliminates manual recontact tracking burden on reps.
- Provides visibility to managers on follow-up adherence.
- Prevents customers from being re-contacted unnecessarily (separate tracking prevents duplicate calls).
- Resolves Pain Points 4 and 5 through automated, system-driven follow-up management.

---

### Candidate 7: Customer Self-Service Portal for Account Updates and Simplified Payment

**Process Steps:**
- Contact the customer (customer initiates via portal)
- Negotiate payment options with customer (automated options offered)
- Take arrangement details
- Receive payment

**Self-Service Criteria Met:** High-volume, Repeatable, Rules-driven (payment options), Lower-risk (straightforward payment)

**Associated Pain Points:**
- **Pain Point 6: Time-Consuming Customer Contact Attempts** — Reps spend significant time waiting for customer to answer or play phone tag.
- **Pain Point 1: Multi-Source Update Discrepancies** — Customer details get out of sync when manual updates occur.
- **Pain Point 2: Manual Record Update and Discrepancies** — Reps must manually record customer's payment promise.

**Jobs-to-be-Done (JTBD):**
- **JTBD-01:** *"When I want to resolve my debt quickly, I want simple, transparent options and clear information on what I owe and how I can pay, so that I can take action immediately without being forced into lengthy conversations."*
- **JTBD-04:** *"When a case is awaiting a promised callback, I want to record and track the promised date, so that the callback is completed on time and the case does not remain stalled."*

**Automation Approach:**
- Self-service web/mobile portal accessible to delinquent account holders:
  - **Account View:** Shows current balance, delinquency status, payment history, and any open arrangements.
  - **Simplified Payment Options:** Displays 3-5 pre-configured arrangement templates (e.g., "Pay in 3 installments," "Pay 50% now, 50% in 30 days," "Full payment today") with clear terms.
  - **Account Update:** Customers can update contact phone number, email, and preferred contact method.
  - **Payment Processing:** For straightforward cases (Routine complexity), customers can agree to arrangement and process payment directly through portal (bank transfer, card payment).
  - **Confirmation and Tracking:** Arrangement details automatically recorded in system; customer receives SMS/email confirmation with payment schedule.
  - **Escalation Path:** If customer selects option outside pre-approved templates or account is flagged as Complex/Specialist, portal routes to rep for negotiation.
- For payment arrangements under £X (configurable threshold), no rep involvement required.
- For complex hardship cases, portal still provides account transparency but requires rep contact for negotiation.

**Impact:**
- Customers can resolve accounts without waiting for rep availability (24/7 access).
- Eliminates phone tag and call waiting time for reps and customers.
- Reduces incoming call volume for representatives (frees capacity for Complex/Specialist cases).
- Single system of record: no manual transcription of customer updates or arrangements.
- Faster resolution for straightforward accounts (customer self-initiates).
- Improves customer experience: transparency, control, and instant access to options.
- Resolves Pain Points 1, 2, and 6 through direct customer interaction and system-recorded outcomes.

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
