# BIM Clash Coordination Toolkit

**Owner:** Sean Wang — BIM Manager  
**Version:** 1.8  
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
│   ├── 01_ProjectReport_ClashGate_Analysis.md  ← Analyse project report → updated gate rules
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

**Step 4 — Analyse your project reports and update gate rules**  
Use the prompt below on Claude, Copilot, or ChatGPT — no Cowork needed, works on any computer. Attach your project report (PDF or Word).

The AI compares the report against the **Hub default gate checklist** (58 built-in items across T1–T4) and applies the following logic:

- **RETAINED** — The report confirms a Hub default. No action needed; item already in platform.
- **SUPPLEMENTED** — The report adds project-specific detail to a Hub default. New item added.
- **SUPERSEDED** — The report overrides a Hub default with stricter or different requirements. New item replaces the default.
- **NEW** — No Hub default covers this. New project-specific item added.

The AI returns a Rule Status Summary (showing what happened to every Hub default), the filtered gate items (SUPPLEMENTED, SUPERSEDED, and NEW only), and a JSON block you upload directly to the platform.

<details>
<summary>📋 Click to expand — Copy this prompt into Claude / Copilot / ChatGPT</summary>

```
You are a senior BIM Coordination Manager with 15+ years of experience across commercial, residential, and specialist construction. Your task is to analyse a project-specific engineering report against an existing Hub default gate checklist, identify what is genuinely new or different, and produce a filtered, non-redundant set of updated gate rules.

---

## COORDINATION FRAMEWORK — STAGE DEFINITIONS

- **T1 — Strategic Constraints & Early Locks**: Structure, civil, seismic, egress, underground, major penetrations, primary service routing — things that cannot be changed once construction starts.
- **T2 — Main Services & Plantroom Coordination**: Main service distribution, ceiling zones, fire walls, plantroom layout — resolved before ceilings and finishes are locked.
- **T3 — Fit-Out, Devices & Maintainability**: Devices, fit-out, access hatches, specialist equipment positions, ceiling-mounted items.
- **T4 — As-Built & Handover Readiness**: Final verification for commissioning, compliance evidence, and FM handover.

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

## HUB DEFAULT GATE CHECKLIST — REFERENCE (do not output these again unless they are modified)

These items are already loaded into the platform. Do not add them again. Use their IDs when flagging overlaps or replacements.

### T1 — Default Items

| ID | Disc | Default Item |
|---|---|---|
| T1-01 | ARCH | Wall dimensions and positions verified — random point test from grids completed |
| T1-02 | ARCH | Wall heights modelled correctly — full height elements identified and confirmed |
| T1-03 | STR | Cross bracing (donobraces) are modelled — check against risers and cushion heads |
| T1-04 | STR | Slab thickness between floors verified (random point test) |
| T1-05 | STR | Intumescent painting on steelwork — service penetration clearances checked (100mm TYP) |
| T1-06 | STR | Structural model included in federated environment for plantrooms, risers, main corridors, and all primary service areas |
| T1-07 | STR | Structural and civil hard constraints modelled or documented sufficiently to support main service route decisions |
| T1-08 | HYD | In-ground foundation beams vs services — pipes in middle third if penetrating; falls on long runs confirmed |
| T1-09 | GEN | Services reticulation strategy aligned with construction build sequence |
| T1-10 | GEN | Major penetrations controlled via a live register — owner, status, and approval authority recorded for each |
| T1-11 | GEN | Primary services use realistic external dimensions, conservative envelopes, or agreed route zones (design-to-install intent) |
| T1-12 | GEN | Major plant placeholders replaced with realistic dimensions or conservative access and maintenance envelopes |
| T1-13 | GEN | Seismic no-go zones, egress protection volumes, and minimum clearance rules defined as model volumes, rules, or documented constraints |
| T1-14 | GEN | New clash tasks can be mapped to G05 Clash Matrix categories before T2 automation or reporting begins |
| T1-15 | GEN | Each system element has one accountable authoring party confirmed for this coordination stage |
| T1-16 | GEN | Placeholder geometry is only used where purpose, owner, and replacement trigger are clearly defined |
| T1-17 | GEN | All coordination issues assigned to the party responsible for action — not the party who raised the issue |
| T1-18 | GEN | Unresolved T1 constraints assigned to accountable owner with due date, or formally accepted as risk before progressing to T2 |
| T1-19 | STR | Fire rating of steel through fire walls — checked against drawings (typically 2D, confirm modelled) |

### T2 — Default Items

| ID | Disc | Default Item |
|---|---|---|
| T2-01 | ARCH | Service walkways modelled in ceiling space — min 900mm wide × 2000mm height, egress routes compliant |
| T2-02 | ARCH | Ceiling heights modelled correctly — Clearance Matrix adjusted to suit |
| T2-03 | ARCH | No services penetrate architect-modelled deflection heads (seismic movement clearance) |
| T2-04 | ARCH | Ceiling/slab thermal or acoustic insulation modelled — spec confirmed |
| T2-05 | ARCH | Acoustic walls with insulation — diagonal brackets modelled, ceiling clearance increased to 100mm |
| T2-06 | HYD | Pipes in walls checked — no hydraulic pipes exceeding wall width |
| T2-07 | HYD | Equal junctions connecting to main drain at ≥15° angle or vertically — confirmed |
| T2-08 | MEC | Duct sizes correct — internal dimensions match design drawings |
| T2-09 | MEC | Services >150mm from ceilings — no installation/access impediment |
| T2-10 | MEC | Fire dampers not within 200mm of each other — spacing confirmed |
| T2-11 | ELE | 150mm clearance between all cable trays confirmed (min 125mm where constrained) |
| T2-12 | ELE | Cable separation between power (LV) and low voltage (data, AV, security) modelled correctly |
| T2-13 | FIR | Fire model transition rule confirmed — when re-coordination is required and who is responsible when subcontractor model replaces design model |
| T2-14 | GEN | Deflection heads on partitions confirmed — services not routing through them |
| T2-15 | GEN | All elements 50mm clear from each other and structure — checked |
| T2-16 | GEN | Insulation thickness modelled correctly on ducts/pipes/mech/hydraulic |
| T2-17 | GEN | Ceiling control surfaces defined by zone, room, or agreed construction area before device and fit-out coordination begins |
| T2-18 | GEN | Main and branch distribution services modelled in active construction zones to agreed coordination accuracy |
| T2-19 | GEN | Insulation, clearance, fire, acoustic, and access assumptions agreed and applied where they drive clash outcomes |
| T2-20 | GEN | Maintenance access volumes initiated for major valves, dampers, FCUs, VAVs, switchboards, pumps, and plant |
| T2-21 | GEN | High-risk seismic and support modelling commenced, or responsibility and timing formally agreed with accountable party |
| T2-22 | GEN | All unresolved T2 issues assigned to correct responsible party with due date, status, and priority recorded |
| T2-23 | ARCH | Firewall layout verified against the fire report — no discrepancies |

### T3 — Default Items

| ID | Disc | Default Item |
|---|---|---|
| T3-01 | ARCH | Acoustic report reviewed — unusual requirements and acoustic wall requirements colour-coded |
| T3-02 | ARCH | RCP coordination complete — ceiling types and fixtures colour-coded, common geometries across trades highlighted |
| T3-03 | HYD | Excess tundish flagged in Revizto — MEC and HYD tundishes identified for team discussion |
| T3-04 | MEC | Flexible duct length ≤3m (target 2.5m) — confirmed |
| T3-05 | MEC | Cooling tower access ladder modelled per AS1657 — spatial requirements confirmed |
| T3-06 | ELE | BMS, Dry Fire, and AV cable trays modelled and confirmed |
| T3-07 | ELE | AV equipment modelled — type and dimensions confirmed against procurement schedule |
| T3-08 | ELE | Floor box numbers and positions align with architectural floor layout |
| T3-09 | FIR | Fire egress routes — minimum widths maintained in ceilings, walkways, and roofs |
| T3-10 | GEN | Ceiling-mounted items modelled (speakers, detectors, sprinklers) — 150mm clearance above FCL confirmed (PCA A-Grade) |
| T3-11 | GEN | Wall-mounted items modelled below ceilings — correctly positioned (not floating) |
| T3-12 | GEN | Plant rooms — spatial check for access and maintenance clearances completed |
| T3-13 | GEN | Final device and terminal layouts coordinated in active construction zones |
| T3-14 | GEN | Access panels, inspection points, and maintenance clearances validated where required |
| T3-15 | GEN | Local penetrations and builders work holes recorded, approved, or assigned for trade resolution as applicable |
| T3-16 | GEN | No unresolved critical clashes remain that would prevent ceiling closure, commissioning, compliance, or safe access |
| T3-17 | GEN | Outstanding T3 issues assigned with construction priority, due date, and responsible party |
| T3-18 | GEN | T3 outputs are suitable to support trade installation, commissioning planning, and site verification |
| T3-19 | GEN | Field change affecting fire, acoustic, egress, seismic, structure, or maintainability — re-clash scope confirmed and responsibility assigned |
| T3-20 | MEC | Grilles aligned with louvres — no misalignment |
| T3-21 | MEC | Service penetration placeholders — all used or removed; none incorrectly placed |

### T4 — Default Items

| ID | Disc | Default Item |
|---|---|---|
| T4-01 | ARCH | Roof walkways — confirmed aligned with plant and services routing |
| T4-02 | GEN | Random check of each trade's 2D drawings against model — spot heights verified |
| T4-03 | GEN | No services run between roof ridgeline and ridgeline steelwork — confirmed |
| T4-04 | GEN | As-built modelling confirmed for mandatory scope — plantrooms, risers, main corridors, major plant, registered penetrations affecting compliance or FM handover |
| T4-05 | GEN | Material deviations from coordinated design captured where they affect operation, access, safety, compliance, or FM handover |
| T4-06 | GEN | Penetrations and supports finalised and aligned between model, register, and site records where required |
| T4-07 | GEN | Final access and compliance checks completed — egress, access hatches, service clearances, seismic no-go zones, and maintenance access |
| T4-08 | GEN | Key equipment and handover assets have correct dimensions, location, identifier, and required asset data per project brief |
| T4-09 | GEN | Residual issues closed, formally accepted, or transferred to defects, commissioning, or handover process — none left unassigned |

---

## YOUR TASK — STEP-BY-STEP

**Step 1 — Extract from the report**
Read the attached project report carefully. Extract every coordination-relevant requirement — clearances, offsets, access zones, installation sequences, penetration rules, material conflicts, and procurement dependencies.

**Step 2 — Compare against Hub defaults**
For each extracted item, compare it against the Hub default list above. Apply these rules strictly:

- **RETAINED** — The extracted item is already covered by a Hub default. Do not output it again. Note which default ID covers it.
- **SUPERSEDED** — A Hub default exists on the same topic, but the project-specific requirement is different, stricter, or contradicts the default. The project requirement takes precedence. Note which default ID is being replaced and why.
- **SUPPLEMENTED** — A Hub default exists on the same general topic, but the project item adds project-specific detail that cannot be inferred from the default. Both the default and the new item apply. Note which default ID it relates to.
- **NEW** — No Hub default covers this. It is a genuinely project-specific requirement.

**Step 3 — Filter output**
Only include SUPERSEDED, SUPPLEMENTED, and NEW items in the output tables and JSON. Do not list RETAINED items in the output tables — they are already in the platform.

**Step 4 — Assign attributes**
For each output item:
- Assign the correct stage (T1/T2/T3/T4)
- Assign the correct discipline code (ARCH, STR, HYD, MEC, ELE, FIR, GEN)
- State the minimum clearance if specified — H (mm) and V (mm) separately. Use null if not specified. Use 0 for hard physical clash (HC).
- Identify the most relevant clash pair (format: DISC vs DISC)
- Cite the source clause or page number

**Step 5 — Flag ambiguities**
If a report clause is ambiguous, note it explicitly rather than assuming. If a project-specific rule conflicts with NZS4219:2009 or standard practice, flag it.

---

## PART 1 — HUMAN-READABLE OUTPUT

### Rule Status Summary

| Hub Default ID | Default Item (short) | Status | Reason / Project Notes |
|---|---|---|---|
| T1-01 | Wall dimensions verified | RETAINED / SUPERSEDED / SUPPLEMENTED | [reason or blank if retained] |
| ... | ... | ... | ... |

Status definitions:
- **RETAINED** — Hub default applies unchanged. Not added to output.
- **SUPERSEDED** — Project report overrides this default. New item in output tables.
- **SUPPLEMENTED** — Project report adds detail to this default. Additional item in output tables.
- **NEW** — No corresponding Hub default. New item in output tables.

Only include SUPERSEDED, SUPPLEMENTED, and NEW items in the gate item tables below.

---

### Updated Gate Items — T1

| # | Status | Disc | Gate Item | H (mm) | V (mm) | Clash Pair | Replaces / Relates to | Source |
|---|---|---|---|---|---|---|---|---|

### Updated Gate Items — T2

| # | Status | Disc | Gate Item | H (mm) | V (mm) | Clash Pair | Replaces / Relates to | Source |
|---|---|---|---|---|---|---|---|---|

### Updated Gate Items — T3

| # | Status | Disc | Gate Item | H (mm) | V (mm) | Clash Pair | Replaces / Relates to | Source |
|---|---|---|---|---|---|---|---|---|

### Updated Gate Items — T4

| # | Status | Disc | Gate Item | H (mm) | V (mm) | Clash Pair | Replaces / Relates to | Source |
|---|---|---|---|---|---|---|---|---|

---

### Procurement Flags

| Item | Discipline | What is pending | When needed by | Stage |
|---|---|---|---|---|

---

### Top 3 Coordination Risks

Write 3–5 sentences summarising the most significant coordination risks this report introduces, focusing on items that are new to this project and not covered by Hub defaults.

---

## PART 2 — JSON OUTPUT FILE

After the human-readable output above, output a section starting with this exact line on its own:

=== CLASH COORDINATION PLATFORM — JSON OUTPUT (copy everything between the braces) ===

Then output a single valid JSON object with EXACTLY this structure. Do not add extra fields. Do not remove fields. Do not use comments. No trailing commas.

{
  "project": "Project name from report, or Unknown if not stated",
  "report": "Document title and version",
  "date": "Today's date in YYYY-MM-DD format",
  "gateItems": [
    {
      "stage": "T1",
      "discipline": "STR",
      "item": "One sentence gate item in plain language",
      "clearanceH": 50,
      "clearanceV": 100,
      "clashPair": "STR vs MEC",
      "source": "Section 4.2",
      "status": "NEW",
      "replacesDefault": null
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
  "projectNotes": "Your 3-5 sentence coordination risk summary as a single string."
}

STRICT RULES FOR THE JSON:
- Include only SUPERSEDED, SUPPLEMENTED, and NEW items in gateItems. Do not include RETAINED items.
- "stage" must be exactly one of: T1, T2, T3, T4
- "discipline" must be exactly one of: ARCH, STR, HYD, MEC, ELE, FIR, GEN
- "clearanceH" and "clearanceV" must be integers in millimetres, or null if not specified
- Use 0 for hard clash (physical contact, zero clearance)
- "clashPair" format is "DISC vs DISC" — example: "MEC vs STR"
- "status" must be exactly one of: NEW, SUPERSEDED, SUPPLEMENTED
- "replacesDefault" is the Hub default ID being superseded or supplemented (e.g., "T1-05"), or null if NEW
- "targetDate" must be "YYYY-MM-DD" format or null
- "projectNotes" must be a single string — no line breaks inside it
- If there are no procurementFlags, output: "procurementFlags": []
- The JSON must be valid — test it mentally before outputting
```

**What to do with the output:**

1. Review the Rule Status Summary in Part 1 — note any SUPERSEDED Hub defaults and manually uncheck those in the platform checklist
2. Save the **entire AI response** as a plain text file: `[ProjectCode]_gate_rules.txt`
3. In the platform, click **📋 Updated Gate Rules** and select that file — the platform automatically finds and extracts the JSON block

> **Alternative:** If you prefer, copy just the JSON block (from `{` to `}`) and save that as the file instead. Both methods work.

If the gate rules don't load, ask the AI: *"Please recheck the JSON block and output a corrected version with no trailing commas and all string values in double quotes."*

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
   📋 Updated Gate Rules
   → Compares against 58 Hub defaults
   → Adds only NEW / SUPPLEMENTED / SUPERSEDED items
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
| 📋 Updated Gate Rules | Upload JSON from Claude/Copilot/ChatGPT → adds only project-specific gate items (NEW, SUPPLEMENTED, SUPERSEDED) — Hub defaults already in platform are not duplicated |
| 📋 Export for Review | Generates a formatted Excel with all gate checklist items for Services Coordinator offline sign-off |
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
