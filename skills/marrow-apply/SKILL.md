---
name: marrow-apply
description: >
  Automatically injects the project's extracted design soul into any frontend task.
  Use this skill on EVERY request that involves building, editing, or reviewing UI —
  including components, pages, layouts, styles, animations, and design decisions.
  Triggers on: any prompt containing words like "build", "create", "make", "design",
  "component", "page", "layout", "button", "form", "card", "nav", "header", "modal",
  "style", "css", "tailwind", "animate", "responsive", "ui", "frontend", "screen",
  "dashboard", "landing", "section", or any request to write JSX, TSX, HTML, or CSS.
  Do NOT trigger on backend-only tasks, database queries, API routes with no UI, or
  pure logic/utility functions with no visual output.
  This skill has no slash command — it runs silently in the background on every
  frontend task. The user never needs to invoke it manually.
---

# Marrow Apply

You are about to build something visual. Before writing a single line of code, this skill loads two things: the **quality baseline** (the floor every UI must meet) and the **project soul** (what makes this UI specifically this UI). Both govern everything you produce. When they conflict, the soul wins.

---

## Step 1 — Load the Quality Baseline

Read `references/quality-baseline.md` from the Marrow skill directory.

This is the universal quality floor — Level 4 SaaS standard. It applies to every project regardless of what `.marrow.md` contains. It defines minimum standards for layout, typography, components, motion, product psychology, and responsiveness.

**Critical rule:** The baseline is the floor. `.marrow.md` is the law. When they conflict — `.marrow.md` always wins. Use the baseline to fill gaps where `.marrow.md` is silent. Never use it to override what `.marrow.md` explicitly defines.

---

## Step 2 — Check for .marrow.md

Look for `.marrow.md` in the project root (and parent directories up to the git root).

**If found:** Read it completely. Every rule in it applies to this task and overrides any conflicting baseline rule. Proceed to Step 3.

**If not found:** Do not block the task. Prepend this notice once:

```
⚠ No .marrow.md found in this project.
  Run /marrow with reference images to extract the design soul.
  Building to Level 4 quality baseline for now — no project soul applied.
```

Then build using only the quality baseline. Do not mention this again in the same session.

---

## Step 3 — Internalize Before You Build

Do not skim `.marrow.md`. Read it as instructions, not documentation.

Before touching the task, answer these internally:

1. **What is the soul of this design in one sentence?** (from Section 0)
2. **What is the brand accent, and what percentage of visual area should it cover?** (from Section 1 + 4)
3. **What spacing unit governs this design, and what rhythm type?** (from Section 2)
4. **What are the 3 brand personality words?** (from Section 0)
5. **What are the top 3 anti-patterns I must not do?** (from Section 8)
6. **What does the quality baseline say about this component type?** (from `quality-baseline.md` — components, motion, product thinking sections)

If you cannot answer 1–5 from `.marrow.md`, the file is incomplete — flag which sections are missing and note which baseline defaults you're using instead.

---

## Step 4 — Build Inside the Soul

Now build what the user asked for. Every decision must satisfy two layers simultaneously:

**Layer 1 — Quality Baseline** (`references/quality-baseline.md`): Does this meet Level 4 standards? Are all states designed? Is motion intentional? Is hierarchy obvious? Is every component custom-crafted?

**Layer 2 — Project Soul** (`.marrow.md`): Is this traceable to a specific rule in the soul? Color, spacing, type, motion, composition — all must come from the extracted soul.

When both layers are satisfied: ship. When they conflict: **soul wins**.

### Enforcement rules while building:

**Color**
- Use only the colors defined in `.marrow.md` Section 4
- Apply the brand accent at its documented visual weight — not more
- If `.marrow.md` is silent on a semantic color (success, error), use baseline defaults

**Spacing**
- Use the base unit from `.marrow.md` Section 2 for all spacing values
- Apply the rhythm type exactly — never tighten spacing to fit more in
- If `.marrow.md` is silent on a specific spacing context, use baseline rhythm rules

**Typography**
- Use the typefaces and scale from `.marrow.md` Section 3 only
- Never introduce a font weight not documented in the soul
- Apply tracking rules exactly — if all-caps labels use 0.08em, every all-caps label uses 0.08em

**Components**
- Follow the button hierarchy from `.marrow.md` Section 5
- Every component must have all states designed (baseline requirement — non-negotiable)
- Match the border-radius documented in the soul exactly
- Follow the interactive feedback philosophy from the soul — quiet if restrained, tactile if expressive

**Motion**
- Use the easing curve and duration scale from `.marrow.md` Section 7
- If the soul's motion personality is "still" — honor it. The baseline says motion is mandatory but **soul wins**
- If the soul has no motion section — use baseline motion standards as default

**Layout**
- Follow the grid and alignment axis from `.marrow.md` Section 6
- Apply baseline layout variety (section rhythm, progressive storytelling) within the soul's compositional rules
- Respect the content-to-canvas ratio — don't fill every pixel

**Product psychology**
- Always apply baseline product psychology rules (trust signals, anxiety reducers, CTA logic)
- These are rarely defined in `.marrow.md` and the baseline governs them by default

---

## Step 5 — Pre-Output Audit

Before showing the result, run both audits internally. Fix failures before delivering.

**Soul audit** (`.marrow.md` Section 11 — Marrow Check):
1. Weight check — brand accent at correct visual proportion?
2. Silence check — canvas-to-content ratio correct?
3. Voice check — does this feel like the 3-word personality?
4. Anti-pattern check — none of the 8 prohibited things present?
5. Removal check — soul intact without the accent?

**Quality audit** (`quality-baseline.md` — Pre-Output Audit):
- [ ] Does this feel templated? → add one distinctive decision if yes
- [ ] Is hierarchy obvious at a glance? → increase contrast between levels if no
- [ ] Are all component states designed? → if any state is missing, it's not done
- [ ] Does every animation improve clarity? → remove it if not
- [ ] Does this build trust and feel premium? → find what makes it feel unfinished if no

Do not mention the audits to the user unless a violation required a decision they should know about.

If a request conflicts with the soul:

```
⚠ Soul conflict: [what was requested] conflicts with [specific .marrow.md rule].
  The closest option that maintains the soul is [X].
  I've used [X] — let me know if you want to override.
```

Never silently break the soul. Never silently refuse. Flag and offer the closest valid alternative.

---

## What This Skill Does NOT Do

- Does not re-run the extraction (that's `/marrow`)
- Does not ask the user questions before building — reads both files and acts
- Does not override user requests — channels them through soul + baseline
- Does not trigger on non-visual tasks (APIs, database, logic, tests with no UI)

---

## If .marrow.md Is Stale or Wrong

Re-run `/marrow` at any time to overwrite `.marrow.md`. The quality baseline never changes between projects — only `.marrow.md` changes.
