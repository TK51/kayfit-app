# Roadmap
### version 1.0

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
