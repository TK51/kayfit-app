# Software Design Specification (SDS)
## Kay Fit App – Updated for GitHub Integration

---

## 1. Document Control

- **Project Name:** Kay Fit App  
- **Version:** 1.1  
- **Author:** [Your Name]  
- **Date:** 2026-01-02  
- **Status:** Approved  

---

## 2. Purpose

Define architecture, modules, functions, libraries, user requirements, and GitHub integration for Kay Fit App.  
This SDS ensures alignment between design and implementation.

---

## 3. Scope

Kay Fit App is a Python-based modular application that generates personalized strength and conditioning programs.

### Features
- Flexible duration: **1–7 cycles (4–28 weeks)**
- Week 0 intake for **RM and ME checks**
- Progressive overload logic for **lifts, gymnastics, and cardio**
- Cardio integration: **bike or skip rope**
- Export options: **PDF and Excel**
- GUI for intake, progress tracking, and program generation
- GitHub-based development workflow with **CI/CD**

---

## 4. System Overview

- **Platform:** Python 3.11+
- **Deployment:** Desktop (`.exe` via PyInstaller)
- **Version Control:** GitHub
- **CI/CD:** GitHub Actions
- **Testing:** pytest
- **Documentation:**  
  - `README.md`  
  - `/docs/API_REFERENCE.md`

---

## 5. Architecture

```text
kayfit_app/
├── core/
│   ├── config.py           # Config-driven constants: RM cycles, gymnastics %, rounding rules
│   ├── planner.py          # Weekly plan generator: combines engine outputs
│   ├── exporter.py         # PDF & Excel export logic
│   ├── utils.py            # Helpers: percentage calculations, rounding logic
│   ├── validator.py        # Data validation for intake and config
│   └── logger.py           # Centralized logging setup
│
├── engine/
│   ├── lifts.py            # RM logic: tables, warm-up & working sets
│   ├── gymnastics.py       # ME scaling logic and set counts per day
│   ├── aux_lifts.py        # Accessory lifts logic and superset integration
│   ├── timing.py           # Timing logic for rounds and cardio intervals
│   ├── percentages.py      # RM & gymnastics percentage cycles
│   └── constructor.py      # Dynamic program builder: goal-based cycle selection
│
├── gui/
│   ├── intake_screen.py    # Week 0 intake form (RMs, ME, constraints)
│   ├── progress_screen.py  # Progress tracking & cycle deltas
│   └── generate_screen.py  # Program generation & export options
│
├── templates/
│   ├── pdf_template.html   # HTML template for PDF export
│   └── excel_template.xlsx # Excel template for export formatting
│
├── output/
│   ├── weekly_pdfs/        # Generated weekly PDFs
│   ├── full_program.pdf   # Full program export
│   └── program.xlsx       # Excel summary export
│
├── docs/
│   ├── architecture/
│   │   ├── diagrams/       # Architecture & data flow diagrams
│   │   └── data_flow.md    # Engine → planner → exporter flow
│   │
│   ├── product/
│   │   ├── concept.md      # Problem statement, philosophy, non-goals
│   │   ├── pitch.md        # Short-form pitch (users / recruiters)
│   │   └── roadmap.md     # Versioned roadmap (v0.x → v1.x)
│   │
│   └── engineering/
│       ├── sds.md          # System Design Specification
│       ├── decisions.md    # Architectural & technical decisions
│       └── risks.md        # Known risks, constraints, mitigation
│
└── tests/
    ├── test_core.py        # Unit tests for core modules
    ├── test_engine.py      # Unit tests for engine logic
    └── test_gui.py         # Unit tests for GUI components


## 6. Key Design Principles

- Config-driven architecture
- Engine modularity
- Planner orchestration
- Validation & logging layer
- GUI separation
- Export layer with templates
- Output organization
- Testing strategy with CI/CD

---

## 7. GitHub Integration

### Repository Structure

- `main` → stable releases
- `dev` → integration branch
- `feature/*` → feature-specific branches

### Project Board

- **Columns:** Backlog | To Do | In Progress | Review | Done
- Tasks mapped to SDS phases

### CI/CD Pipeline

- `test.yml` → runs pytest on push
- `lint.yml` → runs flake8 or black
- `build.yml` → packages app with PyInstaller

### Documentation

- `README.md` → Overview, architecture, roadmap
- `/docs/API_REFERENCE.md` → Full function signatures
- `CONTRIBUTING.md` → Developer guidelines

### Release Management

- GitHub Releases for version tagging
- **Artifacts:**
  - PDF templates
  - Excel templates stored in `/templates`

---

## 8. Functional Requirements

- Week 0 intake for RM and ME values
- Program generation for **4–28 weeks**
- Cardio integration (**bike or rope**)
- Export to **PDF and Excel**
- GUI for intake, progress, and generation

---

## 9. Non-Functional Requirements

- **Performance:** Generate full program in < 2 seconds
- **Usability:** GUI must be intuitive
- **Portability:** Windows executable via PyInstaller
- **Maintainability:** Modular code structure

---

## 10. Libraries & Packages

### Core
- argparse
- logging
- json
- pathlib

### Data
- pandas

### PDF
- WeasyPrint or ReportLab

### Excel
- openpyxl

### GUI
- Tkinter or PyQt

### Packaging
- PyInstaller

### Testing
- pytest

---

## 11. Function Map

> Summarized – full API reference in `/docs`

### core/config.py
- `load_config()`
- `validate_config()`
- `get_rounding_rule()`

### core/planner.py
- `create_week_plan()`
- `generate_full_program()`
- `merge_blocks()`

### engine/timing.py
- `generate_cardio_intervals()`
- `apply_round_timing()`
- `calculate_total_time()`

### engine/lifts.py
- `calculate_rm_table()`
- `generate_lift_cycle()`

### engine/gymnastics.py
- `generate_gymnastics_block()`
- `calculate_gymnastics_reps()`

### gui/intake_screen.py
- `display_intake_form()`
- `save_session_data()`

---

## 12. GUI Requirements

### Screens
- Intake screen (Week 0 data entry)
- Progress tracker
- Generate screen (export options)

### Elements
- **Buttons:** Save Intake, Generate Path
- **Dropdowns:** Goal selection, cardio mode
- **Status indicators:** Completed sessions

---

## 13. Roadmap

### Phase 0: Repo Setup
- Create GitHub repository `kayfit-app`
- Add `.gitignore` (Python template)
- Add `README.md` (from SDS)
- Add `requirements.txt`
- Initialize branch structure (`main`, `dev`)
- Configure GitHub Actions (pytest workflow)

### Phase 1: Core Logic
- Implement `core/config.py`
- Implement `core/utils.py`
- Implement `core/logger.py`
- Implement `core/validator.py`
- Unit tests (`tests/test_core.py`)

### Phase 2: Dynamic Constructor
- Implement `engine/constructor.py`
- Implement `engine/percentages.py`
- Implement `engine/lifts.py`
- Implement `engine/gymnastics.py`
- Implement `engine/aux_lifts.py`
- Unit tests (`tests/test_engine.py`)

### Phase 3: Planner
- Implement `core/planner.py`
- Merge lifts, gymnastics, aux, cardio
- Integrate `generate_cardio_intervals()`
- Validate **4–28 week** generation
- Planner unit tests

### Phase 4: GUI
- Implement intake screen
- Implement progress screen
- Implement generate screen
- Connect GUI to planner/export
- Usability testing

### Phase 5: Export Layer
- Implement `core/exporter.py`
- Add PDF and Excel templates
- Validate formatting
- Integration tests

### Phase 6: Packaging
- Create `setup.py`
- Build `.exe` with PyInstaller
- Configure build pipeline
- Final testing and release tagging
