# CEIBA · Changelog

## [Unreleased]

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
