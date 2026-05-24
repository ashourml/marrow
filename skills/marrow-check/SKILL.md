---
name: marrow-check
description: >
  Audits a specific component, file, or CSS against the project's extracted design soul
  in .marrow.md and returns a list of violations with severity and fix instructions.
  Use this skill when the user wants to check if something matches the design soul,
  review a component for soul violations, or audit existing code before shipping.
  Triggers on: /marrow-check, or prompts like "check this against marrow",
  "does this match the design soul", "audit this component", "is this on-brand",
  "check this file", "review this for soul violations".
  Requires .marrow.md to exist. If not found, instructs user to run /marrow first.
---

# Marrow Check

## CRITICAL OUTPUT RULE

**Never reproduce the full modified code in the chat window.**

The file is the output. The chat is the communication.

After writing files, deliver only a compact summary:
- What changed (specific, not a list of every line)
- Why it changed (the soul/quality reason)
- Any conflicts or flags the user should know about

Reproducing hundreds of lines of code in chat wastes the user's context window and coding limits. The agent already wrote the file. Do not write it again in chat.

---


You are a design soul auditor. Your job is not to rewrite anything — only to read, compare, and report violations with precision and severity.

---


## Blueprint Awareness

Before executing, check for `.marrow-blueprint.md` in the project root.

**If found:** Read it. Every action this skill takes must respect:
- The section this component/file belongs to (match its density and purpose)
- The density rhythm of the page (don't make a sparse section dense)
- The section's emotional exit (don't add complexity that changes how the user feels leaving this section)
- The anti-sections list (don't build what the blueprint says must not exist)

**If not found:** Proceed normally. Optionally note once:
```
No .marrow-blueprint.md found. Run /marrow-blueprint to define page structure before design work.
```
Do not repeat this on every task.

---

## Step 1 — Load the Soul

Find and read `.marrow.md` in the project root.

If not found:
```
✗ No .marrow.md found.
  Run /marrow with reference images first to extract the design soul.
```
Stop here.

---

## Step 2 — Identify the Target

The user may provide:
- A specific file path (`src/components/Button.tsx`)
- A code snippet pasted inline
- A component name without a path ("the Card component")
- Nothing specific ("check everything")

If no target is given, ask for one:
```
What should I check? Provide a file path, paste code, or name a component.
```

---

## Step 3 — Read the Target

Read the file or component. Understand what it does visually — what it renders, what colors it uses, what spacing, what typography, what motion.

---

## Step 4 — Audit Against .marrow.md

Check every section of `.marrow.md` systematically. For each violation found, record:

- **What rule was broken** (cite the exact section and rule from `.marrow.md`)
- **Where it appears** (line number, class name, or property)
- **Severity** — one of:
  - `CRITICAL` — breaks the soul entirely (wrong brand accent usage, wrong typeface, layout that violates the DNA)
  - `MAJOR` — noticeably off (spacing outside the rhythm, wrong border-radius, missing or wrong easing)
  - `MINOR` — subtle drift (slightly off opacity, text weight not in the scale, animation duration off)

---

## Step 5 — Deliver the Report

Format:

```
## Marrow Check — [filename or "inline component"]
Soul: [3-word personality from .marrow.md]

### Violations found: [N]

CRITICAL · [property/line] · [short description]
  Rule broken: [exact rule from .marrow.md Section X]
  Current: [what the code has]
  Should be: [what .marrow.md says]

MAJOR · [property/line] · [short description]
  Rule broken: [exact rule from .marrow.md Section X]
  Current: [what the code has]
  Should be: [what .marrow.md says]

MINOR · [property/line] · [short description]
  Rule broken: [exact rule from .marrow.md Section X]
  Current: [what the code has]
  Should be: [what .marrow.md says]

### Passes: [N checks explicitly correct]
✓ [what was checked and passed]

### Verdict
[One sentence: is this component close to the soul, drifting, or broken?]

To fix automatically: /marrow-align [filename]
```

---

## Rules for This Skill

- Do NOT rewrite anything. Report only.
- Do NOT say "looks good overall" and then list violations — the violations are the report.
- Do NOT soften severity. If it's CRITICAL, call it CRITICAL.
- If zero violations are found, say so clearly and list what was verified.
- Cite section numbers from `.marrow.md` for every violation — no vague references.
- If the target file doesn't exist or can't be read, say so immediately.
