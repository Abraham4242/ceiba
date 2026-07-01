# CEIBA · Product Improvement Plan
*Last updated: 2026-06-30*

## Research Summary

### What the top apps do well

| Platform | Key mechanic | Why it works |
|----------|-------------|--------------|
| Duolingo | Streak + hearts + XP + daily goal | Habit loop: cue → routine → reward |
| Khan Academy | Mastery path + recommended "next" | Removes decision fatigue |
| IXL | SmartScore (0–100 per skill) + diagnostic | Progress feels granular and earned |
| Prodigy | RPG skin over math drills | Dopamine from game rewards, not just grades |
| Quizlet | Flashcard spaced repetition (SM-2) | Timing reviews at the moment of near-forgetting |
| Anki/SM-2 | Interval scheduling based on recall quality | 20–30% fewer reviews for same retention |

### Academic findings applied to Ceiba
- **BKT** (current): estimates P(mastery) via hidden Markov model. Good for "does the student know this?"
- **SM-2** (to add): schedules *when* to review each skill. Reduces unnecessary re-drilling of mastered content.
- **Self-Determination Theory**: students need Autonomy (choose their path), Competence (feel progress), Relatedness (streaks, community). All three must be served.
- **15–20 min/day > 60 min/week**: short daily sessions win on retention. Daily goal UX enforces this.
- **Immediate corrective feedback**: explains *why* the answer is right/wrong → 40% retention improvement vs. no explanation.
- **Spaced retrieval practice**: testing beats re-reading. Each Ceiba session is already this.
- **Gamified feedback loops**: correct answers → sound + animation + XP float = dopamine micro-burst.

---

## Current State (v1.0)

### ceiba-student.html
- ✅ BKT engine (pMastery per skill)
- ✅ 17 skills across 4 subjects (mat/esp/nat/soc)
- ✅ 5 questions per skill (MCQ + fill-in-the-blank)
- ✅ Prerequisite graph (70% mastery unlocks next)
- ✅ XP + streak system (basic)
- ✅ TTS (Web Speech API, es-PA)
- ✅ Hearts (3 per session)
- ❌ No spaced repetition scheduling
- ❌ No "what to do next" recommendation
- ❌ No multi-skill daily session
- ❌ No XP animation / celebration UX
- ❌ No badge/achievement system
- ❌ No level/rank system
- ❌ No daily goal
- ❌ No placement diagnostic
- ❌ No multi-student per device (classroom use)
- ❌ Only 5 questions/skill → gets repetitive

### ceiba-teacher-dashboard.html
- ✅ Roster with add-student
- ✅ Skill heat map (all students × all skills)
- ✅ Student detail view (per-skill BKT bars)
- ✅ Priority alerts (stuck students)
- ✅ Ranking tab
- ❌ No session time tracking
- ❌ No "assign skill" to student
- ❌ No weekly progress / sparkline
- ❌ No export/print
- ❌ Heat map only shows 12/17 skills

---

## Improvement Plan

### Phase 1 — GitHub + Versioning ✅ (this session)
- [x] Create `Abraham4242/ceiba` GitHub repo (public)
- [x] Copy all 7 ceiba files + assets
- [x] Add VERSION.md + CHANGELOG.md
- [x] Tag v1.0.0 — baseline
- [x] Enable GitHub Pages → ceiba served at abraham4242.github.io/ceiba/

### Phase 2 — Student App: Engine + Celebration UX ✅ (this session)

#### 2A. SM-2 Spaced Repetition on top of BKT
- Extend STATE.skills[id] with: `{ pMastery, attempts, correct, lastSeen, interval, easiness, nextDue }`
- SM-2 update on each session end: compute new interval based on session score
- `getReviewQueue()` → returns skills sorted by urgency (past due first, new skills, then learning)

#### 2B. Adaptive "Práctica del día" multi-skill session
- Home screen CTA: big "Practicar ahora" button
- Selects 10 questions from up to 3 skills:
  1. Past-due review skills first
  2. In-progress (learning) skills
  3. New unlocked skill
- Session progress bar spans all 10 questions regardless of skill switches
- Shows skill name badge when transitioning between skills

#### 2C. Recommended Next Action Card
- Prominent card on home screen above subject grid
- Logic: past-due review > new unlocked skill > continue learning
- Shows skill name, subject icon, estimated time ("~3 min")
- "Practicar →" CTA button

#### 2D. Celebration UX
- **Correct answer**: +XP float animation (number flies up and fades)
- **Wrong answer**: subtle shake animation on options
- **Mastery unlocked**: confetti burst (canvas, 60 particles, 1.5s)
- **Session complete**: star rating (1–3 stars based on score%) + animated XP counter
- **Streak milestone** (3, 7, 14, 30): full-width celebration toast

#### 2E. Badge / Achievement System (8 badges)
| Badge | Trigger |
|-------|---------|
| 🌱 Primera semilla | First correct answer |
| ⭐ Primera estrella | First skill mastered |
| 🔥 Semana de fuego | 7-day streak |
| 🧮 Matemático | All math skills mastered |
| 📖 Escritor | All Spanish skills mastered |
| 🌿 Científico | All science skills mastered |
| 🗺️ Explorador | All social skills mastered |
| 👑 Maestro Ceiba | All 17 skills mastered |

#### 2F. Level / Rank System
| Level | XP required | Title |
|-------|------------|-------|
| 1 | 0 | Aprendiz |
| 2 | 100 | Explorador |
| 3 | 300 | Estudiante |
| 4 | 700 | Académico |
| 5 | 1500 | Maestro |

- Level badge shown in topbar
- Level-up toast when crossing threshold

#### 2G. Daily Goal Ring
- Goal: complete 3 exercises per day
- Small animated ring in topbar
- Completes with celebration when goal hit
- Resets at midnight

#### 2H. Multi-Student Welcome (classroom mode)
- On load: check if `ceiba.roster.v1` exists
- If roster found: show student picker ("¿Quién eres tú?" + name list)
- If no roster: show original name input (solo mode)
- Student data stored as `ceiba.student.{name}.v1` (also writes generic key for backwards compat)

#### 2I. Sound Engine (AudioContext, no external deps)
- Correct: bright ascending ding (220→440Hz, 0.1s)
- Wrong: low thud (100Hz, 0.08s)
- Mastery: three-note ascending chord
- Level up: ascending scale
- Muted by default, toggle in topbar alongside TTS

#### 2J. More Questions
- Expand each skill from 5 → 8 questions
- Add context-passage questions (reading comprehension style) for esp/nat/soc
- Add visual description questions ("según el diagrama...")
- Harder "grade 6 only" variants for mixed-grade skills

### Phase 3 — Teacher Dashboard: Reporting + Assignments ✅ (this session)

#### 3A. Session Time Tracking
- STATE adds `timeSpentToday` (minutes), `totalTimeSpent` (minutes)
- Teacher view shows avg time/student, flagging <5 min/day

#### 3B. Assign Priority Skill
- Teacher clicks "Asignar" next to any skill in student detail view
- Writes to `ceiba.assign.{studentName}` localStorage key
- Student app reads this on home screen → shows "Tu maestra asignó: [skill]" card

#### 3C. Weekly Sparkline per Student
- Show 7-day activity bars (XP per day) in student row of roster
- Tiny 40px wide sparkline chart drawn on canvas

#### 3D. Full Heat Map (all 17 skills)
- Current heat map clips at 12; expand to show all 17 with horizontal scroll

#### 3E. Export Summary
- "Copiar reporte" button → copies formatted text to clipboard for teacher to paste into email

### Phase 4 — Diagnostic Placement Test (next session)
- 8 questions sampled across all 4 subjects (2 per subject)
- Runs after grade selection on welcome screen
- Pre-fills BKT priors: correct → pMastery=0.5, wrong → stays at 0.1
- Shows "aquí es donde empiezas" skill map result

### Phase 5 — Content Expansion (ongoing)
- Target: 15 questions per skill (3 difficulty levels × 5)
- Add 4 new skills: mat-ratio-1, esp-texto-1, nat-solar-1, soc-canal-1
- Add "Reto difícil" mode: skip easy questions if BKT > 0.75

---

## Technical Architecture

### Storage schema (v2)
```
ceiba.roster.v1 = [{name, grade}]

ceiba.student.{name}.v1 = {
  name, grade, xp, streak, lastActivityDate,
  dailyGoalDate, dailyGoalCount,          // NEW
  level,                                   // NEW (computed but cached)
  badges: ['primera-semilla', ...],        // NEW
  totalTimeSpent,                          // NEW
  skills: {
    [skillId]: {
      pMastery,
      attempts,
      correct,
      lastSeen,
      interval,       // SM-2: days until next review
      easiness,       // SM-2: E-factor (default 2.5)
      nextDue,        // SM-2: ISO date string
    }
  }
}

ceiba.assign.{name} = { skillId, assignedBy, date }  // teacher assignments
```

### File structure (GitHub repo)
```
ceiba/
├── index.html              → redirect to ceiba.html or standalone landing
├── app.html                → ceiba-student.html (renamed)
├── teacher.html            → ceiba-teacher-dashboard.html (renamed)
├── CHANGELOG.md
├── VERSION.md
└── docs/                   → existing ceiba docs (comarca, boquete, etc.)
```

---

## Success Metrics
- Daily active use: >3 sessions/week per student
- Mastery rate: >1 new skill mastered per week
- Teacher adoption: dashboard checked >2x per week
- Session length: 10–15 min (not too long, not too short)
