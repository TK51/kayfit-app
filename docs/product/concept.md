# Kay Fit App
Cycle-Based Strength & Conditioning Program Generator

## 1. Overview
Kay Fit App is a modular Python application that generates a customized 28-week strength and conditioning program based on Week 0 intake data (RM checks for lifts and ME checks for gymnastics).

**Features:**
- Dynamic program construction
- Goal-based adaptation
- Export options: PDF & Excel

## 2. Program Structure
- Type: Cycle-based strength & conditioning
- Duration: Up to 28 weeks (+ Week 0 for intake/testing)

## 3. Week 0 – Intake Phase
**Purpose:** Establish baseline ME (Max Effort) for gymnastics/bodyweight and RM (Rep Max) for lifts. This data drives all percentage-based calculations for Weeks 1–28.

**Rules:**
### Gymnastics ME Check
- Day 1: 100% effort = 1 round of 100% Effort in each exercise tested once
- Day 2: 2 rounds @ 20% ME
- Day 3: 3 rounds @ 20% ME
- Each round = all gymnastics + auxiliary moves consecutively
- Each round ends with SU count (sum of reps)
- Order of exercises fixed during Week 0 and replicated across all weeks

### RM Check for Lifts
- All main & auxiliary lifts tested across 3 days (2 main lifts + 3 auxiliary per day)
- Range: 3–5 RM for accurate 1RM calculation

**Rest intervals:**
- Main lifts: R10 × 1:00–1:30
- Aux lifts: R5 × 1:00–1:30

**Order of Exercises:**
- Set during Week 0 and mimicked across Weeks 1–28 for consistency (subject to automation)

### Cardio Integration
- Supports bike intervals or skip rope (Single Unders)
- Three-day pattern per week:
  - Day 1: 4 rounds × work/rest (Week 1 = 0:15 / 0:30)
  - Day 2: 3 rounds × work/rest (Week 1 = 0:20 / 0:40)
  - Day 3: 2 rounds × work/rest (Week 1 = 0:30 / 1:00)
- Progression logic: Work duration increases by +5 sec per week for 4-week cycles; rest intervals remain constant
- Skip Rope Mode: Work time converted to estimated reps (~2 skips/sec; 20 sec ≈ 40 skips)
- Fully automated in engine/timing.py via `generate_cardio_intervals()`
- Returns rounds, work/rest times, and rope rep estimates for export

## 4. Weekly Flow (Weeks 1–28)
**Day Structure:**
- Warm-Up: 3–5 min
- Gymnastics: 3–5 rounds at % of ME (Day 1:3, Day 2:4, Day 3:5 rounds)
- Main Lifts:
  - Lift 1: 2 warm-up + 3+ working sets @ % of RM
  - Lift 2: same logic
  - Mixed with auxiliary gymnastics, same number of sets as main lifts
- Aux Lifts: Superset of 3 lifts (3:00 per round)
- Cardio: Bike intervals for recovery
- Cool-Down: 2–5 min free form

## 5. Progression Logic
- RM Cycles: 12RM → 10RM → 8RM → 6RM → 4RM → 2RM → 1RM
- Weekly % Pattern: W1=65%, W2=75%, W3=70%, W4=80%
- Gymnastics Scaling: Auto-calculated from Week 0 ME values

## 6. Exercise Pools
**Main Gymnastics (6):** Pull-Ups, Ring Dips, Chin-Ups, Push-Ups, Abs Bar, Abs Ring  
**Aux Gymnastics (5):** Kneeling Ring Pull-Ups (D1), Bench Dips (D1), Hollow Hold (D2), Sit-Ups (D2), Ring Pull-Ups (D3), Bench Dips (D3)  
**Main Lifts (6):** Bench Press (D1), Back Squat (D1), Barbell Rows (D2), Deadlift (D2), Push Press (D3), Front Squat (D3)  
**Aux Lifts (9):** Snatch Shoulder Press (D1), Shoulder Front Pulls (D1), Biceps Curls (D1), DB Bulgarian Split (D2), DB Goblet Squat (D2), Good Mornings (D2), DB Pullover (D3), DB Flies Bench (D3), DB Lateral Shoulder Raises (D3)  
**Cardio:** Bike, Single Unders

## 7. Load & Percentage Rules
**RM Cycles & Weekly Loads:**  
12RM–1RM: W1 65%, W2 75%, W3 70%, W4 80%  
**Warm-Up Sets:** 2 sets at −25% and −15% of target %  
**Working Sets:**  
- 12RM & 10RM → 3 sets  
- 8RM & 6RM → 4 sets  
- 4RM & 2RM → 5 sets  
- 1RM → 5–6 sets  

**Main Lifts Mixed Rounds:** MAIN LIFT + AUX Gymnastics move (calculated from Week 0)  
- Push/pull pairing logic to avoid fatigue  
- Aux Lifts: Always 3 sets, no warm-up  

**Gymnastics & AUX % per cycle:**  
12RM → 30%,40%,35%,45%  
10RM → 35%,45%,40%,50%  
8RM → 40%,50%,45%,55%  
6RM → 45%,55%,50%,60%  
4RM → 40%,50%,45%,40%  
2RM → 35%,45%,40%,35%  
1RM → 30%,40%,35%,30%  

**Sets per Day:** D1 → 3, D2 → 4, D3 → 5  

**Cardio Pattern:**  
- D1: 4 rounds × work/rest (0:15 / 0:30)  
- D2: 3 rounds × work/rest (0:20 / 0:40)  
- D3: 2 rounds × work/rest (0:30 / 1:00)  
- Work increases +5 sec per week; rest constant

## 8. Timing Rules
- Gymnastics round = max(1, number_of_exercises − 1) min (6 moves → 5 min)  
- Main lifts & aux lifts = 3:00 per round

## 9. Scoring
- Single Unders counted per round as sum of all part 1 reps per round (gymnastics W1–28 or W0 bodyweight)

## 10. Rounding Rules
- Floor rounding applied to all loads  
- Configurable per lift in `config.py`  

```python
ROUNDING_RULES = {
"Bench Press": 2.5,
"Back Squat": 2.5,
"Deadlift": 2.5,
"Push Press": 2.5,
"Front Squat": 2.5,
"Barbell Rows": 2.5,
"Snatch Shoulder Press": 2.0,
"Shoulder Front Pulls": 2.0,
"Biceps Curls": 2.5,
"DB Bulgarian Split": 1.0,
"DB Goblet Squat": 1.0,
"Good Mornings": 2.5,
"DB Pullover": 1.0,
"DB Flies Bench": 1.0,
"DB Lateral Shoulder Raises": 1.0
}

## 11. Outputs
- Full program PDF
- Weekly PDFs
- Excel summary

## Roadmap (with Cardio Integration & Multi-Mode Support)

**Phase 0: Repo Setup**
- Create GitHub repo
- Add README.md, requirements.txt, .gitignore

**Phase 1: Core Logic**
- Implement config.py (exercise pools, RM cycles, gymnastics %, rounding rules)
- Engine modules: lifts, gymnastics, timing, percentages
- Add generate_cardio_intervals() for bike/rope modes

**Phase 2: Dynamic Constructor**
- Goal-based cycle selection (Conditioning, Force, Muscle)
- Exercise selection & ordering logic

**Phase 3: Planner**
- Generate full program (1–7 cycles, 4–28 weeks)
- Merge lifts + gymnastics + aux + cardio

**Phase 4: GUI**
- Intake screen for Week 0
- Progress tracker
- Generate Path button (Week 0 complete, no errors)

**Phase 5: Export Layer**
- PDF & Excel export
- Include cardio details (mode, rounds, work/rest, rope reps)

**Phase 6: Packaging**
- Build .exe with PyInstaller
- Add GitHub Actions for CI/CD

## ✅ Training Perspective & Program Composition

**Strengths**
- Combines progressive overload with gymnastics conditioning
- Push/pull pairing prevents overtraining
- Week 0 intake ensures personalized load calculation
- Config-driven design allows full customization
- Cardio block supports bike or skip rope with progressive load logic

**Focus Areas**
- Early cycles (12RM, 10RM) → Conditioning & muscular endurance
- Mid cycles (8RM, 6RM) → Strength development
- Final cycles (4RM, 2RM, 1RM) → Max strength & neural adaptation

**Why It Works**
- Balanced integration of lifts, bodyweight, and cardio
- Auto-calculated percentages reduce guesswork
- Rounding rules ensure realistic loads
- Cardio progression (+5 sec work per week, rest fixed)
- Skip rope mode converts work time into estimated reps

**Ideal For**
- Intermediate to advanced athletes
- Users seeking full-body coverage without excessive complexity
- Those who prefer flexible cardio options (bike or rope)
