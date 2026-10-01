# Pain Points in the Current Collections Process

This document catalogs the 7 identified pain points from the legacy collections process map, traces the evidence for each, and describes how each pain point affects customers, representatives, and managers.

---

## 1. Multi-Source Update Discrepancies

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

## 2. Manual Record Update and Discrepancies

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

## 3. Broken Arrangements and Re-Contact on Already-Promised Accounts

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
| **Manager** | Lost productivity, account resolution takes longer. Customer satisfaction scores worsen. Increased complaint volume. |

---

## 4. No System-Driven Arrangement Fulfillment Check

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

## 5. Poor Visibility of Promise-to-Pay Fulfillment

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

## 6. Time-Consuming Customer Contact Attempts

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

## 7. Inaccurate Data Undermines Reporting and Compliance

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

All 7 pain points stem from the fundamental challenge: **no single integrated system of record**, forcing manual synchronization across multiple tools, which introduces errors and consumes time that could be spent on customer outcomes.
