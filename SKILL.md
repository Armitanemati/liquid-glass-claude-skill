---
name: liquid-glass-design-system
description: Brand-agnostic design reasoning system for Liquid Glass and glassmorphic interfaces on any platform. Use when asked to use, apply, or redesign with Liquid Glass, glassmorphism, or a glass UI, or to make an interface more Apple-like.
---

# Liquid Glass Design System

A design reasoning system, not a snippet library. Liquid Glass is a **material and interaction language**: translucent material used intentionally to establish functional hierarchy above content.

**Objective:** a clear, spatial, adaptive interface. Not "make it look like glass."
**Success test:** people think "this feels incredibly clean and spatial," never "someone added blur to everything." Liquid Glass should be felt before it is noticed.

This skill controls **material, hierarchy, spatial behavior, transparency, blur, depth, interaction.**
The project's brand system controls **color, type, identity, imagery, tone.** Never mix the two.

**References.** Primary: Apple's Liquid Glass principles (functional layering, translucency, material hierarchy, adaptive appearance, spatial separation, depth, continuity, visual hierarchy, clarity, consistency, contextual interaction). Supporting: glassmorphism practice on transparency, background blur, contrast, depth, edge definition, accessibility, readability. Understand the principles and apply them to the product at hand. Never produce an Apple clone.

---

## 0. Scope and safety

This skill is guidance only. When it is active:
- Work only inside the project the user has explicitly selected or shared. Do not read, scan, or modify anything outside it.
- Do not read environment variables, credentials, keys, tokens, or account data.
- Do not make network requests, install packages, or change global or system settings. When a technique needs a library, name it and let the user decide whether to add it.
- Do not overwrite existing files without the user's request. Propose first (section 3).
- Do not collect, store, or transmit user data. Example content must be fictional.
- Version-specific platform facts in section 14 can age. Flag them for the user to verify rather than fetching anything.

---

## 1. Command interpretation

| User says | Interpret as |
|---|---|
| "Use / apply / make it Liquid Glass", "Liquid Glass style" | Apply this system while preserving the product's existing brand and UX requirements. |
| "Make it glassmorphic", "glass UI" | Use glassmorphism techniques, governed by this system's hierarchy, restraint, and accessibility rules. |
| "Redesign this using Liquid Glass" | Run the full Initialization Protocol (section 3). Redesign the material layer, not unrelated UX. |
| "Make it more Apple-like" | Do NOT copy Apple UI. Increase spatial clarity, material hierarchy, restraint, typography quality, alignment, functional layering, interaction clarity. |

Never interpret any of these as: add `backdrop-filter: blur()`, make cards transparent, add rounded white glass cards, or add gradients and shadows.

---

## 2. Reality check on the reference (read before promising anything)

1. **Native vs web gap.** Apple's Liquid Glass is a native, GPU-rendered material: it *lenses* (bends light) rather than only blurring, carries specular highlights that respond to motion, and each component adapts light/dark to what is beneath it. CSS can convincingly reproduce blur, tint, edge light, and shadow. Refraction via SVG filters inside `backdrop-filter` renders in Chromium-based browsers only; Firefox and Safari do not apply SVG `url()` filters in `backdrop-filter`. On the web, refraction is progressive enhancement and must never be load-bearing for legibility or brand.
2. **Legibility is the known failure mode.** After public readability complaints, iOS 26.1 added a user setting (Clear or Tinted) that raises opacity and contrast. Default toward the more opaque, more legible side. Clear glass is the exception, not the baseline.
3. **Apple's stated usage rules** that this system adopts: glass belongs to the navigation layer that floats above content; do not stack glass on glass (use fills and transparency for separation inside a glass surface); tint only to emphasize primary actions; the clear variant is only for media-rich backgrounds, where a dimming layer is acceptable, and content on top is bold and bright.
4. **Do not overclaim.** When delivering, state plainly which effects are native, which are approximated, and which browsers or OS versions get the fallback.

---

## 3. Project Initialization Protocol (mandatory)

When this skill activates in a project, **do not modify the UI first.** Complete phases A to C, deliver the proposal, then implement. Skip only if the user explicitly says to go straight to implementation, and say what was skipped.

### Phase A: Inspect
Establish, from the selected project's code, files, and screenshots, or by asking the user:
- Product purpose and target users
- Platform(s) and framework(s); OS or browser support targets
- Information architecture and primary user flows
- Existing design system, component library, tokens
- Brand identity: color, typography, imagery, iconography, tone
- Spacing and radius systems (or their absence)
- Responsive behavior and breakpoints
- Accessibility requirements (target WCAG level and any accessibility laws that apply in the product's markets)
- Performance constraints (low-end devices, image-heavy pages)

If a fact cannot be determined, list it as an open question. Do not invent it.

### Phase B: Classify
Produce a layer map (section 4) and answer:
1. Which elements remain **content**
2. Which elements become **functional floating UI**
3. Which existing components should be **removed**
4. Which components should be **consolidated**
5. Where Liquid Glass **improves UX** (with the functional reason)
6. Where Liquid Glass would **make the experience worse** (with the reason)

### Phase C: Propose
Deliver, before any code or design changes:
- Layer map table: element, layer, glass yes/no, material tier, reason
- Material tiers and starting token values for this project
- Brand integration notes (what comes from the Project Brand System)
- Accessibility and fallback plan
- Performance budget (glass layers per view)
- Honest limitations (section 2)
- **Out of scope:** UX problems noticed but not part of the material change, listed separately and not fixed unless the user asks

**Scope rule:** never use Liquid Glass as an excuse to redesign unrelated UX. Consolidating or removing components is proposed, never done silently.

### No project brand yet
Create a **Project Brand System** first (section 12). Do not borrow a brand from another project.

---

## 4. The layer model

| Layer | What it is | Examples | Glass? |
|---|---|---|---|
| **1. Content** | What the user came for | Photography, artwork, products, editorial, illustration, video, maps, dashboards, documents | **No.** Content stays visually dominant. |
| **2. Structural UI** | How content is organized | Sections, grids, containers, typography, hierarchy | **No** by default. Solve with layout, spacing, type. |
| **3. Functional floating UI** | Controls acting on content | Navigation, search, filters, toolbars, contextual actions, floating buttons, menus, sheets, overlays | **Candidate.** Passes the gate question first. |

The interface should feel like it exists above the content, not like the content is made of glass.

### The gate question
Before applying glass to any element, answer: **"What functional role does this material communicate?"**
Valid answers: it floats above scrolling content; it is contextual and temporary; it must stay reachable while content moves beneath it; it needs separation without hiding context.
If there is no meaningful answer: **do not use glass.** Never add glass for decoration.

---

## 5. Material hierarchy

One glass treatment everywhere is a defect. Assign tiers by function.

| Tier | Use for | Starting fill opacity | Starting blur | Notes |
|---|---|---|---|---|
| **None** | Most content, artwork, product imagery, editorial images, page backgrounds, card grids | n/a | n/a | Default for Layers 1 and 2 |
| **Thin** | Icon-only or large-label controls, compact secondary actions, navigation over controlled backdrops | 0.35 to 0.50 | 16 to 20px | Body text not guaranteed legible (see note) |
| **Regular** | Navigation with text, toolbars, search fields, floating action groups, tab bars | 0.50 to 0.65 | 20 to 28px | Workhorse tier |
| **Thick** | Menus, popovers, sheets, dialogs, text-dense overlays | 0.65 to 0.85 | 24 to 32px | Readability outranks translucency |
| **Scrim** | Dimming behind modal sheets and dialogs | Solid tint 0.20 to 0.45 | 0 to 8px | Separates modal context |
| **Clear** (rare) | Controls over full-bleed media only | 0.15 to 0.30 | 12 to 20px | Requires dimming under it and bold, bright foreground |

All values are **starting points**, not rules. Tune against the actual backdrop (section 6).

**Contrast math (worst case, before blur):** a light fill (near #f5f5f7) with near-black text needs about **0.51 fill opacity** to hold 4.5:1 over a pure black backdrop, and about 0.40 for 3:1. A dark fill (near #16161a) with white text needs about **0.59** for 4.5:1 over pure white, and about 0.46 for 3:1. Blur averages extremes and usually helps in practice, but it is not a guarantee. Below those thresholds, restrict the surface to icons and large text, constrain what can pass beneath it, or raise the fill.

**Glass on glass:** inside a glass surface, separate sub-elements with subtle fills, dividers, or opacity changes. Never nest a second backdrop-blurred layer.

---

## 6. Material properties

### Transparency
- Contextual, never one global value. Decide per component from: backdrop complexity, contrast needs, component importance, light/dark context, accessibility.
- Test over the **worst-case backdrop**: busiest image region, lightest and darkest content that can scroll beneath it.

### Blur
- Purpose is material separation, not decoration.
- Increase blur with backdrop complexity and component size; decrease on small controls and on mobile.
- Never blur content itself.

### Saturation and filters
- Restrained: `saturate()` roughly 110 to 150%. Above 180% reads as candy.
- `brightness()` and `contrast()` adjustments within about ±10%, or none.
- The material stays calm; it may subtly pick up color from beneath.

### Tint
- Material base tint comes from the brand's neutral surface color, not white by default.
- Accent tint **only** on the primary action in a group. Tinting everything destroys hierarchy.

### Edge definition
- Enough edge to stay legible over any backdrop: hairline border (about 1px at low alpha), top inner highlight, subtle contrast step, soft shadow.
- No thick white outlines. No obvious borders. The edge suggests separation; it does not draw attention.

### Shadows
- Soft, atmospheric, low alpha, large radius, small offset.
- Shadow color derived from the brand's ink or a deep neutral, not pure black.
- Increase shadow slightly as the surface rises in hierarchy or as content scrolls beneath it. Elevated, never detached.

### Adaptivity (when the background changes)
Choose explicitly, per component:
- Raise opacity toward the tier maximum over busy regions
- Switch foreground light/dark based on the backdrop (native platforms do this; on web, use scroll position or section-level flags, not per-frame pixel sampling)
- Add a scroll edge fade under fixed bars so content softens before it reaches the bar
- Reposition the control away from the busiest region
- Remove glass and use a solid surface

---

## 7. Shape language

### Radius hierarchy (starting scale)
| Element | Radius |
|---|---|
| Large surface (sheet, dialog, panel) | 24 to 32px |
| Medium component (menu, popover, toolbar) | 16 to 24px |
| Control (field, button) | 12 to 16px |
| Small icon button | 10 to 14px |
| Pill | 999px |

Pick one value per role per project and tokenize it. No ad hoc radii.

### Concentricity
Nested shapes share a center: **inner radius = outer radius − padding** (floor at the control minimum). A 28px sheet with 12px padding holds 16px controls. Mismatched nested corners are the fastest way to look cheap.

### Pills
Appropriate for: filters, tags, compact metadata, statuses, compact actions, a single floating control group.
Not for: every heading, every CTA, every navigation item, cards, sections.

---

## 8. Typography, color, gradients

### Typography
- No required font; it comes from the brand. On native Apple platforms the system font is legitimate; on the web do not impose Apple's fonts.
- Clean, highly legible, contemporary, restrained. Decorative type only if the brand requires it.
- Hierarchy through size, weight, spacing, line height, contrast; not through many font styles.
- Text on glass: prefer medium or semibold weights at small sizes; thin weights fail over translucency.

### Color
- Color comes from the brand. Liquid Glass does not require blue/purple gradients, rainbow gradients, neon, white-on-purple, or "futuristic" palettes.
- The material system is constant; the brand system changes. The same material tiers can serve a weather app, a music player, a code editor, or a transit map, each with its own palette.

### Gradients
- Optional. Never used to signal "modern."
- If used: subtle radial ambient light, content-derived color, soft transitions.
- Background is continuous. No banded sections (white, then purple, then blue) unless a deliberate structural transition is required.

---

## 9. Spacing and layout

- Solve spacing and composition **before** adding material. Glass does not rescue a bad layout.
- Base unit 4 or 8px. Scale: 4, 8, 12, 16, 24, 32, 48, 64, 80, 96, 120.
- Generous breathing room. Never compress components to fit more.
- Prioritize alignment, whitespace, hierarchy, rhythm, balance, clear grouping.
- Avoid arbitrary masonry, excess cards, components touching, random floating elements, inconsistent spacing.
- Floating UI keeps a consistent inset from viewport edges (for example 12 to 16px mobile, 16 to 24px desktop) and respects safe areas.

---

## 10. Component decision framework

Answer internally for every component **before styling it**. Record answers in the Phase C layer map for non-trivial components.

1. What is this component?
2. What is its purpose?
3. Content or UI?
4. Persistent or contextual?
5. Does it need to float above content?
6. Does it need material separation?
7. Should it use Liquid Glass? (gate question)
8. Which material tier?
9. Which radius role (and concentric to what)?
10. What contrast is required (text, icons, boundaries)?
11. What happens on hover?
12. What happens on interaction (press, focus, expand, disabled)?
13. What happens on mobile?
14. What happens when the background changes?

### Default classifications (override with reasons)
| Component | Default |
|---|---|
| Top nav / app bar (sticky over scroll) | Regular glass (Thin only if icon-only or over a controlled backdrop) |
| Bottom tab bar / floating nav | Regular glass |
| Search field (floating) | Regular glass; inside a glass bar it is a fill, not a second glass layer |
| Filter / chip bar over content | Thin or Regular glass container; chips are fills inside it |
| Floating action button / contextual toolbar | Regular glass; primary action may take accent tint |
| Menu, popover, dropdown | Thick glass |
| Bottom sheet, dialog | Thick glass plus scrim |
| Toast / snackbar | Thick glass or solid |
| Tooltip | Solid or thick; small text rarely survives translucency |
| Cards, product tiles, article teasers | **No glass** |
| Hero image, galleries, media | **No glass** (content) |
| Page sections, backgrounds | **No glass** |
| Forms in page flow | **No glass**; solid fields |
| Footer | **No glass** |

---

## 11. Interaction, motion, responsive, performance

### States
Every glass control defines: rest, hover (pointer only), pressed, focus-visible, disabled, and expanded where relevant. Glass does not replace state styling.

### Motion
- Reinforces material behavior and communicates state or spatial relationships.
- Allowed: subtle scale (about 0.96 to 1.02 on press), opacity, short translation, material expansion (a control grows into a menu or sheet from its own origin), contextual appearance.
- Durations roughly 150 to 300ms; springs lightly damped, no visible overshoot bounce.
- Avoid bouncing, dramatic or decorative motion.
- Reduced motion: replace movement with opacity changes; never remove state feedback.

### Responsive
- Not desktop-only. On mobile: fewer floating layers, simpler navigation, less blur, no overlapping controls, preserved hierarchy, touch targets at least 44x44pt or 48x48dp.
- Recompose; do not shrink the desktop layout.
- Keep thumb zones and safe areas clear; floating bars must not cover primary content actions.

### Performance
- Backdrop filters are expensive: each one re-samples and blurs what is behind it on every scroll or animation frame.
- Budget: typically no more than 2 to 3 simultaneous backdrop-filtered layers per view on desktop, 1 to 2 on mobile. Justify exceptions.
- Never apply to entire pages, large content grids, image collections, or long lists of items.
- Do not animate blur radius on large surfaces; animate opacity or transform instead.
- Test on mid-range and older devices, not only on a current high-end laptop.

---

## 12. Brand adaptation

This skill is brand-agnostic. Never assume any project's colors, typography, spacing, logo, or imagery unless the **current** project defines them.

### Project Brand System (create or extract at project start)
- Color tokens: background, surface, ink (text), muted ink, accent, accent-ink, border, semantic (success, warning, danger)
- Typography: families, scale, weights, line heights
- Spacing scale
- Radius roles
- Imagery style
- Iconography (set, stroke weight, fill style)
- Tone of voice and content style

### Combination rule
`Liquid Glass Design System (material, hierarchy, depth, interaction)` + `Project Brand System (color, type, identity, imagery, tone)` = project UI.
Glass tints and shadows are derived from brand tokens, never hard-coded white and black.

---

## 13. Accessibility (non-negotiable)

Accessibility wins over aesthetics. Verify, over the worst-case backdrop:
- Text contrast: at least 4.5:1 for body text, 3:1 for large text (WCAG 2.x AA)
- Icons, control boundaries, and focus indicators: at least 3:1 against adjacent colors (WCAG 1.4.11)
- Buttons recognizable as buttons without relying on the glass effect
- Visible focus states; complete keyboard navigation; logical focus order; focus trapped in dialogs and sheets
- Touch targets: WCAG 2.2 minimum 24x24 CSS px; design to 44x44pt (Apple) or 48x48dp (Material)
- Reduced motion respected
- Reduced transparency and increased contrast respected (native settings; on web see section 14 and note limited browser support)
- Forced colors / high contrast mode produces solid, bordered surfaces

**If glass reduces readability, in this order:** increase material opacity → change placement → add contrast (scrim, stronger edge, heavier weight) → remove the glass effect.

Because OS-level "reduce transparency" signals do not reach most browsers, the **default** glass must already pass contrast. A preference media query is a bonus, not the safety net.

---

## 14. Implementation techniques (separate from principles)

The principles above are platform-neutral. Techniques below are one realization each; adapt them to the project's stack. Platform versions and APIs change, so flag version-specific items for the user to confirm.

### Token contract (platform-neutral names)
```
material.{thin|regular|thick|clear}.fill       color with alpha, derived from brand surface
material.{tier}.blur                           length
material.{tier}.saturation                     percentage
material.{tier}.edge                           hairline color and alpha
material.{tier}.highlight                      inner top highlight
material.{tier}.shadow                         color, blur, offset
material.solid.{tier}.fill                     opaque fallback per tier
radius.{surface|component|control|icon|pill}
space.{1..12}
motion.{fast|base|slow}, motion.easing.standard
```

### Web (HTML/CSS; applies to React, Next.js, Vue, Svelte)
```css
:root {
  /* placeholders: replace with the Project Brand System */
  --brand-surface: #f5f5f7;
  --brand-ink: #111114;

  --lg-regular-fill: color-mix(in oklab, var(--brand-surface) 56%, transparent);
  --lg-regular-solid: color-mix(in oklab, var(--brand-surface) 94%, var(--brand-ink));
  --lg-regular-blur: 24px;
  --lg-saturation: 140%;
  --lg-edge: color-mix(in oklab, white 22%, transparent);
  --lg-highlight: color-mix(in oklab, white 35%, transparent);
  --lg-shadow: 0 8px 32px color-mix(in oklab, var(--brand-ink) 10%, transparent);
  --radius-component: 20px;
}

/* Fallback first: legible without backdrop-filter */
.lg-regular {
  background: var(--lg-regular-solid);
  border-radius: var(--radius-component);
  box-shadow: inset 0 1px 0 var(--lg-highlight), inset 0 0 0 1px var(--lg-edge), var(--lg-shadow);
}

@supports ((backdrop-filter: blur(1px)) or (-webkit-backdrop-filter: blur(1px))) {
  .lg-regular {
    background: var(--lg-regular-fill);
    -webkit-backdrop-filter: blur(var(--lg-regular-blur)) saturate(var(--lg-saturation));
    backdrop-filter: blur(var(--lg-regular-blur)) saturate(var(--lg-saturation));
  }
}

@media (prefers-reduced-transparency: reduce) {   /* limited browser support */
  .lg-regular { background: var(--lg-regular-solid); backdrop-filter: none; -webkit-backdrop-filter: none; }
}
@media (prefers-contrast: more) {
  .lg-regular { background: var(--lg-regular-solid); box-shadow: inset 0 0 0 1px var(--brand-ink); backdrop-filter: none; -webkit-backdrop-filter: none; }
}
@media (forced-colors: active) {
  .lg-regular { background: Canvas; border: 1px solid CanvasText; backdrop-filter: none; -webkit-backdrop-filter: none; }
}
@media (prefers-reduced-motion: reduce) {
  .lg-regular { transition-property: opacity; }
}
```
Dark mode: redefine brand tokens and fills under the project's theme mechanism; do not reuse light-mode alphas unchanged (dark glass usually needs a higher fill alpha and a dimmer highlight).

Web gotchas:
- **Backdrop root:** `backdrop-filter` only samples up to the nearest ancestor that creates a backdrop root (for example an ancestor with `filter`, `opacity` below 1, `mask`, `mix-blend-mode`, or its own `backdrop-filter`). Nested glass and glass inside faded containers silently show nothing. Another reason not to nest.
- If the blur bleeds past rounded corners in a given engine, add `overflow: hidden` to the glass element.
- SVG displacement "refraction" is Chromium-only in `backdrop-filter`: gate it behind feature detection and make the non-refracted version the designed baseline.
- Components expose a `material` prop (`"none" | "thin" | "regular" | "thick"`) instead of ad hoc class stacks, so tiers stay enforceable.
- Utility CSS frameworks: define tiers as named utilities or component classes backed by the tokens; do not scatter one-off blur values.

### SwiftUI (Apple platforms with Liquid Glass, version 26 and later)
- Prefer the native material over any custom blur: standard bars, tab bars, toolbars, and sheets adopt Liquid Glass automatically when built with system components.
- Custom floating controls: `.glassEffect()` with an explicit shape; `.buttonStyle(.glass)` for secondary and `.buttonStyle(.glassProminent)` for the single primary action; group related glass elements in a `GlassEffectContainer` so they render and morph as one material.
- Tint via the glass API only for primary emphasis; do not recolor all glass.
- Earlier OS versions: fall back to system `Material` levels (`.ultraThinMaterial` to `.thickMaterial`) mapped to the tiers above.
- Respect `accessibilityReduceTransparency`, `colorSchemeContrast`, and `accessibilityReduceMotion` environment values in any custom material.

### Other platforms
- **Android (Compose/Views):** there is no general in-app backdrop blur. `RenderEffect` (API 31+) blurs a view's own content, not what is behind it; window background blur applies to dialogs and windows. In-app glass needs a third-party library (recommend one; the user decides whether to add it) with a solid fallback, and only on small floating bars.
- **Flutter:** `BackdropFilter` inside `ClipRRect`; keep the count low, and avoid it in scrolling list items.
- **React Native:** use a native blur or glass module chosen by the user, with a solid fallback on platforms where blur is weak or expensive.

### Design tools
- Build each tier as a reusable style: fill (brand surface at tier alpha) + background blur + inner highlight + hairline stroke + soft shadow.
- Publish tiers and radius roles as tokens or variables. Prototype over realistic content, including a worst-case image, never over a flat gray.

---

## 15. Anti-pattern database

If the output starts resembling any of these, stop and correct.

| # | Anti-pattern | Correction |
|---|---|---|
| 1 | Glass card grids | Solid or borderless cards; glass only on the filter bar above |
| 2 | Glass page backgrounds | Continuous brand background; ambient light at most |
| 3 | Glass sections | Structure with spacing and type |
| 4 | Glass inside glass | One material layer; fills and dividers inside |
| 5 | Giant rounded rectangles | Apply the radius hierarchy; reduce surface size |
| 6 | Excessive white transparency | Tint from brand surface; raise opacity |
| 7 | Heavy shadows | Low alpha, large blur, brand-ink color |
| 8 | Neon gradients | Brand palette only |
| 9 | Purple "AI" gradients | Remove; brand palette only |
| 10 | Random floating blobs | Remove; ambient light must be content- or brand-derived |
| 11 | Decorative glass circles | Remove; fails the gate question |
| 12 | Glass everywhere | Rerun the layer map; Layer 3 only |
| 13 | Pills everywhere | Pills for filters, tags, statuses, compact actions only |
| 14 | Excessive blur | Lower toward tier minimum; blur is separation |
| 15 | Low-contrast text | Section 13 remediation order |
| 16 | Generic "AI startup" look | Re-anchor on the Project Brand System |
| 17 | Generic Web3 look | Remove glow, neon, chrome gradients |
| 18 | Generic website-template look | Rebuild hierarchy from content and brand, not from effects |
| 19 | Accent tint on every glass control | Tint the single primary action only |
| 20 | Clear glass over text-heavy or light content | Use Regular or Thick |
| 21 | Refraction or blur as the only affordance | Controls must read as controls with glass disabled |
| 22 | Apple clone (Apple icons, iOS chrome on a web brand) | Adopt principles, not Apple's visual assets |

Visual character check. Should feel: light, spatial, precise, calm, premium, tactile, adaptive, modern, intentional. Must not feel: glossy, plastic, futuristic for its own sake, Web3, generic AI, template-like, neon, overly colorful, excessively rounded, visually noisy.

---

## 16. Design quality test (before finalizing)

Answer each explicitly. Any "no" means revise.

| Check | Question | Evidence to produce |
|---|---|---|
| Hierarchy | Can I immediately tell what is important? | Squint or blur test of the full screen |
| Spatiality | Does the UI feel layered? | Content vs floating UI distinguishable at a glance |
| Material | Does every glass surface communicate function? | Gate-question answer per glass element |
| Restraint | Is glass used selectively? | Count of glass layers per view within budget |
| Clarity | Can everything be understood quickly? | No control relies on glass to be recognized |
| Consistency | Do shapes, spacing, type belong together? | All radii, spacing, type values map to tokens |
| Adaptability | Does the material work over different backgrounds? | Screenshots over lightest, darkest, and busiest backdrops |
| Accessibility | Can users read and interact with it? | Measured contrast ratios, keyboard pass, fallback rendering (no backdrop-filter, forced colors) |
| Brand | Does it belong to this specific product? | Colors, type, imagery traceable to the Project Brand System |

When delivering, report the checks, the measured contrast values where measurable, the fallback behavior, and any limitation that remains. Do not claim a check passed without evidence.
