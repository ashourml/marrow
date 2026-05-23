# Quality Baseline — Level 4 SaaS UI Standard

This file defines the **minimum quality floor** for every frontend task in Marrow.

It applies universally — on every project, for every component, regardless of what `.marrow.md` contains.

## Precedence Rule

**This baseline is the floor. `.marrow.md` is the law.**

When this baseline and `.marrow.md` conflict — `.marrow.md` always wins.

Examples:
- This baseline says "use spring physics" → `.marrow.md` says "this UI is deliberately still" → **no spring physics**
- This baseline says "bento grids, asymmetry" → `.marrow.md` says "strict symmetric editorial grid" → **strict symmetric grid**
- This baseline says "one primary accent, restraint" → `.marrow.md` defines exact restraint levels → **follow `.marrow.md` exactly**

Use this baseline to fill gaps where `.marrow.md` is silent. Never use it to override what `.marrow.md` explicitly defines.

---

## What "Level 4" Means

There are 4 levels of UI output quality:

- **Level 1** — Functional. Works. Looks like a default template.
- **Level 2** — Styled. Colors applied. Looks designed but generic.
- **Level 3** — Polished. Spacing, type, components refined. Acceptable.
- **Level 4** — Inevitable. Every decision feels like the only right decision. Premium. Crafted.

**Never ship below Level 4.** The first draft is always incomplete. Refine before output — do not wait for the user to ask.

Benchmark reference: Linear, Stripe, Raycast, Vercel, Notion, Framer, Perplexity, Arc, Resend, Ramp.

---

## The Core Principle

Good UI is not decoration. Good UI is:

- hierarchy — the eye knows what matters first, second, and what action to take
- flow — the user moves through the screen without friction or confusion
- spacing — silence is structure, not waste
- interaction — every state is designed, not defaulted
- product psychology — every element reduces anxiety or builds trust
- visual rhythm — sections have variety, not uniform stacking
- attention control — contrast and weight are resources, used intentionally
- emotional trust — the UI makes the user feel the product is worth their time
- perceived performance — the UI feels fast even when it isn't
- motion craft — animation guides, never decorates
- micro-detail consistency — nothing is accidentally inconsistent

---

## Layout — Minimum Standards

### Always create
- Visual rhythm between sections — no two adjacent sections should have identical density
- Section variety — alternate between sparse/dense, wide/narrow, text-heavy/visual
- Breathing space — content needs room to exist; silence is not wasted space
- Progressive storytelling — the page has a narrative arc, not just stacked information
- Strong vertical spacing rhythm — sections feel distinct without needing dividers

### Required layout patterns (use contextually, not blindly)
- Bento grids for feature showcases
- Modular card layouts with depth hierarchy
- Asymmetric compositions where content warrants it
- Visual anchors — one dominant element per section that the eye lands on first
- Layered backgrounds — subtle depth through surface differentiation
- Responsive max-width systems — content never stretches to full viewport width

### Never do
- Repetitive "text left / image right" sections stacked without variation
- Template-looking sections where every row looks identical
- Generic uniform card rows with no hierarchy between them
- Endless centered text blocks stacked without rhythm
- Flat sections with no visual differentiation between them

---

## Typography — Minimum Standards

### Always enforce
- Strong heading/body size contrast — the hierarchy must be obvious at a glance
- Tight headlines — headings should be punchy, not paragraph-length
- Short copy blocks — no paragraph walls; break up text with whitespace and visual elements
- Maximum scanability — the user should understand the page without reading every word
- Strong leading on body text — never cramped line-height
- Weight contrast that earns its place — don't use bold randomly

### Copy voice
Transform every label, heading, and CTA from "what it does" to "how it helps":
- ❌ "Analyze your resume using AI"
- ✅ "Know exactly why recruiters reject your CV"

Headlines sell outcomes. Subheads explain the mechanism. CTAs name the next step.

### Never do
- Font sizes that are too close together between levels (creates no hierarchy)
- Paragraph walls — more than 4–5 lines of dense text without visual relief
- Arbitrary font weight changes that don't serve hierarchy
- Letter-spacing applied inconsistently or without purpose

---

## Component Quality — Minimum Standards

Every component must feel custom-crafted, not template-applied.

### Buttons — minimum requirements
- Hover state: must exist, must feel tactile (not just cursor change)
- Active/pressed state: slight scale or opacity shift — the button responds to pressure
- Focus state: visible, accessible, styled (not browser default)
- Transition: 100–150ms ease-out on all state changes
- Depth: primary buttons have presence — not flat rectangles
- Never: flat buttons with no state differentiation

### Cards — minimum requirements
- Subtle border or background differentiation from canvas
- Hover state that signals interactivity without screaming it
- Depth hierarchy — cards that matter more should feel slightly elevated
- Internal spacing that gives content room to breathe
- Never: flat cards that look like divs with padding

### Navigation — minimum requirements
- CTA hierarchy — the primary action is visually distinct from navigation links
- Hover intelligence — hover states are designed, not defaulted
- Active state — current location is clearly indicated
- Spacing balance — nav items have rhythm, not random gaps
- Never: navigation with no active state, no hover feedback, or misaligned items

### Forms & Inputs — minimum requirements
- Focus state: clear, branded, accessible
- Error state: designed, not browser-default
- Label positioning: intentional (floating, above, or inline — never random)
- Placeholder text: helpful, not just field name repeated
- Never: unstyled inputs, no focus ring, no error state

### States — all must be designed
Every component needs all states before it ships:
- Default
- Hover
- Active / pressed
- Focus
- Disabled
- Loading (where applicable)
- Empty (where applicable)
- Error (where applicable)

If a state isn't designed, it isn't done.

---

## Motion — Minimum Standards

### Motion must always
- Guide attention — animate in the direction of user intent
- Improve continuity — transitions connect states, they don't interrupt them
- Create perceived quality — a well-timed transition makes the product feel faster
- Communicate state — animation is information, not decoration
- Reduce harsh transitions — nothing should snap or jump unless intentionally jarring

### Required motion patterns (use contextually)
- Fade + subtle translate on element entrance (not scale from zero — too playful)
- Smooth transforms on interactive state changes (hover, active)
- Opacity layering for depth and reveal
- Staggered reveals for lists and grids — not all at once
- Skeleton loading states — the page continues to exist while data loads

### Motion defaults (override with `.marrow.md` values if defined)
- Default easing: `cubic-bezier(0.25, 0.1, 0.25, 1)` (ease-out — responsive, natural)
- Micro interactions: 100–150ms
- Element transitions: 200–300ms
- Page/panel transitions: 300–400ms
- Always respect `prefers-reduced-motion` — provide static fallbacks

### Never do
- Random animations with no purpose
- Bounce spam — spring physics on everything
- Slow, laggy motion that makes the product feel heavy (>500ms on UI transitions)
- Over-animation — if every element animates, nothing stands out
- Generic fade-in on everything — motion without intention is noise

---

## Color — Minimum Standards (defer to `.marrow.md` for specifics)

When `.marrow.md` is silent on color:

- One primary accent — not multiple competing accent colors
- Controlled saturation — avoid oversaturated, vibrating colors
- Semantic consistency — success is always green, error is always red (unless `.marrow.md` overrides)
- Accessible contrast — WCAG AA minimum on all text, WCAG AAA preferred for body text
- Layered neutrals — backgrounds have depth (canvas → surface → elevated surface → overlay)
- Never: rainbow UI, arbitrary gradients with no purpose, inconsistent palette across components

---

## Product Psychology — Apply Automatically

Every UI is a persuasion system. These elements must appear where relevant — the user should not need to ask for them:

### Trust builders (add where relevant)
- Social proof — testimonials, logos, user counts near conversion points
- Security indicators — near any form asking for sensitive information
- Concrete outcomes — show what success looks like, not just what the product does

### Anxiety reducers (add where relevant)
- Clarify next steps — the user always knows what happens after they click
- Reversibility signals — "you can change this later", "no commitment required"
- Progress indicators — for multi-step flows, show where they are
- Empty state design — a blank state should guide the user to their first action

### Conversion logic (apply contextually)
- CTAs near the point of maximum motivation — after a benefit statement, not before
- CTA hierarchy — one primary action per screen, secondary actions clearly subordinate
- Contextual CTAs — the CTA should match what the user just learned

---

## Product Thinking — Before Every Component

Before writing a component, answer internally:

1. **Why does this exist?** If you can't answer this, the component may not be needed.
2. **What user anxiety does this reduce?** What is the user afraid of before they see this?
3. **What trust does this build?** Does this make the product more believable?
4. **What conversion purpose does this serve?** Is it moving the user closer to a meaningful action?

If none of these questions have strong answers — the component may need rethinking.

---

## Dashboard Design (when building data UIs)

Dashboards must feel: operational, intelligent, alive, high-value.

### Always include
- Data hierarchy — the most important metric is visually dominant
- Modular panels — each panel has a clear single responsibility
- Interaction depth — data is filterable, sortable, or drillable where relevant
- Contextual controls — actions appear near the data they affect
- Actionable insights — don't just display data, signal what matters

### Never do
- Overcrowd — a dashboard that shows everything shows nothing
- Generic admin templates — the dashboard should feel like the product, not a CRM panel
- Meaningless charts — every visualization answers a specific question
- Visual noise — decoration on a dashboard is a failure of information design

---

## Responsiveness — Minimum Standards

Responsiveness is not resizing. It is redesigning for context.

### Mobile requirements
- Re-prioritize hierarchy — mobile shows what matters most, not everything the desktop shows
- Reduce clutter — secondary information can be hidden or collapsed
- Preserve all interactions — hover states become tap states, but must still exist
- Premium spacing — mobile doesn't mean cramped; breathing room is still required
- Optimize touch targets — minimum 44×44px for any interactive element
- Rethink layouts — do not blindly stack desktop sections; some sections need mobile-native treatment

### Never do
- Blindly stack all desktop sections vertically
- Reduce font sizes to fit more content — remove content instead
- Leave hover-only states with no touch equivalent

---

## Pre-Output Audit — Run Before Every Delivery

Before showing any output, run this checklist internally. Fix failures before delivering.

### Visual audit
- [ ] Does this feel templated? → If yes, add one distinctive design decision
- [ ] Is hierarchy obvious at a glance? → If no, increase contrast between levels
- [ ] Is spacing intentional everywhere? → If no, audit every gap and padding value
- [ ] Is there visual rhythm? → If no, vary density between sections or elements
- [ ] Does the UI breathe? → If no, add more canvas space
- [ ] Is there visual fatigue? → If yes, reduce element count or add whitespace

### UX audit
- [ ] Is the primary CTA obvious? → If no, it needs more visual weight
- [ ] Is the flow smooth? → If no, find where the user would hesitate
- [ ] Is anything confusing? → If yes, simplify or add context
- [ ] Is scanning effortless? → If no, improve typographic hierarchy

### Motion audit
- [ ] Does every animation improve clarity? → If no, remove it
- [ ] Is every interaction satisfying? → If no, add tactile state feedback
- [ ] Are all transitions polished? → If no, tune easing and duration

### Product audit
- [ ] Does this build trust? → If no, add a trust signal near the conversion point
- [ ] Does this feel premium? → If no, refine spacing and component depth
- [ ] Would a well-funded SaaS ship this? → If no, find what makes it feel unfinished

**If any audit item fails: fix it before output. Never wait for the user to ask.**

---

## Auto-Refinement Rule

The first draft is always incomplete.

Never wait for the user to say:
- "make it cleaner"
- "make it more premium"
- "improve the spacing"
- "refine the animations"
- "fix the hierarchy"

You must automatically refine. The output must already feel refined before the user asks for refinement.

**Functional is not enough. Beautiful is not enough.**

The UI must feel: inevitable · intentional · expensive · smooth · trustworthy · productized · crafted.

That is the baseline. Everything above it is the soul.
