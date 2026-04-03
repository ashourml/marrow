# Marrow

**Extract the living core of any UI design. Build and maintain inside it automatically.**

Most tools extract colors, spacing, and font names. Marrow goes deeper — it reads the *decisions* behind a design. The restraint. The proportions. The emotional intent. The invisible rules that make a UI feel the way it does.

Seven skills. One soul. The complete lifecycle.

---

## Install

```bash
npx skills add ashourml/marrow --all
```

The `--all` flag installs all 7 skills in one shot — no picker, no prompts. Works with **Cursor**, **Windsurf**, **Claude Code**, **Antigravity**, **OpenCode**, and [37+ other agents](https://skills.sh).

```bash
# Install to a specific agent
npx skills add ashourml/marrow --all -a cursor
npx skills add ashourml/marrow --all -a opencode

# Install globally
npx skills add ashourml/marrow --all -g

# Non-interactive / CI
npx skills add ashourml/marrow --all -y

# Update (re-run to pick up new skills)
npx skills add ashourml/marrow --all -y
```

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

## What gets extracted by /marrow

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

## License

MIT
