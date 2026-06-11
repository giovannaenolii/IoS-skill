# Awwwards-Level Design Patterns

## What Separates Awwwards Sites from Generic AI Output

Awwwards judges look for:
1. **Creative direction** — a point of view, not a template
2. **Typography as layout** — text IS design, not content in a layout
3. **Custom interactions** — things you've never seen in a UI kit
4. **Polish** — pixel-perfect at every size, every state
5. **Speed** — 90+ Lighthouse score alongside stunning visuals

---

## Pattern 1: The Product Showcase (Colbo / Apple style)

**What makes it great:**
- Product on dark background with dramatic rim lighting
- Typography intrudes into product space — layered depth
- Single CTA, maximum $395 — no feature lists
- Technical specs presented in minimal table, not bullet points

**Implementation approach:**
```tsx
// Full-bleed dark canvas
// Product image: absolute positioned, partially behind text
// Hero text: massive, semibold, very tight tracking (-0.05em)
// Price: smaller than product name, light weight
// "Add to Cart": clean white pill button, no drop shadow

// Section 2: specs in ultra-minimal table
// Left: spec label (small, muted, uppercase)
// Right: spec value (clean, slightly brighter)
// Divider: 1px rgba(255,255,255,0.06) lines
// No boxes, no background cards — just spacing
```

**CSS for product page:**
```css
.product-hero {
  background: radial-gradient(ellipse at 60% 40%, rgba(60, 60, 90, 0.5) 0%, #050508 65%);
  min-height: 100dvh;
  display: grid;
  grid-template-columns: 1fr 1fr;
  align-items: center;
}

.product-image {
  transform: rotate(-15deg) translateX(10%);
  filter: drop-shadow(0 40px 80px rgba(0,0,0,0.8));
  /* Product floats and very slightly rotated — never perfectly upright */
}
```

---

## Pattern 2: Car / Product Inspection App (Like the Porsche images)

**What makes it great:**
- Pure white (#FFFFFF) or off-white (#F8F8F6) background — glassmorph
- Cards with subtle 1px borders, no visible box shadows from outside
- Typography: tight, bold for the car name; light for metadata
- Data visualization: circular progress indicators, subtle bar charts
- Status tags: pill-shaped, light background color fills

**Implementation — the minimal card:**
```tsx
// On white background, glass becomes subtle frosted panels
.inspection-card {
  background: rgba(248, 248, 248, 0.9);
  border: 1px solid rgba(0, 0, 0, 0.06);
  border-radius: 20px;
  backdrop-filter: blur(20px);
  /* Shadow: very subtle, warm tint */
  box-shadow: 0 2px 16px rgba(0,0,0,0.06), 0 1px 4px rgba(0,0,0,0.04);
}

/* Accent pills */
.tag-pill {
  background: rgba(0,0,0,0.04);
  border: 1px solid rgba(0,0,0,0.06);
  border-radius: 9999px;
  padding: 4px 10px;
  font-size: 12px;
  font-weight: 500;
  color: rgba(0,0,0,0.5);
}
```

**Data viz on light background:**
```tsx
// Circular progress — semi-donut
// 39% Replaced: #333 or brand color
// 41% Damaged: #E5E5E5 (muted)
// 20% Original: accent lime/green

// Progress bars: 100% wide, 3px tall, rounded
// Filled portion: brand color
// Empty: rgba(0,0,0,0.06)
```

---

## Pattern 3: Car Rental Dashboard (Like the Volvo EX30 image)

**What makes it great:**
- White/light gray base with clean glass panels
- Single strong green accent (Emerald #10B981 or brand green)
- AI assistant panel: chat bubble UI, clean and minimal
- Date/time picker: large typography, tactile feel
- Map: embedded, not full-screen, treated as a component
- Payment card: last 4 digits, standard credit card visual language

**Key layout principle:** Asymmetric bento grid, not columns
```tsx
// Layout grid
// desktop: grid-template-columns: 300px 1fr 300px
// Center: product hero (car image takes 60% of center)
// Left: AI chat overlay on top of car
// Bottom: 3 cards (Location, Dates, Payment) in a row

// Glass on light background — inverted recipe:
.light-glass {
  backdrop-filter: blur(20px) saturate(150%);
  background: rgba(255,255,255,0.75);
  border: 1px solid rgba(255,255,255,0.9);
  box-shadow: 0 8px 32px rgba(0,0,0,0.08), inset 0 1px 0 rgba(255,255,255,1);
}
```

---

## Pattern 4: Typography as Art Direction

**What Awwwards-winning sites do:**
- Headlines run off the edge of the screen intentionally (overflow: hidden)
- Letters overlap image elements — no z-index fear
- Vertical text alongside horizontal — mixed reading directions
- Tracking varies dramatically between sections (tight hero → wide subhead)
- Optical sizing: different styles for same weight at different sizes

```css
/* Overflowing display text */
.hero-overflow-title {
  font-size: clamp(80px, 15vw, 180px);
  font-weight: 800;
  letter-spacing: -0.05em;
  line-height: 0.9;
  overflow: visible; /* let it bleed */
  white-space: nowrap;
}

/* Mixed alignment section */
.section-headline {
  display: grid;
  grid-template-columns: 1fr auto;
  align-items: end;
  gap: 4rem;
}
/* Left: large display text, right: small body paragraph */
/* Creates visual tension and sophistication */
```

---

## Pattern 5: The Bento Feature Grid (Apple.com Style)

**What makes it work:**
- Each cell is a contained world — different background, different interaction
- Cells have different sizes (never equal 3-column grid)
- Animation lives inside each cell (the cell is alive)
- Rounded corners of cells: minimum 28px, Apple uses up to 44px
- Padding inside cells: 40-60px, never less

```tsx
// Grid structure
const bentoLayout = [
  { colSpan: 2, rowSpan: 2 }, // Big hero cell
  { colSpan: 1, rowSpan: 1 }, // Small cell
  { colSpan: 1, rowSpan: 1 }, // Small cell
  { colSpan: 1, rowSpan: 2 }, // Tall cell
  { colSpan: 2, rowSpan: 1 }, // Wide cell
]

// CSS
.bento-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-auto-rows: 300px;
  gap: 16px;
  padding: 16px;
}
```

---

## Pattern 6: Scroll Choreography

**Awwwards scroll — the rules:**
1. First section: immediate, cinematic, full-screen
2. Sticky sections: content changes while container stays (storytelling)
3. Reveal timing: stagger reveals so the eye is always led somewhere
4. Parallax: only on background elements, never on primary content
5. Horizontal: used sparingly for galleries or product showcases

```tsx
// Sticky scroll section
.sticky-container {
  height: 400vh; /* 4x viewport = 4 sticky panels */
}
.sticky-inner {
  position: sticky;
  top: 0;
  height: 100vh;
  overflow: hidden;
}
// Use Framer's useScroll + scrollYProgress to drive content changes
// Map progress [0, 0.25, 0.5, 0.75, 1] to [state1, state2, state3, state4, state5]
```

---

## Calibration Reference: What Scores Mean on Awwwards

| Score | What it looks like |
|-------|-------------------|
| 6-7   | Generic SaaS, Bootstrap, Tailwind defaults |
| 7-8   | Custom design, good typography, some animation |
| 8-8.5 | Strong creative direction, custom interactions, polished |
| 8.5-9 | SOTD candidate, memorable, technically impressive |
| 9+    | SOOTY/HOF level, redefines a category |

**Target:** Always design for 8.5+ quality bar.

---

## Anti-Checklist: What Instantly Kills Quality

- Equal-height columns of exactly 3 cards
- Gradient from purple to blue as the "modern" touch
- Rounded avatar + name + title "team section"
- Pricing table with "Most Popular" badge
- Hero: background image + centered text + two CTA buttons
- Statistics row: 4 numbers with labels (10k+ users, 99% uptime)
- Timeline with dots on a vertical line
- FAQ accordion (it's fine, just not award-worthy alone)
- Any icon that is a rounded square with colored background + white icon inside
