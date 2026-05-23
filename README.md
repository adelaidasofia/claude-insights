# claude-insights


<!-- mycelium-badges:start -->

<p>
  <a href="https://github.com/adelaidasofia/claude-insights/blob/main/LICENSE"><img alt="License" src="https://img.shields.io/github/license/adelaidasofia/claude-insights?color=blue"></a>
  <a href="https://github.com/adelaidasofia/claude-insights/stargazers"><img alt="GitHub stars" src="https://img.shields.io/github/stars/adelaidasofia/claude-insights?color=eab308"></a>
  <a href="https://github.com/adelaidasofia/claude-insights/commits/main"><img alt="Last commit" src="https://img.shields.io/github/last-commit/adelaidasofia/claude-insights"></a>
  <a href="https://github.com/adelaidasofia/claude-insights/issues"><img alt="Open issues" src="https://img.shields.io/github/issues/adelaidasofia/claude-insights"></a>
  <a href="https://myceliumai.co"><img alt="Built by Mycelium AI" src="https://img.shields.io/badge/built_by-Mycelium_AI-15B89A"></a>
</p>

<!-- mycelium-badges:end -->

A Claude Code plugin for weekly and monthly pattern recognition across Obsidian journal entries. Surfaces floor trends, life coach pushback, therapist observations, and advisory panel commentary.

Companion to [claude-daily-journal](https://github.com/adelaidasofia/claude-daily-journal). Works best with entries that use the High-Rise floor tagging format, but will analyze any journal entries.

---

## What it does

Reads your recent journal entries and generates a structured insight report with:

1. **The period at a glance** — floor distribution, trend vs. last period, habit summary
2. **What stood out** — significant moments, recurring themes, commitments vs. reality
3. **Patterns a life coach would flag** — direct, data-driven, slightly uncomfortable
4. **Patterns a therapist would explore** — gentler, curious, sitting with the thread
5. **Panel thoughts** — 3–5 named advisors in their authentic voices, at least one dissenting
6. **Wins to celebrate** — the good stretches that almost always go undocumented
7. **One question to sit with** — not homework, just a question worth carrying

Reports save as structured Obsidian markdown with YAML frontmatter.

---

## Install

Open Claude Code, paste:

    /plugin marketplace add adelaidasofia/claude-insights
    /plugin install claude-insights@claude-insights

Then in any Claude Code session:

```
/weekly
```

or

```
/monthly
```

<details>
<summary>Legacy install</summary>

```bash
claude plugin add github.com/adelaidasofia/claude-insights
```

Or clone manually:

```bash
git clone https://github.com/adelaidasofia/claude-insights ~/.claude/plugins/claude-insights
claude plugin add ~/.claude/plugins/claude-insights
```

</details>

---

## Requirements

- Claude Code
- An Obsidian vault with journal entries (any format works, but floor-tagged entries from claude-daily-journal give richer analysis)

**Strongly recommended companion:**
- [claude-daily-journal](https://github.com/adelaidasofia/claude-daily-journal) — writes the entries this skill analyzes

---

## Tiers

**Light** — highlights and wins only. Good for a quick 2-minute Sunday scan.

**Full** (default) — all 7 sections. Takes 3–5 minutes to read, worth it weekly.

Set your preference in `[VAULT_PATH]/.insights-prefs.md` or tell Claude when you run `/weekly`.

---

## The floor framework

This skill was built around the **High-Rise Emotional Altitude Scale** — a 22-level framework developed by [Adelaida Diaz-Roa](https://github.com/adelaidasofia) as part of *The High-Rise Series*.

The 22 floors run from Disgust (1) through Shame, Guilt, Fear, Anger, Courage, Acceptance, Compassion, Love, Joy, and Peace (22). Each floor has a name and a direction. Over time, your floor trend becomes one of the most honest indicators of how your life is actually going — not how you think it's going.

If you're not using the daily-journal plugin with floor tagging, Claude will infer floors from entry content. Less precise, still useful.

---

## Configuration

On first use, preferences save to `[VAULT_PATH]/.insights-prefs.md`:

```markdown
vault_path: ~/Documents/MyVault
journal_folder: Journal
tier: full
```

---

## Report location

```
[VAULT_PATH]/Journal/Weekly Insights/[YYYY]-W[XX] Weekly Insight.md
[VAULT_PATH]/Journal/Monthly Insights/[YYYY]-[MM] Monthly Insight.md
```

---

## Performance note

The skill uses a journal index file (`[VAULT_PATH]/.journal-index.json`) when available, so it reads one file to locate entries rather than scanning the entire vault. If you have hundreds of entries, build the index once and it stays fast.

The daily-journal skill maintains this index automatically when saving entries. If you're using a different journaling setup, create the index manually — format documented in SKILL.md.

---

## Submitting to the Cowork marketplace

Once your repo is on GitHub, submit at: **[clau.de/plugin-directory-submission](https://clau.de/plugin-directory-submission)**

Anthropic performs basic automated review before listing. "Anthropic Verified" badge requires additional review — you can request that after initial listing.

The community marketplace is a faster first step:

```bash
claude plugin marketplace add anthropics/claude-plugins-community
```

---


## Telemetry

This plugin sends a single anonymous install signal to `myceliumai.co` the first time it loads in a Claude Code session on a given machine.

**What is sent:**
- Plugin name (e.g. `slack-mcp`)
- Plugin version (e.g. `0.1.0`)

**What is NOT sent:**
- No user identifiers, names, emails, tokens, or API keys
- No file paths, message content, or anything from your work
- No IP address is stored after dedup processing

**Why:** Helps the maintainer know which plugins people actually install, so attention goes to the ones that get used.

**Opt out:** Set the environment variable `MYCELIUM_NO_PING=1` before launching Claude Code. The hook will skip the network call entirely. Already-pinged installs leave a sentinel at `~/.mycelium/onboarded-<plugin>` — delete it if you want to reset state.

## License

MIT
