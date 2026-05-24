---
name: marrow-redesign
description: >
  Full project soul alignment in one command. Scans every frontend file in the project,
  builds a prioritized plan, then systematically aligns all components and styles to
  .marrow.md. Smart enough to detect if .marrow.md was updated since the last run and
  only reprocess files affected by what changed — not a full rewrite every time.
  Use this skill when the user wants to align the entire project to the design soul at once,
  just installed marrow mid-project and wants to catch everything up, or updated .marrow.md
  via /marrow-update and wants to propagate only the changed rules across the project.
  Triggers on: /marrow-redesign, or prompts like "align the whole project", "redesign everything
  to match marrow", "apply marrow to all files", "full soul alignment", "catch everything up to
  marrow", "propagate the marrow update", "marrow everything".
  Requires .marrow.md to exist. If not found, instructs user to run /marrow first.
  This is a multi-step agentic command — it will take multiple turns to complete large projects.
  It creates a .marrow-state.json file to track progress and enable smart diff on future runs.
---

# Marrow Redesign

## CRITICAL OUTPUT RULE

**Never reproduce the full modified code in the chat window.**

The file is the output. The chat is the communication.

After writing files, deliver only a compact summary:
- What changed (specific, not a list of every line)
- Why it changed (the soul/quality reason)
- Any conflicts or flags the user should know about

Reproducing hundreds of lines of code in chat wastes the user's context window and coding limits. The agent already wrote the file. Do not write it again in chat.

---


You are running a full project soul alignment. This is the most powerful command in the Marrow system. You will scan the entire project, build a plan, and systematically bring every frontend file into alignment with `.marrow.md` — file by file, with full transparency.

This skill is smart. It tracks what it has already aligned and what changed in `.marrow.md` since the last run. On repeat invocations, it never re-aligns files that are already clean and weren't affected by recent updates.

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

## Step 1 — Load the Soul and State

### 1a. Read .marrow.md

Find and read `.marrow.md` in the project root.

If not found:
```
✗ No .marrow.md found.
  Run /marrow with reference images first to extract the design soul.
  Then run /marrow-redesign to align the whole project.
```
Stop here.

### 1b. Read .marrow-state.json

Look for `.marrow-state.json` in the project root.

This file tracks:
- Which files have been aligned and when
- The `.marrow.md` checksum at the time of last alignment per file
- Which sections of `.marrow.md` changed since the last redesign run

**If `.marrow-state.json` exists → Smart Mode (partial update)**
Read it and determine:
- Which sections of `.marrow.md` changed since last run (compare stored checksum per section vs current content)
- Which files were previously aligned and are therefore candidates for targeted re-alignment only
- Which files have never been touched and need full alignment

**If `.marrow-state.json` does not exist → First Run Mode (full alignment)**
This is a fresh install or first time running redesign. Every frontend file needs full alignment.

Announce the mode clearly:
```
Mode: [First Run — full alignment] OR [Smart Update — only propagating changes to [sections]]
```

---

## Step 2 — Discover and Inventory Frontend Files

Scan the project for all frontend files. Include:

**High priority** (align first)
- Global styles: `globals.css`, `app.css`, `index.css`, `tailwind.config.*`, `theme.*`
- Design tokens: `tokens.*`, `variables.css`, `colors.*`
- Base components: `Button`, `Input`, `Typography`, `Card`, `Badge`, `Link`
- Layout components: `Layout`, `Header`, `Nav`, `Footer`, `Sidebar`

**Medium priority**
- Feature components: anything in `components/`, `features/`, `modules/`
- Page files: `pages/`, `app/` (Next.js), `views/`

**Low priority**
- Composed pages: full page files that use components
- Storybook files (align if present, note they mirror the component)

**Exclude always**
- `node_modules/`, `dist/`, `build/`, `.next/`, `out/`
- Test files (`*.test.*`, `*.spec.*`)
- Auto-generated files (`*.generated.*`, `routeTree.gen.*`)
- Config files that aren't design tokens (`vite.config.*`, `next.config.*`, etc.)

Build a complete inventory list.

---

## Step 3 — Smart Diff (if Smart Mode)

If `.marrow-state.json` exists, determine which rules changed in `.marrow.md`:

| Changed section | Affects |
|---|---|
| Section 4 (colors) | All files using color values — global CSS, every component |
| Section 2 (spacing) | All files using spacing/padding/margin/gap |
| Section 3 (typography) | All files using font, font-size, font-weight, letter-spacing |
| Section 5 (components) | Button, Input, Card, and any component with interactive states |
| Section 7 (motion) | Any file with transitions, animations, keyframes |
| Section 6 (layout) | Layout files, page-level files |
| Section 0 (soul/personality) | No direct code impact — note in plan but no file changes |
| Section 8 (anti-patterns) | All files — anti-patterns can appear anywhere |

Build a **targeted file list**: only files where the changed sections have direct impact.

Files previously aligned and not affected by changed sections → **skip** (mark as "already aligned, no changes needed").

**globals.css is always processed** — even in Smart Mode. Any change to `.marrow.md` may affect the token block or legacy alias mapping. The safe-mode reconciliation in Step 3b is always run, but it is designed to be safe to re-run — it only patches what changed, never removes existing content.

Announce the scope reduction:
```
Smart update: .marrow.md Section 4 (colors) changed.
  globals.css: always reprocessed (safe-mode reconciliation)
  Affects: 12 of 34 component files
  Skipping: 22 files (already aligned, unaffected by color changes)
  Processing: 13 files total (globals.css + 12 components)
```

---

## Step 3b — globals.css Safe-Mode Audit

Before building the plan, run a dedicated audit on every global CSS file found (`globals.css`, `app.css`, `index.css`, `base.css`, `variables.css`, or any file that defines CSS custom properties or resets at the root level).

This step exists because `globals.css` is the most dangerous file in the project. It defines the base layer that everything else inherits from. If it contains conflicting token names, stale values, or CSS properties that contradict `.marrow.md`, every component will fight the soul no matter how well it's aligned.

### What to look for in globals.css

**Conflicting custom properties** — CSS variables that define the same concept as `.marrow.md` tokens but with different names or values:
```
/* globals.css has this: */
--primary: #7C3AED;          /* old purple */
--font-size-base: 16px;

/* .marrow.md says: */
--color-accent: #3B82F6;     /* different name, different value */
--body-size: 15px;           /* different name */
```
These will cause silent overrides. Components using `var(--primary)` will never show the Marrow accent.

**Stale resets that override Marrow's rhythm** — margin/padding resets, line-height globals, or font-size rules on `html`/`body` that contradict the extracted type scale or spacing system.

**Hardcoded values on global selectors** — `a { color: #7C3AED }`, `h1 { font-size: 2.5rem }`, `* { border-radius: 8px }` — any rule targeting broad selectors that will bleed into Marrow-aligned components.

**Old animation/transition globals** — `* { transition: all 0.3s ease }` is a common one that will override every specific duration and easing in `.marrow.md`.

**Duplicate token definitions** — the same concept defined twice under different variable names, creating ambiguity about which one components should use.

### The safe-mode rewrite rules

When rewriting `globals.css`, follow these rules in strict order:

**1 — Map, don't delete**
Never delete an old variable. Instead, map it to the new Marrow token so existing code that references the old name still works:
```css
/* BEFORE */
--primary: #7C3AED;

/* AFTER — map old name to Marrow token, comment explains */
--color-accent: #3B82F6;          /* Marrow: brand accent — ~4% visual weight */
--primary: var(--color-accent);   /* legacy alias — migrate components to --color-accent */
```
This prevents broken components while the project migrates.

**2 — Never remove existing resets that aren't conflicting**
If `box-sizing: border-box`, `margin: 0`, or other foundational resets exist and don't conflict with `.marrow.md`, leave them exactly as-is.

**3 — Resolve conflicts by scope, not deletion**
If a global selector rule (`a`, `h1`, `body`) conflicts with Marrow, scope it down or add a Marrow-specific override below it — never silently remove the original:
```css
/* Original (keep it) */
a {
  color: #7C3AED;
}

/* Marrow override (add below) */
/* marrow: link color — matches Section 4 primary text, not accent */
a {
  color: var(--color-text-primary);
}
```

**4 — Add the full Marrow token block**
After handling all existing properties, append a clearly marked Marrow token block at the end of `:root`. This is the canonical source of truth that all Marrow-aligned components will use:
```css
/* ============================================================
   MARROW DESIGN TOKENS — generated by /marrow
   Source of truth: .marrow.md
   Do not edit manually — use /marrow-update to change values
   ============================================================ */
:root {
  /* canvas */
  --marrow-canvas: [value];

  /* text */
  --marrow-text-primary: [value];
  --marrow-text-secondary: [value];
  --marrow-text-tertiary: [value];

  /* accent — USE AT [XX]% VISUAL WEIGHT ONLY */
  --marrow-accent: [value];

  /* surfaces */
  --marrow-surface: [value];
  --marrow-surface-hover: [value];

  /* borders */
  --marrow-border: [value];
  --marrow-border-focus: [value];

  /* semantic */
  --marrow-success: [value];
  --marrow-error: [value];
  --marrow-warning: [value];

  /* spacing — base unit: [N]px */
  --marrow-space-1: [1×base];
  --marrow-space-2: [2×base];
  --marrow-space-3: [3×base];
  --marrow-space-4: [4×base];
  --marrow-space-6: [6×base];
  --marrow-space-8: [8×base];
  --marrow-space-12: [12×base];
  --marrow-space-16: [16×base];

  /* typography */
  --marrow-font-display: [font], [fallback];
  --marrow-font-body: [font], [fallback];
  --marrow-font-mono: [font], monospace;

  /* motion */
  --marrow-ease: cubic-bezier([values]);
  --marrow-duration-micro: [value]ms;
  --marrow-duration-element: [value]ms;
  --marrow-duration-panel: [value]ms;

  /* radius */
  --marrow-radius-sm: [value]px;
  --marrow-radius-md: [value]px;
  --marrow-radius-lg: [value]px;
}
```

Note the `--marrow-` prefix. This prefix namespacing is intentional — it prevents collision with any existing variables and makes it immediately clear in any component file which tokens are Marrow-sourced.

**5 — Add a conflict map comment at the top of globals.css**
```css
/*
 * MARROW CONFLICT MAP
 * Old variable → New Marrow token
 * ---
 * --primary          → --marrow-accent
 * --font-size-base   → --marrow-font-body (via font-size in type scale)
 * --spacing-md       → --marrow-space-4
 * ---
 * Legacy aliases are kept below for backward compatibility.
 * Migrate components to --marrow-* tokens over time.
 * Remove aliases once migration is complete.
 */
```

### After the globals.css rewrite

Report what was found and what was done:
```
─────────────────────────────────────────
Phase 0 · globals.css — Safe-Mode Reconciliation
─────────────────────────────────────────
Conflicts found: [N]
  · --primary (#7C3AED) conflicts with --marrow-accent (#3B82F6)
    → kept as legacy alias: --primary: var(--marrow-accent)
  · body { font-size: 16px } conflicts with Marrow 15px base
    → scoped: added --marrow-font-body override below
  · * { transition: all 0.3s ease } overrides Marrow motion system
    → replaced with: * { transition: none } + specific Marrow transitions on interactive elements

Marrow token block added: [N] tokens injected into :root
Legacy aliases created: [N] (safe — old names now point to Marrow values)
Non-conflicting rules preserved: [N]

⚠ Migrate these aliases when ready:
  --primary → use --marrow-accent instead
  --spacing-md → use --marrow-space-4 instead
✓ globals.css saved
```

---

## Step 4 — Build the Alignment Plan

Before touching a single file, present the full plan to the user.

```
## Marrow Redesign — Alignment Plan

Mode: [First Run / Smart Update]
Soul: [3-word personality]
Files to align: [N] of [total N] frontend files

### Execution order

Phase 0 — globals.css reconciliation ✓ (already done above)

Phase 1 — Foundation (must go first, everything inherits from these)
  [ ] tailwind.config.ts      — sync --marrow-* tokens into Tailwind theme
  [ ] tokens.ts               — update design token values to match --marrow-* vars

Phase 2 — Base components (everything is built from these)
  [ ] Button.tsx              — [N] violations: wrong radius, wrong hover state
  [ ] Input.tsx               — [N] violations: wrong border, wrong focus ring
  [ ] Typography.tsx          — [N] violations: wrong type scale
  [ ] Card.tsx                — [N] violations: shadow (anti-pattern), wrong padding

Phase 3 — Layout components
  [ ] Header.tsx              — [N] violations: wrong spacing, wrong accent usage
  [ ] Nav.tsx                 — [N] violations: wrong active state style
  [ ] Sidebar.tsx             — [N] violations: wrong surface color

Phase 4 — Feature components
  [ ] [component]             — [N] violations
  ...

Phase 5 — Pages
  [ ] [page]                  — [N] violations
  ...

[Skipped — already aligned, unaffected by changes]
  [N] files skipped

Estimated changes: [N] total violations to fix across all files

Proceed? (Say "yes" or "go" to start, or ask to skip any phase)
```

Wait for user confirmation before proceeding.

---

## Step 5 — Execute Phase by Phase

Work through each phase in order. Rules:

**Within each file:**
- Apply the same surgical alignment logic as `marrow-align`
- Fix every violation
- Preserve all logic, props, and functionality
- Show the aligned file
- Show a compact diff summary

**Between files:**
- After completing each file, update `.marrow-state.json` immediately
- If interrupted mid-run, `.marrow-state.json` allows resuming from exactly where you left off
- Never re-process a file that was already completed in this run

**Output format per file:**
```
─────────────────────────────────────────
[Phase N] · [filename]
─────────────────────────────────────────
[aligned code]

Fixes: [N]
  · [what changed → what it is now]
  · [what changed → what it is now]
✓ Saved
```

**Phase completion:**
```
✓ Phase [N] complete — [N] files aligned, [N] violations fixed
```

---

## Step 6 — Update .marrow-state.json

After every file is aligned, write or update `.marrow-state.json`:

```json
{
  "version": "1.0",
  "last_redesign": "[ISO timestamp]",
  "marrow_checksums": {
    "section_0": "[hash of Section 0 content]",
    "section_1": "[hash]",
    "section_2": "[hash]",
    "section_3": "[hash]",
    "section_4": "[hash]",
    "section_5": "[hash]",
    "section_6": "[hash]",
    "section_7": "[hash]",
    "section_8": "[hash]"
  },
  "aligned_files": {
    "src/components/Button.tsx": {
      "aligned_at": "[ISO timestamp]",
      "violations_fixed": 4,
      "sections_applied": ["section_2", "section_4", "section_5"]
    },
    "src/styles/globals.css": {
      "aligned_at": "[ISO timestamp]",
      "violations_fixed": 8,
      "sections_applied": ["section_2", "section_3", "section_4", "section_7"]
    }
  },
  "skipped_files": {
    "src/components/Icon.tsx": {
      "reason": "already aligned, unaffected by recent changes",
      "last_aligned": "[ISO timestamp]"
    }
  }
}
```

Add `.marrow-state.json` to `.gitignore` if it's not already there (it's machine-specific state, not meant to be committed).

---

## Step 7 — Final Report

```
## Marrow Redesign — Complete

Mode: [First Run / Smart Update]

### Results
  Files aligned:  [N]
  Files skipped:  [N] (already aligned, unaffected)
  Violations fixed: [N] total
    CRITICAL: [N]
    MAJOR:    [N]
    MINOR:    [N]

### By phase
  Phase 0 globals.css:        [N] conflicts resolved · [N] Marrow tokens injected
  Phase 1 Foundation:         [N] files · [N] fixes
  Phase 2 Base components:    [N] files · [N] fixes
  Phase 3 Layout components:  [N] files · [N] fixes
  Phase 4 Feature components: [N] files · [N] fixes
  Phase 5 Pages:              [N] files · [N] fixes

### What's next
  marrow-apply is active — new components will be built in the soul automatically.

  If you update .marrow.md with /marrow-update, run /marrow-redesign again.
  It will only reprocess files affected by what changed.

  To audit any single file: /marrow-check [filename]
  To fix a specific file:   /marrow-align [filename]
```

---

## Resuming an Interrupted Run

If the user runs `/marrow-redesign` and `.marrow-state.json` shows an incomplete previous run (files in the plan that were never marked as aligned):

```
⚡ Resuming previous redesign run from [timestamp]
   Progress: [N] of [N] files completed
   Continuing from: [next file]
```

Resume from the last completed file. Do not restart from the beginning.

---

## Critical Rules for This Skill

1. **Never start executing without presenting the plan first and getting confirmation.** This command touches many files — the user must approve the scope.

2. **Smart mode is non-negotiable.** If `.marrow-state.json` exists, you MUST use it to skip unaffected files. Never do a full rewrite when only colors changed.

3. **globals.css is always Phase 0 — always safe-mode.** Run the reconciliation before anything else on every redesign run, even Smart Mode. Never delete existing CSS properties — map them to Marrow tokens with legacy aliases. The `--marrow-` prefix is mandatory for all injected tokens to prevent collision.

4. **Phase order is load-bearing.** Foundation files (global CSS, tokens, Tailwind config) must be aligned first — everything else inherits from them. Aligning a Button before aligning the token file means the Button may use stale values.

5. **Write `.marrow-state.json` after every file, not at the end.** If the run is interrupted, progress must be recoverable.

6. **Preserve all functionality.** This command touches many files at once — extra caution on preserving logic, props, event handlers, and accessibility attributes.

7. **If a file is too complex or risky to align automatically** (e.g., a 1000-line page file with complex logic tightly coupled to styles), flag it:
   ```
   ⚠ Skipped: [filename] — too complex for automated alignment.
     Run /marrow-align [filename] manually for fine-grained control.
   ```

8. **Max files per turn:** Align no more than 5 files per response turn to keep output reviewable. After each batch, pause and show progress before continuing.
