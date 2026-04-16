---
name: insights
description: Use this skill when the user says /weekly, /monthly, asks for a weekly review, monthly review, or wants to analyze patterns across their journal entries. Reads journal files from the configured vault path, identifies floor trends, surfaces life coach and therapist observations, runs an advisory panel, and saves a structured insight report. Companion to the daily-journal skill — works best with entries that use the High-Rise floor tagging format, but will analyze any journal entries.
version: 1.0.0
---

# Insights — Weekly and Monthly Reflection

Pattern recognition across journal entries. Identifies floor trends, surfaces what a life coach would flag and what a therapist would explore, runs an advisory panel, and saves a structured report.

---

## Setup (first use)

Ask the user for:
1. **Vault path** — root folder of their Obsidian vault. Store as `VAULT_PATH`.
2. **Journal folder** — where entries are stored (default: `Journal/`). If using monthly subfolders (`Journal/YYYY-MM/`), confirm that pattern.
3. **Tier** — Light (highlights + wins only) or Full (life coach, therapist, panel, floor trends). Default: Full.

Save preferences to `[VAULT_PATH]/.insights-prefs.md`. On future invocations, read that file first.

If both the daily-journal and insights plugins are installed, check for shared prefs at `[VAULT_PATH]/.journal-prefs.md` first.

---

## Date range selection

- `/weekly` — current calendar week (Monday–Sunday). If today is Monday or Tuesday, default to the previous week (not enough data yet). User can say "this week" to override.
- `/monthly` — current calendar month. If today is 1st–3rd, default to the previous month. User can say "this month" to override.

---

## Finding entries

**Preferred method — index file:**
Check for `[VAULT_PATH]/.journal-index.json`. If it exists, use it to filter entries by date range without reading every file. Format:

```json
[
  { "file": "Journal/2026-04/Good Day Today.md", "date": "2026-04-14", "floor": "Courage", "floor_level": "Middle" },
  ...
]
```

If the index doesn't exist or is stale (modified more than 24 hours ago), fall back to directory listing.

**Fallback — directory listing:**
List files in the journal folder, filter by filename or creation date to the target date range, then read only the matching files. With monthly subfolders, only read the relevant month folder. Avoid grepping the entire vault.

**Floor detection (if entries don't use the index):**
Look for the floor tag at the bottom of each entry: `*Floor: [FloorName]*` or `floor:` in YAML frontmatter. If neither exists, infer the floor from the entry content using the High-Rise scale (see the daily-journal skill for the full 22-floor definitions).

---

## Report tiers

### Light tier (Pro or quick-review mode)
- Entry count and date range
- Primary floor for the period
- Top 2–3 wins worth celebrating
- One pattern to notice
- One question to sit with

### Full tier (default)
All 7 sections below.

---

## Full report structure

### Section 1: The period at a glance

- Entry count (and gaps — gaps often mean good stretches, not just missed journaling)
- Floor distribution: how many entries on each floor, which floor dominated
- Floor trend: moving up, down, or holding steady vs. the previous period
- Habit summary: movement count, average bedtime, focus block count — whatever was tracked in the entries
- Average floor vs. historical average (if prior insight reports exist to compare against)

### Section 2: What stood out

- The 2–3 most significant moments, themes, or shifts from the entries
- Recurring people, topics, or triggers
- Commitments made vs. what actually happened (accountability check)

### Section 3: Patterns a life coach would flag

Direct. Coach energy, not therapist energy. Examples of the tone:
- "You mentioned [person] three times this week and each time your floor dropped. That's data."
- "You set a movement goal of 4x. You hit 2. Two weeks in a row. What's actually in the way?"
- "You had three high-floor days in a row and then didn't journal for 4 days. The good stretch disappeared because you didn't document it."
- "You're spending significant mental energy on [thing] that isn't in your current priorities. Time to add it intentionally or let it go."

### Section 4: Patterns a therapist would explore

Gentler. Curious. Examples of the tone:
- "There's a thread of [emotion] running through several entries this week you haven't named directly."
- "You mentioned [person/situation] casually but it appeared in 4 of 7 entries. It may be taking up more space than you realize."
- "The gap between what you say you want and what you're doing about it showed up again. Not as a failure — as information."
- "Your highest-floor entry this week was [entry]. What was different about that day?"

### Section 5: Panel thoughts on the period

Select 3–5 advisors most relevant to what came up. 1–2 sentences each, in their authentic voice. At least one must challenge rather than validate.

Use the full panel roster below. Each advisor has a distinct voice — match it when they speak.

**Wealth and strategy:** Naval Ravikant (leverage, specific knowledge, wealth vs. status games — compressed philosophical one-liners) · Warren Buffett (patience, compounding, circle of competence — folksy midwestern, says no to almost everything) · Ray Dalio (radical transparency, pain + reflection = progress — systematic, almost clinical) · Alex Hormozi (execution, value equations, "do the boring work" — blunt, high-energy, zero fluff) · Marc Andreessen (software eating the world, techno-optimism — bold, contrarian) · Howard Marks (second-level thinking, risk vs. uncertainty — thoughtful, memo-style reasoning) · Sam Zell (contrarian value, downside-first — irreverent, street-smart)

**Leadership:** Sheryl Sandberg (scale, resilience, navigating power — polished, direct, empathetic) · Keith Rabois (operator mentality, barrels vs. ammunition — sharp, impatient with mediocrity) · Patrick Collison (craft, speed, taste — quietly intense, precise) · Reid Hoffman (blitzscaling, alliance-building — thinks in systems) · Adam Grant (givers vs. takers, rethinking — evidence-based, generous)

**Gatherings:** Priya Parker (purposeful gathering, generous authority — reframes every event as a choice about what matters)

**Psychology:** Brené Brown (vulnerability as courage, shame resilience — warm, research-backed, direct) · Debbie Ford (shadow work, owning every part of yourself — compassionate but unflinching) · Gabor Maté (trauma-informed, addiction as coping — gentle, occasionally devastating) · Martin Seligman (character strengths, positive psychology — academic but practical) · Robert Greene (power dynamics, mastery, human nature — strategic, historical) · Harriet Lerner (overfunctioning/underfunctioning, The Dance of Anger — names the relational pattern directly)

**Relationships:** Esther Perel (desire vs. security, erotic intelligence — European sophistication) · Terry Real (relational life therapy, "us consciousness" — direct, breaks therapy conventions) · Dr. Stan Tatkin (attachment science, nervous-system-aware relating) · Alain de Botton (philosophy of love, romantic realism — elegant, melancholy, wise) · Logan Ury (behavioral science of dating — practical, action-oriented)

**Health:** Dr. Peter Attia (longevity, metabolic health — medical precision, engineer's mind) · Dr. Stacy Sims (women's exercise physiology, hormone-aware training — evidence-based, fierce) · Dr. Chris Winter (sleep science, circadian rhythms — practical, demystifies insomnia) · Dr. Peter Levine (somatic trauma release — gentle, body-first) · Bessel van der Kolk (body keeps the score, embodied healing — paradigm-shifting)

**Wisdom:** Thich Nhat Hanh (mindfulness, interbeing — gentle, profoundly simple) · Marcus Aurelius (stoic emperor, control what you can — journaled his own struggles) · Yuval Noah Harari (sapiens-level perspective — zooms way out) · Maya Angelou (rising, courage, dignity — voice of earned wisdom) · Oprah Winfrey (turning pain into purpose — earned every word)

**Creativity:** Rick Rubin (presence, subtractive genius — zen-like, listens more than speaks) · Elizabeth Gilbert (creative courage, fear alchemy — warm, funny) · Twyla Tharp (creative habit, showing up is the work — disciplined, no-nonsense)

### Section 6: Wins to celebrate

Things that went well that might get overlooked. Good days matter more to document than bad ones, and this section exists specifically because they almost always get skipped.

### Section 7: One question to sit with

End with ONE question worth thinking about based on the data. Not homework, not an action item. A question.

---

## Save the report

**Weekly:** `[VAULT_PATH]/Journal/Weekly Insights/[YYYY]-W[XX] Weekly Insight.md`
**Monthly:** `[VAULT_PATH]/Journal/Monthly Insights/[YYYY]-[MM] Monthly Insight.md`

Create folders if they don't exist.

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
[habit totals from the entries — movement_total, avg_bedtime, etc.]
---

[Full report]

*Primary floor: [Floor]*
```

After saving, verify the file exists. Report any save failure immediately.

---

## After saving: Update floor notes (optional)

If the vault uses individual floor notes (e.g., `[[Fear]]`, `[[Courage]]`) and has a `## Personal Patterns` section, check whether any floor that appeared 2+ times this period has a new pattern worth adding.

**Worth adding:** Triggers that appeared 2+ times, movement strategies that worked, person-floor correlations, surprises.

**Skip:** Generic observations, one-off events, anything already captured.

Format: `- *(Week of [date])* [observation].`

For monthly insights: do a deeper review — read all accumulated personal patterns and update, merge, or retire stale ones.

If the vault doesn't use floor notes, skip this step silently.

---

## Notes

- Gaps in the journal record are data, not failure. A 4-day gap during a high-floor week often means the user was living, not stuck.
- The life coach section should sting a little. If it's all validation, look harder.
- The therapist section should feel curious, not clinical. Sit with the pattern before labeling it.
- NEVER fail silently. If the journal folder is empty, doesn't exist, or returns no entries in range, say so clearly.
