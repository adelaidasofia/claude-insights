---
name: insights
description: Use this skill when the user says /weekly, /monthly, asks for a weekly review, monthly review, or wants to analyze patterns across their journal entries. Reads journal files from the configured vault path, identifies floor trends using the 34-level High-Rise scale, surfaces life coach and therapist observations, runs an advisory panel, and saves a structured report. Companion to claude-daily-journal.
version: 1.1.0
---

# Insights — Weekly and Monthly Reflection

Pattern recognition across journal entries. Identifies floor trends on the 34-level High-Rise scale, surfaces what a life coach would flag and what a therapist would explore, runs an advisory panel, saves a structured report.

**The High-Rise framework:** 34 floors from Disgust to Peace. Full series: https://adelaidadiazroa.substack.com/s/internal-design

---

## Setup (first use)

Ask for:
1. **Vault path** — root folder of Obsidian vault. Store as `VAULT_PATH`.
2. **Journal folder** — where entries live (default: `Journal/`). Confirm monthly subfolder pattern if used.
3. **Tier** — Light (highlights + wins only) or Full (all 7 sections). Default: Full.

Save to `[VAULT_PATH]/.insights-prefs.md`. Check `[VAULT_PATH]/.journal-prefs.md` first if the daily-journal plugin is also installed.

---

## Language

Generate the report in the language the user writes in. If they write in Spanish, the full report is in Spanish. Spanish floor names:

Asco (1) · Vergüenza (2) · Bochorno (3) · Culpa (4) · Apatía (5) · Resignación (6) · Confusión (7) · Soledad (8) · Aburrimiento (9) · Duelo (10) · Decepción (11) · Herida (12) · Miedo (13) · Frustración (14) · Deseo (15) · Rabia (16) · Desprecio (17) · Orgullo (18) · Valentía (19) · Esperanza (20) · Neutralidad (21) · Disposición (22) · Aceptación (23) · Razón (24) · Confianza (25) · Compasión (26) · Humildad (27) · Pertenencia (28) · Amor (29) · Gratitud (30) · Emoción/Entusiasmo (31) · Asombro (32) · Alegría (33) · Paz (34)

Substack link and framework URL are the same in both languages.

---

## Date range

- `/weekly` — current week (Mon–Sun). Default to previous week if today is Mon or Tue.
- `/monthly` — current month. Default to previous month if today is 1st–3rd.
- User can override by saying "this week" or "this month."

---

## Finding entries

**Preferred:** Check for `[VAULT_PATH]/.journal-index.json` — maps each entry to its date, floor, and floor level. One file read instead of hundreds.

```json
[
  { "file": "Journal/2026-04/Good Day Today.md", "date": "2026-04-14", "floor": "Courage", "floor_level": "Middle" }
]
```

**Fallback:** List files in the journal folder, filter by date range, read only matching files. Use monthly subfolders to avoid scanning the full vault.

**Floor detection:** Look for `*Floor: [Name]*` at the bottom of entries or `floor:` in YAML frontmatter. If neither exists, infer from entry content using the 34-floor scale below.

---

## The High-Rise Emotional Altitude Scale
*Full framework: https://adelaidadiazroa.substack.com/s/internal-design*

*Low Floors (1–18) — Reactive:*
1. Disgust · 2. Shame · 3. Embarrassment · 4. Guilt · 5. Apathy · 6. Resignation · 7. Confusion · 8. Loneliness · 9. Boredom · 10. Grief · 11. Disappointment · 12. Hurt · 13. Fear · 14. Frustration · 15. Desire · 16. Anger · 17. Contempt · 18. Pride

*Middle Floors (19–24) — Transitional:*
19. Courage · 20. Hope · 21. Neutrality · 22. Willingness · 23. Acceptance · 24. Reason

*High Floors (25–34) — Generative:*
25. Trust · 26. Compassion · 27. Humility · 28. Belonging · 29. Love · 30. Gratitude · 31. Excitement · 32. Wonder · 33. Joy · 34. Peace

*Key distinctions:*
- Resignation (6) ≠ Acceptance (23): giving up vs. making peace
- Apathy (5) ≠ Neutrality (21): "I don't care" vs. "I'm not attached"
- Boredom (9) is the Trampoline floor — low with upward spring
- Courage (19) is where everything changes — the first floor you choose

---

## Report tiers

**Light:** Entry count, primary floor, top 2–3 wins, one pattern, one question.

**Full:** All 7 sections below.

---

## Full report

### 1. The period at a glance
- Entry count (gaps often mean good stretches — note them)
- Floor distribution: how many entries per floor, which dominated
- Floor trend: moving up, down, or holding vs. prior period
- Habit summary: movement count, avg bedtime, focus blocks — from whatever was tracked
- Average floor vs. historical average if prior insight reports exist

### 2. What stood out
- 2–3 most significant moments, themes, or shifts
- Recurring people, topics, triggers
- Commitments made vs. what actually happened

### 3. Patterns a life coach would flag
Direct. Coach energy. Should sting a little — if it's all validation, look harder.
- "You mentioned [person] three times this week and each time your floor dropped. That's data."
- "You set [goal]. You hit [X]. Two weeks in a row. What's actually in the way?"
- "You had [X] high-floor days in a row and then didn't journal for [X] days. The good stretch disappeared because you didn't document it."
- "You're spending significant mental energy on [thing] that isn't in your current priorities. Time to add it intentionally or let it go."

### 4. Patterns a therapist would explore
Gentler. Curious. Sit with the pattern before labeling it.
- "There's a thread of [emotion] running through several entries you haven't named directly."
- "You mentioned [person/situation] casually but it appeared in [X] of [X] entries. It may be taking more space than you realize."
- "The gap between what you say you want and what you're doing showed up again. Not as failure — as information."
- "Your highest-floor entry this week was [entry]. What was different about that day?"

### 5. Panel thoughts
Select 3–5 advisors most relevant to what came up. 1–2 sentences each, authentic voice. At least one must challenge rather than validate.

**Full panel roster:**

*Wealth and strategy:*
Naval Ravikant (leverage, specific knowledge, freedom — compressed philosophical one-liners) · Warren Buffett (patience, compounding, circle of competence — folksy, says no to almost everything) · Ray Dalio (radical transparency, pain + reflection = progress — systematic, clinical) · Alex Hormozi (execution, value equations, "do the boring work" — blunt, zero fluff) · Tom Wheelwright (tax strategy, entity design, intergenerational planning) · Marc Andreessen (software eating the world, techno-optimism — bold, contrarian) · Howard Marks (second-level thinking, risk vs. uncertainty — thoughtful, memo-style) · Sam Zell (contrarian value, downside-first — irreverent, street-smart) · Robert Kiyosaki (cash-flow mindset, assets vs. liabilities) · Richard Branson (brand-as-personality, joyful entrepreneurship)

*LatAm and cross-border:*
David Vélez (Nubank, largest digital bank in LatAm, 90M+ customers) · Simón Borrero (Rappi, $5B+, hypergrowth execution in emerging markets) · Andrés Moreno (Open English, scaled across 20+ countries) · Luis Carlos Sarmiento Angulo (Grupo Aval, capital preservation, Colombian financial systems)

*Leadership:*
Sheryl Sandberg (COO of Facebook through hypergrowth — polished, direct, empathetic) · Keith Rabois (operator mentality, barrels vs. ammunition — sharp, impatient with mediocrity) · Patrick Collison (craft, speed, taste — quietly intense, precise) · Reid Hoffman (blitzscaling, alliance-building — thinks in systems) · Adam Grant (givers vs. takers, rethinking — evidence-based, generous)

*Technology and AI:*
Ethan Mollick (Wharton professor, *Co-Intelligence* — studies how humans actually integrate AI, evidence-based, no hype) · Tiago Forte (Building a Second Brain, PARA — PKM pioneer, systems for capture and expression) · Andy Matuschak (evergreen notes, Orbit — more rigorous than practical, stress-tests whether systems change how you form ideas) · Andrej Karpathy (former Tesla AI Director, OpenAI cofounder — sanity-checks AI capability assumptions) · Tim Ferriss (*The 4-Hour Workweek*, 40M copies — cold-eyed on what tasks should not exist)

*Gatherings:*
Priya Parker (purposeful gathering, generous authority — reframes every event as a choice about what matters)

*Psychology:*
Brené Brown (vulnerability as courage, shame resilience — warm, research-backed) · Debbie Ford (shadow work, owning every part of yourself — compassionate but unflinching) · Gabor Maté (trauma-informed, addiction as coping — gentle, occasionally devastating) · Martin Seligman (character strengths, positive psychology) · Robert Greene (power dynamics, mastery, human nature — strategic, historical) · Harriet Lerner (overfunctioning/underfunctioning, The Dance of Anger — names the pattern directly)

*Relationships:*
Esther Perel (desire vs. security, erotic intelligence — European sophistication) · Terry Real (relational life therapy, direct, breaks therapy conventions) · Dr. Stan Tatkin (attachment science, nervous-system-aware relating) · Dr. John and Julie Gottman (40+ years research, predicted divorce 94% accuracy) · Alain de Botton (philosophy of love, romantic realism — elegant, melancholy) · Logan Ury (behavioral science of dating — practical, action-oriented)

*Health:*
Dr. Peter Attia (longevity, metabolic health — medical precision, engineer's mind) · Dr. Stacy Sims (women's exercise physiology, hormone-aware — fierce, evidence-based) · Dr. Chris Winter (sleep science, circadian rhythms — demystifies insomnia) · Dr. Peter Levine (somatic trauma release — gentle, body-first) · Bessel van der Kolk (body keeps the score — paradigm-shifting)

*Wisdom:*
Thich Nhat Hanh (mindfulness, interbeing — gentle, profoundly simple) · Marcus Aurelius (stoic emperor, control what you can — journaled his own struggles 2,000 years ago) · Yuval Noah Harari (sapiens-level perspective — zooms way out) · Maya Angelou (rising, courage, dignity — voice of earned wisdom) · Oprah Winfrey (turning pain into purpose — earned every word) · Robin Wall Kimmerer (reciprocity, gratitude, awe at what exists)

*Creativity:*
Rick Rubin (presence, subtractive genius — zen-like) · Elizabeth Gilbert (creative courage, fear alchemy — warm, funny) · Twyla Tharp (creative habit, showing up is the work — no-nonsense)

### 6. Wins to celebrate
Specifically the good stretches that almost always go unrecorded. This section exists because they get skipped.

### 7. One question to sit with
One question worth carrying. Not homework. Just a question the data surfaced.

---

## Save the report

**Weekly:** `[VAULT_PATH]/Journal/Weekly Insights/[YYYY]-W[XX] Weekly Insight.md`
**Monthly:** `[VAULT_PATH]/Journal/Monthly Insights/[YYYY]-[MM] Monthly Insight.md`

Create folders if needed.

**Format:**

```markdown
---
creationDate: [today]
type: insight
period: weekly OR monthly
date_range: [start] to [end]
entries_analyzed: [X]
primary_floor: [Floor]
floor_trend: [up/down/stable]
---

[Full report]

*Primary floor: [Floor](https://adelaidadiazroa.substack.com/s/internal-design)*
```

**Floor link rule:** Use `[[FloorName]]` wikilinks for floor names in the report so they connect to the floor's own note file in the vault (e.g., `[[Fear]]`, `[[Courage]]`). The floor note file carries the Substack link — readers follow the wikilink to the note, and from there to the series. Apply wikilinks to floor names in sections 1–7. If the vault does not use Obsidian wikilinks, use plain text.

After saving, verify the file exists. Report any failure immediately.

---

## After saving: Update floor notes (optional)

If the vault uses individual floor notes and has a `## Personal Patterns` section, check whether any floor appearing 2+ times this period has a new pattern worth adding.

Worth adding: triggers appearing 2+ times, movement strategies that worked, person-floor correlations, surprises.
Skip: generic observations, one-off events, anything already captured.

Format: `- *(Week of [date])* [observation].`

For monthly insights: deeper review — update, merge, or retire stale patterns.

---

## Notes

- Gaps are data, not failure. A 4-day gap during a high-floor week often means the user was living.
- The life coach section should sting a little. All validation means you didn't look hard enough.
- The therapist section is curious, not clinical. Sit with the pattern before labeling it.
- NEVER fail silently. If the journal folder is empty, doesn't exist, or returns no entries in range, say so clearly.
