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

You are about to build something visual. Before writing a single line of code, this skill loads the project's design soul and makes it the law for everything you produce.

---

## Step 1 — Check for .marrow.md

Look for `.marrow.md` in the project root (and parent directories up to the git root).

**If found:** Read it completely. Every rule in it applies to this task. Proceed to Step 2.

**If not found:** Do not block the task. Instead, prepend a brief notice to your response:

```
⚠ No .marrow.md found in this project.
  Run /marrow with reference images to extract the design soul.
  Building with general best practices for now.
```

Then proceed with high-quality frontend defaults. Do not ask the user to run `/marrow` repeatedly — say it once.

---

## Step 2 — Internalize Before You Build

Do not skim `.marrow.md`. Read it as instructions, not documentation.

Before touching the task, answer these internally:

1. **What is the soul of this design in one sentence?** (from Section 0)
2. **What is the brand accent, and what percentage of visual area should it cover?** (from Section 1 + 4)
3. **What spacing unit governs this design, and what rhythm type?** (from Section 2)
4. **What are the 3 brand personality words?** (from Section 0)
5. **What are the top 3 anti-patterns I must not do?** (from Section 8)

If you cannot answer all 5 from `.marrow.md`, the file is incomplete — flag which sections are missing and note what defaults you're using.

---

## Step 3 — Build Inside the Soul

Now build what the user asked for. Every decision — spacing, color, type, motion, component structure — must be traceable back to a rule in `.marrow.md`.

### Enforcement rules while building:

**Color**
- Use only the colors defined in Section 4
- Apply the brand accent at its documented visual weight — not more
- If you find yourself reaching for a color not in the palette, stop and find the closest documented color instead

**Spacing**
- Use the base unit from Section 2 for all spacing values
- Apply the rhythm type: if it's contextual, tight inside components and generous between. If regular, stick to the scale
- Never tighten spacing to "fit more in" — that breaks the silence rule

**Typography**
- Use the typefaces and scale from Section 3 only
- Never introduce a new font weight that isn't documented
- Apply tracking rules exactly — if all-caps labels use 0.08em, every all-caps label uses 0.08em

**Components**
- Follow the button hierarchy from Section 5 — don't invent a new button style
- Match the border-radius documented — don't round corners more because it "looks friendlier"
- Follow the interactive feedback philosophy exactly

**Motion**
- Use the easing curve from Section 7 as the default for all transitions
- Use the duration scale — don't use 300ms if the scale says micro interactions are 100ms
- If the design's motion personality is "still", do not add hover animations that weren't explicitly asked for

**Layout**
- Follow the grid and alignment axis from Section 6
- Respect the content-to-canvas ratio — don't fill every pixel
- Never break the layout DNA (e.g., if it's editorial, don't make it look like a dashboard)

---

## Step 4 — Marrow Check Before Delivering

Before showing the result, run the Marrow Check from Section 11 of `.marrow.md` internally.

If any check fails:
- Fix the violation before delivering
- Do not mention the check to the user unless a violation required a significant decision they should know about

If a check cannot pass because the user's request conflicts with the soul (e.g., "make this button bright red" when the palette has no red), **flag it clearly**:

```
⚠ Soul conflict: This design's palette doesn't include red (Section 4).
  The closest option that maintains the soul is [X].
  I've used [X] — let me know if you want to override.
```

Never silently break the soul. Never silently refuse. Flag and offer the closest valid alternative.

---

## What This Skill Does NOT Do

- It does not re-run the extraction (that's `/marrow`)
- It does not ask the user questions before building — it reads `.marrow.md` and acts
- It does not override user requests — it channels them through the soul
- It does not trigger on non-visual tasks (APIs, database, logic, tests with no UI)

---

## If .marrow.md Is Stale or Wrong

The user can re-run `/marrow` at any time with new images to overwrite `.marrow.md`. This skill always reads the current file — no cache, no memory of previous versions.
