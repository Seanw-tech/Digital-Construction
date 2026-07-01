# Prompt: Project Report → Updated Gate Rules Analysis

**Version:** 2.4 (updated 2026-07-01 · aligned to Toolkit v2.7)

**How to use:** Copy the full prompt block below. Paste it into a new Claude, Copilot, or ChatGPT session. Attach your project report (PDF, Word, or paste the text). The AI will compare the report against the Hub default checklist, filter duplicates and overlaps, and return only what needs to change — clearly showing what's retained, added, consolidated, or replaced. The output rows map each item onto the existing G05 Item Categories and go straight into the `<ProjectName>_Gate Mapping` tab of your matrix — **that tab is the single source of truth. No standalone CSV file is produced or needed.** In Cowork, the AI writes the rows directly into the tab; in a chat-only tool, paste the rows block into the tab. The coordinator reviews in-tab (Review = YES/NO) and you load everything with one button.

Works with: Mechanical Services Report, Hydraulic Design Report, Acoustic Report, Fire Engineering Report, Structural Report, BEP, Coordination Drawings Package, Specification Sections.

---

## THE PROMPT

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

**Step 4 — Assign attributes & map to the G05 matrix**
For each output item:
- Assign the correct stage (T1/T2/T3/T4)
- Assign the correct discipline code (ARCH, STR, HYD, MEC, ELE, FIR, GEN)
- State the minimum clearance if specified — H (mm) and V (mm) separately. Use null if not specified. Use 0 for hard physical clash (HC).
- Identify the most relevant clash pair (format: DISC vs DISC)
- **Map to the G05 Clash Matrix (per Hub default T1-14):** choose Selection A (row category) and Selection B (column category) from the EXISTING Item Categories only — never invent a new category. Give the Matrix Cell (the row×column intersection, e.g. `V28`) where known. Assign a Rec. Priority (T1–T5) and a Rec. Clearance code (HC / C50 / C100V / C150V / CXXXV).
- Cite the source clause or page number

**Existing G05 Item Categories — use these exact names for Selection A/B:**
ARC_Columns*, ARC_Ceiling, ARC_Doors*, ARC_Gen Model & Casework*, ARC_Roof, ARC_Fire & Acoustic Wall, ARC_Windows, ARC_Services Walkway, ARC_Accessible Path, SRV_Access Panel, ARC_Lighting Fixtures, ARC_Plumbing Fixtures, ARC_SOG Floor Insulation, STR_Seismic Elements, STR_Conc work Excl Floor Slab, STR_Steelwork (Bracing and Columns), STR Floor, HYD_Uninsulated Pipes and Acc, HYD_Pipe Insulation, HYD_Uninsulated Hot and Cold Pipes and Acc, HYD_Hot and Cold Insulation, HYD_Plumbing Fixture, MEC_Air Terminals, MEC_Uninsulated Duct and Acc, MEC_Duct Insulation, MEC_Pipe Insulation, MEC_Uninsulated Pipes and Acc, MEC_Uninulated Flexi duct, MEC_Equipment, ELE_Cable Tray and Fittings, ELE_Conduit*, ELE_Electrical Equip., ELE_Small Devices, ELE_Services Lighting Fixtures, FIR_Fire Pipes, FIR_Sprinklers Heads, FIR_Heat or Smoke Detectors. Items that are process/documentation rather than a spatial clash (e.g. responsibility, as-built) get Rec. Priority T5 and may leave the Matrix Cell blank.

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

## PART 2 — GATE MAPPING ROWS (write straight into the `<ProjectName>_Gate Mapping` tab)

After Part 1, produce the rows that populate the `<ProjectName>_Gate Mapping` tab of the G05 matrix, from row 3 down. **The tab is the deliverable — do not save a standalone CSV/`.csv` file.** In Cowork, write the rows directly into that tab in the workbook. In a chat-only tool, output the block below once so the BIM Manager can paste it into the tab. Either way the matrix `.xlsx` is the only artifact that moves forward; the coordinator fills the `Review (Y/N)` column in the tab (leave `Review (Y/N)` and `Comment` blank when generating).

Use this exact header row, followed by one data row per NEW, SUPPLEMENTED, or SUPERSEDED item:

```
Gate ID,Stage,Disc,Status,Proposed Gate Item,Selection A (row category),Selection B (col category),Matrix Cell,Rec. Priority,Rec. Clearance,H (mm),V (mm),Clash Pair,Source,Review (Y/N),Comment
GR-T1-01,T1,STR,NEW,[item text],STR_Seismic Elements,HYD_Uninsulated Hot and Cold Pipes and Acc,V28,T3,CXXXV,,,HYD vs STR,[Section X.X],,
GR-T2-03,T2,MEC,SUPPLEMENTED,[item text],ARC_Fire & Acoustic Wall,MEC_Uninsulated Duct and Acc,Z12,T2,C50,250,250,MEC vs FIR,[Section X.X],,
```

CSV rules:
- Gate ID format `GR-<stage>-<nn>` (e.g. GR-T2-03)
- Status is one of: NEW, SUPERSEDED, SUPPLEMENTED
- Selection A / Selection B must be exact existing Item Category names (see Step 4 list) — existing categories only
- Matrix Cell is the row×column intersection (e.g. V28) if known, else leave blank
- Rec. Priority is T1–T5; Rec. Clearance is HC / C50 / C100V / C150V / CXXXV, or `-`
- H and V are in millimetres; leave blank if not specified
- If any field contains a comma, wrap it in double quotes
- `Review (Y/N)` and `Comment` are intentionally blank — the coordinator fills them in the matrix tab
- When output as a block (chat-only tools), give it with no extra text above or below so it pastes cleanly into the tab — but never save it as a separate `.csv` file; the matrix tab holds the rows

---

## PART 3 — (ALTERNATIVE / LEGACY) AWAIT COORDINATOR REVIEW THEN CONVERT TO JSON

> Primary path is Part 2: the rows live in the `<ProjectName>_Gate Mapping` tab and you upload the matrix once. Part 3 (JSON) remains only for cases where you need the AI to process sign-off detail, or a chatbot that cannot write the matrix tab cleanly. The retired standalone-CSV file path (`GateReview.csv`) is no longer used — the reviewed matrix tab is read directly.

After the rows are in the tab, add this message:

---
Gate mapping rows are in the `<ProjectName>_Gate Mapping` tab.

**Next step (recommended):** The coordinator sets `Review (Y/N)` per row in that tab and returns the workbook; you then click **📂 Upload Project Matrix and Update Gate Rules** once to load the matrix and the approved gate rules together — one file, no separate CSV.

**Legacy fallback (only if the one-button upload is unavailable):** re-attach the reviewed matrix `.xlsx` here and I will convert the Review = YES rows to platform JSON.
---

When the user attaches the completed Excel in this session, process it as follows — do not wait for further instructions:

- Detect the format: if column headers contain "Proposed Gate Item" and "Status" → Format A (coordinator-reviewed Prompt 01 table)
- For each row where REVIEW = YES: extract Stage, Disc, Proposed Gate Item, Status, H (mm), V (mm), Source, Replaces Hub Default
- For each row where REVIEW = NO or N/A: exclude from JSON
- Extract sign-off details if present (Reviewer Name, Role, Date, Comments)
- Output PART 1 — Review Summary (YES/NO/N/A counts per stage, list of NO items)
- Output PART 2 — Platform JSON preceded by this exact delimiter line:

=== CLASH COORDINATION PLATFORM JSON — PASTE INTO UPDATED GATE RULES ===

Output a single valid JSON object with this structure:

{
  "project": "[project name from report]",
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

JSON rules:
- Only include items where REVIEW = YES
- "stage" must be exactly one of: T1, T2, T3, T4
- "discipline" must be exactly one of: ARCH, STR, HYD, MEC, ELE, FIR, GEN
- "clearanceH" and "clearanceV" must be integers in millimetres, or null if not specified
- "status" must be exactly one of: NEW, SUPERSEDED, SUPPLEMENTED
- "replacesDefault" is the Hub default ID (e.g. "T1-05") or null if NEW
- Only include gateSignOffs entries where Reviewer Name AND Date are both filled; date must be YYYY-MM-DD
- The JSON must be valid — no trailing commas

---

```

---

## What to Do with the Output

**Step 1 — Review Part 1**
Check the Rule Status Summary. Note any SUPERSEDED Hub defaults — these are flagged automatically in the platform once the gate items load.

**Step 2 — Paste the Part 2 rows into the matrix**
Copy the Part 2 CSV block into the `<ProjectName>_Gate Mapping` tab of your G05 matrix, starting at row 3 (rename the blank `ProjectName_Gate Mapping` tab that ships in the template matrix). Selection A/B map onto existing Item Categories only. Send the workbook to the Services Coordinator.

**Step 3 — Coordinator reviews in the tab**
The coordinator sets `Review (Y/N)` per row directly in the tab, adds comments, and returns the workbook — the tab doubles as the sign-off sheet.

**Step 4 — Upload once (recommended)**
In the platform, click **📂 Upload Project Matrix and Update Gate Rules** → select the workbook. One upload rebuilds all T1–T4 tasks from the matrix **and** injects every `Review = YES` gate item from the Gate Mapping tab. No separate file, no JSON, no chatbot schema variation.

> **Alternatives / fallback:** a standalone reviewed `GateReview.csv` still works via the hidden legacy import; the AI-JSON route (Part 3, saved as `.txt`) remains for sign-off detail; and if this session was closed, use `02_ChecklistReview_Import.md` (Prompt 02) in a new session.

---

## Tips for Best Results

- **Attach the full document** — don't paste summaries. The AI reads the source directly.
- **For large reports (50+ pages)**, add: *"Focus on Sections [X] and [Y] first. Note any other relevant clauses you encounter."*
- **For acoustic reports**, add: *"Pay particular attention to wall build-up specifications, penetration isolation requirements, and minimum separation distances between service penetrations and acoustic-rated elements."*
- **For structural reports**, add: *"Identify all transfer zones, post-tensioned slab areas, load-bearing wall locations, and any engineer-specified clearance zones around structural elements."*
- **For BEPs**, add: *"Extract modelling standards, workset naming conventions, and any coordination-specific requirements that affect how selection sets should be named in Revizto."*
