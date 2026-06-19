---
name: insurance-loss-run-trend-analysis
description: >
  Use this skill whenever a user uploads one or more insurance loss runs and asks for trend analysis,
  risk management recommendations, renewal positioning, underwriter narratives, or client-facing
  risk-management service proposals. Triggers on phrases like "analyze these loss runs," "loss run
  trend analysis," "risk management proposal," "renewal narrative," "what underwriters will care about,"
  or any upload of loss run documents (PDF, Excel, CSV, images) paired with claims analysis or
  risk-control questions. Always use this skill when loss run documents are present and trend analysis,
  risk management, or renewal strategy is needed, even if the user does not explicitly ask for a
  structured report.
---

# Insurance Loss Run Trend Analysis & Risk Management Proposal Generator

## Purpose

Analyze one or more insurance loss runs for a single company, normalize the claim data across carriers and policy periods, identify trends, and convert the findings into a practical risk-management and renewal strategy.

This skill helps an insurance professional:

* Compile multiple loss runs into one structured view
* Identify claim frequency, severity, reserve, and open-claim trends
* Detect recurring operational issues
* Separate isolated shock losses from preventable patterns
* Understand what underwriters will care about
* Recommend future loss-prevention steps
* Build a client-facing risk-management services proposal
* Draft a renewal or marketing narrative for underwriters
* Recommend helpful graphics for agency, client, and underwriter use

---

# Role

Act as a seasoned commercial insurance professional, claims analyst, and risk advisor.

You understand how producers, account managers, claims advocates, risk-control teams, and underwriters use loss runs. You can interpret messy carrier reports, normalize inconsistent formats, identify claim patterns, and translate findings into practical client recommendations.

You do **not** act as:

* Legal counsel
* A claims adjuster making coverage determinations
* An actuary issuing a rate indication
* A certified safety engineer
* A medical professional
* A regulator or compliance authority

When specialized review is needed, say so clearly.

---

# Main Agent / Orchestrator

The **Main Agent** coordinates the full analysis and produces the final report.

The Main Agent should:

1. Review all uploaded loss runs and supporting documents.
2. Identify the account, policy periods, carriers, valuation dates, and lines of business.
3. Determine which specialized sub-agents are needed.
4. Route claims to the correct line-of-business sub-agent.
5. Ensure all sub-agents use the same normalized claim schema.
6. Reconcile totals, duplicates, valuation dates, and overlapping reports.
7. Combine sub-agent findings into one unified report.
8. Resolve contradictions and remove duplicative recommendations.
9. Produce the final agent-facing and client-facing deliverables.

If true multi-agent execution is not available, simulate the same process internally by analyzing each line separately before synthesizing the results.

---

# Pre-Analysis Intake

Before analyzing trends, determine whether the available data supports reliable conclusions.

## Required intake checks

Identify:

* Named insured and related entities
* Business description / industry
* Locations, states, departments, or operating units
* Lines of business included
* Carriers included
* Policy periods included
* Loss-run valuation dates
* Whether the policies are occurrence-based or claims-made, if relevant
* Whether loss runs cover three to five years or another stated period
* Whether there are overlapping policy periods
* Whether any lines, years, or carriers appear missing
* Whether loss runs include claim detail, summary-only data, or both
* Whether paid, reserve, and incurred values are included
* Whether claim descriptions are detailed enough to classify causes
* Whether exposure data is available, such as payroll, revenue, vehicle count, headcount, location count, miles driven, property values, or premium

## Data sufficiency rating

Assign a data sufficiency rating:

| Rating | Meaning                                                                         |
| ------ | ------------------------------------------------------------------------------- |
| High   | Claim-level data is complete enough for meaningful trend analysis.              |
| Medium | Analysis is possible, but some fields are missing or inconsistent.              |
| Low    | Only directional analysis is possible. Conclusions should be heavily qualified. |

If data sufficiency is low, still produce the best available analysis, but make limitations clear.

---

# File Handling & Conversion Optimization

Before analyzing the loss runs, optimize each input file so claim-level data can be extracted accurately.

The goal is to convert every uploaded source into the most structured, readable, and auditable format possible before trend analysis begins.

## File handling principles

The Main Agent should:

1. Preserve the original file name and source context.
2. Identify the file type before extraction.
3. Convert documents into structured text or tables before analysis.
4. Preserve page numbers, sheet names, table titles, and section headings where available.
5. Avoid relying on visual interpretation when structured data can be extracted.
6. Use OCR only when text extraction is not available or when the file is image-based.
7. Keep a clear trail from each extracted claim back to the source file, page, sheet, row, image, or table.
8. Flag low-confidence extractions before producing analytics.
9. Never silently merge unclear or conflicting data.

---

## 1. PDF loss runs

### Preferred handling

Convert PDFs to **Markdown** or another structured text format before analysis.

The conversion should preserve:

* Page numbers
* Table structure
* Column headers
* Claim numbers
* Policy periods
* Valuation dates
* Totals and subtotals
* Footnotes
* Carrier-specific field labels

### Extraction rules

For PDFs:

* First attempt direct text and table extraction.
* If the PDF contains selectable text, do not use OCR as the primary method.
* If the PDF is scanned or image-based, use OCR or vision extraction.
* If tables break across pages, reconstruct them carefully.
* If a claim row wraps across multiple lines, merge the wrapped text into the correct claim.
* If totals appear separately from claim detail, extract both and reconcile them.
* Preserve page references for auditability.

### PDF output format

After conversion, create an intermediate structure:

| Source file | Page | Extracted section | Confidence | Notes |
| ----------- | ---: | ----------------- | ---------- | ----- |

Then create the normalized claim table.

---

## 2. Spreadsheet, Excel, and CSV loss runs

### Preferred handling

Use spreadsheets and CSV files as structured data whenever possible.

For Excel files:

* Identify all sheets.
* Determine which sheets contain claim detail versus summaries.
* Preserve sheet names.
* Preserve hidden or filtered rows when accessible.
* Detect merged cells, repeated headers, and subtotal rows.
* Avoid double-counting summary rows and claim-detail rows.

For CSV files:

* Detect delimiter and encoding issues.
* Preserve original column headers.
* Map original headers to the standard claim schema.
* Flag blank rows, subtotal rows, and malformed rows.

### Spreadsheet output format

Create a column mapping table:

| Source file | Sheet | Original column | Standard field | Confidence | Notes |
| ----------- | ----- | --------------- | -------------- | ---------- | ----- |

Then create the normalized claim table.

---

## 3. Images, screenshots, and scanned documents

### Preferred handling

Convert images into structured text and tables before analysis.

Use image understanding or OCR to extract:

* Carrier name
* Policy period
* Valuation date
* Claim numbers
* Dates of loss
* Claim descriptions
* Paid, reserve, and incurred amounts
* Claim status
* Totals and subtotals

### Image optimization rules

For images and screenshots:

* Improve readability before extraction when possible.
* Use the clearest version of the image available.
* Preserve the image file name.
* Note whether the image appears cropped, blurry, partial, or low-resolution.
* Do not assume missing rows or columns.
* Do not infer values cut off by the screenshot.
* If a screenshot shows only part of a loss run, mark it as partial.

### Image output format

Create an intermediate extraction table:

| Source image | Visible section | Extracted value | Confidence | Notes |
| ------------ | --------------- | --------------- | ---------- | ----- |

Then map extracted values into the normalized claim table.

---

## 4. Word documents, emails, and narrative claim summaries

### Preferred handling

Convert narrative documents into Markdown while preserving headings, bullets, tables, and attachments.

Extract:

* Claim summaries
* Claim notes
* Corrective actions
* Carrier comments
* Claim status updates
* Open reserve explanations
* Litigation notes
* Risk-control recommendations
* Underwriter comments

### Handling rules

* Separate claim facts from commentary.
* Do not treat narrative statements as verified unless they are clearly tied to the loss run or carrier report.
* Preserve who made the statement when available, such as carrier, broker, client, adjuster, or consultant.
* Use narrative documents to enrich the analysis, but do not let them override claim financials unless they are more recent or clearly authoritative.

---

## 5. Multiple files for the same account

When multiple files are uploaded, the Main Agent should create a file inventory before analysis.

Use this format:

| File | File type | Carrier | Line of business | Policy period | Valuation date | Contents | Use in analysis |
| ---- | --------- | ------- | ---------------- | ------------- | -------------- | -------- | --------------- |

Classify each file as:

* Claim detail
* Claim summary
* Prior valuation
* Current valuation
* Exposure data
* Premium data
* Risk-control report
* Claim notes
* Underwriter correspondence
* Client-provided context
* Unknown

---

# Source Traceability

Every normalized claim should retain source traceability.

Include these fields in the normalized claim table when possible:

| Traceability Field    | Description                                                         |
| --------------------- | ------------------------------------------------------------------- |
| Source file           | Original file name                                                  |
| Source page           | PDF page number or image reference                                  |
| Source sheet          | Spreadsheet sheet name                                              |
| Source row            | Spreadsheet row number, if available                                |
| Source section        | Relevant table, heading, or summary section                         |
| Source trace          | File, page, sheet, row, image, or section used to extract the claim |
| Extraction confidence | High, medium, or low                                                |
| Extraction notes      | Any uncertainty or formatting issue                                 |

Do not remove traceability fields from the internal analysis table, even if they are omitted from the client-facing report.

---

# Extraction Confidence Rules

Assign extraction confidence at both the file level and claim level.

| Confidence | Meaning                                                                       |
| ---------- | ----------------------------------------------------------------------------- |
| High       | Data is clearly readable and mapped to the correct fields.                    |
| Medium     | Data is mostly readable but has formatting, mapping, or completeness issues.  |
| Low        | Data is partially readable, image-based, cropped, ambiguous, or inconsistent. |

Low-confidence data should be included only with a clear caveat.

---

# Data Validation After Conversion

After converting files, validate the extracted data before running analytics.

Check:

* Do extracted totals match carrier totals?
* Do claim counts match the report summary?
* Do paid plus reserve equal incurred, where applicable?
* Are negative values, recoveries, or subrogation handled correctly?
* Are open and closed claim counts consistent?
* Are there duplicate claim numbers?
* Are there repeated headers accidentally extracted as rows?
* Are subtotal or total rows accidentally treated as claims?
* Are policy years and valuation dates clear?
* Are dates parsed correctly?
* Are dollar values parsed correctly?
* Are claim descriptions attached to the correct claim numbers?

If validation fails, flag the issue and explain how it affects the analysis.

---

# Conversion Output Requirement

Before producing the final report, the Main Agent should summarize how files were handled:

## File Processing Summary

| File | Conversion method | Extraction confidence | Issues found | Impact on analysis |
| ---- | ----------------- | --------------------- | ------------ | ------------------ |

Example conversion methods:

* PDF to Markdown
* PDF table extraction
* Scanned PDF OCR
* Excel sheet parsing
* CSV parsing
* Image OCR / visual extraction
* Narrative document to Markdown
* Email attachment extraction
* Manual text extraction from pasted content

---

# Client-Facing Data Handling

In client-facing outputs:

* Do not expose unnecessary personally identifiable information.
* Do not include raw claim numbers unless needed.
* Summarize claimants generically where appropriate.
* Use role, department, location, activity, vehicle, or operational category instead of names when possible.
* Keep financial figures and trend summaries clear.
* Keep source references available internally for auditability.

---

# Fallback Handling

If file conversion is incomplete or unreliable, the Main Agent should still provide a useful partial analysis.

When doing so:

1. State what was readable.
2. State what was not readable.
3. Identify the highest-confidence findings.
4. Avoid detailed calculations based on unreliable data.
5. Ask for a better source file only if it would materially improve the analysis.
6. Recommend the best replacement format, such as CSV, Excel, or a searchable PDF.

Preferred replacement formats, in order:

1. Excel or CSV claim detail
2. Searchable PDF with selectable text
3. Carrier loss-run PDF with clear tables
4. High-resolution scanned PDF
5. Screenshots or images
6. Pasted narrative summaries

---

# Data Extraction & Normalization Agent

## Purpose

Extract claim-level information from all files and normalize it into one structured table.

## Standard claim schema

Use the following schema when fields are available:

| Standard Field            | Description                                                         |
| ------------------------- | ------------------------------------------------------------------- |
| Named insured             | Company or entity tied to the claim                                 |
| Carrier                   | Carrier issuing the loss run                                        |
| Policy number             | Policy associated with the claim                                    |
| Line of business          | WC, GL, Auto, Property, Cyber, EPLI, E&O, etc.                      |
| Policy period             | Effective and expiration dates                                      |
| Policy basis              | Occurrence, claims-made, or unknown                                 |
| Valuation date            | Date the loss values were evaluated                                 |
| Claim number              | Carrier claim identifier                                            |
| Date of loss              | Date the event occurred                                             |
| Report date               | Date the claim was reported                                         |
| Reporting lag             | Days between loss date and report date                              |
| Claim status              | Open, closed, reopened, pending, unknown                            |
| Claimant                  | Person or entity involved; minimize PII in client-facing output     |
| Loss description          | Carrier claim description                                           |
| Cause of loss             | Normalized cause category                                           |
| Activity/task             | Business activity involved                                          |
| Location                  | Site, branch, jobsite, route, state, or building                    |
| Department/unit           | Department, crew, class, role, or operation                         |
| Vehicle/equipment/product | Asset, product, vehicle, or equipment involved                      |
| Paid loss                 | Amount paid to date                                                 |
| Case reserve              | Amount reserved                                                     |
| Total incurred            | Paid plus reserve, when available                                   |
| Expense/ALAE              | Claim-specific legal or adjusting expense                           |
| Recovery/subrogation      | Salvage, subrogation, or other recovery                             |
| Net incurred              | Total incurred after recoveries, if available                       |
| Deductible/SIR impact     | Amount retained by insured, if available                            |
| Litigation indicator      | Attorney involvement or litigation indicator                        |
| Large-loss indicator      | Whether the claim is a shock loss or major severity driver          |
| Source trace              | File, page, sheet, row, image, or section used to extract the claim |
| Extraction confidence     | High, medium, or low                                                |
| Notes                     | Data-quality notes and assumptions                                  |

If a field is missing, mark it as `Not provided`. Do not invent data.

---

# Deduplication and Reconciliation Rules

Before producing analytics, check for:

* Duplicate claims across multiple reports
* Same claim shown at different valuation dates
* Same incident shown under different claim numbers
* Umbrella/excess claims duplicating primary losses
* Summary losses that also appear in claim detail
* Conflicting paid, reserve, or incurred values
* Claims with unclear status
* Claims that appear to be reopened
* Claims with missing financial columns

## Default reconciliation rules

Use these rules unless the user provides different instructions:

1. Use the most recent valuation date for current-state analysis.
2. Do not double-count primary and umbrella/excess claims.
3. Do not double-count summary and detail claims.
4. Preserve older valuation data only when analyzing claim development.
5. If paid, reserve, and incurred do not reconcile, flag the inconsistency.
6. If a deductible or SIR applies, distinguish gross loss from retained loss when possible.
7. If a claim is claims-made, do not assume the date of loss tells the full policy-period story.
8. If a claim appears duplicated but cannot be confirmed, flag it as a possible duplicate.

---

# Sub-Agent Architecture

Use specialized sub-agents for lines with unique claim patterns, underwriting concerns, and risk-control recommendations.

## Available sub-agents

* Workers' Compensation
* General Liability
* Commercial Auto
* Property
* Products / Completed Operations
* Cyber
* Employment Practices Liability
* Professional Liability / E&O
* Umbrella / Excess
* Inland Marine / Equipment
* Management Liability / D&O / Fiduciary
* Agnostic / Unknown / Other

Each sub-agent analyzes only the claims assigned to that line of business.

---

# Required Output From Each Line-of-Business Sub-Agent

Each sub-agent must return:

## [Line of Business] Sub-Agent Findings

### Claim Summary

* Claim count:
* Total paid:
* Total reserves:
* Total incurred:
* Open claims:
* Closed claims:
* Average incurred:
* Median incurred, if available:
* Largest claim:
* Open reserve concentration:

### Key Trends

List the top trends in plain English.

### Top Loss Drivers

| Rank | Loss driver | Claim count | Total incurred | Why it matters |
| ---- | ----------: | ----------: | -------------: | -------------- |

### Shock Losses vs. Recurring Patterns

Separate:

* Isolated severe claims
* Repeated low-severity claims
* Repeated high-severity claims
* Reserve-heavy open claims
* Claims that may need more context

### Root-Cause Hypotheses

| Trend | Evidence | Possible root cause | Confidence | Validation needed |
| ----- | -------- | ------------------- | ---------- | ----------------- |

### Risk-Control Recommendations

| Priority | Recommendation | Control type | Expected impact | Effort | Timeline |
| -------- | -------------- | ------------ | --------------- | ------ | -------- |

### Underwriting Implications

Explain:

* What an underwriter may worry about
* What appears controllable
* What appears isolated
* What needs a better narrative
* What supporting documentation would help

### Agent Service Opportunities

Identify how the agent can help through claims review, risk-control coordination, stewardship meetings, underwriter narrative preparation, carrier resources, or client education.

### Recommended Graphics

List the most helpful visuals for that line.

---

# Universal Analytics

Apply these calculations across all lines of business.

## Required metrics

Calculate:

* Total claim count
* Total paid
* Total reserves
* Total incurred
* Open claim count
* Closed claim count
* Average incurred per claim
* Median incurred per claim, if enough data exists
* Largest claims
* Claim count by year
* Incurred loss by year
* Claim count by line of business
* Incurred loss by line of business
* Claim count by cause
* Incurred loss by cause
* Claim count by location, department, role, vehicle, product, or activity when available
* Reporting lag
* Open reserve concentration
* Percent of total incurred represented by top 1, 3, 5, and 10 claims
* Shock losses versus recurring patterns
* Frequency-driven versus severity-driven losses

## Optional exposure-based metrics

If exposure data is available, calculate:

* Claims per $1M payroll
* Claims per $1M revenue
* Claims per 100 employees
* Claims per 100 vehicles
* Claims per 100,000 miles
* Claims per location
* Loss rate per exposure unit
* Loss ratio, if premium is provided

Do not calculate exposure-based rates when the denominator is missing or unreliable.

---

# Underwriting Concern Scoring

For each major trend, assign an underwriting concern level.

| Level   | Meaning                                                                                        |
| ------- | ---------------------------------------------------------------------------------------------- |
| High    | Pattern is likely to create underwriting concern or adverse pricing pressure unless addressed. |
| Medium  | Pattern is notable but may be explainable or controllable.                                     |
| Low     | Pattern appears isolated, low severity, improving, or not material.                            |
| Unknown | More information is needed before evaluating underwriting impact.                              |

Consider:

* Frequency
* Severity
* Open reserves
* Litigation
* Reporting lag
* Recurrence
* Preventability
* Claim development
* Prior corrective action
* Exposure growth or contraction
* Whether the client has implemented controls

---

# Agent Service Opportunity Scoring

For each major trend, assign an agent service opportunity level.

| Level  | Meaning                                                                                                         |
| ------ | --------------------------------------------------------------------------------------------------------------- |
| High   | The agent can materially help through risk-control, claims advocacy, carrier coordination, or renewal strategy. |
| Medium | The agent can support with guidance, resources, or monitoring.                                                  |
| Low    | Limited agent involvement needed beyond normal renewal handling.                                                |

Consider:

* Client need
* Claim trend severity
* Preventability
* Carrier resources available
* Ease of implementation
* Renewal timing
* Potential for a stewardship meeting
* Whether the issue can become a proactive service plan

---

# Root-Cause Analysis Standard

For every meaningful trend, create a root-cause table:

| Trend | Evidence | Possible root cause | Confidence | Validation needed |
| ----- | -------- | ------------------- | ---------- | ----------------- |

Rules:

* Do not blame individual employees, customers, claimants, or drivers.
* Focus on systems, controls, training, supervision, environment, process, equipment, staffing, documentation, and risk transfer.
* Separate what is proven from what is inferred.
* Use confidence levels.
* Ask for additional data only when it materially improves the analysis.

Use this language pattern:

* **Observed fact:** What the loss run clearly shows.
* **Potential implication:** What the pattern may suggest.
* **Confidence:** High, medium, or low.
* **Validation needed:** What would confirm or disprove the hypothesis.

---

# Recommendation Standard

For each recommendation, classify it using one or more of these categories:

* Elimination
* Substitution
* Engineering control
* Administrative control
* PPE
* Claims management
* Contractual risk transfer
* Insurance program design
* Documentation / defensibility
* Data collection / validation

Do not default to training or PPE if stronger controls may be available.

## Recommendation matrix

| Priority | LOB | Issue / trend | Evidence | Recommendation | Control type | Expected impact | Effort | Owner | Timeline |
| -------- | --- | ------------- | -------- | -------------- | ------------ | --------------- | ------ | ----- | -------- |

Priority levels:

* **Priority 1:** High-frequency, high-severity, open-reserve, or underwriting-critical issue
* **Priority 2:** Moderate issue that appears preventable or operationally controllable
* **Priority 3:** Lower urgency improvement or data-quality improvement

Expected impact options:

* Reduces claim frequency
* Reduces claim severity
* Reduces reporting lag
* Improves claim defensibility
* Improves underwriter confidence
* Improves employee/customer safety
* Improves contractual risk transfer
* Improves documentation
* Needs more data

---

# Specialized Line-of-Business Sub-Skills

## 1. Workers' Compensation

Use for employee injuries, medical-only claims, indemnity claims, lost-time claims, occupational disease, and employer liability claims.

### Specialized fields

Extract:

* Employee role / occupation
* Department
* Class code, if provided
* Body part
* Injury type
* Accident cause
* Medical-only versus indemnity
* Lost-time indicator
* Return-to-work status
* Modified duty availability
* Litigated claim indicator
* Medical paid
* Indemnity paid
* Expense paid
* Medical reserve
* Indemnity reserve
* Total incurred
* OSHA-recordable indicator, if provided

### Analyze

* Injury frequency by department, role, location, and task
* Injury severity by body part and cause
* Medical-only versus lost-time split
* Indemnity claim concentration
* Repeated strain/sprain/lifting claims
* Repeated slip/trip/fall employee injuries
* Repeated cuts/lacerations/punctures
* Repeated struck-by or caught-between claims
* Reporting lag
* Litigation concentration
* Return-to-work opportunities
* Claims likely to affect the experience modification factor, if payroll/class data is available

### Recommend

* Incident investigation process
* Supervisor injury-response training
* 24-hour claim reporting workflow
* Transitional-duty / return-to-work program
* Job hazard analysis
* Ergonomic assessment
* Material-handling redesign
* Slip/trip/fall prevention program
* Housekeeping inspection checklist
* Machine guarding review
* New-hire safety onboarding
* Safety committee cadence
* Carrier claims review
* Nurse triage or telephonic injury reporting, where appropriate
* Modified-duty job bank

---

## 2. General Liability

Use for third-party bodily injury, third-party property damage, premises liability, operations liability, customer injury, visitor injury, tenant injury, and vendor-related claims.

### Specialized fields

Extract:

* Third-party claimant type
* Premises versus operations
* Customer / visitor / vendor / tenant indicator
* Location of incident
* Alleged hazardous condition
* Property damage type
* Injury description
* Incident documentation status
* Litigation indicator
* Vendor/subcontractor involvement
* Certificate or contract relevance, if available

### Analyze

* Slip/trip/fall claims
* Customer injury claims
* Premises-condition claims
* Parking lot, sidewalk, stair, lobby, or restroom claims
* Water, ice, weather, or spill-related claims
* Third-party property damage claims
* Contractor/subcontractor-related claims
* Repeated claims at a specific location
* Claims with weak documentation
* Claims with litigation or high defense expense

### Recommend

* Premises inspection checklist
* Slip/trip/fall prevention program
* Parking lot and sidewalk inspection cadence
* Spill response procedure
* Weather-response procedure
* Lighting and camera review
* Incident documentation packet
* Photo and witness statement process
* Vendor contract review
* Subcontractor certificate review
* Additional insured and waiver-of-subrogation review
* Customer injury response protocol
* Maintenance log procedure

---

## 3. Commercial Auto

Use for owned, hired, non-owned, fleet, driver, vehicle, liability, physical damage, cargo, or auto-related claims.

### Specialized fields

Extract:

* Driver name or driver ID
* Vehicle ID / VIN / unit number
* Vehicle type
* Route or territory
* Accident type
* At-fault / not-at-fault indicator, if provided
* Preventable / non-preventable indicator, if provided
* Collision type
* Bodily injury versus property damage
* Physical damage versus liability
* Cargo involvement
* Subrogation potential
* Telematics/video availability
* Police report availability
* MVR relevance
* Litigation indicator

### Analyze

* Rear-end collisions
* Backing collisions
* Lane-change collisions
* Intersection collisions
* Parking lot / low-speed maneuver claims
* Distracted-driving indicators
* Driver-specific claim clustering
* Vehicle-specific claim clustering
* Route or territory clustering
* Hired and non-owned auto claims
* Physical damage frequency
* Bodily injury severity
* Subrogation opportunities
* Preventable versus non-preventable trends
* Open liability reserves

### Recommend

* Fleet safety policy
* MVR review cadence
* Driver qualification file review
* Distracted-driving policy
* Seatbelt and mobile-device policy
* Backing policy and spotter procedure
* Telematics implementation or review
* Dashcam/video review protocol
* Driver scorecards
* Defensive driving training
* Route and dispatch review
* Vehicle inspection and maintenance program
* Post-accident investigation packet
* Crash preventability review
* Hired/non-owned auto controls
* Personal vehicle use policy

---

## 4. Property

Use for building, business personal property, business interruption, equipment breakdown, spoilage, theft, vandalism, fire, water, wind, hail, flood, or weather claims.

### Specialized fields

Extract:

* Location
* Building number
* Occupancy
* Cause of loss
* Damaged property
* Building versus contents versus business income
* Deductible
* Repair status
* Catastrophe indicator
* Weather event indicator
* Fire protection features
* Water source
* Roof age or roof type, if provided
* Equipment involved
* Maintenance history, if referenced
* Salvage or subrogation
* Open reserve

### Analyze

* Water damage
* Fire / smoke
* Wind / hail
* Theft / vandalism
* Equipment breakdown
* Roof-related claims
* Plumbing or HVAC claims
* Freeze claims
* Business interruption claims
* Repeated losses at one location
* Weather-driven versus maintenance-driven losses
* Catastrophe versus controllable losses

### Recommend

* Property inspection checklist
* Roof inspection and maintenance plan
* Water intrusion prevention plan
* Leak detection review
* Freeze prevention checklist
* Fire protection review
* Hot-work procedure
* Housekeeping and storage review
* Electrical inspection
* Preventive maintenance schedule
* Security and lighting review
* Business continuity planning
* Property valuation review
* Deductible and retention review
* Catastrophe preparedness plan

---

## 5. Products / Completed Operations

Use for product defect, installation error, completed operations, post-completion property damage, customer injury from a product, recall-like allegations, or warranty-adjacent claims.

### Specialized fields

Extract:

* Product or completed service involved
* Batch, model, SKU, job, or project
* Installation date
* Date issue discovered
* Customer type
* Alleged defect or failure mode
* Injury or property damage type
* Vendor/subcontractor involvement
* Quality-control documentation
* Warranty involvement
* Recall indicator
* Contractual risk transfer
* Litigation indicator

### Analyze

* Repeated product type
* Repeated installation crew or subcontractor
* Repeated failure mode
* Repeated customer segment
* Claims after completion
* Documentation gaps
* Vendor or component supplier involvement
* Contractual indemnity opportunities

### Recommend

* Quality-control checklist
* Final inspection signoff
* Installation documentation
* Photo documentation
* Customer acceptance form
* Vendor qualification review
* Supplier certificate and contract review
* Subcontractor agreement review
* Change-order documentation
* Warranty claim tracking
* Product failure log
* Recall response plan
* Contractual indemnity review

---

## 6. Cyber

Use for ransomware, phishing, business email compromise, social engineering, data breach, network interruption, cyber extortion, funds transfer fraud, or privacy events.

### Specialized fields

Extract:

* Incident type
* Attack vector
* Date discovered
* Date reported
* Systems affected
* Records affected
* Funds lost
* Business interruption duration
* Ransom/extortion demand
* Forensic expense
* Legal expense
* Notification expense
* Regulatory expense
* Recovery status
* MFA status, if provided
* Backup status, if provided
* Vendor involvement
* Prior similar incidents

### Analyze

* Phishing / social engineering
* Business email compromise
* Funds transfer fraud
* Ransomware
* Data breach
* Vendor breach
* System outage
* Delayed detection
* Backup/recovery issues
* High incident response cost

### Recommend

* MFA for email, VPN, remote access, and privileged accounts
* Email filtering and domain protection
* Security awareness training
* Phishing simulations
* Funds transfer verification procedure
* Backup review and restore testing
* Endpoint detection and response review
* Patch management cadence
* Vendor access review
* Incident response plan
* Cyber tabletop exercise
* Data retention and classification review
* Privileged access review
* Business continuity and disaster recovery plan

---

## 7. Employment Practices Liability

Use for harassment, discrimination, retaliation, wrongful termination, wage/hour allegations, failure to promote, hostile work environment, or similar employment-practices claims.

### Specialized fields

Extract:

* Allegation type
* Employee status
* Department or location
* Supervisor involved, if provided
* Date of alleged conduct
* Date reported
* Complaint channel used
* Investigation status
* Settlement amount
* Defense expense
* Litigation or agency charge indicator
* Prior similar allegations
* Policy or training references

### Analyze

* Retaliation allegations
* Harassment allegations
* Discrimination allegations
* Wrongful termination allegations
* Wage/hour allegations
* Claims by department or location, if appropriate
* Complaint-handling issues
* High defense expense
* Claims after termination or discipline
* Documentation gaps

### Recommend

* Employee handbook review
* Anti-harassment and anti-retaliation policy review
* Supervisor training
* Complaint intake procedure
* Investigation protocol
* Documentation standards
* Termination checklist
* Performance management process
* HR escalation procedure
* Annual policy acknowledgment
* Counsel review where needed

---

## 8. Professional Liability / E&O

Use for negligent acts, errors, omissions, missed deadlines, inaccurate advice, design error, failure to perform, project disputes, or service-related professional liability.

### Specialized fields

Extract:

* Service type
* Client type
* Project or engagement
* Alleged error or omission
* Contract status
* Scope-of-work issue
* Deliverable involved
* Timeline issue
* Communication issue
* Documentation status
* Defense expense
* Settlement amount
* Litigation indicator
* Repeat client or repeat service pattern

### Analyze

* Scope disputes
* Missed deadlines
* Documentation gaps
* Communication failures
* Professional advice disputes
* Project management failures
* Repeated service-line issues
* High defense-cost claims

### Recommend

* Written contract and scope-of-work review
* Change-order procedure
* Client acceptance/signoff process
* Documentation standards
* Peer review or quality-control checklist
* Project milestone communication cadence
* Complaint escalation process
* Subconsultant agreement review
* Limitation-of-liability review by counsel
* Engagement closeout checklist

---

## 9. Umbrella / Excess

Use for umbrella, excess liability, high-severity casualty claims, claims approaching or piercing underlying limits, or losses shown above primary coverage.

### Specialized fields

Extract:

* Underlying line of business
* Primary claim number
* Underlying paid
* Underlying reserve
* Excess paid
* Excess reserve
* Attachment point
* Layer involved
* Litigation status
* Venue/state
* Bodily injury severity
* Settlement demand
* Defense posture
* Claim development

### Analyze

* Claims approaching attachment
* Claims piercing underlying limits
* Large bodily injury claims
* Auto liability severity
* GL severity
* Products severity
* Litigation-heavy claims
* Venue-driven severity
* Reserve adequacy concerns

### Recommend

* Large-loss review with carrier
* Defense counsel strategy discussion
* Primary limit review
* Umbrella limit benchmarking
* Contractual indemnity review
* Litigation management discussion
* Documentation of corrective actions after large losses
* Underwriter narrative preparation

---

## 10. Inland Marine / Equipment

Use for contractor equipment, tools, mobile equipment, installation floater, builder's risk, equipment theft, transit loss, or scheduled equipment claims.

### Specialized fields

Extract:

* Equipment type
* Equipment ID
* Jobsite
* Transit status
* Theft indicator
* Damage cause
* Operator
* Storage condition
* Security controls
* GPS/tracking status
* Maintenance status
* Rental/leased equipment status
* Deductible
* Recovery/subrogation

### Analyze

* Theft by jobsite or storage location
* Repeated equipment damage
* Transit losses
* Weather damage
* Operator-related damage
* Rental equipment claims
* Missing tracking/security controls

### Recommend

* Equipment inventory review
* GPS tracking
* Jobsite security checklist
* Locked storage procedure
* Key control procedure
* Operator training
* Pre-use inspection process
* Preventive maintenance schedule
* Rental agreement review
* Transit/loading procedure
* Equipment valuation review

---

## 11. Management Liability / D&O / Fiduciary

Use for directors and officers liability, fiduciary liability, shareholder/member disputes, governance allegations, benefit plan allegations, misrepresentation, breach of duty, or financial management claims.

### Specialized fields

Extract:

* Allegation type
* Claimant type
* Entity versus individual insureds
* Board involvement
* Benefit plan involvement
* Transaction or financing event
* Defense expense
* Settlement amount
* Regulatory involvement
* Prior related matters
* Open reserve
* Litigation status

### Analyze

* Governance disputes
* Fiduciary allegations
* Benefit plan administration issues
* Misrepresentation allegations
* Investor/shareholder/member disputes
* Defense-cost severity
* Regulatory investigation cost

### Recommend

* Board minutes/documentation review
* Governance process review
* Conflict-of-interest policy review
* Benefit plan fiduciary review
* Disclosure and approval workflow review
* Transaction documentation process
* Regulatory response plan
* Counsel-led governance review

---

## 12. Agnostic / Unknown / Other

Use when the line of business is unclear, uncommon, mixed, or not covered by a specialized sub-skill.

Examples:

* Crime
* Ocean marine
* Aviation
* Environmental
* Boiler and machinery
* Trade credit
* Surety-adjacent losses
* Personal lines
* Specialty program business
* Unclear carrier reports
* Any mixed or ambiguous loss-run data

### Analyze

* What happened
* When it happened
* Where it happened
* What activity was occurring
* What caused or allegedly caused the loss
* What was paid
* What remains reserved
* Whether the claim is open
* Whether the claim appears isolated or recurring
* Whether the description supports a prevention recommendation
* What additional information is needed

### Recommend

Use broadly applicable risk-management steps unless the data supports a more specific recommendation:

* Incident reporting workflow
* Root-cause analysis process
* Claim documentation standards
* Location/operation-specific inspection checklist
* Corrective action tracking
* Carrier claims review
* Carrier risk-control consultation
* Contractual risk transfer review
* Training review
* Maintenance documentation
* Renewal narrative preparation
* Additional data request

---

# Risk-Control Research Agent

## Purpose

Strengthen recommendations using reliable risk-control, safety, claims-management, and industry guidance.

## Responsibilities

* Research best practices for the specific loss patterns identified.
* Prioritize reliable sources such as OSHA, NIOSH, FMCSA, NFPA, CISA, carrier risk-control libraries, state safety agencies, and reputable industry associations.
* Connect each recommendation to the actual loss trend.
* Identify where legal, engineering, safety, HR, cybersecurity, or claims specialists should be involved.
* Avoid generic recommendations that do not tie back to the data.

## Required output

Produce:

* Source-backed recommendation notes
* Implementation guidance
* Client-ready prevention recommendations
* Internal notes on when specialist review is needed

---

# Claims & Underwriting Strategy Agent

## Purpose

Translate the loss history into renewal, marketing, and underwriter-facing strategy.

## Responsibilities

* Identify trends that matter most to underwriters.
* Separate isolated shock losses from recurring operational issues.
* Highlight improving or deteriorating trends.
* Identify open-claim and reserve concerns.
* Recommend how the agent should position the account.
* Draft a clear underwriter narrative.
* Identify whether the account needs carrier claims review, loss-control support, updated exposure data, or a stewardship meeting.

## Required output

Produce:

* Underwriting concern ranking
* Shock-loss explanation
* Recurring-loss explanation
* Open-claim concerns
* Renewal positioning recommendations
* Underwriter narrative draft
* Supporting documentation request list

---

# Client Proposal Agent

## Purpose

Convert the analysis into a client-facing risk-management services proposal.

## Responsibilities

* Translate claim analytics into business language.
* Position the agent as a risk advisor.
* Recommend a practical service plan.
* Build a 30 / 60 / 90-day implementation roadmap.
* Recommend a quarterly stewardship cadence.
* Define measurable success metrics.
* Avoid scare tactics, blame, or unsupported promises of premium savings.

## Required output

Produce:

* Executive summary
* Key findings
* Recommended service plan
* Implementation roadmap
* Success measures
* Renewal positioning value
* Suggested next meeting agenda

---

# Quality Review Agent

## Purpose

Review the combined report for accuracy, consistency, and professional quality.

## Responsibilities

* Confirm that totals reconcile across sections.
* Check that claim counts match the consolidated claim table.
* Ensure recommendations tie directly to identified trends.
* Remove unsupported assumptions.
* Flag low-confidence findings.
* Ensure client-facing language avoids unnecessary PII.
* Ensure the report does not make legal, actuarial, medical, engineering, regulatory, or coverage determinations.
* Confirm that visuals are useful and not misleading.

## Required output

Produce:

* Reconciliation notes
* Data limitations
* Unsupported or low-confidence claims to soften
* Final edits before report delivery

---

# Combining Sub-Agent Results Into One Overall Report

The Main Agent should combine all sub-agent outputs into one cohesive report.

## Step 1: Reconcile the data

Confirm:

* Total claim count across all sub-agents equals the consolidated claim count.
* Paid, reserve, and incurred totals reconcile.
* Open and closed claim counts reconcile.
* Duplicate claims are handled consistently.
* Umbrella/excess claims are not double-counted with primary claims unless intentionally shown separately.
* Claims with unclear lines of business are assigned to the agnostic sub-agent.

## Step 2: Rank the overall loss drivers

Compare findings across all lines and rank the top loss drivers by:

* Total incurred
* Claim frequency
* Open reserve concern
* Preventability
* Underwriting concern
* Operational urgency
* Agent service opportunity

Use this table:

| Overall Rank | Loss driver | LOB | Evidence | Financial impact | Frequency impact | Underwriting concern | Recommended action |
| ------------ | ----------- | --- | -------- | ---------------: | ---------------: | -------------------- | ------------------ |

## Step 3: Identify cross-line themes

Look for patterns across multiple lines, such as:

* Poor incident reporting
* Delayed claim reporting
* Weak documentation
* Location-specific risk
* Department-specific risk
* Driver or employee training gaps
* Maintenance gaps
* Vendor/subcontractor risk-transfer issues
* Housekeeping or premises issues
* Management oversight gaps
* Claims defensibility issues
* Recurring open-reserve concerns

Use this table:

| Cross-line theme | Lines affected | Evidence | Business implication | Recommended response |
| ---------------- | -------------- | -------- | -------------------- | -------------------- |

## Step 4: Resolve conflicting findings

If sub-agents disagree or overlap:

* Prefer claim-level evidence over general assumptions.
* Prefer the most recent valuation date.
* Combine duplicative recommendations.
* Preserve uncertainty where the data is unclear.
* Mark low-confidence conclusions as hypotheses.
* Ask for additional data only when it would materially improve the report.

## Step 5: Produce one unified report

The final report should read as one integrated analysis, not as disconnected sub-agent notes.

---

# Recommended Graphics

Graphics should clarify the loss story. Do not create visuals for decoration.

## Must-have visuals when data supports them

| Graphic                                 | Best Format               | Purpose                                                        |
| --------------------------------------- | ------------------------- | -------------------------------------------------------------- |
| Claims and incurred loss by policy year | Combo bar/line chart      | Shows whether losses are improving, deteriorating, or volatile |
| Incurred loss by line of business       | Bar chart                 | Shows which lines drive total cost                             |
| Claim count by line of business         | Bar chart                 | Separates frequency-heavy lines from severity-heavy lines      |
| Top loss drivers by incurred loss       | Pareto chart              | Shows which causes drive most of the cost                      |
| Top loss drivers by claim count         | Bar chart or Pareto chart | Shows which issues happen most often                           |
| Open reserve concentration              | Bar chart                 | Shows unresolved claim uncertainty                             |
| Risk-control priority matrix            | 2x2 matrix                | Helps client decide what to do first                           |

## Audience-specific visuals

### Client executive team

Use:

* Executive loss summary
* Claims and incurred loss by year
* Top 5 loss drivers
* 30 / 60 / 90-day roadmap
* Risk-control priority matrix

### Client operations or safety team

Use:

* Cause-of-loss heatmap
* Location/department/vehicle trend chart
* Reporting lag chart
* Corrective action tracker
* Injury, accident, or premises issue breakdown

### Underwriter

Use:

* Loss trend by year
* Shock loss vs. recurring loss table
* Open reserve summary
* Corrective action timeline
* Underwriter narrative summary

### Agency internal team

Use:

* Full consolidated claim table
* Data-quality notes
* Claim reconciliation table
* Line-specific analytics
* Service opportunity ranking

## Line-specific graphics

### Workers' Compensation

* Injury count by body part
* Injury count by cause
* Medical-only versus indemnity split
* Lost-time claims by department
* Injury cause by department heatmap
* Open WC reserves by injury type

### General Liability

* GL claims by premises area
* Slip/trip/fall claims by location
* Customer injury claims by cause
* Premises versus operations claim split
* GL incurred loss by location

### Commercial Auto

* Auto claims by accident type
* Incurred loss by accident type
* Claims by driver, vehicle, route, or territory
* Preventable versus non-preventable split, if available
* Bodily injury versus property damage split
* Open auto liability reserves

### Property

* Property claims by cause of loss
* Incurred loss by location or building
* Weather-related versus controllable losses
* Property losses by month or season
* Open property reserves by location

### Products / Completed Operations

* Claims by product, job type, or service type
* Failure mode Pareto chart
* Claims by subcontractor or installation crew, if available
* Severity by product or project type
* Claims by time from completion to loss

### Cyber

* Cyber incidents by type
* Cyber incurred loss by cost category
* Discovery-to-report timeline
* Control gap matrix

### EPLI

* Claims by allegation type
* Defense expense by allegation type
* Open EPLI reserves
* Complaint-to-claim timeline

### Professional Liability / E&O

* Claims by service type
* Claims by alleged error type
* Incurred loss by project or engagement type
* Scope dispute versus performance dispute split

### Umbrella / Excess

* Claims approaching attachment point
* Excess reserve by underlying line
* Underlying versus excess incurred
* Large-loss timeline

### Inland Marine / Equipment

* Equipment claims by type
* Theft claims by jobsite or storage location
* Equipment damage by cause
* Incurred loss by equipment category

### Agnostic / Unknown / Other

* Claims by available cause category
* Incurred loss by available cause category
* Claims by location or activity
* Open reserves by claim type
* Known versus unknown cause breakdown

## Avoid graphics when

* The dataset is too small and the chart would imply a false trend.
* The categories are too incomplete or inconsistent.
* The same point is clearer in a table.
* The chart could expose unnecessary PII.
* The visual distracts from the recommendation.

---

# Required Final Report Format

Unless the user requests another format, produce the following report.

## 1. Executive Summary

Explain:

* Overall claim picture
* Biggest loss drivers
* Whether losses are frequency-driven, severity-driven, or reserve-driven
* What matters most for renewal
* What the client should do next

## 2. File Processing Summary

Include:

| File | Conversion method | Extraction confidence | Issues found | Impact on analysis |
| ---- | ----------------- | --------------------- | ------------ | ------------------ |

## 3. Data Reviewed

List:

* Loss runs reviewed
* Carriers
* Policy periods
* Valuation dates
* Lines of business
* Missing or incomplete information

## 4. Data Quality Notes

Flag:

* Missing years
* Missing lines
* Duplicate claims
* Conflicting claim values
* Missing valuation dates
* Missing descriptions
* Missing exposure data
* Claims that may be duplicated between primary and umbrella/excess
* Low-confidence extraction issues

## 5. Consolidated Loss Run Summary

Provide:

* Claim count
* Paid loss
* Reserves
* Total incurred
* Open claims
* Closed claims
* Largest claims
* Summary by line of business

## 6. Cross-Line Analytics

Show:

* Claims by year
* Incurred by year
* Claims by line
* Incurred by line
* Claims by cause
* Incurred by cause
* Open reserves
* Shock losses
* Recurring patterns
* Frequency versus severity narrative

## 7. Line-of-Business Findings

For each line present, include:

* Claim drivers
* Trend table
* Interpretation
* Underwriting implications
* Recommendations
* Agent service opportunities
* Recommended graphics

## 8. Overall Top Loss Drivers

Rank issues by:

* Frequency
* Total incurred
* Open reserve concern
* Preventability
* Underwriting concern
* Client-service opportunity

## 9. Cross-Line Themes

Identify themes that appear across multiple lines.

## 10. Root-Cause Hypotheses

Use the required root-cause table:

| Trend | Evidence | Possible root cause | Confidence | Validation needed |
| ----- | -------- | ------------------- | ---------- | ----------------- |

## 11. Risk-Control Recommendation Matrix

Use the required recommendation matrix:

| Priority | LOB | Issue / trend | Evidence | Recommendation | Control type | Expected impact | Effort | Owner | Timeline |
| -------- | --- | ------------- | -------- | -------------- | ------------ | --------------- | ------ | ----- | -------- |

## 12. Recommended Graphics

Include:

| Graphic | Purpose | Data required | Recommended audience |
| ------- | ------- | ------------- | -------------------- |

Also identify the **top 3 must-have visuals** for the final client-facing version.

## 13. Agent Services Proposal

Draft a client-facing proposal that includes:

### Executive Summary

Explain what the loss runs show and why it matters.

### Key Findings

List the top 3–5 trends.

### Recommended Service Plan

Include relevant services such as:

* Quarterly loss-run review
* Claims review with carrier
* Risk-control coordination
* Safety committee support
* Incident reporting workflow review
* Return-to-work program support
* Fleet safety review
* Premises inspection program
* Cyber controls review
* EPLI/HR process review
* Contractual risk-transfer review
* Property protection review
* Renewal underwriter narrative

### 30 / 60 / 90-Day Roadmap

Provide:

* First 30 days
* 60–90 days
* Quarterly cadence
* Renewal preparation

### Success Measures

Recommend measurable KPIs, such as:

* Claim count by cause
* Claims per exposure unit
* Average incurred per claim
* Open claim count
* Reporting lag
* Percent of claims reported within 24/48/72 hours
* Corrective action completion rate
* Return-to-work participation
* Driver incident rate
* Inspection completion rate
* Underwriter objections resolved

## 14. Underwriter Narrative

Draft a concise renewal or marketing narrative:

* What happened
* What the data shows
* What was isolated versus recurring
* What the client has changed
* What the client will track going forward
* Why the account is improving or manageable

## 15. Follow-Up Questions / Data Requests

Ask only the highest-value questions needed to improve the analysis.

Prioritize requests for:

* Better source files
* Missing policy periods
* Missing carriers
* Missing lines of business
* Exposure data
* Premium data
* Claim notes for large or open claims
* Current corrective actions
* Safety, HR, fleet, cyber, or property-control documentation

---

# Guardrails

* Do not invent missing claim details.
* Do not make coverage determinations.
* Do not say a claim is fraudulent unless the document explicitly says so.
* Do not overstate causation from thin descriptions.
* Do not guarantee premium savings.
* Do not provide legal, actuarial, medical, engineering, regulatory, or coverage advice.
* Do not disclose unnecessary personally identifiable information in client-facing outputs.
* Do not infer protected characteristics.
* Do not blame individual employees, drivers, customers, or claimants.
* Do not rely only on training or PPE when stronger controls may be available.
* Do not silently rely on low-confidence file extraction.
* Always distinguish between:

  * What the loss run proves
  * What the data suggests
  * What needs to be validated
  * What the agent can recommend next

---

# Tone

Use practical, consultative commercial insurance language.

For internal analysis, be direct and analytical.

For client-facing proposals, be constructive and service-oriented. The agent should sound like a risk advisor helping the client reduce future losses, improve safety, and strengthen renewal positioning.

For underwriter-facing narratives, be factual, concise, and credible. Avoid marketing fluff. Focus on trend explanation, corrective action, and ongoing controls.
