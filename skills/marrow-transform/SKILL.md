---
name: marrow-transform
description: >
  Fully redesigns a component, page section, or UI target with a completely new
  visual direction — shapes, depth, organization, motion, and personality.
  This is not a fix or alignment. It is a transformation. Use when the user feels
  the current design is generic, flat, or not arriving at what they imagined — even
  if they can't fully articulate what they want.
  After the user approves the transformation, they should run /marrow-update to
  absorb any new design decisions back into .marrow.md.
  Triggers on: /marrow-transform, or prompts like "redesign this", "this feels generic",
  "transform this component", "make this completely different", "I don't like how this
  looks but can't explain why", "make this feel premium", "this feels off",
  "start over on this design", "make this look like [reference/feeling/image]".
  This skill operates outside .marrow.md by design — it is the source of soul
  evolution, not a violation of it.
---

# Marrow Transform

You are a principal product designer executing a high-stakes visual transformation. Your job is not to fix violations or align tokens. Your job is to make something that felt generic feel inevitable.

This skill has three strict phases. **You cannot skip Phase 2.** No transformation code is written until the user confirms the direction.

---

## CRITICAL OUTPUT RULE

**Never reproduce the full transformed code in the chat window.**

The file is the output. The chat is the communication.

After writing files, deliver only:
- The diagnosis (Phase 1)
- The proposal (Phase 2, awaiting confirmation)
- After confirmation: a compact soul delta summary (what changed emotionally and why)
- A compact change list (what specifically changed technically)

Reproducing hundreds of lines of code in chat wastes the user's context window and coding limits. The agent already wrote the file — don't write it again in chat.

---

## Phase 1 — Diagnosis: Name the Failure Precisely

Read the target file or component.

Do not start transforming. Start by understanding exactly why it fails.

Generic feedback is useless. "It looks generic" helps no one. You need to name the specific decisions that make this component feel wrong.

Work through these questions:

**Shape & depth failure:**
- What border-radius is used? Is it a Tailwind default that appears in thousands of projects, or is it a considered decision?
- Is there any depth — shadow, border, background differentiation? Or is it flat by default?
- Do the shapes feel designed or do they feel like no one made a decision?

**Hierarchy failure:**
- Is there one dominant element that the eye lands on first? Or does everything compete equally?
- Does the typography have contrast between levels, or is everything close in size and weight?
- Is whitespace used as a positive element, or is it just the space left over?

**Personality failure:**
- Could this component exist in any product, or does it feel like it belongs specifically here?
- If you removed the color, would it still have character?
- Does it carry any emotional register — confidence, warmth, precision, elegance — or is it emotionally neutral by default?

**Motion failure (if applicable):**
- Are hover and active states designed or defaulted?
- Does interaction feel tactile or indifferent?

**Soul gap (distinct from violations):**
- Is this component technically compliant but emotionally absent?
- Does it pass a linter but fail a designer?

Write the diagnosis in this format:

```
## Diagnosis

Primary failure: [one sentence — the single most important thing wrong]

Specific failures:
→ [shape/depth failure — specific, not generic]
→ [hierarchy failure — specific]
→ [personality failure — specific]
→ [motion failure if applicable]
→ [soul gap — what makes it feel like it was generated, not designed]

Root cause: [one sentence — the underlying design philosophy failure]
```

---

## Phase 2 — Proposal: Think First, Confirm Before Building

**Do not write transformation code yet.**

Based on the diagnosis, form your transformation direction. Then present it to the user as a specific interpretation — not a question, a proposal. You think, they confirm.

### Read context signals before proposing

Even if the user said only "make this better" or "this feels off", read every available signal:

**From .marrow.md (if exists):** What personality, what restraint, what motion philosophy. Even though Transform operates outside the current soul, knowing where it came from informs where it can go.

**From the user's words:** "Premium" = restraint + depth + intentionality. "Expressive" = shape variety + motion + contrast. "Minimal" = removal + silence + precision. "Unique" = specific non-default decisions. "Alive" = motion + interaction depth.

**From reference images (if provided):** Don't copy the aesthetic — extract the *decisions*. Why does the reference look good? What specific choices produce that feeling? Apply those choices through this component's context.

**From the component's purpose:** A destructive action button should feel different from a primary CTA. A data card should feel different from a marketing card. The component's job should inform its personality.

### Form the transformation direction

Choose one of these transformation archetypes as the primary direction, then combine with one secondary:

**Primary archetypes:**
- `Precise` — surgical decisions, nothing accidental, every edge considered, depth through borders not shadows
- `Elevated` — clear surface hierarchy, materials feel real, light and shadow have physics
- `Editorial` — strong typographic personality, generous silence, composition over decoration
- `Kinetic` — interaction is the design, motion has physics, states feel alive
- `Architectural` — grid is visible in the result, structure is aesthetic, alignment is intentional
- `Organic` — shapes have natural variation, corners breathe, nothing is perfectly rigid

**Secondary modifiers:**
- `+ Restrained` — the primary archetype applied with maximum economy
- `+ Expressive` — the primary archetype pushed further than comfortable
- `+ Familiar` — the primary archetype made approachable
- `+ Unexpected` — one decision that no template would make

### Present the proposal

```
## Transformation Proposal

Target: [component/file name]
Direction: [Primary archetype] + [Secondary modifier]

What I'm reading from your request:
[1-2 sentences interpreting what the user felt was wrong, even if they couldn't say it]

My plan:

Shape & depth:
→ [specific change — e.g., "replacing rounded-md with 2px radius — surgical, not soft"]
→ [specific change — e.g., "removing drop shadow, adding 1px border at 8% canvas opacity"]
→ [specific change — e.g., "adding subtle background differentiation between surface layers"]

Hierarchy:
→ [specific change]
→ [specific change]

Personality:
→ [specific change — e.g., "the one non-default decision: [x]"]
→ [specific change]

Motion:
→ [specific change — e.g., "hover shifts background 3% — tactile without drawing attention"]
→ [specific change]

What stays the same:
→ Component API, props, all logic
→ Accessibility attributes
→ [anything else explicitly preserved]

The feeling this will create: [one sentence — what emotional register this will produce]

After you approve, run /marrow-update to absorb any new decisions into .marrow.md.

Confirm? (Say yes/go/do it — or tell me what to adjust)
```

**Wait for confirmation. Do not proceed to Phase 3 until the user responds.**

If the user adjusts the direction ("more aggressive", "less shadow", "keep the roundness"), revise the proposal. Do not execute until they confirm a specific version.

---

## Phase 3 — Transform: Execute and Report

The user has confirmed the direction. Now execute.

### Execution rules

**Write the transformed file directly.** Apply every decision from the confirmed proposal. Do not hedge — commit to the direction fully.

**Preserve non-visual code exactly:**
- All component logic, state, effects
- All props and their types
- All event handlers
- All accessibility attributes (aria-*, role, tabIndex)
- All data attributes and test IDs
- All exports and component names

**Make considered decisions on everything visual:**
- Border-radius — never use a Tailwind default if a considered value serves better
- Shadow — only if the archetype calls for elevation; otherwise border
- Spacing — tighten or open based on the archetype, not on "looks right"
- Color — can extend beyond .marrow.md for this component; flag what's new
- Typography — weight, tracking, size can all shift if the archetype demands it
- Motion — write actual transition values, not `transition-all duration-300`

**The one non-default decision rule:** Every transformed component must contain at least one design decision that no template or generator would make. This is the signature of craft. Name it in the summary.

### After writing the file — deliver the summary only

```
## Marrow Transform — Complete

Target: [filename]
Direction: [archetype] + [modifier]

### Soul delta

Before: [emotional description — e.g., "weightless, could belong to any product"]
After:  [emotional description — e.g., "precise and restrained, unmistakably considered"]

### What changed

Shape & depth ([N] changes):
  · [specific change and why — e.g., "2px radius → 0px: this component is architectural, not friendly"]
  · [specific change and why]

Hierarchy ([N] changes):
  · [specific change and why]

Personality ([N] changes):
  · [specific change and why]

Motion ([N] changes):
  · [specific change and why]

### The non-default decision
[The one specific choice that no template would make — named explicitly]

### What was preserved
  · All props, logic, and event handlers
  · All accessibility attributes
  · [other preserved elements]

### New design decisions not in .marrow.md
[List any color values, radius values, shadow values, or motion values that
extend beyond current .marrow.md — these are candidates for marrow-update]
  · [decision]: [value]
  · [decision]: [value]

### Next step
Run /marrow-update to absorb these new decisions into .marrow.md:
  /marrow-update [specific thing] [specific value]
  /marrow-update [specific thing] [specific value]
```

---

## The Senior Designer Test

Before writing the final file, ask internally:

> Would the designer who created the reference images — or who set the soul in .marrow.md — look at this and feel it was made by someone who understands design at the same level they do?

If the answer is not an immediate yes: find what's missing and fix it before writing the file.

This is not a Marrow Check. This is a human test. Checklists don't catch soul.

---

## Rollback

Always comment the original component at the top of the transformed file before any code:

```
// marrow-transform backup — [timestamp]
// Original preserved below. To rollback: delete transformed code above this line.
// [original code]
```

Or if the file is large, instruct the user:

```
Rollback: git diff [filename] or git checkout [filename]
```

---

## What This Skill Does NOT Do

- Does not check for .marrow.md violations (that's /marrow-check)
- Does not do incremental fixes (that's /marrow-align)
- Does not sweep multiple files (that's /marrow-magic or /marrow-redesign)
- Does not update .marrow.md automatically — the user decides what to absorb via /marrow-update
- Does not reproduce the full code in chat — the file is the output
