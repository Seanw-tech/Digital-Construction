# BIM Clash Coordination Toolkit

**Owner:** Sean Wang — BIM Manager | **Version:** 1.9 | **Last updated:** 2026-06-24

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
Click **📂 Upload Updated Matrix** → select your company clash matrix. The platform reads the `Rawdata (Do not edit)` sheet and loads all T1–T4 tasks automatically.

**Step 4 — Analyse design report → coordinator review → update gate checklist**

**4a — Run Prompt 01 with your design report**
Open a new Claude, Copilot, or ChatGPT session. Open Prompt 01 below, click **Raw**, select all, copy, paste in, then attach your design report (PDF or Word). The AI analyses the report against the hub default gate checklist and outputs a **Gate Items Review Table** — save or copy this table into Excel.

> 📋 **[Prompt 01 — Analyse design report → gate items review table](Prompts/01_ProjectReport_ClashGate_Analysis.md)**

**4b — Services Coordinator review**
Send the Excel to your Services Coordinator. The coordinator fills in YES / NO / N/A for each proposed gate item, adds comments for any rejected items, and signs off the bottom of the Excel. The completed Excel is returned to you.

**4c — Run Prompt 02 with the reviewed Excel**
Open a new AI session. Open Prompt 02 below, click **Raw**, select all, copy, paste in, then attach the completed Excel from the coordinator. The AI reads the review responses and outputs a JSON block.

> 📋 **[Prompt 02 — Reviewed Excel → JSON for platform import](Prompts/02_ChecklistReview_Import.md)**

Save the entire AI response as a `.txt` file → platform: **📋 Updated Gate Rules** → upload. The platform adds all approved items to the gate checklist and auto-signs off completed stages.

> Step 4 and Step 5 both use Prompt 02. It handles the project-specific items table (from Prompt 01) and the full hub defaults checklist (from Export for Review) — same prompt, same upload path.

**Step 5 — Review hub defaults with coordinator (optional but recommended)**
Click **📋 Export for Review** → send Excel to coordinator → coordinator fills YES/NO/N/A and signs off → return Excel → Prompt 02 → save as `.txt` → **📋 Updated Gate Rules**.

**Step 6 — Work through the gates**
For each stage T1 → T4: complete the Pre-Clash Gate Checklist → gate unlocks → **⬇ Export CSV** → run Revizto clash detection → log run in the Run Log tab.

**Step 7 — Transfer to another PC (optional)**
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
| 📂 Upload Updated Matrix | Upload updated company clash matrix → platform rebuilds all tasks (edits preserved) |
| 📋 Updated Gate Rules | Upload `.txt` from AI → adds gate items, ticks checkboxes, auto-signs off stages |
| 📋 Export for Review | Generates Excel for coordinator offline review (YES/NO/N/A + sign-off block) |
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
