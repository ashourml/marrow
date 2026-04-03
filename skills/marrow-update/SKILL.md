---
name: marrow-update
description: >
  Surgically updates a specific section of .marrow.md without re-running the full
  extraction. Accepts a new value, color, image, or description and patches only
  the relevant section — leaving everything else intact.
  Use this skill when the user wants to update one part of the extracted soul,
  change the brand accent color, update spacing rules, replace a typeface,
  refine the brand personality, or extract color from a new reference image.
  Triggers on: /marrow-update, or prompts like "update the accent color to X",
  "change the brand color", "update spacing in marrow", "the font changed to X",
  "update marrow with this new color", "patch marrow", "update just the accent",
  "marrow-update accent #FF6B6B", "update the palette from this image".
  Requires .marrow.md to exist. If not found, instructs user to run /marrow first.
---

# Marrow Update

You are a surgical `.marrow.md` patcher. The user wants to update one specific thing without re-extracting the whole soul. Your job: patch exactly what was asked, recalculate anything downstream of that change, and leave everything else untouched.

---

## Step 1 — Load the Soul

Find and read `.marrow.md` in the project root.

If not found:
```
✗ No .marrow.md found.
  Run /marrow with reference images first to extract the design soul.
  Then use /marrow-update to patch specific values.
```
Stop here.

---

## Step 2 — Identify What to Update

The user may specify:

**Color updates**
- `marrow-update accent #FF6B6B` — change the brand accent hex
- `marrow-update accent [image]` — extract a new accent from an image
- `marrow-update palette [image]` — re-extract the full color palette from a new image
- `marrow-update canvas #FAFAF8` — change the background/canvas color
- `marrow-update text #1A1A1A` — change the primary text color
- A gradient image → extract dominant colors and map them to palette roles

**Typography updates**
- `marrow-update font [Font Name]` — change the heading or body typeface
- `marrow-update heading-font [Font Name]`
- `marrow-update body-font [Font Name]`
- `marrow-update type-scale [description]` — e.g., "tighter, less dramatic contrast"

**Spacing updates**
- `marrow-update spacing [description]` — e.g., "tighter, base unit is 6px now"
- `marrow-update base-unit 6px`
- `marrow-update rhythm contextual`

**Personality updates**
- `marrow-update personality [3 words]` — e.g., "bold, irreverent, precise"
- `marrow-update sacred-rule [new rule]`
- `marrow-update anti-patterns` — re-derive anti-patterns from new context

**Motion updates**
- `marrow-update easing [curve or description]`
- `marrow-update motion slow` / `marrow-update motion fast`

**Full section replacement**
- `marrow-update colors` — re-extract color system from a new image
- `marrow-update typography` — re-derive type rules from new image or description

If the request is ambiguous, ask one clarifying question before proceeding.

---

## Step 3 — Handle Image Input (if provided)

If the user provides an image alongside the update request:

**For accent/color updates:**
- Identify the dominant color(s) in the image
- Determine which role each color serves (canvas, accent, text, surface)
- Extract approximate hex values
- Note the visual weight each color occupies in the image
- Map them to the appropriate palette slots in `.marrow.md`

**For palette updates:**
- Extract the full color story from the image
- Apply the same analysis as Phase 2.4 of `/marrow` (color as decision, not just hex)
- Replace the entire Section 4 of `.marrow.md`

**For gradient images:**
- Identify the 2–4 dominant hues in the gradient
- Determine if this suggests a color temperature shift (warm/cool)
- Update temperature and saturation strategy in Section 4

---

## Step 4 — Calculate Downstream Impact

Some updates ripple into other sections. Always check:

| Updated | May affect |
|---|---|
| Brand accent | Section 1 (weight %), Section 4 (accent rules), Section 11 (Marrow Check values) |
| Canvas color | Section 4 (temperature, contrast partners), Tailwind config |
| Full palette | Section 4 entirely, CSS custom properties, Tailwind config |
| Typeface | Section 3 (personality description), Section 0 (soul statement tone) |
| Base unit | Section 2 (all spacing rules), Section 5 (button sizing, input sizing) |
| Personality words | Section 0 (soul statement), Section 8 (anti-patterns may shift) |
| Sacred rule | Section 0, Section 8 |

List the downstream sections you're also updating and why.

---

## Step 5 — Patch .marrow.md

Write the updated sections back to `.marrow.md`. Rules:

- **Patch only** — do not regenerate sections that weren't affected
- Preserve all existing content outside the patched sections exactly
- Update the file header to note the patch:
  ```
  > Last patched: [what was updated] via /marrow-update
  ```
- Update the Tailwind config and CSS custom properties sections if color or spacing changed

---

## Step 6 — Deliver the Patch Report

```
## Marrow Update — [what was updated]

### Patched
Section [N] · [section name]
  Before: [old value]
  After:  [new value]

### Downstream updates
Section [N] · [what changed and why]

### .marrow.md saved ✓

### Impact on your codebase
[If the change is significant — e.g., accent color changed — note which
 components are most likely to need re-alignment and suggest running
 /marrow-magic or /marrow-align [filename] to propagate the change.]
```

---

## Rules for This Skill

- **Patch, never regenerate.** Only the requested section and its direct downstream effects change.
- If the user provides a vague update ("make it more warm"), interpret it as specifically as possible and confirm: "I'm updating the color temperature to warm — shifting canvas from cool gray to warm off-white. Correct?"
- If the update would fundamentally contradict the current soul (e.g., changing from a restrained minimal brand to a bold maximalist one), flag it: "This change would significantly alter the soul — consider running /marrow again with new reference images instead."
- Never delete sections from `.marrow.md`
- Always show before/after for every patched value
- After a color update, always update both the Tailwind config and the CSS custom properties sections
