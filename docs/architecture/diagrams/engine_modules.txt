# Engine Module Relationships

## Overview
The engine layer is responsible for constructing a complete training program
from validated user input and configuration rules.

The engine is composition-based, not hierarchical.
`constructor.py` orchestrates logic; it does not calculate everything itself.

---

## Module Responsibilities

### constructor.py (Orchestrator)
- Entry point for program construction
- Selects cycles and logic paths based on goals
- Aggregates outputs into a unified training model

Depends on:
- lifts.py
- gymnastics.py
- aux_lifts.py
- percentages.py
- timing.py

---

### lifts.py
Purpose:
- RM-based calculations
- Warm-up sets
- Working sets per lift

Inputs:
- 1RM values
- Percentage tables
- Rounding rules

Outputs:
- Structured lift sets (weight, reps, sets)

---

### gymnastics.py
Purpose:
- Max-effort (ME) scaling
- Bodyweight movement prescription

Inputs:
- ME intake data
- Gymnastics percentage cycles

Outputs:
- Rep targets per movement and day

---

### aux_lifts.py
Purpose:
- Accessory lift logic
- Superset pairing
- Volume balancing

Inputs:
- Main lift context
- Goal-based accessory rules

Outputs:
- Auxiliary movement blocks

---

### percentages.py
Purpose:
- Centralized percentage definitions
- RM cycles
- Gymnastics cycles

Used by:
- lifts.py
- gymnastics.py

---

### timing.py
Purpose:
- Rest intervals
- Time caps
- Cardio interval timing

Outputs:
- Timing metadata attached to sets or blocks

---

## Dependency Direction

percentages
   |
   +--> lifts -----------+
   |                     |
   +--> gymnastics -----+|
   |                    ||
   +--> timing          ||
                         +--> constructor
aux_lifts ---------------+

---

## Design Constraints
- No engine module imports GUI code
- No engine module imports exporter code
- No circular dependencies
- Constructor coordinates, modules calculate
