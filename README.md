# BIM Clash Coordination Toolkit

**Owner:** Sean Wang — BIM Manager  
**Version:** 1.5  
**Last updated:** 2026-06-20

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
│   ├── 01_ProjectReport_ClashGate_Analysis.md  ← Analyse any project report → gate rules
│   └── 02_NewProject_Setup.md                  ← Configure the platform for a new project
│
└── Projects/
    └── _Template/                        ← Copy this folder for each new project
        └── [ProjectCode]_notes.md        ← Project-specific notes and overrides log
```

> 📊 **See `Clash_Coordination_Workflow.svg`** for a visual overview of the full process.

---

## Quick Start — New Project in 5 Steps

**Step 1 — Copy the Projects/_Template folder**  
Rename it to your project code (e.g. `Projects/ABC_Tower/`).

**Step 2 — Open the Platform**  
Open `Platform/Clash_Coordination_Platform.html` in Chrome. No installation required. Fill in the Project Name and BIM Lead fields at the top right.

**Step 3 — Upload your Clash Matrix**  
Click **📂 Upload Updated Matrix** in the top right. Select your project's G05 Clash Detection Matrix Excel file. The platform reads the `Rawdata (Do not edit)` sheet and loads all T1–T4 tasks automatically.

**Step 4 — Analyse your project reports**  
Use the prompt below on Claude, Copilot, or ChatGPT — no Cowork needed, works on any computer. Attach your project reports (PDF or Word). The AI returns structured gate checklist items and a JSON block you upload directly to the platform.

<details>
<summary>📋 Click to expand — Copy this prompt into Claude / Copilot / ChatGPT</summary>

```
You are a senior BIM Coordination Manager with 15+ years of experience. Review the attached project report and extract all coordination requirements, clearance rules, and clash-relevant constraints. Output them as structured pre-clash gate checklist items for a staged clash detection platform.

---

## STAGE DEFINITIONS

- T1 — Strategic Constraints & Early Locks: Structure, civil, seismic zones, underground, major penetrations, primary service routing — things that cannot be changed once construction starts.
- T2 — Main Services & Plantroom Coordination: Main service distribution, ceiling zones, fire walls, plantroom layout — resolved before ceilings and finishes are locked.
- T3 — Fit-Out, Devices & Maintainability: Devices, fit-out, access hatches, specialist equipment positions, ceiling-mounted items.
- T4 — As-Built & Handover Readiness: Final verification for commissioning, compliance evidence, and FM handover.

The platform already has standard NZS4219:2009 seismic clearances. Extract only PROJECT-SPECIFIC requirements that add to or differ from standard rules.

---

## DISCIPLINE CODES

Use these codes exactly — no variations:
- ARCH (Architectural)
- STR (Structural)
- HYD (Hydraulic/Plumbing)
- MEC (Mechanical)
- ELE (Electrical)
- FIR (Fire)
- GEN (General / multi-discipline)

---

## INSTRUCTIONS

1. Extract every coordination-relevant requirement — clearances, offsets, access zones, installation sequences, penetration rules, material conflicts, and procurement dependencies.

2. Assign each item to T1, T2, T3, or T4.

3. Write each checklist item in plain, buildable language — one sentence, actionable, no jargon.

4. State clearances as integers in millimetres. Use null if not specified. If it is a hard physical clash (zero clearance), use 0 for both H and V.

5. Flag procurement dependencies where coordination cannot be finalised until a supplier or subcontractor is confirmed.

---

## PART 1 — HUMAN-READABLE TABLES

Output the following four tables. Group items within each stage by discipline in this order: STR → HYD → MEC → ELE → FIR → ARCH → GEN.

### T1 — Strategic Constraints Gate Items
| # | Discipline | Checklist Item | H (mm) | V (mm) | Clash Pair | Source |
|---|---|---|---|---|---|---|

### T2 — Main Services Gate Items
| # | Discipline | Checklist Item | H (mm) | V (mm) | Clash Pair | Source |
|---|---|---|---|---|---|---|

### T3 — Fit-Out & Devices Gate Items
| # | Discipline | Checklist Item | H (mm) | V (mm) | Clash Pair | Source |
|---|---|---|---|---|---|---|

### T4 — Handover Gate Items
| # | Discipline | Checklist Item | H (mm) | V (mm) | Clash Pair | Source |
|---|---|---|---|---|---|---|

### Procurement Flags
| Item | Discipline | What is pending | When needed by | Stage |
|---|---|---|---|---|

### Top 3 Coordination Risks
Write 3–5 sentences summarising the most significant coordination risks this report introduces.

---

## PART 2 — JSON OUTPUT FILE

After the tables above, output a section that starts with this exact line on its own line:

=== CLASH COORDINATION PLATFORM — JSON OUTPUT (copy everything between the braces) ===

Then output a single valid JSON object with EXACTLY this structure. Do not add extra fields. Do not remove fields. Do not use comments inside the JSON. Do not use trailing commas.

{
  "project": "Project name from report, or Unknown if not stated",
  "report": "Document title and version from report",
  "date": "Today's date in YYYY-MM-DD format",
  "gateItems": [
    {
      "stage": "T1",
      "discipline": "STR",
      "item": "One sentence checklist item in plain language",
      "clearanceH": 50,
      "clearanceV": 100,
      "clashPair": "STR vs MEC",
      "source": "Section 4.2 or page number"
    }
  ],
  "procurementFlags": [
    {
      "item": "Short description of what is pending",
      "discipline": "MEC",
      "pending": "What must be confirmed before coordination can proceed",
      "targetDate": "YYYY-MM-DD or null",
      "stage": "T2"
    }
  ],
  "projectNotes": "Your 3-5 sentence coordination risk summary goes here as a single string."
}

STRICT RULES FOR THE JSON:
- "stage" must be exactly one of: T1, T2, T3, T4
- "discipline" must be exactly one of: ARCH, STR, HYD, MEC, ELE, FIR, GEN
- "clearanceH" and "clearanceV" must be integers in millimetres, or null if not specified
- Use 0 for hard clash (physical contact, zero clearance)
- "clashPair" format is "DISC vs DISC" — for example: "MEC vs STR"
- "targetDate" must be "YYYY-MM-DD" format or null
- "projectNotes" must be a single string — no line breaks inside it
- If there are no procurementFlags, output: "procurementFlags": []
- Every string value must use double quotes — no single quotes anywhere in the JSON
- The JSON must be valid — test it mentally before outputting
```

**What to do with the output:**

1. Review the human-readable tables for accuracy
2. Copy everything between the outer `{` and `}` braces of the JSON block
3. Paste into a plain text file and save as `[ProjectCode]_gate_rules.txt`
4. In the platform, click **📤 Pre-Clash Gate Updates Upload** — gate items appear immediately as checkboxes in the correct stage checklist

If the JSON doesn't load, paste it into [jsonlint.com](https://jsonlint.com) to find the error, or ask the AI: *"Please recheck the JSON and output a corrected version with no trailing commas and all string values in double quotes."*

> **Important:** Clash task updates (clearance overrides, new task pairs) must always be made in the G05 Clash Matrix first, then re-uploaded. Do not include clash task data in the JSON.

</details>

**Step 5 — Work through the gates**  
For each stage (T1 → T2 → T3 → T4):
- Use the discipline filter on the Pre-Clash Gate Checklist to focus on one trade at a time
- Complete the checklist — gate status changes from 🔒 to ✅ automatically
- Use ✏️ Edit on any task row to override clearance values for this project
- If a new clash pair is identified, update the G05 Matrix in Excel and re-upload
- Click **⬇ Export CSV** to get the Revizto-ready task list
- Log each coordination run in the Run Log tab

**Step 6 — Transfer to another PC (optional)**  
Click **⬆ Export Session** to save all tasks, gate progress, project gate items, and log to a JSON file.  
On the other PC, open the platform and click **⬇ Import Session** to restore everything instantly.

---

## Workflow Overview

```
G05 Clash Matrix (Excel)
        │
        ▼  Upload Updated Matrix
┌─────────────────────────────────┐
│   BIM Clash Coordination        │
│   Platform (HTML dashboard)     │
│                                 │
│  [Left]          [Right]        │
│  Pre-Clash    Revizto Clash     │
│  Gate         Task Output       │
│  Checklist    (filterable       │
│  T1–T4        table, CSV        │
│  gates        export)           │
└─────────────────────────────────┘
        │                   │
        │ Gate = ✅          │ Export CSV
        ▼                   ▼
  Run Revizto          Revizto Clash
  Clash Detection      Automation Tasks
  for this stage       Loaded Manually

        │
        ▼  Project Report (PDF/Word)
   Claude / Copilot / ChatGPT Prompt
   (any computer, no Cowork needed)
        │
        ▼  Copy JSON output block
   📤 Pre-Clash Gate Updates Upload
   → Gate items injected as checkboxes
   → Procurement flags → Rules tab notes
   → New task pairs? Update G05 Matrix
     and re-upload — NOT through platform
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
| 📤 Pre-Clash Gate Updates Upload | Upload JSON from Claude/Copilot/ChatGPT → gate items injected as checkboxes into the correct stage |
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
