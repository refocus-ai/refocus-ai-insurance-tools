# Quote Comparison Skill

Compare two insurance quotes for the same insured side by side. This skill guides Claude through a structured review covering premium differences, coverage gaps, rating inputs, endorsements, bind-readiness issues, and producer follow-up questions — across any line of business.

Built by [ReFocus AI](https://www.refocusai.com).

---

## What It Does

When you upload two insurance quotes and ask Claude to compare them, this skill instructs Claude to:

1. Normalize formatting differences so only real differences are flagged (e.g. "ACV" and "Actual Cash Value" are treated as the same)
2. Review every visible field across both documents — coverage terms, deductibles, rating inputs, discounts, endorsements, fees, and premium components
3. Flag missing, suspicious, or placeholder values that could affect bind readiness or accuracy
4. Produce a structured seven-section output covering the executive summary, a full difference table, premium reconciliation, likely premium drivers, coverage and legal-contract flags, bind-readiness cleanup items, and producer follow-up questions

It works for any line of business: personal auto, homeowners, commercial property, general liability, workers compensation, umbrella, and others.

---

## How to Install

### Cursor & Claude (Desktop)

The Cursor and Claude desktop apps do not have a `/plugin`
command. Install this skill from the UI instead:

1. Open **Settings** and go to **Customize**.
2. Under **Personal plugins**, click **+**.
3. Select **Create plugin and add marketplace**.
4. Click **Add from repository**.
5. Enter this repository URL:

   `https://github.com/refocus-ai/refocus-ai-insurance-tools`

6. Install the **Insurance Quote Comparison** skill from the
   marketplace.

The skill is now available in chat. It loads automatically when you
upload two quote documents, or you can invoke it manually:

- **Cursor:** `/insurance-quote-compare`
- **Claude Desktop:** `/quote-comparison:insurance-quote-compare`

### Claude (claude.ai)

1. Open [Claude.ai](https://claude.ai) and sign in.
2. Click **Projects** in the left sidebar and create a new Project, or open an existing one.
3. Click **Project Instructions**.
4. Open [`SKILL.md`](./skills/insurance-quote-compare/SKILL.md) in this folder, copy the full contents, and paste them into the Project Instructions field.
5. Save the instructions.

The skill is now active for every conversation in that Project.

---

## How to Use

Start a conversation inside the Project, upload both quote documents (PDF works best), and send a message like one of these:

- "Compare these two quotes."
- "Why is the premium different between these two?"
- "Which of these quotes is correct?"
- "Review these for bind readiness."

Claude will produce the full seven-section comparison without any additional prompting.

---

## Output Structure

| Section | What It Contains |
|---|---|
| 1. Executive Summary | Premium difference, coverage equivalency assessment, top drivers, major concerns |
| 2. Difference Table | Every identified difference with field, values from each document, source location, materiality rating, and notes |
| 3. Premium Reconciliation | Line-by-line premium breakdown comparing both documents by component |
| 4. Likely Premium Drivers | Ranked list of differences most likely causing the premium gap |
| 5. Coverage and Legal-Contract Review Flags | Form differences, endorsement changes, exclusions, valuation language, subjectivities |
| 6. Bind-Readiness and Cleanup Items | Missing values, placeholder data, inconsistencies, items needing confirmation |
| 7. Producer Follow-Up Questions | Grouped questions for the insured, the carrier, and internal agency review |

---

## Document Labeling

The skill labels documents as follows by default:

- Document 1: **Intelliagent Quote** (ReFocus AI platform-generated quote)
- Document 2: **Producer Quote** (manually produced carrier website quote)

If you are comparing two quotes that are not from IntelliAgent, you can tell Claude at the start of your message how to label them. For example: "Label Document 1 as the Travelers quote and Document 2 as the Progressive quote."

---

## What It Does Not Do

- It does not provide legal advice. Items requiring legal or compliance review are flagged for your attention.
- It does not access external systems, carrier portals, or policy databases. It works only from the documents you upload.
- It does not make a binding recommendation. The output is a structured review to support the producer's decision, not replace it.
- It will not guess or fill in missing values. If something is not in the document, it says so explicitly.

---

## Requirements

- One of the supported platforms above (Cursor, Claude Desktop, Claude.ai, ChatGPT, Gemini, or OpenClaw)
- Two insurance quote or proposal documents for the same insured
- PDF format is recommended for best results

---

## License

MIT License. See the [repository LICENSE](../../LICENSE) for details.
