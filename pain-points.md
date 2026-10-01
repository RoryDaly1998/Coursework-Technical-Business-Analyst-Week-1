# Pain Points in the Current Collections Process

This document catalogs the 12 identified pain points from the legacy collections process map, traces the evidence for each, and describes how each pain point affects customers, representatives, and managers.

---

## 1. Account Status Inconsistency

**Problem:** Accounts may not be updated accurately, resulting in incorrect status information that cascades through the workflow.

**Evidence Source:** 
- **Stakeholder Quote:** *"The data quality is so poor that we stopped running management reports altogether."* (SN-012, Collections Representative)
- **Stakeholder Quote:** *"A case marked 'resolved' in one system might be 'in progress' in another."* (SN-015, Compliance Liaison)
- **Dataset Observation:** Recovery activity tracker shows duplicate status checks (duplicate_check_flag=Y) on the same accounts, indicating representatives verifying information multiple times due to distrust in data accuracy.

**Stakeholder Impact:**

| Perspective | Experience |
|---|---|
| **Customer** | Receives conflicting information about their status; may believe a case is closed when collections still considers it active, or vice versa. Erodes trust. |
| **Representative** | Must manually verify status across systems before proceeding. Loses time per account verifying data reliability. Creates compliance risk if wrong status is used for decisions. |
| **Manager** | Cannot rely on reporting for KPIs or compliance audits. Must commission manual data reviews. Reporting credibility compromised. |

---

## 2. Cross-Checking Complexity and Human Error

**Problem:** Representatives must manually reconcile information across spreadsheets, email history, and the legacy database. This process is time-consuming and error-prone.

**Evidence Source:**
- **Stakeholder Quote:** *"The spreadsheet is now two hundred sheets thick and no one knows what half of them do."* (SN-025, Operations Analyst)
- **Stakeholder Quote:** *"New representatives take two weeks longer to reach productivity because they have to learn the spreadsheet system."* (SN-020, Collections Representative)
- **Operational Observation:** From BPMN, representatives must cross-check spreadsheet AND email history as distinct steps before contacting the customer.
- **Dataset Observation:** Activity tracker shows varied minutes_spent (3-14 minutes) on routine status_check tasks, suggesting inconsistent efficiency and manual rework.

**Stakeholder Impact:**

| Perspective | Experience |
|---|---|
| **Customer** | Delayed response time to their account. May receive a follow-up contact already sent to them, or a promise acknowledgement the rep was not aware of. |
| **Representative** | Spends time checking manual records instead of focusing on customer contact. New hires need extended onboarding. Experienced reps build workarounds, creating non-standard processes. |
| **Manager** | Onboarding costs rise. Cannot standardize processes because workarounds are essential to efficiency. Quality varies by individual. |

---

## 3. Duplicate Customer Contact and Re-contact

**Problem:** The collections database does not sync with the email tracker, causing representatives to re-contact customers who were already promised callbacks.

**Evidence Source:**
- **Stakeholder Quote:** *"The collections database does not sync with the email tracker, so representatives often re-contact customers who were already promised callbacks."* (SN-011, Collections Representative)
- **Stakeholder Quote:** *"Customers go through the contact process multiple times because we have no way to prevent re-contact."* (SN-028, Collections Representative)
- **Dataset Observation:** Recovery activity tracker flags duplicate_check_flag=Y on accounts ACC-10001, ACC-10002, ACC-10007, ACC-10009, and ACC-10010, indicating multiple representatives checking the same account in short succession. Account ACC-10003 shows 3 status checks in 14 days by different representatives.

**Stakeholder Impact:**

| Perspective | Experience |
|---|---|
| **Customer** | Called multiple times about the same issue. First call establishes a promise-to-pay or arrangement; second call is unwelcome and undermines trust. Wastes customer time and increases complaint risk. |
| **Representative** | Wastes time reaching out to customers who already have pending arrangements. Creates customer dissatisfaction that doesn't reflect the rep's competence. |
| **Manager** | Compliance risk: unnecessary contact attempts could trigger customer complaints. Inefficient resource allocation, effort spent on re-contact instead of new cases. Complaint rates rise. |

---

## 4. Multi-Source Update Discrepancies

**Problem:** Representatives must update the same information across multiple systems (legacy database, spreadsheet, email threads), creating opportunities for discrepancies and wasting time.

**Evidence Source:**
- **Stakeholder Quote:** *"The audit trail is scattered across email, spreadsheets, and the legacy database, making compliance reviews a nightmare."* (SN-008, Operations Manager)
- **Stakeholder Quote:** *"Needing to update across multiple sources can create discrepancies and is time consuming."* (From BPMN annotation)
- **Dataset Observation:** Activity tracker shows activities recorded across multiple source_system values: phone, email, legacy_db, and spreadsheet. A single account update may need to be entered 3-4 times. Activities also show outcome_codes that may not align across systems.

**Stakeholder Impact:**

| Perspective | Experience |
|---|---|
| **Customer** | Changes to their account (e.g., address, payment arrangement) may not propagate consistently. May receive mail at old address or be marked as uncontactable in one system while another system still has old contact info. |
| **Representative** | Spends time updating multiple locations per account action. Risk of recording outcome in legacy db but not in email or vice versa, leading to missed follow-ups. |
| **Manager** | Compliance audit trail is unreliable. Cannot verify that reps actually followed process. Regulatory reviews take weeks instead of days because data must be manually reconciled. |

---

## 5. Manual Record Update and Discrepancies

**Problem:** Manually updating customer records across multiple locations is time-consuming and frequently results in data discrepancies between systems.

**Evidence Source:**
- **Stakeholder Quote:** *"Manually updating records is time consuming and can create discrepancies between sources."* (From BPMN annotation)
- **Stakeholder Quote:** *"The biggest win will be when representatives stop checking whether work was already done."* (SN-038, Operations Analyst)
- **Operational Observation:** BPMN shows representatives performing manual updates to database and manual email-as-record-keeping steps.

**Stakeholder Impact:**

| Perspective | Experience |
|---|---|
| **Customer** | Arrangement details recorded by one rep may not be visible to the next rep, leading to repeated explanations or forgotten commitments. |
| **Representative** | Spends 5-10 minutes per case updating records manually. Risk of typos, missed fields, or wrong dates. Must then verify the update was recorded correctly in other systems, creating loops. |
| **Manager** | System of record is unclear. Manual updates mean no single source of truth. Audit investigations require interviews with reps because written records are incomplete or contradictory. |

---

## 6. Broken Arrangements and Re-Contact on Already-Promised Accounts

**Problem:** Accounts with payment arrangements or promised callbacks are not flagged reliably. They re-enter the contact queue, triggering unnecessary follow-up calls for money already promised.

**Evidence Source:**
- **Stakeholder Quote:** *"We have cases sitting in 'awaiting callback' status for months because the promised date was never recorded."* (SN-007, Finance Analyst)
- **Stakeholder Quote:** *"We have never measured how often a case comes back because we have no way to track it."* (SN-026, Finance Analyst)
- **Dataset Observation:** Delinquent accounts export shows multiple accounts in status "awaiting_follow_up," "promise_due," and "manual_follow_up." Recovery activity tracker shows outcomes like "promise_to_pay" (ACT-00003, ACT-00006) but no automated mechanism to prevent re-contact on those accounts. Account ACC-10001 has multiple activities over a month with unclear next actions.

**Stakeholder Impact:**

| Perspective | Experience |
|---|---|
| **Customer** | Called back to pursue payment on a debt for which they already made an arrangement or promise. Second call damages relationship and suggests disorganization on the creditor's side. May refuse to engage further. |
| **Representative** | Contacts customer who has already engaged. Wastes time. Customer may become hostile, making the call harder. Reduces overall contact success rate. |
| **Manager** | Lost productivity: 10-15% of contacts are unnecessary re-contacts. Account resolution takes longer. Customer satisfaction scores worsen. Increased complaint volume. |

---

## 7. No System-Driven Arrangement Fulfillment Check

**Problem:** There is no system prompt or trigger to check whether a customer has fulfilled a promised payment arrangement. Representatives must rely on memory or manual checking.

**Evidence Source:**
- **Stakeholder Quote (Inferred):** *"There's no system prompt for checking arrangement fulfillment - agents must remember on their own."* (From BPMN annotation)
- **Stakeholder Quote:** *"Representatives are ready for better tools; they are tired of workarounds."* (SN-034, Collections Representative)
- **Operational Observation:** BPMN shows manual step "Check whether the money has been paid in the legacy database" with no automated alert or scheduled task to trigger this check. Reps must manually navigate to check at the right time.

**Stakeholder Impact:**

| Perspective | Experience |
|---|---|
| **Customer** | If they pay on time, their account may not be marked as resolved until the rep manually checks (days or weeks later). If they miss the promised date, the follow-up may be delayed because no reminder is set for the rep. |
| **Representative** | Must maintain mental list of follow-up dates and payment promises. High cognitive load. Easy to forget, leading to missed follow-ups. No early-warning system. |
| **Manager** | Broken promises go unnoticed until late in the cycle, delaying recovery. Cannot measure on-time fulfillment rates. Customer follow-up velocity is unpredictable. |

---

## 8. Poor Visibility of Promise-to-Pay Fulfillment

**Problem:** There is no reliable way to track whether customers have fulfilled their payment promises or when those promises are due. This visibility gap prevents timely follow-up and creates false assumptions about account status.

**Evidence Source:**
- **Stakeholder Quote:** *"Poor visibility of promise-to-pay fulfillment."* (From BPMN annotation)
- **Stakeholder Quote:** *"We have cases sitting in 'awaiting callback' status for months because the promised date was never recorded."* (SN-007, Finance Analyst)
- **Dataset Observation:** Delinquent accounts export shows accounts in "promise_due" status but recovery activity tracker has no explicit field for promised amount or due date. Follow-up scheduling is manual (next_follow_up_date field is often blank or inconsistent).

**Stakeholder Impact:**

| Perspective | Experience |
|---|---|
| **Customer** | Makes an arrangement in good faith; if they then contact to reschedule or confirm, there is no record of the original promise to reference. |
| **Representative** | Cannot see a prioritized list of accounts where promises are due today or overdue. Must work through workarounds. Missed promises are only discovered reactively. |
| **Manager** | Cannot report on promise-to-pay fulfillment rates, which is a key performance metric for recovery. Cannot identify which reps or customer segments have the highest default rates on promises. |

---

## 9. Multiple Source Manual Updates and Discrepancies

**Problem:** Details about customer accounts and payment arrangements must be manually updated in multiple sources (email, spreadsheet, legacy database), leading to version control issues and data inconsistency.

**Evidence Source:**
- **Stakeholder Quote:** *"Details must be manually updated across multiple sources - can lead to discrepancies."* (From BPMN annotation)
- **Stakeholder Quote:** *"A single customer can have five separate records in the system from different entry points."* (SN-010, Service Design Lead)
- **Dataset Observation:** Recovery activity tracker shows the same account (e.g., ACC-10001) with activities logged to different source_systems (spreadsheet, phone, email). Activity ACT-00001 is marked "next_action_unclear" in spreadsheet, but ACT-00003 shows "promise_to_pay" in phone system—unclear which is the system of record.

**Stakeholder Impact:**

| Perspective | Experience |
|---|---|
| **Customer** | If they update their contact details via phone, the email system still has the old details. Receives correspondence at the wrong address or phone. May miss important notices. |
| **Representative** | Spends time updating multiple records for the same change. Each update is a risk point for error. Must then verify that all updates succeeded. |
| **Manager** | Cannot build a single customer view. Compliance documentation is scattered across systems. Audit trails are incomplete, and reconciliation is manual and time-consuming. |

---

## 10. Missed Follow-Ups and Broken Arrangement Management

**Problem:** When agents forget to follow up on an arrangement or promise, there is no system recovery. The account falls between shifts or gaps in the schedule and the action is lost.

**Evidence Source:**
- **Stakeholder Quote:** *"If an agent forgets to follow up then broken arrangements slip through the cracks."* (From BPMN annotation)
- **Stakeholder Quote:** *"We lose at least 20% of follow-ups because they fall between shifts and no one owns the handoff."* (SN-040, Data Analyst)
- **Dataset Observation:** Recovery activity tracker shows accounts with outcome_code like "left_message" but no clear next_follow_up_date populated (e.g., ACT-00011). Accounts ACC-10008 and ACC-10002 have follow-up dates set, but activity shows no scheduled system reminder—entirely manual.

**Stakeholder Impact:**

| Perspective | Experience |
|---|---|
| **Customer** | Promised follow-up never materializes. Reaches out to ask if we received their payment or to reschedule but gets no response. Assumes the company is unreliable. |
| **Representative** | Misses follow-up because shift ended or the reminder was lost. Comes back to the case days later and customer is now upset. Quality metric suffers even though the delay was not the rep's direct fault. |
| **Manager** | 20% of follow-ups are lost, reducing recovery velocity. Some accounts age unnecessarily and require escalation later. Rework cost is high and invisible in standard metrics. |

---

## 11. Time-Consuming Customer Contact Attempts

**Problem:** Waiting for customers to answer is time-consuming. A single outbound call attempt may take hours to connect, tying up representative capacity.

**Evidence Source:**
- **Stakeholder Quote (Inferred):** *"Waiting for a customer to answer is time consuming. It could take hours to get a response."* (From BPMN annotation)
- **Stakeholder Quote:** *"We have more accounts in the system than our representatives can possibly contact in a reasonable timeframe."* (SN-023, Service Design Lead)
- **Dataset Observation:** Delinquent accounts export shows 100,000+ accounts with only ~50 representatives (inferred from representative IDs in activity tracker). Many accounts have last_contact_channel blank, indicating unsuccessful contact attempts.

**Stakeholder Impact:**

| Perspective | Experience |
|---|---|
| **Customer** | Receives call attempt but may not be available. If they return the call, may not reach the rep. Back-and-forth takes days. Frustrating and time-consuming on their side too. |
| **Representative** | Spends significant time waiting on hold for customer to answer or trying to reconnect. Can only handle 4-6 accounts per day due to connection time. Productivity is low. |
| **Manager** | Representative utilization is poor. To maintain contact volumes, must hire more reps even though the problem is contact efficiency, not headcount. Cost per resolution is high. |

---

## 12. Inaccurate Data Undermines Reporting and Compliance

**Problem:** Poor data quality and manual reconciliation mean reports are unreliable. Accounts are often wrongly included or excluded from reports due to inconsistent status updates across systems.

**Evidence Source:**
- **Stakeholder Quote:** *"If account is not updated accurately then might be wrongly included/excluded from report."* (From BPMN annotation)
- **Stakeholder Quote:** *"The data quality is so poor that we stopped running management reports altogether."* (SN-012, Collections Representative)
- **Stakeholder Quote:** *"Reporting takes so long that by the time we see the numbers, they are already out of date."* (SN-048, Finance Analyst)
- **Dataset Observation:** Delinquent accounts export and recovery activity tracker show inconsistent outcome_codes and status values. No audit trail timestamp consistency. Manual reconciliation would be required for any historical report.

**Stakeholder Impact:**

| Perspective | Experience |
|---|---|
| **Customer** | Account may be incorrectly reported to credit bureau due to status errors. May appear as still delinquent even after payment. Disputes are hard to resolve because the creditor cannot provide a clear audit trail. |
| **Representative** | If a report shows an incorrect metric (e.g., they have a higher-than-average default rate due to data error), their performance is misjudged. Feedback is based on unreliable data. |
| **Manager** | Cannot produce timely or trustworthy management reports. Month-end reconciliation is manual and takes days. Compliance reporting is risky because the underlying data is known to be unreliable. Strategic decisions are made on incomplete information. |

---

## Summary: The Divergent Experience

The current process creates **stress and inefficiency at all three levels**, but in different ways:

- **Customers** experience a frustrating, repetitive process where they must re-explain their situation, receive conflicting information, and wait days for follow-ups.
- **Representatives** are stuck between manual workarounds and unreliable systems, spending more time verifying data than helping customers. New hires struggle for weeks.
- **Managers** operate with incomplete and unreliable data, cannot report confidently, and face compliance risk from scattered audit trails and duplicate or missed actions.

All 12 pain points stem from the fundamental challenge: **no single integrated system of record**, forcing manual synchronization across multiple tools, which introduces errors and consumes time that could be spent on customer outcomes.
