# Marrow

**Extract the living core of any UI design.**

Most tools extract colors, spacing, and font names. Marrow goes deeper — it reads the *decisions* behind a design. The restraint. The proportions. The emotional intent. The invisible rules that make a UI feel the way it does.

Give it reference images. Get back a complete rules file your agent can use to build new UI in the exact same soul.

---

## Install

```bash
npx skills add yourusername/marrow
```

Works with **Cursor**, **Windsurf**, **Claude Code**, **Antigravity**, **OpenCode**, and [37+ other agents](https://skills.sh).

```bash
# Install to a specific agent only
npx skills add yourusername/marrow -a cursor
npx skills add yourusername/marrow -a opencode
npx skills add yourusername/marrow -a claude-code
npx skills add yourusername/marrow -a windsurf

# Install globally across all your projects
npx skills add yourusername/marrow -g

# Update to the latest version anytime
npx skills update
```

---

## Usage

Drop your reference images into the conversation and invoke:

```
/marrow
```

Or just describe what you want:

```
Extract the design soul from these screenshots
Match this UI's feeling when you build components
Read this design and give me the rules
Build with the same soul as this reference
```

Marrow accepts Figma exports, live product screenshots, or any mix.

---

## What you get

A complete **agent rules file** covering:

| Layer | What it extracts |
|---|---|
| **Visual Weight Map** | Proportional weight of every element — stops agents painting everything in the brand color |
| **Space & Rhythm** | Base unit, rhythm type, content-to-canvas ratio, the silence rules |
| **Typography as Personality** | Typeface voice, scale contrast, weight philosophy, tracking intent |
| **Color as Decision** | Every color with role, weight, emotional function, and hard usage rules |
| **Interaction Micro-Patterns** | Button hierarchy, touch targets, state visibility, feedback philosophy |
| **Layout & Composition DNA** | Grid discipline, alignment axis, component relationships |
| **Motion & Animation Soul** | Easing curves, duration scale, what moves and what stays still |
| **Brand Personality** | 3-word personality, voice, the one sacred rule |
| **Anti-Patterns** | 5–8 specific things this design rejects, and why |
| **Tailwind Config** | Ready-to-paste token values |
| **CSS Custom Properties** | Full variable system |
| **Marrow Check** | 5 questions the agent asks itself before shipping any component |

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

The difference is the difference between a design that looks right and one that *feels* right.

---

## Why "Marrow"

Bone marrow is the living core inside the structure. You don't see it. But remove it and everything dies.

That's what this extracts — not the surface. The core.

---

## License

MIT
