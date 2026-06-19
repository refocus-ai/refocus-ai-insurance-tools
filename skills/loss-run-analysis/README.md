# Loss Run Trend Analysis Skill

Analyze one or more insurance loss runs for a single company, normalize claim data across carriers and policy periods, identify trends, and convert findings into a practical risk-management and renewal strategy.

Built by [ReFocus AI](https://www.refocusai.com).

---

## What It Does

When you upload loss runs and ask Claude to analyze them, this skill instructs Claude to:

1. Convert and normalize loss runs from PDF, Excel, CSV, images, and narrative documents into a structured claim table
2. Reconcile duplicates, valuation dates, and overlapping reports across carriers and policy periods
3. Analyze trends by line of business — frequency, severity, reserves, and open claims
4. Separate isolated shock losses from recurring operational patterns
5. Produce risk-control recommendations, an agent services proposal, and an underwriter renewal narrative
6. Recommend audience-specific graphics for client, underwriter, and agency use

It supports all major commercial lines: workers' compensation, general liability, commercial auto, property, products/completed operations, cyber, EPLI, professional liability/E&O, umbrella/excess, inland marine/equipment, management liability/D&O, and other specialty lines.

---

## How to Install

1. Open [Claude.ai](https://claude.ai) and sign in.
2. Click **Projects** in the left sidebar and create a new Project, or open an existing one.
3. Click **Project Instructions**.
4. Open [`insurance-loss-run-trend-analysis.skill.md`](./insurance-loss-run-trend-analysis.skill.md) in this folder, copy the full contents, and paste them into the Project Instructions field.
5. Save the instructions.

The skill is now active for every conversation in that Project.

---

## How to Use

Start a conversation inside the Project, upload your loss run documents (PDF, Excel, or CSV work best), and send a message like one of these:

- "Analyze these loss runs and identify trends."
- "Build a risk management proposal from these loss runs."
- "What will underwriters care about at renewal?"
- "Separate shock losses from recurring patterns."
- "Draft an underwriter narrative for this account."

Claude will produce the full 15-section report without additional prompting.

---

## Output Structure

| Section | What It Contains |
|---|---|
| 1. Executive Summary | Overall claim picture, top drivers, renewal priorities, next steps |
| 2. File Processing Summary | How each uploaded file was converted and extraction confidence |
| 3. Data Reviewed | Carriers, policy periods, valuation dates, lines of business |
| 4. Data Quality Notes | Missing data, duplicates, conflicts, low-confidence extractions |
| 5. Consolidated Loss Run Summary | Totals by line, open/closed counts, largest claims |
| 6. Cross-Line Analytics | Trends by year, line, cause, frequency vs. severity |
| 7. Line-of-Business Findings | Per-LOB drivers, trends, recommendations, and graphics |
| 8. Overall Top Loss Drivers | Ranked issues across all lines |
| 9. Cross-Line Themes | Patterns spanning multiple lines of business |
| 10. Root-Cause Hypotheses | Evidence-based cause analysis with confidence levels |
| 11. Risk-Control Recommendation Matrix | Prioritized controls with owners and timelines |
| 12. Recommended Graphics | Audience-specific visual recommendations |
| 13. Agent Services Proposal | Client-facing service plan with 30/60/90-day roadmap |
| 14. Underwriter Narrative | Renewal or marketing narrative for carrier submission |
| 15. Follow-Up Questions | Highest-value data requests to improve the analysis |

---

## Supported File Types

| Format | Handling |
|---|---|
| PDF loss runs | Text/table extraction or OCR for scanned documents |
| Excel / CSV | Structured sheet parsing with column mapping |
| Images / screenshots | OCR or visual extraction with confidence flags |
| Word / email / narrative | Markdown conversion for claim notes and context |

For best results, provide Excel or CSV claim detail when available.

---

## What It Does Not Do

- It does not provide legal, actuarial, medical, engineering, or coverage advice.
- It does not make coverage determinations or rate indications.
- It does not access external systems, carrier portals, or policy databases. It works only from the documents you upload.
- It does not guarantee premium savings or invent missing claim details.
- It will not guess or fill in missing values. If something is not in the document, it says so explicitly.

---

## Requirements

- A [Claude.ai](https://claude.ai) account (free or paid)
- One or more insurance loss run documents for a single account
- PDF or Excel format recommended for best extraction results

---

## License

MIT License. See the [repository LICENSE](../../LICENSE) for details.
