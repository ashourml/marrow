---
name: marrow-magic
description: >
  Scans the current project's frontend files, finds the components most out of
  alignment with .marrow.md, and fixes them automatically — without the user
  specifying a target. The zero-argument soul alignment sweep.
  Use this skill when the user wants to broadly align the project to the design soul,
  fix whatever is most off without specifying a file, or run a soul sweep across
  multiple components at once.
  Triggers on: /marrow-magic, or prompts like "fix everything to match marrow",
  "align my whole project", "soul sweep", "fix the worst violations",
  "everything feels off", "clean up all components to match the design".
  Requires .marrow.md to exist. If not found, instructs user to run /marrow first.
---

# Marrow Magic

You are running a soul sweep. No target was specified — you find the worst offenders yourself, prioritize them, and fix them.

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

## Step 2 — Discover Frontend Files

Scan the project for frontend files. Priority order:

1. `src/components/` — component files (`.tsx`, `.jsx`, `.vue`)
2. `src/app/` or `src/pages/` — page-level files
3. `src/styles/` or any global CSS/Tailwind files
4. Any file the user has open or recently modified (if determinable from context)

Exclude: test files, Storybook files, node_modules, generated files, `.d.ts` files.

If no frontend files are found, say:
```
✗ No frontend files found in standard locations.
  Point me at a specific file with /marrow-align [filename].
```

---

## Step 3 — Triage by Soul Violation Severity

Quickly scan found files and score each one by soul violations. Prioritize:

1. Files with CRITICAL violations (wrong brand accent, wrong typeface, anti-pattern violations)
2. Files with many MAJOR violations
3. Shared/global files (a broken global CSS breaks everything downstream)

Select the **top 3 most violated files** to fix in this pass. Do not attempt to fix everything — depth over breadth.

Tell the user what you found before fixing:

```
## Marrow Magic — Soul Sweep

Found [N] frontend files. Biggest soul violations:

1. [filename] — [N] violations ([severity summary])
2. [filename] — [N] violations ([severity summary])
3. [filename] — [N] violations ([severity summary])

Fixing all three now...
```

---

## Step 4 — Fix Each File

For each of the top 3 files, apply the same surgical alignment logic as `marrow-align`:

- Fix all violations
- Preserve all logic and functionality
- Show the fixed file
- Show a compact diff summary

Format per file:

```
### [filename] — [N] fixes

[aligned code]

Changes: [bullet list of what changed]
```

---

## Step 5 — Session Summary

After all fixes:

```
## Sweep complete

Fixed [total N] soul violations across [N] files.

Remaining: [N] files with violations not yet fixed.
Run /marrow-magic again to continue the sweep, or target a specific file with /marrow-align [filename].

Untouched files with known violations:
- [filename] — [N] violations
- [filename] — [N] violations
```

---

## Rules for This Skill

- Never fix more than 3 files per invocation — keeps output focused and reviewable
- Always show what you're going to fix BEFORE fixing it
- Never touch files outside src/ or the project's source directory
- Never modify config files, package.json, or non-UI files
- If a file has zero violations, skip it silently — don't report "checked and passed" for every file
- Preserve every component's public API, logic, and functionality
