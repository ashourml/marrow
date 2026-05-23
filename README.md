# Marrow

**Extract the living core of any UI design. Build and maintain inside it automatically.**

Most tools extract colors, spacing, and font names. Marrow goes deeper — it reads the *decisions* behind a design. The restraint. The proportions. The emotional intent. The invisible rules that make a UI feel the way it does.

Seven skills. One soul. The complete lifecycle.

---

## Install

The CLI auto-detects which agents you have installed and routes skills to the correct directory. The repo has no agent-specific folders — the CLI handles all placement.

### Install for a specific agent (recommended)

```bash
# OpenCode only
npx skills add yourusername/marrow --skill '*' -a opencode

# Cursor only
npx skills add yourusername/marrow --skill '*' -a cursor

# Windsurf only
npx skills add yourusername/marrow --skill '*' -a windsurf

# Claude Code only
npx skills add yourusername/marrow --skill '*' -a claude-code

# Antigravity only
npx skills add yourusername/marrow --skill '*' -a antigravity

# Multiple specific agents (not all)
npx skills add yourusername/marrow --skill '*' -a opencode -a cursor
```

### Install for all detected agents

```bash
# Routes only to agents the CLI finds on your machine
npx skills add yourusername/marrow --all
```

> **`--all` vs `-a`:** `--all` installs to every agent the CLI detects on your machine — not every possible agent. If you only have OpenCode installed, it only goes to OpenCode. Use `-a [agent]` when you want to be explicit and bypass detection entirely.

### Global install (follows you across all projects)

```bash
# Global install for OpenCode only
npx skills add yourusername/marrow --skill '*' -a opencode -g

# Global install for all detected agents
npx skills add yourusername/marrow --all -g
```

### Non-interactive (CI/CD, dotfiles)

```bash
npx skills add yourusername/marrow --skill '*' -a opencode -y
```

### List available skills before installing

```bash
npx skills add yourusername/marrow --list
```

### Update

```bash
# Re-run your install command to get the latest — same command, adds -y to skip prompts
npx skills add yourusername/marrow --skill '*' -a opencode -y
```

Works with **Cursor**, **Windsurf**, **Claude Code**, **Antigravity**, **OpenCode**, and [37+ other agents](https://skills.sh).

---

## The 7 skills

| Skill | Invoke | What it does |
|---|---|---|
| `marrow` | `/marrow` | Reads reference images → extracts soul → saves `.marrow.md` |
| `marrow-apply` | Automatic | Silently injects `.marrow.md` into every frontend task |
| `marrow-check` | `/marrow-check` | Audits a file for soul violations — reports, doesn't fix |
| `marrow-align` | `/marrow-align` | Rewrites one file to match `.marrow.md` — surgical, preserves logic |
| `marrow-magic` | `/marrow-magic` | No target needed — scans project, fixes the 3 worst offenders |
| `marrow-update` | `/marrow-update` | Patches one section of `.marrow.md` without re-extracting everything |
| `marrow-redesign` | `/marrow-redesign` | Full project alignment in one command — smart diff on repeat runs |

---

## The complete lifecycle

### Start fresh — extract once, build forever

```
/marrow  [drop reference images]
→ extracts soul across 9 analysis layers
→ saves .marrow.md
→ marrow-apply activates automatically

"build a button"     → soul injected automatically
"create a modal"     → soul injected automatically
"make a dashboard"   → soul injected automatically
```

### Start mid-project — catch everything up at once

Already have code and just installed Marrow? One command:

```
/marrow-redesign
→ Phase 0: globals.css safe-mode reconciliation
    — maps old CSS variables to Marrow tokens via legacy aliases
    — injects full --marrow-* token block
    — resolves conflicts without deleting anything
→ scans every frontend file in the project
→ presents a full prioritized plan (Foundation → Base components → Layout → Features → Pages)
→ waits for your confirmation
→ aligns everything phase by phase
→ saves .marrow-state.json to track what was aligned and when
```

### When something looks off — audit and fix

```
/marrow-check src/components/Card.tsx
→ lists every violation with severity: CRITICAL / MAJOR / MINOR
→ cites the exact rule from .marrow.md for each violation

/marrow-align src/components/Card.tsx
→ rewrites Card.tsx to match the soul
→ preserves all logic, props, and accessibility

/marrow-magic
→ no target — finds the 3 most violated files and fixes them
```

### When the design evolves — patch and propagate

```
/marrow-update accent #FF6B6B
→ patches only the accent in .marrow.md
→ updates Tailwind config + CSS custom properties
→ tells you which files are affected

/marrow-redesign
→ reads .marrow-state.json — knows what changed
→ only reprocesses files affected by the accent update
→ skips the 22 files that are clean and unaffected
→ "Smart update: Section 4 changed. Processing 12 of 34 files."
```

---

## Smart diff — how marrow-redesign knows what to skip

After every run, `/marrow-redesign` saves `.marrow-state.json` — a record of which files were aligned and which sections of `.marrow.md` were applied to each.

On the next run, it compares the current `.marrow.md` against the stored checksums per section. If only Section 4 (colors) changed, it only reprocesses files that use color. Files that use only spacing, typography, and motion — and weren't touched by the color change — are skipped entirely.

```
First run after /marrow:       aligns all 34 files
After /marrow-update accent:   aligns 12 files (color-affected only)
After /marrow-update spacing:  aligns 18 files (spacing-affected only)
After /marrow-update font:     aligns 14 files (typography-affected only)
```

No wasted work. No risk of overwriting something already correct.

---

## The quality baseline

Every Marrow build runs on two layers simultaneously:

| Layer | File | Purpose |
|---|---|---|
| **Floor** | `references/quality-baseline.md` | Level 4 SaaS quality standard — applies universally |
| **Law** | `.marrow.md` | The extracted soul of this specific project |

The baseline ensures every component has all states designed, every animation has purpose, every layout has rhythm, and every CTA has conversion logic — regardless of what the soul says. The soul defines *how* those standards are expressed for this specific design.

**When they conflict: the soul wins.** A deliberately still UI overrides the baseline's motion requirements. A rigidly symmetric editorial grid overrides the baseline's asymmetry suggestions. The baseline fills gaps. The soul sets the rules.

 by /marrow

| Layer | What Marrow reads |
|---|---|
| **Visual Weight Map** | Proportional weight of every element — the number that stops agents over-applying the brand color |
| **Space & Rhythm** | Base unit, rhythm type, content-to-canvas ratio, the silence rules |
| **Typography as Personality** | Typeface voice, scale contrast, weight philosophy, tracking intent |
| **Color as Decision** | Every color with role, weight, emotional function, and hard usage rules |
| **Interaction Micro-Patterns** | Button hierarchy, touch targets, state visibility, feedback philosophy |
| **Layout & Composition DNA** | Grid discipline, alignment axis, component relationships |
| **Motion & Animation Soul** | Easing curves, duration scale, what moves and what stays still |
| **Brand Personality** | 3-word personality, voice, the one sacred rule |
| **Anti-Patterns** | 5–8 specific things this design rejects — wired as hard rules, not suggestions |

---

## Files Marrow creates

| File | What it is | Commit? |
|---|---|---|
| `.marrow.md` | The extracted design soul — source of truth for all rules | ✅ Yes |
| `.marrow-state.json` | Alignment state for smart diff — machine-specific | ❌ No (in .gitignore) |

**globals.css** is never created by Marrow — it's your existing file. Marrow's redesign command adds a `--marrow-*` token block to it and maps any conflicting old variables to the new tokens via legacy aliases. Your existing CSS is never deleted — only extended and reconciled.

---

## Why "Marrow"

Bone marrow is the living core inside the structure. You don't see it. But remove it and everything dies.

That's what this extracts — not the surface. The core.

---

## How to update the quality baseline

The quality baseline lives at `skills/marrow/references/quality-baseline.md` in the repo. It ships with a curated Level 4 SaaS standard but it's yours to edit.

**When to update it:**
- Your team has specific standards beyond the defaults (e.g., always use skeleton loaders, never use tooltips on mobile)
- You've found a pattern the baseline misses (e.g., a specific dashboard component rule)
- A benchmark reference has changed (e.g., a new product you want to align with)
- You want to add stack-specific rules (e.g., "always use Framer Motion `layoutId` for shared element transitions")

**How to update:**

```bash
# 1. Edit the baseline directly
code skills/marrow/references/quality-baseline.md

# 2. Commit and push
git add skills/marrow/references/quality-baseline.md
git commit -m "update quality baseline: [what you changed]"
git push

# 3. Anyone using your fork gets the update on next install/update
npx skills add yourusername/marrow --skill '*' -a [your-agent] -y
```

**What NOT to put in the baseline:**
- Project-specific rules (those go in `.marrow.md` via `/marrow` or `/marrow-update`)
- Rules that only apply to one brand or design style
- Anything that should vary between projects

The baseline is universal. `.marrow.md` is specific. Keep them separate.

---

## License

MIT
