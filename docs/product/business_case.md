# keyfitapp-doc-business_case-vision.txt
# Business Case & Product Vision – Kay Fit App - Version 1 (Automation)

## 1. Executive Summary
Kay Fit App is a modular Python desktop application that generates personalized strength and conditioning programs. Using Week 0 intake data (RM for lifts, ME for gymnastics), the app constructs a fully automated 4–28 week cycle-based program with integrated cardio. It targets intermediate to advanced athletes seeking a full-body, configurable program with PDF/Excel export and lightweight GUI.

The app prioritizes modularity, automation, and repeatable workflows, enabling users to create a consistent training plan without manual calculation or intervention.

---

## 2. Business Case

### Problem Statement
Athletes and coaches face repetitive calculations when designing long-term strength and conditioning programs. Common issues include:
- Manual tracking of RM and ME percentages
- Integrating lifts, gymnastics, and cardio consistently
- Exporting plans for reference or sharing
- Adjusting programs for progression without errors

### Solution
Kay Fit App solves these problems by:
- Automating program generation based on Week 0 intake
- Integrating multi-mode cardio with progression logic
- Combining main lifts, auxiliary lifts, and gymnastics conditioning in configurable cycles
- Providing exports to PDF and Excel for offline reference
- Offering a GUI for intake, progress tracking, and program generation

### Benefits
- Time-saving: eliminates manual computation and program assembly
- Accuracy: automatic percentage calculations and rounding rules reduce errors
- Consistency: Week 0 intake drives all subsequent cycles with fixed exercise order
- Flexibility: supports multiple cardio modes and adjustable exercise pools
- Reproducibility: program output can be saved, versioned, and reused

---

## 3. Target Audience
- Intermediate and advanced athletes
- Strength & conditioning coaches
- Users who prefer configurable, full-body programs
- Individuals who want cycle-based progression without manual tracking

---

## 4. Product Vision

### Mission
To provide a lightweight, configurable desktop application that generates personalized, cycle-based strength and conditioning programs with minimal user effort and maximum reliability.

### Goals
- **Automated Program Construction:** Generate 4–28 week plans based on initial testing data
- **Multi-Mode Cardio Integration:** Support bike or skip rope with automated progression
- **Configurable Exercise Pools:** User selects main lifts, auxiliary lifts, and gymnastics exercises
- **Export Capability:** Generate PDF and Excel outputs for each week or full program
- **Modular Architecture:** Separate engine, planner, GUI, and export layers for maintainability
- **Testing & Validation:** Include sanity checks, unit tests, and simulation routines to ensure correctness

### Core Features
- Week 0 intake form for RM and ME
- Dynamic construction of weekly sessions
- Cardio progression with adjustable work/rest intervals
- Push/pull pairing and aux-lift integration to prevent overtraining
- Floor rounding rules configurable per lift
- PDF and Excel export using templates
- GUI for intake, program preview, progress tracking, and export
- CI/CD pipeline for automated testing and packaging

### Optional Enhancements
- Preview weekly plans before export
- Settings panel for adjusting percentages, rounding rules, and cardio defaults
- User input validation with error messages
- Modular unit testing and simulation routines to validate program generation

---

## 5. Strategic Fit
- Aligns with personal goals of creating reproducible, accurate, and configurable programs
- Supports modular software development practice and GitHub workflow
- Lightweight desktop deployment ensures portability and offline use
- Provides clear path for future enhancements without scope creep

---

## 6. Success Metrics
- Program generation time < 2 seconds
- Zero calculation errors in RM/ME percentages
- User can complete Week 0 intake without issues
- Exported PDFs/Excel match planned sessions
- Modular code passes all unit and integration tests
- Positive user experience with GUI intake, progress, and generation

---

## 7. Next Steps
1. Finalize SDS-aligned architecture and modular function mapping
2. Implement Week 0 intake, core engine, and planner
3. Integrate multi-mode cardio and percentage logic
4. Develop GUI for intake, progress tracking, and generation
5. Add PDF/Excel export and templates
6. Implement basic validation, simulation routines, and unit tests
7. Package with PyInstaller and deploy `.exe`
8. Version and release via GitHub with CI/CD

---

## 8. Vision Statement
Kay Fit App empowers users to generate accurate, repeatable, and personalized strength and conditioning programs. It bridges the gap between manual programming and automated progression, providing a reliable tool for athletes and coaches to track, plan, and execute multi-week training cycles efficiently.

---------------------------------------

# Business Case & Product Vision – Kay Fit App - Version 2 (Structure & Progress)

## 1. Executive Summary
Kay Fit App is a modular Python desktop application that generates a structured, cycle-based strength and conditioning program. Based on Week 0 intake data (RM for lifts, ME for gymnastics), it produces a full 4–28 week plan with integrated cardio.

In good hands, this tool gives any athlete a clear structure for training. The load percentages are designed not to overwhelm, but to progressively guide the user toward stronger and more balanced physical development, steadily improving all components of fitness.

---

## 2. Business Case

### Problem Statement
Athletes often lack a clear, consistent framework to develop strength, conditioning, and endurance simultaneously. Programs may be fragmented, hard to follow, or lack measurable progression.

### Solution
Kay Fit App addresses this by:
- Providing a complete 28-week program blueprint, built from initial Week 0 testing (4–28 weeks depending on goals (conditioning, strength, muscle growth), without redoing any testing)
- Structuring lifts, gymnastics, and cardio into a coherent cycle
- Offering clear, explainable progression with appropriate load percentages
- Allowing athletes to follow a plan confidently, ensuring measurable and steady improvements

### Benefits
- Clear training structure for all fitness components
- Progressive overload designed to invite growth rather than exhaustion
- Complete program roadmap for 28 weeks
- Config-driven design ensures each athlete works within safe, explainable limits
- Cardio and auxiliary exercises integrated to support recovery and balance

---

## 3. Target Audience
- Intermediate to advanced athletes seeking full-body development
- Users who want measurable, structured, and explainable progress
- Coaches or self-coached individuals needing a repeatable program framework

---

## 4. Product Vision

### Mission
To provide athletes with a clear, structured program that encourages consistent growth across all fitness domains, using safe and progressive load planning.

### Goals
- **Structured Program Delivery:** Provide a full 28-week plan against which the athlete works
- **Progressive but Safe Load:** Load percentages invite growth, avoiding overtraining
- **Multi-Component Fitness:** Combine lifts, gymnastics, auxiliary work, and cardio for balanced development
- **Configurable Exercise Pools:** User can define main and auxiliary exercises, preserving consistency
- **Export & Reference:** PDF and Excel outputs to track and follow the plan

### Core Features
- Week 0 intake to establish baseline ME and RM
- Cycle-based weekly planning (4–28 weeks)
- Cardio integration with bike or skip rope
- Clear push/pull and auxiliary exercise organization
- Floor rounding rules for realistic weight assignments
- PDF and Excel outputs for reference and tracking
- GUI for intake, progress overview, and generation

### Optional Enhancements
- Weekly plan preview before export
- Settings panel for adjusting percentages, rounding rules, or cardio defaults
- Input validation with error messages
- Unit tests and simulation routines for sanity checks

---

## 5. Strategic Fit
- Encourages consistent and measurable physical development
- Maintains modular and maintainable architecture for future expansion
- Provides clear structure and roadmap, not just automated calculations
- Emphasizes explainable, progressive growth in all fitness domains

---

## 6. Success Metrics
- Athletes can follow the program week-to-week without ambiguity
- Load percentages and progressions feel manageable but effective
- Generated PDFs/Excel match planned sessions exactly
- All exercises, rounds, and percentages align with Week 0 baseline

---

## 7. Next Steps
1. Finalize modular architecture and function mapping
2. Implement Week 0 intake and engine for lifts, gymnastics, and cardio
3. Build planner and generate 28-week cycle
4. Develop GUI for intake, progress, and export
5. Implement PDF/Excel templates and export routines
6. Add basic validation and simulation routines
7. Package with PyInstaller and release via GitHub

---

## 8. Vision Statement
Kay Fit App empowers athletes to train with structure, clarity, and steady progression. By following the program, they gain measurable improvements across all physical components, guided by safe, explainable loads, and a coherent 28-week roadmap.
