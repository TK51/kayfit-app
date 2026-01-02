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
│   ├── config.py        # Config-driven constants
│   ├── planner.py       # Weekly plan generator
│   ├── exporter.py      # PDF & Excel export
│   ├── utils.py         # Helpers (rounding, % calc)
│   ├── validator.py     # Data validation
│   ├── logger.py        # Logging setup
├── engine/
│   ├── lifts.py         # RM logic
│   ├── gymnastics.py    # ME scaling
│   ├── aux_lifts.py     # Accessory lifts
│   ├── timing.py        # Round timing & cardio intervals
│   ├── percentages.py   # RM & gymnastics % cycles
│   ├── constructor.py   # Dynamic program builder
├── gui/
│   ├── intake_screen.py # Week 0 intake
│   ├── progress_screen.py
│   ├── generate_screen.py
├── templates/
│   ├── pdf_template.html
│   └── excel_template.xlsx
├── output/
│   ├── weekly_pdfs/
│   ├── full_program.pdf
│   └── program.xlsx
└── tests/
    ├── test_core.py
    ├── test_engine.py
    ├── test_gui.py
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
