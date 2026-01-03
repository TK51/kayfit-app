-- kayfitapp-functions-code.txt

-- # 1. Generate_cardio_intervals()
Here’s the generate_cardio_intervals function updated for multi-mode cardio (bike or skip rope) with rep estimation for rope and 4-week progression (+5 sec work per week, rest fixed):

#✅ Python Implementation
# Python
def generate_cardio_intervals(week_num: int, mode: str = "bike") -> dict:
"""
Generate progressive cardio intervals for a 4-week cycle.
Supports 'bike' or 'rope' modes.

Args:
week_num (int): Week number (1–4)
mode (str): 'bike' or 'rope'

Returns:
dict: {
'day1': {'rounds': int, 'work_sec': int, 'rest_sec': int, 'rope_reps': int or None},
'day2': {...},
'day3': {...}
}
"""
if week_num < 1 or week_num > 4:
raise ValueError("Week number must be between 1 and 4.")

# Base rest intervals (fixed)
rest_day1, rest_day2, rest_day3 = 30, 40, 60

# Work progression (+5 sec per week)
work_day1 = 15 + (week_num - 1) * 5
work_day2 = 20 + (week_num - 1) * 5
work_day3 = 30 + (week_num - 1) * 5

# Rounds per day
rounds_day1, rounds_day2, rounds_day3 = 4, 3, 2

# Rope rep estimation (average speed: ~2 skips/sec)
def estimate_rope_reps(work_sec: int) -> int:
avg_speed = 2 # skips per second
return work_sec * avg_speed

# Build output
cardio_plan = {
'day1': {
'rounds': rounds_day1,
'work_sec': work_day1,
'rest_sec': rest_day1,
'rope_reps': estimate_rope_reps(work_day1) if mode == "rope" else None
},
'day2': {
'rounds': rounds_day2,
'work_sec': work_day2,
'rest_sec': rest_day2,
'rope_reps': estimate_rope_reps(work_day2) if mode == "rope" else None
},
'day3': {
'rounds': rounds_day3,
'work_sec': work_day3,
'rest_sec': rest_day3,
'rope_reps': estimate_rope_reps(work_day3) if mode == "rope" else None
}
}

return cardio_plan

---
## engine/timing.py
- apply_round_timing(session_plan: dict, duration: int = 3) → Add timing info to mixed rounds
- calculate_total_time(rounds: int, duration: int) -> int → Compute total session time
- sum_single_unders(rounds: list) -> int → Calculate SU score per round
- calculate_gymnastics_round_time(num_exercises: int) -> int → Dynamic timing: max(1, num_exercises − 1)
- generate_cardio_intervals(week_num: int, mode: str = "bike") -> dict → Generate progressive cardio intervals for a 4-week cycle; supports 'bike' or 'rope' modes with rope rep estimation, 4-week work progression (+5 sec per week), fixed rest

---

2. Simulate_week_plan & validate_full_program
## tests/simulation.py
- simulate_week_plan(week_num: int, rm_values: dict, gymnastics_data: dict) -> dict
  → Generate a week plan without exporting; returns the complete dict for inspection
- validate_full_program(weeks: int = 28, rm_values: dict, gymnastics_data: dict) -> bool
  → Run simulate_week_plan for all weeks; check for missing data, negative weights/reps, or misaligned sets; returns True if valid

3. validate_gui_inputs & dispaly_input_errors

## gui/intake_screen.py
- validate_gui_inputs(data: dict) -> list
  → Return list of errors/warnings for incorrect or incomplete inputs (e.g., RM <=0, ME <=0, missing exercises)
- display_input_errors(errors: list)
  → Show pop-up or inline messages listing errors/warnings for user correction

4. preview_week_plan
## gui/generate_screen.py
- preview_week_plan(week_plan: dict)
  → Display read-only week plan preview, including lifts, sets, gymnastics, aux moves, and cardio intervals; optionally navigate weeks 1–28

5. display_settings_panel
## gui/settings_screen.py
- load_settings()
  → Load user overrides from JSON/INI; fallback to default config if missing
- save_settings(overrides: dict)
  → Persist user changes for future sessions
- display_settings_panel()
  → GUI for adjusting percentages, rounding rules, or cardio preferences
