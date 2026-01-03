# kayfitapp-doc-snapshot.txt

# Kay Fit App – Week 0 → Full Program Flow

## Concept: Test, Set, Go
Week 0 acts as a **calibration phase**:
- **RM for lifts** and **ME for gymnastics** measured
- **Baseline weights, reps, and max effort** established
- Cardio intervals recorded (bike or skip rope)

Once Week 0 is complete, the **planner auto-generates 4–28 week program** depending on goals:
- 4-week cycle → short-term conditioning or strength push
- 8–28 weeks → full progression toward strength, hypertrophy, or conditioning goals
- All percentages, sets, reps, and cardio progressions are **anchored in real Week 0 results**

---

## Week 0 Example (Summarized)

| Day | Exercise Type | Key Measures |
|-----|---------------|--------------|
| 1   | Gymnastics    | Pull-Ups 13 reps, Ring Dips 12 reps, etc. |
|     | RM Lifts      | Bench Press 65 kg, Back Squat 90 kg |
|     | Cardio        | Bike 4 rounds × 15s work / 30s rest |
| 2   | Gymnastics    | 20% ME, 2 rounds, sum reps 27 |
|     | RM Lifts      | Barbell Rows 67.5 kg, Deadlift 100 kg |
|     | Cardio        | Bike 3 rounds × 20s work / 40s rest |
| 3   | Gymnastics    | 20% ME, 3 rounds, sum reps 27 |
|     | RM Lifts      | Push Press 55 kg, Front Squat 67.5 kg |
|     | Cardio        | Bike 2 rounds × 30s work / 60s rest |

---

## Flow Diagram – Week 0 → Full Program (ASCII / Markdown)

```text
  [Week 0 Intake]
      |
      |-- RM Check (Lifts)
      |-- ME Check (Gymnastics)
      |-- Cardio Baseline (Bike / Rope)
      |
      v
  [Program Generator]
      |
      |-- Apply % progression per lift & gymnastics
      |-- Assign push/pull & aux pairings
      |-- Cardio intervals with +5s/week work
      |
      v
  [4–28 Week Plan]
      |
      |-- Week 1 → Week N (based on goal, full cycle-based plan auto-generated)
      |-- All sets, reps, weights, and cardio pre-calculated
      |-- Export to PDF / Excel
      |
      v
  [Athlete Execution]
      |
      |-- Follow plan without recalculating
      |-- Track progress, focus on execution
