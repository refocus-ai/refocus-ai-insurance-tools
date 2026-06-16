---
name: insurance-quote-compare
description: >
  Use this skill whenever a user uploads two insurance quotes, proposals, bindable quotes,
  applications, or policies for the same insured and asks why the premiums differ, which is
  correct, which to bind, or how they compare. Triggers on phrases like "compare these quotes,"
  "why is the premium different," "Intelliagent vs producer quote," "which quote is right,"
  or any upload of two insurance documents paired with a comparison or discrepancy question.
  Always use this skill when two insurance documents are present and a comparison is needed,
  even if the user does not explicitly ask for a structured review.
---

# Insurance Quote Comparison Skill

## Purpose

Compare two insurance quotes for the same insured side by side using a line-of-business-agnostic
insurance, underwriting, rating, and legal-contract review framework. The goal is to identify
every visible difference that may affect premium, coverage breadth, underwriting eligibility,
rating accuracy, bind readiness, customer decision-making, and compliance or E&O exposure.

**Always label the documents as follows:**
- Document 1: **Intelliagent Quote** (the ReFocus AI platform-generated quote)
- Document 2: **Producer Quote** (the manually produced carrier website quote)

---

## Core Instructions

### Step 1: Normalize Before Flagging Differences

Before listing any difference, confirm it is substantive and not just a formatting variation.
The following are examples of equivalent representations that should NOT be flagged as differences:

- $500,000 vs. 500000
- ACV vs. Actual Cash Value
- RCV vs. Replacement Cost Value
- Comp vs. Comprehensive
- UM/UIM vs. Uninsured/Underinsured Motorist
- HO-3 vs. Homeowners 3 Special Form
- Wind/Hail vs. Windstorm or Hail

If two values may be equivalent but labeled differently, include them in the table with a note:
"Potentially equivalent label — confirm if carrier treats these the same."

### Step 2: Do Not Guess

Use only the uploaded documents. Never infer, assume, or fill in values from general knowledge.

- If a value is not visible: state **Not found in provided document.**
- If a value is unclear: state **Unclear in provided document.**
- If premium impact cannot be supported from the documents: state **Premium impact cannot be estimated from the provided documents.**
- Do not assume a missing value means zero, waived, excluded, or intentionally omitted unless the document explicitly says so.

### Step 3: Flag Suspicious or Placeholder Values

Flag any value that is:
- Present in one document but absent in the other
- Blank, "Unknown," "TBD," or "N/A"
- Zero where a real value is expected
- A likely placeholder (e.g., 12345678, 999999999, repeated digits, impossible dates, fake VINs)
- Internally inconsistent or not supported by another part of the same document
- Potentially system-defaulted without insured confirmation

---

## What to Compare

Review every visible field. The categories below are a floor, not a ceiling.

**Document and Policy Metadata**
Carrier, program, quote number, policy number, transaction type, quote date, effective date,
expiration date, policy term, state, agency/producer information, billing company, plan or form selected.

**Insured and Risk Information**
Named insured, additional insureds, loss payees, mortgagees, lienholders, mailing address,
risk address, garaging address, contact information, occupancy, use, operations, business description.

**Covered Objects and Exposure Basis**
All applicable exposure details regardless of line of business. Examples include but are not limited to:
vehicles, VINs, drivers, usage, mileage, garaging, license status, violations, claims history;
homes, buildings, roof details, construction type, square footage, year built, protection class, occupancy;
scheduled property, equipment, jewelry, valuables, watercraft, recreational vehicles;
business operations, class codes, payroll, sales, revenue, employee count, subcontractor exposure, territories;
umbrella or excess underlying policies, underlying limits, retained limits, covered exposures.

**Coverage Terms**
All limits (coverage, sublimit, aggregate, per-occurrence, per-person, split, combined single),
valuation method (replacement cost, ACV, agreed value, functional replacement cost), coinsurance,
loss settlement terms, covered causes of loss, optional coverages, extensions, restrictions.

**Deductibles, Retentions, Waiting Periods**
All-peril, per-coverage, wind/hail, hurricane, earthquake, water, theft, glass, comprehensive,
collision, percentage deductibles, self-insured retentions, waiting periods, elimination periods.

**Forms, Endorsements, Exclusions, Conditions**
Policy form differences, endorsements added/removed/changed, exclusions added/removed/changed,
form edition dates, amendatory endorsements, special conditions, protective safeguard requirements,
subjectivities, underwriting conditions, notices affecting coverage or cancellation.

**Rating, Underwriting, and Eligibility Inputs**
Territory, protection class, construction type, roof type/age/condition, occupancy, usage,
mileage, driver characteristics, prior insurance, lapse history, claims history, violations,
credit tier or insurance score tier (if shown), class codes, payroll, sales, revenue, employee count,
carrier-specific rating tiers, underwriting questions, eligibility answers, any defaults or assumed values.

**Discounts, Credits, Surcharges, Taxes, and Fees**
All discounts applied in one document but not the other, credits, debits, surcharges, fees,
taxes, state assessments, policy fees, agency fees, inspection fees, installment fees,
paid-in-full discounts, multi-policy, good driver, new home, loyalty, telematics, or carrier-specific discounts.

**Premium and Payment Details**
Base premium, coverage-level premium, endorsement premium, taxes, fees, total policy premium,
annualized/monthly/installment premium, down payment, installment amounts, number of installments,
payment method, billing plan. Note clearly whether premiums are being compared on the same basis
(annual vs. monthly vs. installment).

---

## Output Format

Produce all seven sections below in order.

---

### Section 1: Executive Summary

A concise summary covering:
- Total premium difference (if both are visible)
- Whether the quotes appear coverage-equivalent
- Top likely premium drivers
- Any major bind-readiness or compliance concerns

---

### Section 2: Difference Table

Present every identified difference using this table:

| Field | Intelliagent Quote Value | Producer Quote Value | Source Location | Materiality | Notes |
|---|---|---|---|---|---|

**Materiality scale:**
- **High** — likely affects premium, coverage, eligibility, bind readiness, or legal/compliance review
- **Medium** — may affect rating, underwriting, or customer decision-making
- **Low** — likely administrative, formatting, or non-rating difference
- **Unknown** — cannot determine materiality from the documents alone

For object-specific fields, label the object clearly in the Field column. Examples:
- Vehicle 1 — 2022 Toyota Camry — Collision Deductible
- Driver 2 — License Status
- Location 1 — Roof Year
- Building 1 — Construction Type
- Scheduled Item 3 — Limit
- Umbrella — Underlying Auto Liability Limit

---

### Section 3: Premium Reconciliation

If documents provide enough detail, reconcile the premium difference by component:

| Premium Component | Intelliagent Quote | Producer Quote | Difference | Notes |
|---|---|---|---|---|

Include: base premium, coverage-level premium, endorsement premium, discounts, surcharges,
taxes, fees, installment charges, total premium.

If documents do not provide enough detail, explain what is missing and why reconciliation is not possible.

---

### Section 4: Likely Premium Drivers

Rank differences most likely causing the premium gap:

| Rank | Difference | Likely Premium Impact | Why It Matters |
|---|---|---|---|

Only estimate dollar impact if the documents explicitly support it. Otherwise use:
High likely impact / Medium likely impact / Low likely impact / Unknown impact.

---

### Section 5: Coverage and Legal-Contract Review Flags

Identify differences that may affect the legal or coverage meaning of the quote or policy. Focus on:
- Different policy forms or endorsement versions
- Added or removed exclusions or conditions
- Different valuation language
- Missing required forms
- State-specific notices
- Protective safeguard requirements
- Subjectivities or underwriting assumptions
- Material application accuracy concerns

**Do not provide legal advice.** Flag items that may require producer, carrier, compliance, or legal review.

---

### Section 6: Bind-Readiness and Cleanup Items

| Issue | Found In | Why It Matters | Recommended Follow-Up |
|---|---|---|---|

Include: missing values, placeholder values, suspicious values, inconsistent values, coverage gaps,
eligibility concerns, values requiring insured confirmation, values requiring carrier or underwriter confirmation.

---

### Section 7: Producer Follow-Up Questions

A concise list of specific questions to resolve before deciding which quote is correct or bindable.
Group by:

**Insured/Customer Questions**
**Carrier/Underwriter Questions**
**Internal Agency Cleanup Questions**
