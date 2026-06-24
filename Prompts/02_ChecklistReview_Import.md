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

## Input

Attach or paste the content of the completed coordinator review Excel. The file will have sheets named T1, T2, T3, T4. Each sheet has:

- Column A: Item number (#)
- Column B: Stage
- Column C: Discipline
- Column D: Checklist Item text
- Column E: Review (YES / NO / N/A) — **filled by coordinator**
- Column F: Comment — **filled by coordinator**
- Sign-off block at the bottom with Reviewer Name, Reviewer Role / Company, Date Reviewed, Overall Comments

---

## Your Task

Read the completed Excel and do the following:

### Step 1 — Extract review responses

For each stage (T1, T2, T3, T4), read every data row and extract:
- Item number (column A)
- Review value (column E): YES, NO, or N/A
- Comment (column F): any text the coordinator added

Only include items where the coordinator has entered a review value (YES / NO / N/A). Skip blank rows.

### Step 2 — Extract sign-off details

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

[Write the summary table here — stage by stage, then a list of all NO items needing action]

---

### PART 2: Platform JSON

=== CLASH COORDINATION PLATFORM JSON — PASTE INTO UPDATED GATE RULES ===

```json
{
  "project": "[project name from the Excel header]",
  "date": "[today's date in YYYY-MM-DD format]",
  "checklistReview": {
    "T1": [
      { "num": 1, "review": "YES", "comment": "" },
      { "num": 2, "review": "NO", "comment": "Comment from coordinator here" },
      { "num": 3, "review": "N/A", "comment": "Not applicable — no acoustic walls on this project" }
    ],
    "T2": [],
    "T3": [],
    "T4": []
  },
  "gateSignOffs": {
    "T1": {
      "name": "Reviewer full name",
      "role": "Reviewer role / company",
      "date": "YYYY-MM-DD",
      "comment": "Overall comments from sign-off block"
    }
  }
}
```

---

## Rules

- Include ALL items where a review value was entered — even if the comment is blank
- Use exact values: `"YES"`, `"NO"`, or `"N/A"` (uppercase, no variations)
- Item numbers (`num`) must match the # column in the Excel exactly (1-indexed)
- Only include stages in `gateSignOffs` where Reviewer Name AND Date Reviewed are filled
- Do not include stages in `gateSignOffs` where the sign-off block is blank
- Date format in `gateSignOffs` must be `YYYY-MM-DD`
- If the coordinator left a stage entirely blank (no reviews), omit that stage from `checklistReview` or include it as an empty array
- The `=== CLASH COORDINATION PLATFORM JSON` delimiter line must appear exactly as shown — the platform uses it to find the JSON block in your response

---

## What the Platform Does With This JSON

| Field | Platform action |
|---|---|
| `checklistReview.T1[].review = "YES"` | Checkbox ticked |
| `checklistReview.T1[].review = "N/A"` | Checkbox ticked (no action needed) |
| `checklistReview.T1[].review = "NO"` | Checkbox left unticked; 💬 badge added with coordinator comment |
| `checklistReview.T1[].comment` | Shown as hover tooltip on the 💬 badge |
| `gateSignOffs.T1` | Auto-signs off that gate stage with coordinator's name, role, and date |

---

*Platform: BIM Clash Coordination Platform · Prompt 02 v1.0 · 2026-06-24*
