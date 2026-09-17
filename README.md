# Liquid Glass Claude Skill - Design System

A **Claude Skill** (`SKILL.md`) for designing **Liquid Glass** and **glassmorphism** interfaces: Apple-style layering, material tiers, accessible contrast, and fallbacks for web, SwiftUI, and mobile. Brand-agnostic, so it works for any product.

Works with Claude Code, Claude apps, and other tools that support the open Agent Skills format.

It is a **design reasoning system**, not a collection of CSS snippets. It teaches an AI agent (or a design team) *when* translucent material helps, *where* it belongs, and *how* to keep it legible, accessible, and fast.

![Fictional example: floating navigation, action group, and filter bar in glass over content that stays solid](examples/example-media-app.png)

## What is inside

```
liquid-glass-claude-skill/
├── SKILL.md                         the skill (all guidance lives here)
├── README.md
├── LICENSE
├── .gitignore
└── examples/
    ├── example-media-app.html       fictional, self-contained reference page
    ├── example-media-app.png        default state
    └── example-media-app-sheet.png  modal sheet state
```

## How to use it

- **Claude Code:** copy the `liquid-glass-claude-skill` folder into a `.claude/skills/` folder (in your project or your user-level skills folder). If you downloaded a ZIP from GitHub, rename the folder to `liquid-glass-claude-skill` first, because the folder name must match the skill name.
- **Claude apps:** zip the `liquid-glass-claude-skill` folder and upload it as a custom skill in your settings.
- **Other AI tools:** paste the contents of `SKILL.md` into the tool's custom instructions.

Then ask for things like:

- "Make this Liquid Glass"
- "Redesign this settings screen using Liquid Glass"
- "Use a glassmorphic UI for the navigation"
- "Make it more Apple-like"

The skill first inspects the project and proposes a layer map. It does not start changing the UI until that proposal exists.

## What's new

**Field notes from a production build** (section 17). The skill was applied end to end on a live site, and the things that were measured rather than assumed are now in it:

- a Figma Glass effect → CSS mapping, with the numbers that actually matched the rendered look (they are not the slider numbers)
- edge-concentrated lensing on the web: a displacement map built from the element's own outline, delivered through `feImage` inside `backdrop-filter`
- three engine bugs that silently kill the effect (mask + backdrop-filter in Chrome, `url()` dropping the whole declaration in Safari/Firefox, `@theme inline` baking tokens in Tailwind v4)
- Apple's scroll edge effect, content-aware shadow, tinted primary action and press illumination, translated to CSS with measured contrast
- how to measure contrast over glass, whether a blur is even visible, and what each filtered layer costs per frame
- rules for working with a product owner: reference render first, one knob per property, revertable polish commits

## Core ideas

1. **Glass is for floating, functional UI** (navigation, search, filters, toolbars, menus, sheets). Content stays solid and dominant.
2. **Every glass surface must answer:** "What functional role does this material communicate?" No answer, no glass.
3. **Material tiers, not one effect:** thin, regular, thick, scrim, and a rare clear variant.
4. **Brand stays separate:** the skill controls material and hierarchy; each project's brand controls color, type, and identity.
5. **Accessibility wins:** contrast is checked against the worst-case backdrop, with solid fallbacks.

## The example

`examples/example-media-app.html` is a fictional media library. All names, labels, and artwork are invented, and the artwork is drawn with CSS gradients. Open the file in a browser. It loads no fonts, images, scripts, or other external resources.

It shows three glass layers (navigation, hero action group, filter bar), a thick glass sheet with a scrim, solid content tiles, fallbacks for reduced transparency, higher contrast and forced colors, and a recomposed mobile layout.

## Safety

The skill is guidance only. It tells the agent to stay inside the project you select, to leave credentials and environment variables alone, and not to make network requests, install packages, or overwrite files without your request.

## Limitations

- Native Liquid Glass (on Apple platforms) bends light and reacts to motion. On the web, CSS reproduces blur, tint, edges, and shadow well. Refraction effects are limited to some browsers and are treated as optional.
- Opacity, blur, and performance numbers are starting points, not standards. Test on real content and real devices.
- Platform APIs change. Check version-specific details before shipping.

## References

- [Apple Human Interface Guidelines: Materials](https://developer.apple.com/design/human-interface-guidelines/materials)
- [WWDC25: Meet Liquid Glass](https://developer.apple.com/videos/play/wwdc2025/219/)
- [MDN: backdrop-filter](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/backdrop-filter)
- [WCAG 2.2](https://www.w3.org/TR/WCAG22/)

## Disclaimer

This is an independent project. It is not affiliated with, sponsored by, or endorsed by Apple Inc. Apple, iOS, SwiftUI, and Liquid Glass are referenced only to describe design principles and may be trademarks of Apple Inc.

## License

[MIT](LICENSE)
