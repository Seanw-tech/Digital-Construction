# Prompt: Project Report → Updated Gate Rules Analysis

**Version:** 2.0 (updated 2026-06-20)

**How to use:** Copy the full prompt block below. Paste it into a new Claude, Copilot, or ChatGPT session. Attach your project report (PDF, Word, or paste the text). The AI will compare the report against the Hub default checklist, filter duplicates and overlaps, and return only what needs to change — clearly showing what's retained, added, consolidated, or replaced.

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

---

## What to Do with the Output

**Step 1 — Review Part 1**
Check the Rule Status Summary. Note any SUPERSEDED Hub defaults — these will be handled when the coordinator's review comes back.

**Step 2 — Send Part 2 to the coordinator for review**
Copy the Gate Items Review Table (Part 2) into Excel and send it to the Services Coordinator. The coordinator fills in YES / NO / N/A for each proposed item, adds comments, and signs the bottom.

**Step 3 — Run Prompt 02 after review**
Once the coordinator returns the completed Excel, use **Prompt 02** (`02_ChecklistReview_Import.md`) to convert it to JSON. Save the AI response as `.txt` → upload via **📋 Updated Gate Rules** in the platform. The platform adds approved items to the gate checklist.

> **Part 3 JSON** is included for reference or advanced use. The recommended path is always Part 2 → coordinator review → Prompt 02 → platform.

If items don't load: ask the AI: *"Please recheck the JSON block and output a corrected version with no trailing commas and all string values in double quotes."*

---

## Tips for Best Results

- **Attach the full document** — don't paste summaries. The AI reads the source directly.
- **For large reports (50+ pages)**, add: *"Focus on Sections [X] and [Y] first. Note any other relevant clauses you encounter."*
- **For acoustic reports**, add: *"Pay particular attention to wall build-up specifications, penetration isolation requirements, and minimum separation distances between service penetrations and acoustic-rated elements."*
- **For structural reports**, add: *"Identify all transfer zones, post-tensioned slab areas, load-bearing wall locations, and any engineer-specified clearance zones around structural elements."*
- **For BEPs**, add: *"Extract modelling standards, workset naming conventions, and any coordination-specific requirements that affect how selection sets should be named in Revizto."*
