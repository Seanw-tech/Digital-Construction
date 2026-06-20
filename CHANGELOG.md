# BIM Clash Coordination Toolkit — Changelog

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
