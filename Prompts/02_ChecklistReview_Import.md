# Prompt 02 — Gate Checklist Review Import
## BIM Clash Coordination Platform · v1.0

---

## Purpose

The Services Coordinator has completed the gate checklist review Excel and returned it to you. This prompt converts that filled Excel into a JSON file that the platform can import directly via the **📋 Updated Gate Rules** button — no manual checkbox clicking required.

---

## How to Use This Prompt

1. Export the gate checklist Excel from the platform using **📋 Export for Review**
2. Send the Excel to the Services Coordinator for review
3. Coordinator fills in the REVIEW column (YES / NO / N/A) and COMMENT column, then completes the SIGN-OFF block at the bottom of each stage sheet
4. Coordinator returns the completed Excel to you
5. **Upload the completed Excel to this AI session** (attach the file, or paste its content below)
6. Run this prompt — the AI will output a JSON file
7. Save the entire AI response as a `.txt` file
8. In the platform, click **📋 Updated Gate Rules** → upload the `.txt` file
9. The platform automatically updates all checklist items, adds comment badges, and signs off completed stages

---

## Input — Two Accepted Formats

This prompt handles two different input files. **Detect which format you have received and follow the matching path below.**

---

### Format A — Prompt 01 Gate Items Review Table

This file comes from the BIM Manager who ran Prompt 01 against a project report. The coordinator has reviewed the AI's proposed gate items and filled in the REVIEW and COMMENT columns.

The table has these columns:

| # | Stage | Disc | Proposed Gate Item | Status | Replaces Hub Default | H (mm) | V (mm) | Source | REVIEW (YES/NO/N/A) | COMMENT |

- **REVIEW = YES** → Include this gate item in the platform checklist
- **REVIEW = NO** → Exclude this item (coordinator rejected it)
- **REVIEW = N/A** → Not applicable to this project, exclude

**JSON output for Format A: use `gateItems[]`** — only include items where REVIEW = YES.

---

### Format B — Export for Review Excel (hub defaults checklist)

This file comes from the platform's **📋 Export for Review** button. It has sheets named T1, T2, T3, T4, each with:

- Column A: Item number (#) — sequential row numbers matching hub defaults
- Column B: Stage
- Column C: Discipline
- Column D: Checklist Item text
- Column E: Review (YES / NO / N/A) — **filled by coordinator**
- Column F: Comment — **filled by coordinator**
- Sign-off block at the bottom: Reviewer Name, Reviewer Role / Company, Date Reviewed, Overall Comments

**JSON output for Format B: use `checklistReview{}`** — map each item's review state to its row number.

---

## Your Task

### Step 1 — Detect input format

Look at the column headers:
- If the header row contains "Proposed Gate Item" and "Status" → **Format A** (Prompt 01 table)
- If the header row contains "Checklist Item" and has T1/T2/T3/T4 as sheet names with sign-off blocks → **Format B** (Export for Review)

Then follow the matching extraction steps below.

### Step 2A — Format A: Extract approved gate items

For each row where REVIEW = YES:
- Stage, Discipline, Proposed Gate Item text, Status, H (mm), V (mm), Source, Replaces Hub Default

For each row where REVIEW = NO or N/A: skip (exclude from JSON).

### Step 2B — Format B: Extract checklist review responses

For each stage (T1, T2, T3, T4), read every data row and extract:
- Item number (column A)
- Review value (column E): YES, NO, or N/A
- Comment (column F)

Only include items where the coordinator has entered a review value. Skip blank rows.

### Step 2C — Extract sign-off details

For each stage, find the SIGN-OFF block and extract:
- Reviewer Name
- Reviewer Role / Company
- Date Reviewed
- Overall Comments

Only include a sign-off entry if Reviewer Name AND Date Reviewed are both filled in.

### Step 3 — Summarise outstanding items

List all items marked NO with their stage, number, discipline, item text, and coordinator comment. These are the items that need resolution before the gate can be formally closed.

### Step 4 — Output

Produce two parts:

**PART 1 — Review Summary**

A concise table for each stage showing:
- Total items reviewed
- YES count / NO count / N/A count
- Outstanding NO items with coordinator comments
- Sign-off status per stage

**PART 2 — Platform JSON**

Output the JSON block below, preceded by the delimiter line exactly as shown.

---

## Output Format

### PART 1: Review Summary

[Write the summary table here — detected format, stage-by-stage counts (YES/NO/N/A), then a list of all NO items needing action]

---

### PART 2: Platform JSON

Output the JSON block preceded by the delimiter line exactly as shown. Use Format A or Format B schema depending on the input detected.

=== CLASH COORDINATION PLATFORM JSON — PASTE INTO UPDATED GATE RULES ===

**If Format A (Prompt 01 gate items table) — use `gateItems[]`:**

```json
{
  "project": "[project name]",
  "date": "[today YYYY-MM-DD]",
  "gateItems": [
    {
      "stage": "T1",
      "discipline": "STR",
      "item": "Approved gate item text here",
      "clearanceH": 50,
      "clearanceV": 100,
      "clashPair": "STR vs MEC",
      "source": "Section 4.2",
      "status": "NEW",
      "replacesDefault": null
    }
  ],
  "gateSignOffs": {
    "T1": { "name": "Reviewer name", "role": "Role / Company", "date": "YYYY-MM-DD", "comment": "" }
  }
}
```

**If Format B (Export for Review hub defaults Excel) — use `checklistReview{}`:**

```json
{
  "project": "[project name from Excel header]",
  "date": "[today YYYY-MM-DD]",
  "checklistReview": {
    "T1": [
      { "num": 1, "review": "YES", "comment": "" },
      { "num": 2, "review": "NO", "comment": "Not yet resolved — pending structural drawings" },
      { "num": 3, "review": "N/A", "comment": "No acoustic walls on this project" }
    ],
    "T2": [],
    "T3": [],
    "T4": []
  },
  "gateSignOffs": {
    "T1": { "name": "Reviewer name", "role": "Role / Company", "date": "YYYY-MM-DD", "comment": "" }
  }
}
```

---

## Rules

- Only one JSON output per session — use the format matching the detected input
- Format A: only include items where REVIEW = YES in `gateItems[]`; omit NO and N/A items entirely
- Format B: include ALL items where a review value was entered, including NO and N/A
- Use exact values: `"YES"`, `"NO"`, or `"N/A"` (uppercase only)
- `gateSignOffs`: only include stages where Reviewer Name AND Date Reviewed are filled; date must be `YYYY-MM-DD`
- The `=== CLASH COORDINATION PLATFORM JSON` delimiter line must appear exactly as shown

---

## What the Platform Does With This JSON

| Field | Platform action |
|---|---|
| `gateItems[]` (Format A) | Adds approved coordinator-reviewed items to the Pre-Clash Gate Checklist |
| `checklistReview.T1[].review = "YES"` | Checkbox ticked |
| `checklistReview.T1[].review = "N/A"` | Checkbox ticked (not applicable, no action needed) |
| `checklistReview.T1[].review = "NO"` | Checkbox unticked; 💬 badge added with coordinator comment |
| `gateSignOffs.T1` | Auto-signs off that gate stage with coordinator name, role, and date |

---

*Platform: BIM Clash Coordination Platform · Prompt 02 v1.1 · 2026-06-24*
