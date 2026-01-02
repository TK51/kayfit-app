# Kay Fit App
Cycle-Based Strength & Conditioning Program Generator

## Overview
Kay Fit App is a modular Python application that generates personalized strength and conditioning programs based on Week 0 intake data (RM checks for lifts and ME checks for gymnastics). It supports dynamic program construction, goal-based adaptation, and export to PDF/Excel.

**Key Features**
- Week 0 intake for RM and ME checks
- Flexible duration: 1–7 cycles (4–28 weeks)
- Progressive overload logic for lifts, gymnastics, and cardio
- Cardio integration: bike or skip rope
- Export options: PDF and Excel
- GUI for intake, progress tracking, and program generation

---


## Architecture
```
kayfit_app/
├── core/
│   ├── config.py          # Config-driven constants: RM cycles, gymnastics %, rounding rules
│   ├── planner.py         # Weekly plan generator: combines engine outputs
│   ├── exporter.py        # PDF & Excel export logic
│   ├── utils.py           # Helpers: percentage calculations, rounding logic
│   ├── validator.py       # Data validation for intake and config
│   ├── logger.py          # Centralized logging setup
├── engine/
│   ├── lifts.py           # RM logic: table generation, warm-up & working sets
│   ├── gymnastics.py      # ME scaling logic and set count per day
│   ├── aux_lifts.py       # Accessory lifts logic and superset integration
│   ├── timing.py          # Timing logic for rounds and cardio intervals
│   ├── percentages.py     # RM & gymnastics percentage cycles
│   ├── constructor.py     # Dynamic program builder: goal-based cycle selection
├── gui/
│   ├── intake_screen.py   # GUI for Week 0 intake form
│   ├── progress_screen.py # GUI for progress tracking
│   ├── generate_screen.py # GUI for program generation and export options
├── templates/
│   ├── pdf_template.html  # HTML template for PDF export
│   └── excel_template.xlsx # Excel template for export formatting
├── output/
│   ├── weekly_pdfs/       # Folder for individual weekly PDFs
│   ├── full_program.pdf   # Placeholder for full program PDF
│   └── program.xlsx       # Placeholder for Excel summary
└── tests/
    ├── test_core.py       # Unit tests for core modules
    ├── test_engine.py     # Unit tests for engine logic
    ├── test_gui.py        # Unit tests for GUI components
```

## Roadmap
**Phase 0: Repo Setup**
- Create GitHub repository
- Add `.gitignore` (Python template)
- Add README.md (this file)
- Add `requirements.txt`
- Initialize branch structure (`main`, `dev`)
- Configure GitHub Actions for CI/CD (pytest workflow)

**Phase 1: Core Logic**
- Implement config, utils, logger, validator
- Add unit tests for core modules

**Phase 2: Dynamic Constructor**
- Implement engine logic for lifts, gymnastics, percentages
- Add unit tests for engine modules

**Phase 3: Planner**
- Implement weekly plan generator
- Validate full program generation

**Phase 4: GUI**
- Intake, progress, and generation screens

**Phase 5: Export Layer**
- PDF & Excel export functionality

**Phase 6: Packaging**
- Build executable and configure CI/CD for release

---

## How to Run MVP
```bash
# Clone repo
git clone https://github.com/<your-org>/kayfit-app.git
cd kayfit-app

# Install dependencies
pip install -r requirements.txt

# Run MVP (CLI)
python main.py --goal strength --cycles 1 --cardio rope


Requirements

Python 3.11+
pandas
pytest (for tests)
(Future) WeasyPrint, openpyxl, PyInstaller


License
MIT License
