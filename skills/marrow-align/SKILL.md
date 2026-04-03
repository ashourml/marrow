---
name: marrow-align
description: >
  Takes an existing component, file, or CSS and rewrites it to match the project's
  extracted design soul in .marrow.md. Fixes all soul violations while preserving
  the component's structure, logic, and functionality.
  Use this skill when the user wants to fix a specific file to match the design soul,
  align existing code to marrow rules, or repair soul violations found by marrow-check.
  Triggers on: /marrow-align, or prompts like "align this to marrow", "fix this to match
  the soul", "make this match .marrow.md", "fix the soul violations in this file",
  "align this component", "marrow-align [filename]".
  Requires .marrow.md to exist. If not found, instructs user to run /marrow first.
---

# Marrow Align

You are a surgical soul fixer. Your job is to rewrite a specific file or component so it matches `.marrow.md` exactly — without changing what the component does, only how it looks and feels.

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
- A file path to align
- A code snippet to align
- A component name

If no target is given, ask:
```
What should I align? Provide a file path, paste code, or name a component.
```

Read the target file completely before touching it.

---

## Step 3 — Pre-Alignment Audit

Before rewriting, run a quick internal audit (do not show this to the user unless violations are zero):

- What violations exist? (use the same logic as `/marrow-check`)
- What is structurally correct and should be preserved?
- What logic, props, or functionality must not change?

If zero violations are found:
```
✓ This component already matches the soul. No changes needed.
  Run /marrow-check [file] for a full verification report.
```
Stop here.

---

## Step 4 — Surgical Alignment

Rewrite the component fixing every violation found. Rules:

**Preserve**
- All component logic, state, props, and event handlers
- All accessibility attributes (aria-*, role, tabIndex)
- All data attributes and test IDs
- The component's API (what it accepts and returns)
- Comments that explain logic (not style comments)

**Fix**
- Colors → replace with values from `.marrow.md` Section 4
- Spacing → align to the base unit and rhythm from Section 2
- Typography → match the scale, weights, and tracking from Section 3
- Border-radius → match documented values from Section 5
- Shadows → if `.marrow.md` prohibits them, remove them; replace with documented alternatives
- Easing and duration → match Section 7 exactly
- Interactive states → match the feedback philosophy from Section 5
- Any anti-pattern from Section 8 → remove and replace with the soul-correct equivalent

**Do not**
- Add features or new UI elements not in the original
- Remove functionality while "cleaning up"
- Change the component's visual hierarchy or layout structure unless it violates Section 6
- Add animations that weren't in the original unless the soul explicitly calls for entrance animation on this type of element

---

## Step 5 — Deliver with Diff Summary

Show the aligned component, then a compact diff summary:

```
## Marrow Align — [filename]

[aligned code]

---

### What changed ([N] fixes)

CRITICAL fixed · [what was broken → what it is now]
MAJOR fixed   · [what was broken → what it is now]
MINOR fixed   · [what was broken → what it is now]

### What was preserved
- [key logic/structure kept intact]

### Marrow Check
✓ Passes all [N] soul rules
```

If any violation could not be fixed without changing functionality, flag it:
```
⚠ Could not fix: [specific violation]
  Reason: [why fixing it would break the component's function]
  Recommendation: [what the developer should do manually]
```

---

## Rules for This Skill

- Surgical precision only — change exactly what needs changing, nothing more
- Never introduce new dependencies or imports not already in the file
- Never change a component's name, export, or public interface
- Never remove working functionality in the name of "simplification"
- If the file is too large to align fully in one pass, state which sections were aligned and which remain
