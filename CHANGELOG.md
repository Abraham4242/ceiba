# CEIBA · Changelog

## [Unreleased]

## [1.1.2] - 2026-07-01
### Added
- True/False question type (`tf`) — two large toggle buttons (Verdadero/Falso) with ✓/✗ icons
- SVG + MCQ question type (`svg-mcq`) — inline SVG graphic displayed above MCQ options
- Multiselect question type (`multiselect`) — select all correct answers with checkboxes; partial credit shows missed correct answers
- Tap-to-sequence ordering type (`order`) — tap items in correct order; sequence numbers appear and can be untapped/re-ordered; items shuffle on each render
- SVG generator functions: `svgFractionCircle`, `svgFractionBar`, `svgNumberLine`, `svgRectangle`, `svgSquare`, `svgPercentBar`, `svgTwoCircles`, `svgQ`
- All 17 skills expanded to 10–13 questions (up from 5–8), using all five question types
- `qState` per-question state object (resets on each new question)
- Shake animation extended to cover tf-wrong and order-wrong elements
- Type labels for all new question types in exercise topbar

## [1.1.1] - 2026-07-01
### Fixed
- Badge/level toasts no longer bleed into non-exercise screens (offscreen translate increased)
- Exercise topbar skill name truncates with ellipsis instead of wrapping 3 lines
- Exercise screen height constrained to dvh with scroll on body

## [1.1.0] - 2026-06-30
### Added
- SM-2 spaced repetition scheduling on top of BKT engine
- Adaptive "Practica del dia" multi-skill daily session (10 questions, up to 3 skills)
- Recommended next action card on home screen
- XP float animation on correct answers
- Canvas confetti on skill mastery
- Badge / achievement system (8 badges)
- Level / rank system (Aprendiz → Maestro, 5 levels)
- Daily goal ring (3 exercises = goal, resets midnight)
- Multi-student classroom mode (roster-based student picker)
- AudioContext sound engine (correct/wrong/mastery/level-up sounds)
- Shake animation on wrong answers
- Expanded question banks (8 questions per skill, up from 5)
- Teacher dashboard: assign priority skill to student
- Teacher dashboard: assignment notification card for students
- Teacher dashboard: full 17-skill heat map (was clipped at 12)
- Teacher dashboard: export summary to clipboard
- GitHub repo with versioning + GitHub Pages

### Changed
- Student state schema v2: adds SM-2 fields, badges, level, daily goal, time tracking
- Multi-student storage: `ceiba.student.{name}.v1` per student, roster at `ceiba.roster.v1`
- Home screen redesigned: recommended card above subject grid

## [1.0.0] - 2026-06-26
### Initial release
- BKT engine with 17 skills across 4 subjects
- 5 questions per skill (MCQ + fill-in-the-blank)
- Prerequisite graph (70% mastery gates)
- XP + streak system
- TTS via Web Speech API (es-PA)
- Hearts system (3 per session)
- Teacher dashboard: roster, skill heat map, student detail, priority alerts
