# BIM Clash Coordination Toolkit — Changelog

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
