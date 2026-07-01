# BIM Clash Coordination Toolkit

**Owner:** Sean Wang — BIM Manager | **Version:** 2.6 | **Last updated:** 2026-07-01

Stage-gated clash detection and digital coordination toolkit. Built around NZS4219:2009, Revizto Clash Automation, and a T1–T4 coordination framework.

> 📊 See `Clash_Coordination_Workflow.svg` for a visual overview of the full process.

---

## Toolkit Contents

```
BIM_Clash_Coordination_Toolkit/
├── README.md
├── CHANGELOG.md
├── Clash_Coordination_Workflow.svg       ← Visual workflow diagram (open in browser)
├── Platform/
│   └── Clash_Coordination_Platform.html  ← Main dashboard (open in Chrome)
└── Prompts/
    ├── 01_ProjectReport_ClashGate_Analysis.md
    └── 02_ChecklistReview_Import.md
```

---

## Quick Start

**Step 1 — Copy template**
Copy `Projects/_Template/` and rename it to your project code (e.g. `Projects/ABC_Tower/`).

**Step 2 — Open the platform**
Open `Platform/Clash_Coordination_Platform.html` in Chrome. Enter the Project Name and BIM Lead.

**Step 3 — Upload your Clash Matrix**
Click **📂 Upload Project Matrix and Update Gate Rules** → select your company clash matrix. The platform reads the `Rawdata (Do not edit)` sheet and loads all T1–T4 tasks automatically. If the workbook also contains a `<ProjectName>_Gate Mapping` tab, its coordinator-approved (Review = YES) gate items are imported in the **same** upload — one file, both jobs.

**Step 4 — Analyse design report → coordinator review → update gate checklist**

**4a — Run Prompt 01 with your design report**
In a new Claude, Copilot, or ChatGPT session, open the Prompt 01 link below → **Raw** → select all → copy → paste in, then attach your design report (PDF or Word). The AI checks the report against the hub default gate checklist and returns a **Gate Items Review Table as CSV**. Save it as `GateReview.csv` and open in Excel.

> 📋 **[Prompt 01 — Analyse design report → gate items CSV for coordinator review](Prompts/01_ProjectReport_ClashGate_Analysis.md)**

**4b — Services Coordinator review**
Send `GateReview.csv` (or the Excel) to your Services Coordinator. They mark each proposed item YES / NO / N/A, comment on any rejections, sign off, and return the file.

**4c — Add gate items to the matrix, review, upload once**
Paste the reviewed items into a new tab in your G05 matrix named `<ProjectName>_Gate Mapping` (a ready-made blank tab ships in the template matrix). Columns:

> Gate ID · Stage · Disc · Status · Proposed Gate Item · Selection A/B · Matrix Cell · Rec. Priority/Clearance · H (mm) · V (mm) · Clash Pair · Source · Review (Y/N) · Comment

The Services Coordinator sets **Review = Yes/No** on each row. Then click **📂 Upload Project Matrix and Update Gate Rules** once — the platform loads the matrix **and** injects every Review = YES item in a single step. Superseded and supplemented hub defaults are still auto-flagged.

> **Alternative (separate review file):** you can still send a standalone `GateReview.csv` / Excel for review — a hidden legacy import path accepts it. The AI-JSON route (save as `.txt`) remains available for capturing sign-off detail; if the original session was closed, use Prompt 02 (`02_ChecklistReview_Import.md`) in a new session.

**Step 5 — Work through the gates**
For each stage T1 → T4: complete the Pre-Clash Gate Checklist → gate unlocks → **⬇ Export CSV** → run Revizto clash detection → log run in the Run Log tab.

**Step 6 — Transfer to another PC (optional)**
Click **⬆ Export Session** to save everything to JSON. On the other PC click **⬇ Import Session** to restore.

---

## Platform Features

| Feature | What it does |
|---|---|
| T1–T4 Stage tabs | Tasks from your clash matrix split by coordination stage |
| Pre-Clash Gate Checklist | Discipline-filtered checklist — must be ✅ before running each stage in Revizto |
| Revizto Clash Task Output | Task table with search, filter, mark-as-loaded, and CSV export |
| Gate Status | Auto shows 🔒 Locked / ⚠️ Partial / ✅ Open based on checklist progress |
| ✏️ Edit Task | Override clearance code, H/V values, Revizto priority, add a reason note |
| 📐 Rules & Standards | NZS4219:2009 seismic table, clearance codes, gap matrix, project notes |
| 📂 Upload Project Matrix and Update Gate Rules | One upload does both: rebuilds all T1–T4 tasks from the matrix (edits preserved) **and** imports Review = YES rows from the workbook's `<ProjectName>_Gate Mapping` tab — adds gate items, ticks checkboxes, auto-flags superseded/supplemented defaults |

| 🌙 / ☀️ Theme toggle | Light/dark mode — preference saved |
| ⬆ Export Session / ⬇ Import Session | Portable JSON snapshot — restore any project on any PC |
| ⬇ Export CSV | Revizto-ready task export with overrides and notes |
| Run Log | Dated record of each coordination run |

---

## Clearance Codes Reference

| Code | H (mm) | V (mm) | Use case |
|---|---|---|---|
| HC | 0 | 0 | Hard Clash — physical intersection not acceptable |
| C50 | 50 | 50 | Standard services separation, all directions |
| C100V | 50 | 100 | Ceiling face vs services above |
| C150V | 50 | 150 | Project-specific vertical constraint |
| C600V | 50 | 600 | Access panel maintenance zone |
| C1500 | 50 | 1500 | Air terminal vs smoke/heat detector |

Revizto priority: Pipes >50mm Ø → **Major** · Pipes ≤50mm → **Minor** · HC on structural/fire → **Critical**

---

## Seismic Reference — NZS4219:2009

| Condition | H (mm) | V (mm) |
|---|---|---|
| Unrestrained vs Unrestrained | 250 | 50 |
| Unrestrained vs Restrained | 150 | 50 |
| Restrained vs Restrained | 50 | 50 |
| Penetration through structure | 50 | 50 |

Penetration clearances: Ductwork 12mm · Pipework 15mm · Cable Tray 25mm

---

## File Naming Convention

| File type | Convention | Example |
|---|---|---|
| Clash Matrix | `[ProjectCode]_G05_Clash_Matrix_v[X].xlsx` | `ABC_G05_Clash_Matrix_v3.xlsx` |
| Revizto Export | `Revizto_Tasks_[Stage]_[ProjectCode]_[Date].csv` | `Revizto_Tasks_T2_ABC_2026-07-01.csv` |

---

## CHANGELOG

See `CHANGELOG.md` for version history and project deployment record.
