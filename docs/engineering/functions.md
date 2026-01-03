# kayfitapp-functions.txt  # - 20260103
# ✅ Full Function Map per Module

## core/config.py
- load_config() → Load exercise pools, RM cycles, gymnastics %, rounding rules
- validate_config() → Ensure all lists and cycles are consistent
- get_rounding_rule(lift_name: str) -> float → Return per-lift rounding precision

## core/planner.py
- create_week_plan(week_num: int, rm_values: dict, gymnastics_data: dict) -> dict  
  → Build one week’s plan combining lifts, gymnastics, aux moves, cardio
- generate_full_program(weeks: int = 28) -> list  
  → Generate entire program structure
- merge_blocks(lifts_block: dict, gymnastics_block: dict, aux_block: dict, cardio_block: dict) -> dict  
  → Combine all sections into a session plan

## core/exporter.py
- export_to_pdf(program_data: dict, separate: bool = True)  
  → Generate full PDF and weekly PDFs
- export_to_excel(program_data: dict)  
  → Generate Excel file for all weeks
- format_week_for_export(week_plan: dict) -> dict  
  → Prepare week data for templates

## core/utils.py
- calculate_percentage(base_value: float, pct: float) -> float  
  → Generic percentage calculator
- round_weight(value: float, lift_name: str) -> float  
  → Floor rounding using per-lift precision from config
- validate_rm_values(rm_values: dict)  
  → Check RM inputs for correctness

## core/validator.py
- validate_intake_data(data: dict) -> bool  
  → Validate Week 0 intake structure
- validate_config_tables() -> bool  
  → Ensure RM and gymnastics % tables align

## core/logger.py
- setup_logger() -> logging.Logger  
  → Initialize centralized logging for all modules

## engine/lifts.py
- calculate_rm_table(rm_value: float) -> dict  
  → Generate 1RM–12RM table
- get_working_sets_count(rm_type: str) -> int  
  → Return correct number of working sets
- generate_lift_cycle(rm_values: dict, week_num: int) -> dict  
  → Compute lifts for a given week based on RM % pattern
- generate_warmup_sets(target_pct: float, rm_value: float) -> list  
  → Compute warm-up weights for the week

## engine/gymnastics.py
- generate_gymnastics_block(week_num: int, rm_type: str) -> dict  
  → Build gymnastics section for a week
- get_gymnastics_percentages(rm_type: str) -> list  
  → Return % list for cycle
- calculate_gymnastics_reps(me_value: int, pct: float) -> int  
  → Compute reps from ME check using floor rounding
- get_sets_per_day(day_num: int) -> int  
  → Return 3, 4, or 5 sets based on day

## engine/aux_lifts.py
- select_aux_lifts(week_num: int) -> list  
  → Choose accessory lifts for the week
- generate_aux_block(aux_lifts: list, rm_values: dict, week_num: int) -> dict  
  → Compute accessory loads for the week

## engine/timing.py
- apply_round_timing(session_plan: dict, duration: int = 3)  
  → Add timing info to mixed rounds
- calculate_total_time(rounds: int, duration: int) -> int  
  → Compute total session time
- sum_single_unders(rounds: list) -> int  
  → Calculate SU score per round
- calculate_gymnastics_round_time(num_exercises: int) -> int  
  → Dynamic timing: max(1, num_exercises − 1) 
- generate_cardio_intervals(week_num: int, intensity_pattern: list) -> dict  
  → Dynamically compute cardio (bike, rope) intervals based on cycle progression and user goal

## engine/percentages.py
- get_rm_cycle_percentages() -> list  
  → Return weekly RM % pattern [65, 75, 70, 80]
- get_gymnastics_cycle_percentages(rm_type: str) -> list  
  → Return gymnastics % progression for cycle
- validate_percentage_tables()  
  → Ensure all cycles align with config

## engine/constructor.py
- select_exercises(main_lifts: list, aux_lifts: list, gymnastics: list, cardio: list) -> dict  
  → Build schema from user selections
- apply_order(exercise_schema: dict, order: list) -> dict  
  → Apply chosen sequence for sessions
- select_cycles_by_goal(goal: str, duration: int) -> list  
  → Map goal (Conditioning, Force, Muscle) to RM cycles
- apply_custom_percentages(custom_pct_dict: dict)  
  → Override defaults if needed

## gui/intake_screen.py
- display_intake_form() → UI for Week 0 data entry
- save_session_data() → Store intake after each training day
- check_completion_status() → Verify all 3 sessions done

## gui/progress_screen.py
- show_progress_tracker() → Display completed sessions
- update_progress() → Update after each intake

## gui/generate_screen.py
- display_generate_button() → Show “GENERATE PATH” when ready
- trigger_export() → Call planner + exporter to generate outputs

✅ This is the final, updated function map aligned with your architecture and improved design principles.

# ADD ON - 20260103

## gui/intake_screen.py
- display_intake_form() → UI for Week 0 data entry
- save_session_data() → Store intake after each training day
- check_completion_status() → Verify all 3 sessions done
- validate_gui_inputs(data: dict) → Return list of errors/warnings for incorrect or incomplete inputs
- display_input_errors(errors: list) → Show errors/warnings in GUI for user correction

## gui/progress_screen.py
- show_progress_tracker() → Display completed sessions
- update_progress() → Update after each intake

## gui/generate_screen.py
- display_generate_button() → Show “GENERATE PATH” when ready
- trigger_export() → Call planner + exporter to generate outputs
- preview_week_plan(week_plan: dict) → Display a read-only preview of the generated week plan

## gui/settings_screen.py
- display_settings_panel() → GUI for adjusting percentages, rounding rules, or cardio preferences
- load_settings() → Load user overrides from JSON/INI, fallback to default config
- save_settings(overrides: dict) → Persist user changes for future sessions

## tests/simulation.py
- simulate_week_plan(week_num: int, rm_values: dict, gymnastics_data: dict) → Generate a week plan for inspection without export
- validate_full_program(weeks: int = 28, rm_values: dict, gymnastics_data: dict) → Run simulation for all weeks, check for missing or inconsistent data
