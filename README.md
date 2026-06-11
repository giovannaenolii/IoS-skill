# Glass Design iOS Skill

**Awwwards-tier glassmorphism, iOS design, and Apple-level minimalism for AI coding agents.**

Gives your AI agent the design vocabulary, technical patterns, and taste to produce interfaces that could win design awards — not just look "glass-y".

---

## What This Skill Does

Stops AI from generating:
- Flat `backdrop-blur(10px)` that doesn't look like glass at all
- Dark gradient with purple glow = "modern UI"
- Generic cards, 3-column layouts, centered heroes
- Missing inner highlights (the #1 sign of fake glass)
- Linear easing instead of spring physics

Forces AI to produce:
- Properly engineered glass panels (6-property composite)
- Designed backgrounds (glass needs content to blur)
- iOS HIG-accurate spacing, type, and color systems
- Spring physics exclusively — iOS-calibrated presets
- Depth hierarchy through varying blur intensity
- Specular highlights that simulate real light on glass

---

## Install

```bash
npx skills add https://github.com/yourusername/glass-skill
```

Or copy `skills/glass-skill/SKILL.md` into your project / Claude Code context.

---

## Skills in This Repo

| Skill | Install Name | Description |
|-------|-------------|-------------|
| glass-skill | `glass-design-ios` | Primary skill — glassmorphism, iOS HIG, Awwwards-level polish |

---

## What's in the Skill

```
skills/glass-skill/
├── SKILL.md                          # Main skill (read first)
└── references/
    ├── glass-components.md           # Full component library (NavBar, Cards, Inputs, Modals, Toast, etc.)
    ├── ios-patterns.md               # Deep iOS HIG (Dynamic Island, Sheets, Tab Bar, Context Menu)
    ├── backgrounds.md                # Background systems (mesh, bokeh, aurora, grain, grid)
    ├── motion-library.md             # Spring presets, entrance variants, scroll animations, hover effects
    └── awwwards-examples.md          # Pattern breakdowns of award-winning design, anti-checklist
```

---

## Usage Examples

### Basic Request
> "Create a product showcase page for my app with glassmorphism"

AI produces: Mesh gradient background, bokeh orbs, noise overlay, properly engineered glass panels with inner highlights, spring-physics entrance animations, iOS typography scale.

### iOS App Screen
> "Design an iOS-style car purchase inspection screen"

AI produces: Light-mode glass cards, pill tags, data visualization with circular progress, iOS list groups, proper safe area handling.

### Dashboard
> "Create a rental car dashboard with AI assistant panel"

AI produces: Bento grid layout, light glass panels, single accent color, embedded map component, chat UI, date/time picker with large typography.

### Product Page (Dark)
> "Make a dark product page like Apple or Colbo"

AI produces: Dark canvas with radial vignette, product image with dramatic lighting treatment, oversized display typography, minimal spec table, animated mesh background.

---

## Design Dials (in SKILL.md)

| Dial | Default | Range | Effect |
|------|---------|-------|--------|
| `GLASS_INTENSITY` | 8 | 1-10 | Blur strength, opacity, refraction complexity |
| `DEPTH_LAYERS` | 7 | 1-10 | Number of Z-axis planes, parallax depth |
| `MOTION_PHYSICS` | 7 | 1-10 | Spring complexity, magnetic effects |
| `LIGHT_REALISM` | 9 | 1-10 | Specular highlights, caustic simulation |
| `MINIMALISM_PURITY` | 8 | 1-10 | Negative space, breathing room |

Override in your prompt:
> "Set GLASS_INTENSITY to 10, I want visionOS-level translucency"

---

## The Glass Doctrine (Core Principles)

1. **Depth over Decoration** — Blur implies depth. Never blur emptiness.
2. **Light has a Source** — Every glass panel needs coherent top-left refraction.
3. **Restraint over Excess** — Max 3 glass layers per viewport.
4. **Spring Physics Always** — Zero linear easing. iOS-calibrated springs everywhere.
5. **Design the Background** — Glass is only as good as what's behind it.

---

## Stack Defaults

- **Framework:** Next.js 14+ App Router (RSC)
- **Styling:** Tailwind CSS v3 + CSS custom properties
- **Motion:** Framer Motion (UI), GSAP ScrollTrigger (scroll sequences only)
- **Fonts:** Geist / Plus Jakarta Sans (Inter is banned)
- **Icons:** @phosphor-icons/react (never Lucide, never emoji)

---

## Design Awards Calibration

| Output Quality | Awwwards Score |
|----------------|---------------|
| Generic AI slop | 6-7 |
| Custom but safe | 7-8 |
| **Target with this skill** | **8.5-9** |
| SOTD territory | 8.5+ |

---

## License

MIT — use freely in commercial projects.
