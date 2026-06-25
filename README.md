# BIM Clash Coordination Toolkit

**Owner:** Sean Wang — BIM Manager | **Version:** 1.9 | **Last updated:** 2026-06-24

Stage-gated clash detection and digital coordination toolkit. Built around NZS4219:2009, Revizto Clash Automation, and a T1–T4 coordination framework.

> 📊 **See `Clash_Coordination_Workflow.svg`** for a visual overview of the full process.

---

## Toolkit Contents

```
BIM_Clash_Coordination_Toolkit/
├── README.md
├── CHANGELOG.md
├── Clash_Coordination_Workflow.svg       ← Visual workflow diagram (open in browser)
│
├── Platform/
│   └── Clash_Coordination_Platform.html  ← Main coordination dashboard (open in Chrome)
│
├── Prompts/
│   ├── 01_ProjectReport_ClashGate_Analysis.md
│   └── 02_ChecklistReview_Import.md
│
└── Projects/
    └── _Template/
        └── [ProjectCode]_notes.md
```

---

## Quick Start

**Step 1 — Copy template**
Copy `Projects/_Template/` and rename it to your project code (e.g. `Projects/ABC_Tower/`).

**Step 2 — Open the platform**
Open `Platform/Clash_Coordination_Platform.html` in Chrome. Enter the Project Name and BIM Lead.

**Step 3 — Upload your Clash Matrix**
Click **📂 Upload Updated Matrix** → select your company clash matrix. The platform reads the `Rawdata (Do not edit)` sheet and loads all T1–T4 tasks automatically.

**Step 4 — Analyse project reports → coordinator review → update gate checklist**

**4a — Run Prompt 01** — open a new Claude, Copilot, or ChatGPT session. Expand the prompt below, copy all text, paste it in, then attach your project report (PDF or Word).

<details>
<summary>📋 Prompt 01 — Analyse project report against hub gate checklist (click to expand)</summary>

<pre>
You are a senior BIM Coordination Manager with 15+ years of experience across commercial, residential, and specialist construction. Your task is to analyse a project-specific engineering report against an existing Hub default gate checklist, identify what is genuinely new or different, and produce a filtered, non-redundant set of updated gate rules.

---

## COORDINATION FRAMEWORK — STAGE DEFINITIONS

- **T1 — Strategic Constraints &amp; Early Locks**: Structure, civil, seismic, egress, underground, major penetrations, primary service routing — things that cannot be changed once construction starts.
- **T2 — Main Services &amp; Plantroom Coordination**: Main service distribution, ceiling zones, fire walls, plantroom layout — resolved before ceilings and finishes are locked.
- **T3 — Fit-Out, Devices &amp; Maintainability**: Devices, fit-out, access hatches, specialist equipment positions, ceiling-mounted items.
- **T4 — As-Built &amp; Handover Readiness**: Final verification for commissioning, compliance evidence, and FM handover.

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
| T2-09 | MEC | Services &gt;150mm from ceilings — no installation/access impediment |
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
| T4-02 | GEN | Random check of each trade&#x27;s 2D drawings against model — spot heights verified |
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

Before the gate item tables, output this summary table. Every Hub default must appear here with its status.

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

## PART 2 — GATE ITEMS REVIEW TABLE (send to coordinator for sign-off)

After Part 1, output this review table. This is the file the BIM Manager will send to the Services Coordinator for review and approval before any items enter the platform.

Output one row per NEW, SUPPLEMENTED, or SUPERSEDED item. Leave the REVIEW and COMMENT columns blank — the coordinator fills these in.

| # | Stage | Disc | Proposed Gate Item | Status | Replaces Hub Default | H (mm) | V (mm) | Source | REVIEW (YES/NO/N/A) | COMMENT |
|---|---|---|---|---|---|---|---|---|---|---|
| 1 | T1 | STR | [item text] | NEW | - | [H or blank] | [V or blank] | [Section X.X] | | |
| 2 | T2 | MEC | [item text] | SUPPLEMENTED | T2-08 | 150 | 200 | [Section X.X] | | |

- # is a sequential row number starting from 1
- Status is one of: NEW, SUPERSEDED, SUPPLEMENTED
- Replaces Hub Default is the Hub default ID (e.g. T2-08) for SUPERSEDED/SUPPLEMENTED items, or - for NEW
- H and V are in millimetres; leave blank if not specified
- REVIEW and COMMENT columns are intentionally blank — the coordinator fills them in

---

## PART 3 — JSON REFERENCE (included for completeness)

After Part 2, output a section starting with this exact line on its own:

=== CLASH COORDINATION PLATFORM JSON — PASTE INTO UPDATED GATE RULES ===

Then output a single valid JSON object with EXACTLY this structure. Do not add extra fields. Do not remove fields. Do not use comments. No trailing commas.

{
  &quot;project&quot;: &quot;Project name from report, or Unknown if not stated&quot;,
  &quot;report&quot;: &quot;Document title and version&quot;,
  &quot;date&quot;: &quot;Today&#x27;s date in YYYY-MM-DD format&quot;,
  &quot;gateItems&quot;: [
    {
      &quot;stage&quot;: &quot;T1&quot;,
      &quot;discipline&quot;: &quot;STR&quot;,
      &quot;item&quot;: &quot;One sentence gate item in plain language&quot;,
      &quot;clearanceH&quot;: 50,
      &quot;clearanceV&quot;: 100,
      &quot;clashPair&quot;: &quot;STR vs MEC&quot;,
      &quot;source&quot;: &quot;Section 4.2&quot;,
      &quot;status&quot;: &quot;NEW&quot;,
      &quot;replacesDefault&quot;: null
    }
  ],
  &quot;procurementFlags&quot;: [
    {
      &quot;item&quot;: &quot;Short description of what is pending&quot;,
      &quot;discipline&quot;: &quot;MEC&quot;,
      &quot;pending&quot;: &quot;What must be confirmed before coordination can proceed&quot;,
      &quot;targetDate&quot;: &quot;YYYY-MM-DD or null&quot;,
      &quot;stage&quot;: &quot;T2&quot;
    }
  ],
  &quot;projectNotes&quot;: &quot;Your 3-5 sentence coordination risk summary as a single string.&quot;
}

STRICT RULES FOR THE JSON:
- Include only SUPERSEDED, SUPPLEMENTED, and NEW items in gateItems. Do not include RETAINED items.
- &quot;stage&quot; must be exactly one of: T1, T2, T3, T4
- &quot;discipline&quot; must be exactly one of: ARCH, STR, HYD, MEC, ELE, FIR, GEN
- &quot;clearanceH&quot; and &quot;clearanceV&quot; must be integers in millimetres, or null if not specified
- Use 0 for hard clash (physical contact, zero clearance)
- &quot;clashPair&quot; format is &quot;DISC vs DISC&quot; — example: &quot;MEC vs STR&quot;
- &quot;status&quot; must be exactly one of: NEW, SUPERSEDED, SUPPLEMENTED
- &quot;replacesDefault&quot; is the Hub default ID being superseded or supplemented (e.g., &quot;T1-05&quot;), or null if NEW
- &quot;targetDate&quot; must be &quot;YYYY-MM-DD&quot; format or null
- &quot;projectNotes&quot; must be a single string — no line breaks inside it
- If there are no procurementFlags, output: &quot;procurementFlags&quot;: []
- The JSON must be valid — test it mentally before outputting

</pre>

</details>

The AI returns a **Rule Status Summary** plus a **Gate Items Review Table** (Part 2) listing all proposed NEW / SUPPLEMENTED / SUPERSEDED items.

**4b — Send the review table to the coordinator**
Copy the Part 2 table into Excel and send it to your Services Coordinator to fill in YES / NO / N/A and sign off.

**4c — Run Prompt 02** — once the coordinator returns the Excel, open a new AI session, expand the prompt below, copy all text, paste it in, then attach the completed Excel.

<details>
<summary>📋 Prompt 02 — Convert coordinator Excel to JSON for platform import (click to expand)</summary>

<pre>
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

This file comes from the BIM Manager who ran Prompt 01 against a project report. The coordinator has reviewed the AI&#x27;s proposed gate items and filled in the REVIEW and COMMENT columns.

The table has these columns:

| # | Stage | Disc | Proposed Gate Item | Status | Replaces Hub Default | H (mm) | V (mm) | Source | REVIEW (YES/NO/N/A) | COMMENT |

- **REVIEW = YES** → Include this gate item in the platform checklist
- **REVIEW = NO** → Exclude this item (coordinator rejected it)
- **REVIEW = N/A** → Not applicable to this project, exclude

**JSON output for Format A: use `gateItems[]`** — only include items where REVIEW = YES.

---

### Format B — Export for Review Excel (hub defaults checklist)

This file comes from the platform&#x27;s **📋 Export for Review** button. It has sheets named T1, T2, T3, T4, each with:

- Column A: Item number (#) — sequential row numbers matching hub defaults
- Column B: Stage
- Column C: Discipline
- Column D: Checklist Item text
- Column E: Review (YES / NO / N/A) — **filled by coordinator**
- Column F: Comment — **filled by coordinator**
- Sign-off block at the bottom: Reviewer Name, Reviewer Role / Company, Date Reviewed, Overall Comments

**JSON output for Format B: use `checklistReview{}`** — map each item&#x27;s review state to its row number.

---

## Your Task

### Step 1 — Detect input format

Look at the column headers:
- If the header row contains &quot;Proposed Gate Item&quot; and &quot;Status&quot; → **Format A** (Prompt 01 table)
- If the header row contains &quot;Checklist Item&quot; and has T1/T2/T3/T4 as sheet names with sign-off blocks → **Format B** (Export for Review)

Then follow the matching extraction steps below.

### Step 2A — Format A: Extract approved gate items

For each row where REVIEW = YES:
- Stage, Discipline, Proposed Gate Item text, Status, H (mm), V (mm), Source, Replaces Hub Default

For each row where REVIEW = NO or N/A: skip (exclude from JSON).

Extract sign-off details if present (Reviewer Name, Role, Date, Comments).

### Step 2B — Format B: Extract checklist review responses

For each stage (T1, T2, T3, T4), read every data row and extract:
- Item number (column A)
- Review value (column E): YES, NO, or N/A
- Comment (column F)

Only include items where the coordinator has entered a review value. Skip blank rows.

Extract sign-off block details for each stage (Reviewer Name, Reviewer Role / Company, Date Reviewed, Overall Comments). Only include a sign-off if Reviewer Name AND Date Reviewed are both filled.

### Step 3 — Summarise outstanding items

List all items marked NO with their stage, item text, and coordinator comment. These need resolution before the gate closes.

### Step 4 — Output

Produce two parts:

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

[Write the summary table here — detected format, stage-by-stage counts (YES/NO/N/A), then a list of all NO items needing action]

---

### PART 2: Platform JSON

Output the JSON block preceded by the delimiter line exactly as shown. Use Format A or Format B schema depending on the input detected.

=== CLASH COORDINATION PLATFORM JSON — PASTE INTO UPDATED GATE RULES ===

**If Format A (Prompt 01 gate items table) — use `gateItems[]`:**

```json
{
  &quot;project&quot;: &quot;[project name]&quot;,
  &quot;date&quot;: &quot;[today YYYY-MM-DD]&quot;,
  &quot;gateItems&quot;: [
    {
      &quot;stage&quot;: &quot;T1&quot;,
      &quot;discipline&quot;: &quot;STR&quot;,
      &quot;item&quot;: &quot;Approved gate item text here&quot;,
      &quot;clearanceH&quot;: 50,
      &quot;clearanceV&quot;: 100,
      &quot;clashPair&quot;: &quot;STR vs MEC&quot;,
      &quot;source&quot;: &quot;Section 4.2&quot;,
      &quot;status&quot;: &quot;NEW&quot;,
      &quot;replacesDefault&quot;: null
    }
  ],
  &quot;gateSignOffs&quot;: {
    &quot;T1&quot;: { &quot;name&quot;: &quot;Reviewer name&quot;, &quot;role&quot;: &quot;Role / Company&quot;, &quot;date&quot;: &quot;YYYY-MM-DD&quot;, &quot;comment&quot;: &quot;&quot; }
  }
}
```

**If Format B (Export for Review hub defaults Excel) — use `checklistReview{}`:**

```json
{
  &quot;project&quot;: &quot;[project name from Excel header]&quot;,
  &quot;date&quot;: &quot;[today YYYY-MM-DD]&quot;,
  &quot;checklistReview&quot;: {
    &quot;T1&quot;: [
      { &quot;num&quot;: 1, &quot;review&quot;: &quot;YES&quot;, &quot;comment&quot;: &quot;&quot; },
      { &quot;num&quot;: 2, &quot;review&quot;: &quot;NO&quot;, &quot;comment&quot;: &quot;Not yet resolved — pending structural drawings&quot; },
      { &quot;num&quot;: 3, &quot;review&quot;: &quot;N/A&quot;, &quot;comment&quot;: &quot;No acoustic walls on this project&quot; }
    ],
    &quot;T2&quot;: [],
    &quot;T3&quot;: [],
    &quot;T4&quot;: []
  },
  &quot;gateSignOffs&quot;: {
    &quot;T1&quot;: { &quot;name&quot;: &quot;Reviewer name&quot;, &quot;role&quot;: &quot;Role / Company&quot;, &quot;date&quot;: &quot;YYYY-MM-DD&quot;, &quot;comment&quot;: &quot;&quot; }
  }
}
```

---

## Rules

- Only one JSON output per session — use the format matching the detected input
- Format A: only include items where REVIEW = YES in `gateItems[]`; omit NO and N/A items entirely
- Format B: include ALL items where a review value was entered, including NO and N/A
- Use exact values: `&quot;YES&quot;`, `&quot;NO&quot;`, or `&quot;N/A&quot;` (uppercase only)
- `gateSignOffs`: only include stages where Reviewer Name AND Date Reviewed are filled; date must be `YYYY-MM-DD`
- The `=== CLASH COORDINATION PLATFORM JSON` delimiter line must appear exactly as shown

---

## What the Platform Does With This JSON

| Field | Platform action |
|---|---|
| `gateItems[]` (Format A) | Adds approved coordinator-reviewed items to the Pre-Clash Gate Checklist |
| `checklistReview.T1[].review = &quot;YES&quot;` | Checkbox ticked |
| `checklistReview.T1[].review = &quot;N/A&quot;` | Checkbox ticked (not applicable, no action needed) |
| `checklistReview.T1[].review = &quot;NO&quot;` | Checkbox unticked; 💬 badge added with coordinator comment |
| `gateSignOffs.T1` | Auto-signs off that gate stage with coordinator name, role, and date |

---

*Platform: BIM Clash Coordination Platform · Prompt 02 v1.1 · 2026-06-24*
</pre>

</details>

Save the entire AI response as a `.txt` file. In the platform, click **📋 Updated Gate Rules** → upload the file.

> Both Step 4 and Step 5 use the same Prompt 02 path. Prompt 02 handles the project-specific gate items table (from Prompt 01) and the full checklist Excel (from Export for Review).

**Step 5 — Review hub defaults with coordinator (optional but recommended)**
Click **📋 Export for Review** → send Excel to coordinator → coordinator fills YES/NO/N/A and signs off → return Excel → Prompt 02 → save as `.txt` → **📋 Updated Gate Rules**.

**Step 6 — Work through the gates**
For each stage T1 → T4: complete the Pre-Clash Gate Checklist (use the discipline filter) → gate unlocks → **⬇ Export CSV** → run Revizto clash detection → log run in the Run Log tab.

**Step 7 — Transfer to another PC (optional)**
Click **⬆ Export Session** to save everything to JSON. On the other PC, click **⬇ Import Session** to restore.

---

## Platform Features

| Feature | What it does |
|---|---|
| T1–T4 Stage tabs | Tasks from your G05 matrix split by coordination stage |
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
