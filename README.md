# BIM Clash Coordination Toolkit

**Owner:** Sean Wang — BIM Manager  
**Version:** 1.0  
**Last updated:** 2026-06-16

A project-agnostic toolkit for structured, stage-gated clash detection and digital coordination. Deploy once per project. Built around NZS4219:2009, Revizto Clash Automation, and a T1–T4 staged coordination framework.

---

## What's in the Toolkit

```
BIM_Clash_Coordination_Toolkit/
├── README.md                             ← You are here
├── CHANGELOG.md                          ← Version history + project deployments
│
├── Platform/
│   └── Clash_Coordination_Platform.html  ← Main coordination dashboard (open in Chrome)
│
├── Prompts/
│   ├── 01_ProjectReport_ClashGate_Analysis.md  ← Analyse any project report → gate rules
│   └── 02_NewProject_Setup.md                  ← Configure the platform for a new project
│
└── Projects/
    └── _Template/                        ← Copy this folder for each new project
        └── [ProjectCode]_notes.md        ← Project-specific notes and overrides log
```

---

## Quick Start — New Project in 5 Steps

**Step 1 — Copy the Projects/_Template folder**  
Rename it to your project code (e.g. `Projects/ABC_Tower/`).

**Step 2 — Open the Platform**  
Open `Platform/Clash_Coordination_Platform.html` in Chrome. No installation required. Fill in the Project Name and BIM Lead fields at the top right.

**Step 3 — Upload your Clash Matrix**  
Click **📂 Upload Updated Matrix** in the top right. Select your project's G05 Clash Detection Matrix Excel file. The platform reads the `Rawdata (Do not edit)` sheet and loads all T1–T4 tasks automatically.

**Step 4 — Analyse your project reports**  
Use the prompt in `Prompts/01_ProjectReport_ClashGate_Analysis.md`. Paste the prompt into a Claude session, attach each project report (mechanical, acoustic, structural, BEP). Claude returns structured gate checklist items, clearance overrides, and custom tasks — copy them directly into the platform.

**Step 5 — Work through the gates**  
For each stage (T1 → T2 → T3 → T4):
- Complete the Pre-Clash Gate checklist (watch the gate status change from 🔒 to ✅)
- Use ✏️ Edit on any task to override clearance values for this project
- Use ＋ Add Custom Task for clash pairs not in the standard matrix
- Click **⬇ Export CSV** to get the Revizto-ready task list
- Log each coordination run in the Run Log tab

---

## Platform Features

| Feature | What it does |
|---|---|
| T1–T4 Stage tabs | 425 standard tasks (from your uploaded matrix) split by coordination stage |
| Pre-Clash Gate Checklist | Discipline-tagged checklist items that must be ✅ before running each stage in Revizto |
| Gate Status | Automatically shows 🔒 Locked / ⚠️ Partial / ✅ Open based on checklist progress |
| ✏️ Edit Task | Override clearance code, H/V values, Revizto priority, and add a reason note |
| ＋ Add Custom Task | Add project-specific clash pairs not in the standard matrix |
| 📐 Rules & Standards | NZS4219:2009 seismic table, clearance code reference, discipline gap matrix, project rules |
| 📂 Upload Matrix | Upload updated G05 Excel → platform rebuilds all tasks automatically |
| ⬇ Export CSV | Revizto-ready export including overrides, custom tasks, type flag, and notes |
| Run Log | Dated record of each coordination session |

---

## Your Clash Matrix (G05) — Back-End Workflow

The platform reads from your Excel G05 matrix — you keep working in Excel as normal.

When you update the matrix (new tasks, changed clearances, new project scope):
1. Save the Excel file
2. Click **📂 Upload Updated Matrix** in the platform
3. Platform rebuilds everything — your custom edits and overrides are preserved

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
