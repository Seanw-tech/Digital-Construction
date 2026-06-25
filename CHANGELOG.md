# BIM Clash Coordination Toolkit — Changelog

---

## v2.4 — 2026-06-25

### Audit fixes
- **Prompt 01 v2.2:** Removed stale Part 4 (old JSON Reference section, now superseded by Part 3 single-session workflow). Updated "What to Do" section: Steps 2 and 3 now match the current CSV → attach-to-same-session workflow; Prompt 02 demoted to fallback only.
- **Prompt 02 v1.2:** Removed reference to the deleted "Export for Review" button. Updated purpose block to clearly state it is a fallback for when the original Prompt 01 session is closed; How to Use steps revised to match CSV-based workflow.
- **README:** Removed stale "Export for Review path" note from Step 4c; replaced with accurate fallback note about Prompt 02.
- **Platform v2.3:** Checklist now sorted GEN > ARCH > STR > MEC > HYD > ELE > FIR on page load (previously only sorted after gate items were injected).

---

## v2.3 — 2026-06-25

### Platform
- Checklist discipline sort (GEN > ARCH > STR > MEC > HYD > ELE > FIR) now runs on page load via `init()` in addition to after gate item injection — hub default items are now correctly ordered before any project items are uploaded.

---

## v2.2 — 2026-06-25

### Platform
- Hub default checklist items are now visually marked when a project gate item references them via `replacesDefault` / `replaces_relates`:
  - **SUPERSEDED** → item dims to 45% opacity, label gets strikethrough, red left border, and a red **SUPERSEDED** badge (hover for tooltip)
  - **SUPPLEMENTED** → amber left border and an amber **MODIFIED** badge indicating a project supplement applies
- Project items are never marked — only the referenced hub defaults are affected
- Dark theme variants added for both states

---

## v2.1 — 2026-06-25

### Platform — Hotfix
- Updated Gate Rules upload now handles `data.project` being an object (AI sometimes returns it as `{name, project_no, ...}` instead of a plain string) — extracts `.name` field; no longer crashes with `.substring is not a function`
- Upload now accepts the alternate AI JSON schema where gate items are under `data.items[]` with fields `gate_item` (instead of `item`), `clearance.h_mm` / `clearance.v_mm` (instead of `clearanceH` / `clearanceV`), and `clash_pair` (instead of `clashPair`) — both schemas now work interchangeably

---

## v2.0 — 2026-06-25

### Workflow
- Single-session review: Prompt 01 now outputs Gate Items as CSV (save as GateReview.csv, open in Excel) — eliminates the copy-paste markdown table step
- Reviewed Excel attaches to the **same** Prompt 01 session — no new session, no Prompt 02 copy-paste; AI auto-detects the attachment and outputs JSON directly
- JSON conversion logic (formerly Part 3) embedded in Prompt 01 — Prompt 02 now covers only the legacy Export for Review path

### Platform
- Checklist items injected via Updated Gate Rules now show a status badge:
  - **NEW** (green) — coordinator-approved items not in the hub defaults
  - **UPDATED** (amber) — items with status SUPPLEMENTED or SUPERSEDED (modifies an existing hub default)
- Hover tooltip on each badge shows the full status and description
- `📋 Export for Review` button removed from header — workflow now routes through single-session CSV/AI path
- G05 Clash Detection Matrix (`DIG_G05_Clash_Detection_Matrix.xlsx`) removed from push script — file is confidential and must not be published to the public repository

### Prompts
- `01_ProjectReport_ClashGate_Analysis.md` updated: Part 2 changed from markdown table to CSV format with exact column headers for Excel; Part 3 rewritten as "Await Coordinator Review then Convert to JSON" — AI waits for reviewed Excel to be attached in the same session before outputting JSON; JSON schema for Format A (gateItems[]) embedded directly in prompt
- `02_ChecklistReview_Import.md` restructured: steps reorganised as Step 2A / 2B / 2C to remove duplicate step blocks introduced by a previous editing error

### README
- Rewritten as pure markdown (no HTML blocks) — fixes GitHub rendering where `<details>` + `<pre>` broke the entire parser and showed headers as `# text` and bold as `**text**`
- Prompts linked as clickable file references instead of embedded content
- Step 5 (hub defaults review) removed — no longer a required workflow step
- Step text updated: "select your G05 Excel" → "select your company clash matrix"

### Other
- `Clash_Coordination_Workflow.svg` updated with swimlane diagram showing Digital Engineering Team and Pre Construction Team (Structure & Services) responsibilities with handoff arrows

---

## v1.9 — 2026-06-24

### Platform
- Import Review button removed — replaced by AI-mediated workflow (Prompt 02 below)
- `loadClaudeOutput` (Updated Gate Rules button) now handles two additional JSON fields:
  - `checklistReview` — updates checkbox states per item (YES/N/A = ticked, NO = unticked with comment badge)
  - `gateSignOffs` — auto-signs off a stage gate when coordinator name and date are present
- Comment badge (💬) added inline on checklist items where coordinator entered a NO with a reason — hover to read full text

### Prompts
- `01_ProjectReport_ClashGate_Analysis.md` updated to v2.1: added Part 2 (Gate Items Review Table) output — Excel-ready table of proposed NEW/SUPPLEMENTED/SUPERSEDED items for coordinator sign-off before entering the platform; JSON moved to Part 3 and marked as reference only
- `02_ChecklistReview_Import.md` added (v1.1) — handles two input formats: (A) Prompt 01 gate items review table (coordinator-approved items -> gateItems[]) and (B) Export for Review hub defaults Excel (checklistReview{} + gateSignOffs{}); both go through Updated Gate Rules

---

## v1.8 — 2026-06-20

### Platform
- Button renamed: "Additional Gate Rules" → "Updated Gate Rules"
- Header layout fixed: white-space:nowrap on btn-io and btn-theme; button row set to flex-wrap:nowrap — no more text wrapping
- Upload Matrix and Updated Gate Rules buttons moved from header to Revizto Clash Task Output card header in all four stage panels (T1–T4) — buttons now sit parallel to the checklist at stage level; hidden file inputs remain in DOM for JavaScript targeting
- A3 landscape layout: body/main/stage-panel now use full-height flex column chain (height:100vh, overflow:hidden); Gate Checklist and Clash Task table scroll within fixed-height panels; all chrome elements (card-header, toolbar, filter row, stats, signoff) set to flex-shrink:0; Rules tab and Run Log wrapped in scrollable containers; footer and nav also flex-shrink:0; page no longer grows vertically
- Updated Gate Rules upload now accepts the full AI response file (not just the extracted JSON block) — parser tries JSON.parse first, then searches for the `=== CLASH COORDINATION PLATFORM ===` delimiter, then falls back to first-`{`/last-`}` extraction; works with Claude, Copilot, and ChatGPT output formats

### Prompts
- `01_ProjectReport_ClashGate_Analysis.md` rewritten as v2.0: full Hub default reference (T1–T4, 58 items) embedded in prompt; AI compares extracted items against defaults and assigns RETAINED / SUPERSEDED / SUPPLEMENTED / NEW status; Part 1 output now includes Rule Status Summary table; JSON updated with `status` and `replacesDefault` fields; deprecated `overrides` and `customTasks` removed; discipline codes corrected to ARCH

---

## v1.7 — 2026-06-20

### Platform
- Dark / Light theme toggle added to header (🌙 Dark / ☀️ Light button) — preference persisted in localStorage
- Full dark theme CSS overrides implemented across all structural elements (header, nav, cards, tables, modals, forms, checklist, log)
- Rules tab dark overrides fixed: discipline-pair gap matrix, clearance breakdown chips, info box, service rules lists, project notes textarea
- Matrix cell colours now theme-aware (pastel for light, vivid for dark) via `getSTYLE()` function
- README updated to v1.6 (missed in previous push)

---

## v1.6 — 2026-06-20

### Platform
- Gate Sign-Off added to all four stage checklists (T1–T4): Services Coordinator signs off each gate before CSV export and clash detection can proceed
- Sign-off modal records name, role, date, and optional comment — persisted in localStorage and session export/import
- Sign-off badge appears in checklist card header once a stage is signed off
- CSV Export now shows a warning toast if the stage has not been signed off
- `revokeSignOff()` function allows sign-off to be corrected without losing checklist state
- Execution map revised: Services Coordinator (Step 2) signs off gate before BIM Coordinator (Step 3) runs clash detection
- **📋 Export for Review** button added to header — generates a formatted Excel file (one sheet per stage) with all gate checklist items pre-populated and a sign-off block at the bottom; intended for Services Coordinator offline review without needing to open the platform

### Prompts
- `01_ProjectReport_ClashGate_Analysis.md` updated: added full default checklist (T1–T4) as reference for AI to compare against before adding new items
- Added instruction to avoid duplicating existing default items and to flag outdated/superseded defaults
- Added "Checklist Review — Existing Default Items to Flag" table to PART 1 output

---

## v1.5 — 2026-06-20

### Workflow
- Added `UPDATE_PROTOCOL.md` — standing reference for the version-controlled update process; defines the 5-step protocol Claude follows before every push
- Rewrote `push_to_github.ps1` — single `$VERSION`/`$CHANGES` header at the top; all 6 files now share one consistent commit message; added pre-push file existence check and Y/N confirmation prompt; added links to live site and commit history on completion
- Updated Digital Construction `CLAUDE.md` — added Update Protocol section so Claude automatically follows the correct steps in every session
- Updated `README.md` — version bumped to 1.5, last-updated date corrected

---

## v1.4 — 2026-06-20

### Platform
- Pre-Clash Gate Checklist: added discipline filter dropdown (ARCH / STR / HYD / MEC / ELE / FIR / GEN) across all four stages
- Gate items from Claude/Copilot/ChatGPT JSON upload now inject directly as checkboxes into the correct stage checklist (highlighted with blue left border)
- Project gate items persist in localStorage and survive page reload and session export/import
- Removed clash task override processing from the Claude output upload — overrides must be made in the G05 matrix
- Toast messages updated to reflect gate item count only (no override count)

### Checklists (Framework Alignment)
- T4 cleaned: removed 4 misplaced items (firewall layout, fire rating of steel, grilles/louvres alignment, service penetration placeholders); T4 renumbered to 9 items
- T1: added T1-19 (STR — fire rating of steel through fire walls)
- T2: added T2-23 (ARCH — firewall layout verified against fire report)
- T3: added T3-20 (MEC — grilles aligned with louvres), T3-21 (MEC — service penetration placeholders)

### Colours & Tags
- HC clearance badge changed to red (`#7f1d1d / #fca5a5`)
- C600V clearance badge changed to green (`#064e3b / #6ee7b7`)
- All fire discipline tags standardised to `.disc-FIR` / `FIR` (red `#b91c1c`) — `.disc-FIRE` removed

### Prompts
- `01_ProjectReport_ClashGate_Analysis.md` updated: removed Clash Task Overrides and New Custom Clash Tasks sections; JSON schema simplified to `gateItems` + `procurementFlags` + `projectNotes`; prompt rewritten for cross-platform compatibility (Claude / Copilot / ChatGPT)

---

## v1.2 / v1.3 — 2026-06-19

### Platform
- Parsing helpers (`parseSheetRows`, `toCode`, `CLR_HV`, `catToStage`, `parseWorkbook`) extracted to top level — both upload and auto-load use identical logic
- HC and C600V colours updated throughout (CSS badges + gap matrix STYLE object + legend)
- `disc-FIRE` standardised to `disc-FIR` across platform HTML and all local copies

---

## v1.0 — 2026-06-16

**Initial release.**

### Platform
- T1–T4 staged clash task dashboard built from DIG_G05 matrix (425 active tasks)
- Pre-clash gate checklists per stage, sourced from DIG_G08 Services & General Model Checklist
- Gate status indicator (Locked / Partial / Open)
- Discipline and clearance filters
- ✏️ Task override — edit clearance code, H/V values, priority, reason note per task
- ＋ Custom task — add project-specific clash pairs not in the standard matrix
- 📐 Rules & Standards tab — NZS4219:2009 seismic table, clearance code reference, discipline-pair gap matrix, service-specific rules, project notes field
- 📂 Upload Updated Matrix — SheetJS-powered Excel upload, auto-rebuilds all tasks
- ⬇ Export CSV — Revizto-ready, includes overrides, custom tasks, type flag, notes
- Run Log — coordination session history with export
- All overrides, custom tasks, and project notes auto-saved in browser localStorage

### Prompts
- `01_ProjectReport_ClashGate_Analysis.md` — Analyse any project services report and extract T1–T4 gate rules, clearance overrides, custom tasks, and procurement flags
- `02_NewProject_Setup.md` — Configure the platform for a new project

### Framework
- Coordination staged framework (T1–T4) aligned to NZS4219:2009
- Clearance codes: HC, C50, C100V, C150V, C600V, C1500

---

## Project Deployments

_Record each project that uses this toolkit. Add a row when you deploy._

| Project Code | Project Name | Deployed | Matrix Version | Platform Version | BIM Lead | Notes |
|---|---|---|---|---|---|---|
| NL | NL Project (pilot) | 2026-06-16 | G05 v1 | v1.0 | Sean Wang | Pilot project — toolkit built from this project's documents |

---

## Planned Improvements

- [ ] Gate checklist items editable from within the platform (project-specific additions without needing Claude)
- [ ] Multi-project view — compare coordination status across projects
- [ ] Revizto API integration — auto-sync issue status back to platform
- [ ] Seismic restraint zone visualiser linked to NZS4219 table
