# BIM Clash Coordination Toolkit

**Owner:** Sean Wang — BIM Manager  
**Version:** 1.9  
**Last updated:** 2026-06-24

A project-agnostic toolkit for structured, stage-gated clash detection and digital coordination. Deploy once per project. Built around NZS4219:2009, Revizto Clash Automation, and a T1–T4 staged coordination framework.

---

## What's in the Toolkit

```
BIM_Clash_Coordination_Toolkit/
├── README.md                             ← You are here
├── CHANGELOG.md                          ← Version history + project deployments
├── Clash_Coordination_Workflow.svg       ← Visual workflow diagram (open in browser)
│
├── Platform/
│   └── Clash_Coordination_Platform.html  ← Main coordination dashboard (open in Chrome)
│
├── Prompts/
│   ├── 01_ProjectReport_ClashGate_Analysis.md  ← Analyse project report → updated gate rules JSON
│   └── 02_ChecklistReview_Import.md            ← Convert completed coordinator Excel → JSON for import
│
└── Projects/
    └── _Template/                        ← Copy this folder for each new project
        └── [ProjectCode]_notes.md        ← Project-specific notes and overrides log
```

> 📊 **See `Clash_Coordination_Workflow.svg`** for a visual overview of the full process.

---

## Quick Start — New Project in 6 Steps

**Step 1 — Copy the Projects/_Template folder**  
Rename it to your project code (e.g. `Projects/ABC_Tower/`).

**Step 2 — Open the Platform**  
Open `Platform/Clash_Coordination_Platform.html` in Chrome. No installation required. Fill in the Project Name and BIM Lead fields at the top right.

**Step 3 — Upload your Clash Matrix**  
Click **📂 Upload Updated Matrix** in the top right. Select your project's G05 Clash Detection Matrix Excel file. The platform reads the `Rawdata (Do not edit)` sheet and loads all T1–T4 tasks automatically.

**Step 4 — Analyse project reports → expert review → update gate checklist**  
This step uses two AI prompts and an expert review in between. No direct JSON upload to the platform — all proposed items go through the coordinator first.

**4a — Run Prompt 01 with your project report**  
Copy the prompt below into Claude, Copilot, or ChatGPT, then attach your project report (PDF or Word). No Cowork needed — works on any computer.

> 📋 **[Open Prompt 01 →](Prompts/01_ProjectReport_ClashGate_Analysis.md)** — click to open, then click **Raw** → select all → copy into your AI session.

The AI compares the report against the **Hub default gate checklist** (58 built-in items across T1–T4) and applies the following logic:

- **RETAINED** — The report confirms a Hub default. No action needed; item already in platform.
- **SUPPLEMENTED** — The report adds project-specific detail to a Hub default. New item added.
- **SUPERSEDED** — The report overrides a Hub default with stricter or different requirements. New item replaces the default.
- **NEW** — No Hub default covers this. New project-specific item added.

The AI returns: a Rule Status Summary, and a **Gate Items Review Table** (Part 2 of the response) listing all proposed NEW / SUPPLEMENTED / SUPERSEDED items — formatted as a spreadsheet-ready table for expert sign-off.

**4b — Send the review table to the coordinator**  
Copy the Part 2 Gate Items Review Table from the AI response into Excel (or save the AI response and use it directly). Send the Excel to your Services Coordinator or subject-matter expert. The coordinator fills in the REVIEW column (YES / NO / N/A) and a COMMENT column, then completes the sign-off block.

**4c — Run Prompt 02 to convert the reviewed Excel to JSON**  
Once the coordinator returns the completed Excel, copy the prompt below into Claude, Copilot, or ChatGPT and attach the completed Excel. The AI reads the review responses and outputs a JSON block.

> 📋 **[Open Prompt 02 →](Prompts/02_ChecklistReview_Import.md)** — click to open, then click **Raw** → select all → copy into your AI session.

Save the entire AI response as a `.txt` file. In the platform, click **📋 Updated Gate Rules** → upload the file. The platform automatically:
- Adds all coordinator-approved gate items (YES items) to the Pre-Clash Gate Checklist
- Leaves NO items excluded, with a 💬 comment badge showing the coordinator's reason
- Signs off the gate stage if the coordinator completed the sign-off block

**Step 5 — Review hub defaults with the coordinator (optional but recommended)**  
Step 4 covers project-specific gate items. This step reviews the 58 built-in hub defaults to confirm which apply to this project.

1. In the platform, click **📋 Export for Review** — generates an Excel with all hub default checklist items for each stage (T1–T4), plus any items already added in Step 4
2. Send the Excel to the Services Coordinator
3. Coordinator fills in YES / NO / N/A for each item, adds comments for NO items, and completes the sign-off block
4. Coordinator returns the completed Excel
5. Upload the filled Excel to Claude, Copilot, or ChatGPT using **Prompt 02** (same prompt above)
6. Save the entire AI response as a `.txt` file → platform: **📋 Updated Gate Rules** → upload

> Both Step 4 and Step 5 use the same Prompt 02 → Updated Gate Rules path. Prompt 02 handles both the project-specific items table (from Prompt 01) and the full checklist Excel (from Export for Review).

**Step 6 — Work through the gates**  
For each stage (T1 → T2 → T3 → T4):
- Use the discipline filter on the Pre-Clash Gate Checklist to focus on one trade at a time
- Complete the checklist — gate status changes from 🔒 to ✅ automatically
- Use ✏️ Edit on any task row to override clearance values for this project
- If a new clash pair is identified, update the G05 Matrix in Excel and re-upload
- Click **⬇ Export CSV** to get the Revizto-ready task list
- Log each coordination run in the Run Log tab

**Step 7 — Transfer to another PC (optional)**  
Click **⬆ Export Session** to save all tasks, gate progress, project gate items, and log to a JSON file.  
On the other PC, open the platform and click **⬇ Import Session** to restore everything instantly.

---

## Workflow Overview

```
G05 Clash Matrix (Excel)          Project Report (PDF/Word)
        │                                   │
        ▼  Upload Updated Matrix             ▼  Prompt 01
┌─────────────────────────────────┐   Claude / Copilot / ChatGPT
│   BIM Clash Coordination        │         │
│   Platform (HTML dashboard)     │         ▼  Save as .txt
│                                 │   📋 Updated Gate Rules
│  [Left]          [Right]        │   → Adds NEW / SUPPLEMENTED / SUPERSEDED items
│  Pre-Clash    Revizto Clash     │   → Procurement flags → Rules tab
│  Gate         Task Output       │
│  Checklist    (filterable       │         │
│  T1–T4        table, CSV        │         ▼  Export for Review
│  gates        export)           │   Excel → Services Coordinator
└─────────────────────────────────┘         │
        │                   │               ▼  Coordinator fills YES/NO/N/A
        │ Gate = ✅          │ Export CSV    │  + sign-off block
        ▼                   ▼               │
  Run Revizto          Revizto Clash        ▼  Prompt 02
  Clash Detection      Automation Tasks  Claude / Copilot / ChatGPT
  for this stage       Loaded Manually      │
                                            ▼  Save as .txt
                                      📋 Updated Gate Rules
                                      → Ticks YES/N/A items
                                      → Flags NO items with comment badge
                                      → Auto signs off completed gates
```

---

## Platform Features

| Feature | What it does |
|---|---|
| T1–T4 Stage tabs | Tasks from your uploaded G05 matrix split by coordination stage |
| Pre-Clash Gate Checklist | Discipline-tagged checklist with filter dropdown — must be ✅ before running each stage in Revizto |
| Revizto Clash Task Output | Task table (right panel) — search, filter by discipline or clearance, mark as loaded, export CSV |
| Gate Status | Automatically shows 🔒 Locked / ⚠️ Partial / ✅ Open based on checklist progress |
| ✏️ Edit Task | Override clearance code, H/V values, Revizto priority, and add a reason note per task |
| 📐 Rules & Standards | NZS4219:2009 seismic table, clearance code reference, discipline gap matrix with breakdown, project notes |
| 📂 Upload Updated Matrix | Upload updated G05 Excel → platform rebuilds all tasks automatically |
| 📋 Updated Gate Rules | Upload JSON from Claude/Copilot/ChatGPT → handles two workflows: (1) Prompt 01 output — adds project-specific gate items (NEW, SUPPLEMENTED, SUPERSEDED); (2) Prompt 02 output — updates checkbox states, adds comment badges, and auto-signs off completed gates from coordinator review |
| 📋 Export for Review | Generates a formatted Excel (one sheet per stage) for Services Coordinator offline review — YES/NO/N/A columns, comment column, sign-off block; return the completed file through Prompt 02 |
| 🌙 / ☀️ Theme toggle | Switch between light and dark mode — preference saved between sessions |
| ⬆ Export Session | Save all tasks, gate states, project gate items, and run log to a portable JSON file |
| ⬇ Import Session | Load a session file on any PC to restore a project's full setup instantly |
| ⬇ Export CSV | Revizto-ready export including overrides, type flag, and notes |
| Run Log | Dated record of each coordination session |

---

## Your Clash Matrix (G05) — Back-End Workflow

The platform reads from your Excel G05 matrix — you keep working in Excel as normal.

When you update the matrix (new tasks, changed clearances, new project scope):
1. Save the Excel file
2. Click **📂 Upload Updated Matrix** in the platform
3. Platform rebuilds everything — your task edits are preserved

The platform always shows which matrix is loaded and when it was last uploaded.

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

## Revizto Priority Logic

| Condition | Priority |
|---|---|
| HC clearance on structural or fire elements | Critical |
| Fire pipes, structural clashes | Critical |
| HYD pipes, MEC uninsulated ducts | Major |
| ELE, MEC general | Major |
| Small bore pipes, minor clearances | Minor |

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
| Model Checklist | `[ProjectCode]_G08_Model_Checklist.xlsx` | `ABC_G08_Model_Checklist.xlsx` |
| Revizto Export | `Revizto_Tasks_[Stage]_[ProjectCode]_[Date].csv` | `Revizto_Tasks_T2_ABC_2026-07-01.csv` |
| Platform snapshot | `[ProjectCode]_Platform_[Date].html` | `ABC_Platform_2026-07-01.html` (save a copy at milestones) |


---

## CHANGELOG

See `CHANGELOG.md` for version history and project deployment record.
                                                                                                                                                                                    