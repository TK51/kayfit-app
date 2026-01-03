# KayFit App – Data Flow

## Overview
This document describes how user input is transformed into a structured training program
and exported into user-facing formats (PDF, Excel).

The system is intentionally linear:
Intake → Validation → Program Construction → Planning → Export.

No hidden state. No magic.

---

## 1. User Intake (GUI)

**Source**
- `gui/intake_screen.py`

**Input**
- 1RM / max reps (Week 0)
- Gymnastics max-effort data
- Training constraints (days/week, goal, equipment)

**Output**
- Raw user data object (unvalidated)

---

## 2. Validation & Normalization

**Source**
- `core/validator.py`
- `core/config.py`

**Responsibilities**
- Validate numeric ranges (RMs, reps, percentages)
- Apply rounding rules
- Enforce config constraints (allowed cycles, % bands)

**Output**
- Normalized intake payload
- Validation errors (if any)

---

## 3. Program Construction (Engine)

**Source**
- `engine/constructor.py`

**Responsibilities**
- Select RM cycle based on goal
- Select gymnastics scaling logic
- Combine lifts, gymnastics, auxiliaries, timing

**Uses**
- `engine/lifts.py`
- `engine/gymnastics.py`
- `engine/aux_lifts.py`
- `engine/percentages.py`
- `engine/timing.py`

**Output**
- Structured training model (weeks → days → movements)

---

## 4. Weekly Planning

**Source**
- `core/planner.py`

**Responsibilities**
- Split program into weekly blocks
- Apply day-specific logic (intensity, volume)
- Prepare export-ready structures

**Output**
- Weekly plans
- Full program plan

---

## 5. Export

**Source**
- `core/exporter.py`
- `templates/`

**Formats**
- PDF (HTML → PDF)
- Excel summary

**Output**
- `/output/weekly_pdfs/*.pdf`
- `/output/full_program.pdf`
- `/output/program.xlsx`

---

## Data Flow Summary
GUI Intake
↓
Validator / Config
↓
Engine Constructor
↓
Planner
↓
Exporter
↓
User Files


---

## Design Notes
- All transformations are deterministic.
- No module mutates global state.
- Output can always be regenerated from intake + config.

