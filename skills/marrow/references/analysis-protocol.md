# Visual Analysis Protocol

This reference file contains the deep methodology for reading UI images with the precision of a senior design systems architect. Read this before beginning any analysis.

---

## How to See Like a Designer

Most AI tools look at UI images and see: colors, fonts, spacing. That is the surface. You must look deeper.

A trained designer looks at a UI and asks:
- **What decision was made here, and what alternative was rejected?**
- **What does this element say to the user, beyond what it communicates?**
- **What would be missing if this were removed?**
- **Why is this element exactly this size and not slightly larger or smaller?**

Your job is to reverse-engineer the *decisions*, not just the *output*.

---

## Reading Visual Hierarchy

Every UI screen has a dominant visual force — one element that wins the competition for attention. Find it.

Then find what is second. And what is third. This is the hierarchy.

Now ask: **Is the hierarchy earned?** Does the most important element win because of genuine visual priority (size, contrast, position, isolation), or does it win by default because everything else is quiet?

Strong hierarchy = intentional contrast between levels.
Weak hierarchy = everything at similar weight, nothing leads.

Document which type of hierarchy strategy this UI uses.

---

## Reading Color Temperature and Emotional Register

Colors have temperature (warm/cool) and emotional register (energetic/calm, heavy/light, corporate/human).

When reading a palette:

1. **Find the chromatic center of gravity.** What is the average hue temperature across all colors?
2. **Find the saturation strategy.** Are colors vivid and punchy, muted and sophisticated, or nearly achromatic with one chromatic accent?
3. **Find the value range.** Does the UI live mostly in light tones, dark tones, or a dramatic full range?
4. **Find the tension point.** Every good palette has one element that creates visual tension — the color that stands apart. This is usually (not always) the brand accent.

---

## Reading Spatial Rhythm

Spacing is not just numbers. It is rhythm. Like music.

Rhythm can be:
- **Regular** — consistent intervals, creates predictability and calm (4px / 8px / 16px / 32px)
- **Proportional** — intervals grow by ratio, creates natural tension (8 / 13 / 21 / 34 — Fibonacci-like)
- **Contextual** — spacing varies based on content relationship (tight inside a component, generous between components)
- **Dramatic** — deliberately large voids next to deliberately tight groups

When reading spacing, don't just measure — listen to the rhythm. Is it a steady beat, or does it syncopate?

---

## Reading Typography as Voice

Typefaces have voices. A font is not just a rendering — it is a personality carrier.

Categories (simplified):

| Category | Voice | Common brands |
|----------|-------|---------------|
| Geometric sans | Rational, modern, precise | Technology, startups |
| Humanist sans | Warm, accessible, trustworthy | Healthcare, education |
| Transitional serif | Authoritative, refined | Finance, publishing |
| Slab serif | Bold, honest, sturdy | Manufacturing, outdoor |
| Display / experimental | Distinctive, opinionated | Fashion, culture |

When you identify a typeface, describe its voice. Do not just name it.

Also read: **how type is used** matters as much as which type.
- All-caps labels = structural, not decorative = signals data hierarchy
- Italic = emphasis, motion, reference
- Uppercase tracking = distance, luxury, editorial
- Mixing weights heavily = typographic expression vs. restraint

---

## Reading Motion From Static Images

Static images contain motion signals. Look for:

**Implies fast motion:**
- Small, tight spacing
- Sharp edges, no border-radius or minimal
- High contrast between states
- Dense information

**Implies slow, deliberate motion:**
- Generous whitespace
- Large radii on corners
- Gradual opacity transitions implied by element arrangement
- Layers and overlapping elements

**Implies spring/physics-based motion:**
- Playful scale differences between elements
- Elements that feel "placed" rather than positioned
- Asymmetry that suggests movement

**Implies no motion (intentional):**
- Extremely minimal, no-decoration design
- Print-like composition
- Explicit restraint everywhere else

---

## Reading Interaction Design From Static States

Even without hover states or interactions, static images reveal interaction design philosophy:

**Discoverability signals:**
- If interactive elements look interactive (obvious affordance) = low discoverability trust (assumes first-time users)
- If interactive elements are subtle = high discoverability trust (assumes sophisticated/returning users)

**Touch vs. cursor signals:**
- Target sizes 44×44px or more = mobile-native
- Tight targets, complex hover states implied = desktop-native
- Both = designed for responsiveness

**Feedback philosophy:**
- Heavy borders, strong shadows, high-contrast states = wants user to feel every interaction
- Subtle, low-contrast feedback = wants interaction to feel effortless, invisible

---

## Reading Brand Restraint vs. Brand Expression

The biggest failure in AI-generated design is brand overexpression. The agent sees "brand color: orange" and uses orange everywhere.

To read brand restraint correctly:

1. **Count how many times the brand accent appears on one screen.**
2. **Calculate roughly what percentage of screen area it covers.**
3. **Note what it is always applied to.** (Only CTAs? Only selected states? Only icons?)
4. **Note what it is never applied to.** (Never background? Never text? Never borders?)

A brand accent that covers 3% of the screen and only appears on one CTA button is a *punctuation mark*. The rule is: use it exactly as the designer uses it, not more.

A brand color used freely across backgrounds, buttons, and text is a *dominant force*. This is a different design philosophy and must be described differently.

**Both are valid. Neither can be described with just a hex code.**

---

## Red Flags During Analysis

Stop and re-examine if you find yourself:
- Writing "the UI uses a blue color scheme" — too vague
- Listing colors without role or weight
- Using "clean", "minimal", "modern" without explaining the specific decision that creates that impression
- Describing a font as "sans-serif" without describing its personality
- Treating all space as dead space rather than analyzing its purpose
- Saying an animation is "smooth" without describing its easing, duration, or trigger

These are the hallmarks of shallow analysis. They produce rules that break the soul.

---

## The Soul Test

Before finalizing analysis, ask these 5 questions:

1. If I removed the brand accent entirely, would this UI still have a soul? (If yes: the soul lives in structure. If no: the accent IS the soul — rare but valid.)
2. Could this UI be used by a different company with just a color swap? (If yes: the design is not yet specific enough.)
3. What is the one decision in this UI that no template would make? (That is the soul's origin point.)
4. What would a developer get wrong if given only the color palette and font name? (That gap is what the rules file must close.)
5. If this UI had a soundtrack, what would it be? (This sounds abstract but produces very concrete design language — "it would be a quiet solo piano piece" vs "a tight jazz quartet" gives more actionable direction than "minimal" vs "complex".)
