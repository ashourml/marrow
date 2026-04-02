# Marrow

**Extract the living core of any UI design. Build inside it automatically.**

Most tools extract colors, spacing, and font names. Marrow goes deeper — it reads the *decisions* behind a design. The restraint. The proportions. The emotional intent. The invisible rules that make a UI feel the way it does.

Two skills. One workflow.

---

## Install

```bash
npx skills add yourusername/marrow
```

Works with **Cursor**, **Windsurf**, **Claude Code**, **Antigravity**, **OpenCode**, and [37+ other agents](https://skills.sh).

```bash
# Install to a specific agent
npx skills add yourusername/marrow -a cursor
npx skills add yourusername/marrow -a opencode
npx skills add yourusername/marrow -a claude-code

# Install globally across all your projects
npx skills add yourusername/marrow -g

# Update anytime
npx skills update
```

---

## How it works

### Step 1 — Extract once per project

Drop your reference images and run:

```
/marrow
```

Marrow reads the images across 9 analysis layers — visual weight, space & rhythm, typography as personality, color as decision, interaction patterns, layout DNA, motion soul, brand personality, and anti-patterns — then writes everything to `.marrow.md` in your project root.

### Step 2 — Build. Forever.

That's it. From this point, every frontend task you give the agent is automatically intercepted by `marrow-apply`. It reads `.marrow.md` silently, internalizes the soul, and builds inside it — without you ever mentioning it again.

```
"build a settings page"     → marrow-apply reads .marrow.md → builds in the soul
"create a modal component"  → marrow-apply reads .marrow.md → builds in the soul
"make a navigation bar"     → marrow-apply reads .marrow.md → builds in the soul
```

No slash command. No manual reference. It just works.

---

## The two skills

| Skill | Invocation | What it does |
|---|---|---|
| `marrow` | `/marrow` — run once | Reads reference images → extracts soul → saves `.marrow.md` |
| `marrow-apply` | Automatic | Intercepts every frontend task → reads `.marrow.md` → builds inside the soul |

---

## What gets extracted

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

Plus: Tailwind config, CSS custom properties, and the Marrow Check — 5 questions the agent asks itself before shipping any component.

---

## The problem it solves

Standard token extraction gives agents:

```
--color-primary: #3B82F6
```

The agent uses blue on everything.

Marrow gives agents:

```
Brand accent — #3B82F6
Visual weight: ~4% of UI
Appears exclusively on: primary CTAs and selected states
NEVER appears on: backgrounds, borders, body text
Emotional function: signals something can be acted on
Danger zone: using it as fill turns punctuation into wallpaper
```

And then `marrow-apply` makes sure the agent reads that *before* it writes a single component — every time, automatically.

---

## Soul conflicts

If a user request conflicts with the extracted soul, `marrow-apply` doesn't silently break it — it flags and offers the closest valid alternative:

```
⚠ Soul conflict: This design's palette doesn't include red (Section 4).
  The closest option that maintains the soul is [X].
  I've used [X] — let me know if you want to override.
```

---

## Why "Marrow"

Bone marrow is the living core inside the structure. You don't see it. But remove it and everything dies.

That's what this extracts — not the surface. The core.

---

## License

MIT
