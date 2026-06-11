---
name: glass-design-ios
description: |
  Senior UI/UX Engineer specialized in Awwwards-level glassmorphism, iOS/Apple-inspired minimalism, and ultra-premium web/app design. Enforces frosted glass surfaces, liquid depth systems, spatial hierarchy, Apple HIG principles, and Awwwards-tier visual polish. Use this skill whenever the user mentions glassmorphism, frosted glass, iOS design, Apple HIG, visionOS, blur effects, premium UI, liquid glass, Awwwards quality, ultra-modern design, or wants interfaces that look like they could be from Apple or win design awards. Trigger even for vague requests like "make it look really premium", "modern app design", "glass UI", "futuristic interface", "high-end SaaS", or "make it look stunning". When in doubt, use this skill.
---

# Glass Design iOS — Awwwards-Tier Frosted Glass & Apple-Inspired UI Skill

## 1. ACTIVE BASELINE CONFIGURATION

- GLASS_INTENSITY: 8 (1=Solid/Opaque, 10=Pure Invisible Glass)
- DEPTH_LAYERS: 7 (1=Flat, 10=Deep Spatial Parallax like visionOS)
- MOTION_PHYSICS: 7 (1=Static, 10=Full Spring Physics + Magnetic)
- LIGHT_REALISM: 9 (1=Flat Color, 10=Full Specular + Caustic Simulation)
- MINIMALISM_PURITY: 8 (1=Dense Info, 10=Absolute Apple-Level Breathing Room)

**AI Instruction:** These baselines drive all design decisions. Never ask the user to adjust them unless they explicitly request a style change. Adapt dynamically to user prompts. These values power Sections 3–8.

---

## 2. CORE PHILOSOPHY — THE GLASS DOCTRINE

Glass design is not a visual trick — it is a **spatial language**. Every surface must communicate where it lives in Z-space. Every blur must earn its existence by revealing what's behind it.

### The Three Laws of Glass
1. **Depth over Decoration:** Blur implies depth. A blurred surface must have content behind it worth revealing. Never blur emptiness.
2. **Light has a Source:** Every glass panel must have a coherent light origin — top-left refraction highlight, bottom-right shadow, consistent across all panels.
3. **Restraint over Excess:** Max 3 glass layers per viewport. Beyond 3, depth collapses into noise.

### The Apple Design Principles (Non-Negotiable)
- **Clarity:** Content is always readable through glass — minimum 4.5:1 contrast ratio on all text
- **Deference:** UI serves content, never competes with it
- **Depth:** Realistic motion and layering communicate hierarchy
- **No Skeuomorphism Kitsch:** Real materials, not cartoon glass. No rainbow reflections on UI unless it's a holographic card effect

---

## 3. GLASSMORPHISM ENGINEERING (The Full Technical Stack)

### 3.1 The Base Glass Recipe

Do NOT use naive `backdrop-filter: blur(10px)` alone. This is amateur-tier. The full glass panel is a composite of 6 properties working together:

```css
/* TIER 1: Standard Glass Panel */
.glass-panel {
  /* 1. The Blur Foundation */
  backdrop-filter: blur(20px) saturate(180%);
  -webkit-backdrop-filter: blur(20px) saturate(180%);

  /* 2. The Tinted Fill — always semi-transparent */
  background: rgba(255, 255, 255, 0.08);

  /* 3. The Edge Refraction — simulates glass thickness */
  border: 1px solid rgba(255, 255, 255, 0.18);

  /* 4. The Top-Edge Light Catch — the most important line */
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.3),   /* top refraction */
    inset 0 -1px 0 rgba(0, 0, 0, 0.08),        /* bottom edge */
    0 8px 32px rgba(0, 0, 0, 0.12),             /* ambient shadow */
    0 2px 8px rgba(0, 0, 0, 0.08);              /* contact shadow */

  /* 5. Border Radius — never sharp corners on glass */
  border-radius: 20px;

  /* 6. Overflow hidden for content clipping */
  overflow: hidden;
}
```

### 3.2 Glass Tier System (GLASS_INTENSITY-driven)

```css
/* TIER 1 — Subtle Overlay (GLASS_INTENSITY 1-3) */
/* Use for: subtle cards, secondary surfaces */
backdrop-filter: blur(8px) saturate(120%);
background: rgba(255, 255, 255, 0.04);
border: 1px solid rgba(255, 255, 255, 0.08);

/* TIER 2 — Classic Frosted (GLASS_INTENSITY 4-6) */
/* Use for: nav bars, side panels, modals */
backdrop-filter: blur(20px) saturate(180%);
background: rgba(255, 255, 255, 0.10);
border: 1px solid rgba(255, 255, 255, 0.20);

/* TIER 3 — Deep Frost (GLASS_INTENSITY 7-8) */
/* Use for: primary panels, hero cards */
backdrop-filter: blur(40px) saturate(200%) brightness(110%);
background: rgba(255, 255, 255, 0.12);
border: 1px solid rgba(255, 255, 255, 0.25);

/* TIER 4 — Liquid Glass / visionOS (GLASS_INTENSITY 9-10) */
/* Use for: floating windows, spatial UI */
backdrop-filter: blur(80px) saturate(220%) brightness(115%) contrast(1.05);
background: rgba(255, 255, 255, 0.06);
border: 1px solid rgba(255, 255, 255, 0.35);
box-shadow:
  inset 0 2px 0 rgba(255, 255, 255, 0.5),
  inset 0 -1px 0 rgba(0, 0, 0, 0.1),
  0 32px 64px rgba(0, 0, 0, 0.2),
  0 0 0 0.5px rgba(0, 0, 0, 0.05);
```

### 3.3 Dark Mode Glass (The Premium Variant)

Dark glass is not inverting white glass. It requires a completely different recipe:

```css
/* Dark Glass Panel */
.glass-dark {
  backdrop-filter: blur(32px) saturate(180%) brightness(0.9);
  background: rgba(12, 12, 20, 0.65);
  border: 1px solid rgba(255, 255, 255, 0.06);
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.08),
    inset 0 -1px 0 rgba(0, 0, 0, 0.3),
    0 20px 40px rgba(0, 0, 0, 0.4),
    0 1px 0 rgba(255, 255, 255, 0.02);
}
```

### 3.4 Colored Glass (Chromatic Panels)

For accent glass panels (green, blue, etc.):

```css
/* Emerald Glass */
background: rgba(16, 185, 129, 0.08);
border-color: rgba(16, 185, 129, 0.25);
box-shadow: inset 0 1px 0 rgba(16, 185, 129, 0.3), 0 8px 32px rgba(16, 185, 129, 0.15);

/* Tinted backdrop */
backdrop-filter: blur(24px) saturate(200%) hue-rotate(0deg);
```

---

## 4. BACKGROUND SYSTEMS (What Glass Blurs MATTERS)

Glass without a rich background is nothing. The background must be intentionally designed to make glass pop:

### 4.1 Mesh Gradient (The Gold Standard)
```css
.mesh-background {
  background:
    radial-gradient(ellipse at 20% 20%, rgba(120, 40, 200, 0.4) 0%, transparent 60%),
    radial-gradient(ellipse at 80% 80%, rgba(0, 180, 255, 0.3) 0%, transparent 60%),
    radial-gradient(ellipse at 50% 50%, rgba(255, 100, 50, 0.2) 0%, transparent 70%),
    linear-gradient(135deg, #0a0a12 0%, #12101e 50%, #0d1520 100%);
  animation: meshShift 12s ease-in-out infinite alternate;
}

@keyframes meshShift {
  0% { background-position: 0% 0%, 100% 100%, 50% 50%; }
  100% { background-position: 10% 10%, 90% 90%, 55% 45%; }
}
```

### 4.2 Noise Texture Overlay (Essential for Depth)
```css
/* Add film grain — makes glass feel physical */
.noise-overlay::before {
  content: '';
  position: fixed;
  inset: 0;
  opacity: 0.03;
  pointer-events: none;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)'/%3E%3C/svg%3E");
  z-index: 9999;
}
```

### 4.3 Bokeh Blobs (Animated Depth)
```jsx
// Animated background orbs — optimized with will-change
const blobs = [
  { cx: "20%", cy: "30%", r: "40%", color: "rgba(139, 92, 246, 0.35)" },
  { cx: "80%", cy: "70%", r: "35%", color: "rgba(59, 130, 246, 0.3)" },
  { cx: "60%", cy: "20%", r: "30%", color: "rgba(16, 185, 129, 0.25)" },
];
// Animate with Framer Motion, never with JS scroll listeners
// Use transform: translate() only — no left/top animation
```

---

## 5. iOS / APPLE HIG SYSTEM

### 5.1 Typography — Apple's Exact Scale

```css
/* SF Pro DNA — replicated in web */
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap');
/* Use Inter as SF Pro substitute — closest match available on web */
/* For premium: use Geist or Plus Jakarta Sans */

:root {
  /* Apple Text Sizes (exact HIG values) */
  --text-large-title: clamp(2rem, 5vw, 3.5rem);    /* 34pt */
  --text-title1: clamp(1.75rem, 3.5vw, 2.75rem);   /* 28pt */
  --text-title2: clamp(1.375rem, 2.5vw, 1.75rem);  /* 22pt */
  --text-title3: clamp(1.125rem, 2vw, 1.375rem);   /* 20pt */
  --text-headline: 1.0625rem;                        /* 17pt semibold */
  --text-body: 1.0625rem;                            /* 17pt */
  --text-callout: 1rem;                              /* 16pt */
  --text-subhead: 0.9375rem;                         /* 15pt */
  --text-footnote: 0.8125rem;                        /* 13pt */
  --text-caption1: 0.75rem;                          /* 12pt */
  --text-caption2: 0.6875rem;                        /* 11pt */

  /* Letter spacing — Apple uses negative tracking for large type */
  --tracking-display: -0.04em;
  --tracking-title: -0.025em;
  --tracking-body: -0.01em;

  /* Line height — Apple HIG */
  --leading-tight: 1.1;
  --leading-snug: 1.25;
  --leading-normal: 1.4;
  --leading-relaxed: 1.6;
}
```

### 5.2 iOS Spacing System

```css
:root {
  /* iOS Base Unit: 4pt */
  --space-1: 4px;
  --space-2: 8px;
  --space-3: 12px;
  --space-4: 16px;   /* standard horizontal margin */
  --space-5: 20px;
  --space-6: 24px;
  --space-8: 32px;
  --space-10: 40px;
  --space-12: 48px;
  --space-16: 64px;
  --space-20: 80px;

  /* iOS Corner Radii */
  --radius-sm: 8px;      /* small buttons, tags */
  --radius-md: 12px;     /* cards, inputs */
  --radius-lg: 16px;     /* panels */
  --radius-xl: 20px;     /* modals, sheets */
  --radius-2xl: 28px;    /* large cards */
  --radius-full: 9999px; /* pills, icons */

  /* iOS Safe Areas */
  --safe-top: env(safe-area-inset-top);
  --safe-bottom: env(safe-area-inset-bottom);
}
```

### 5.3 Apple Color System

```css
:root {
  /* iOS System Colors — exact values */
  --ios-blue: #007AFF;
  --ios-green: #34C759;
  --ios-indigo: #5856D6;
  --ios-orange: #FF9500;
  --ios-pink: #FF2D55;
  --ios-purple: #AF52DE;
  --ios-red: #FF3B30;
  --ios-teal: #5AC8FA;
  --ios-yellow: #FFCC00;

  /* iOS Grays */
  --ios-gray: #8E8E93;
  --ios-gray2: #AEAEB2;
  --ios-gray3: #C7C7CC;
  --ios-gray4: #D1D1D6;
  --ios-gray5: #E5E5EA;
  --ios-gray6: #F2F2F7;

  /* iOS Backgrounds */
  --ios-bg-primary: #000000;         /* dark mode system bg */
  --ios-bg-secondary: #1C1C1E;       /* elevated surface */
  --ios-bg-tertiary: #2C2C2E;        /* grouped content */
  --ios-bg-quaternary: #3A3A3C;      /* deeply elevated */

  /* iOS Separator */
  --ios-separator: rgba(60, 60, 67, 0.36);
  --ios-separator-opaque: #38383A;
}
```

### 5.4 Dynamic Island Patterns

```jsx
// Dynamic Island morphing component
// Key principle: single pill that expands to different states
const dynamicIslandVariants = {
  compact: { width: 126, height: 37, borderRadius: 20 },
  expanded: { width: 371, height: 84, borderRadius: 44 },
  notification: { width: 230, height: 37, borderRadius: 20 },
};
// Use Framer Motion layoutId="dynamic-island" for seamless morphing
// NEVER use CSS transitions for this — Framer layout animations only
```

### 5.5 iOS Sheet & Modal Patterns

```css
/* Bottom Sheet — iOS style */
.ios-sheet {
  border-radius: 20px 20px 0 0;  /* Only top corners rounded */
  backdrop-filter: blur(40px) saturate(180%);
  background: rgba(28, 28, 30, 0.85);

  /* Drag handle */
  .drag-handle {
    width: 36px;
    height: 5px;
    border-radius: 3px;
    background: rgba(60, 60, 67, 0.3);
    margin: 8px auto 0;
  }
}
```

---

## 6. DEPTH & SPATIAL SYSTEM (DEPTH_LAYERS-driven)

Glass design lives or dies by its depth simulation. Implement a strict Z-axis hierarchy:

### 6.1 The 7-Layer Spatial Stack

```
Z-Layer 0: Background (mesh gradients, video, imagery)
Z-Layer 1: Background glass (subtle, barely visible overlay)
Z-Layer 2: Content plane (main page content, text)
Z-Layer 3: Card plane (glass panels, containers)
Z-Layer 4: Floating plane (popovers, tooltips, inline menus)
Z-Layer 5: Overlay plane (modals, sheets, drawers)
Z-Layer 6: System plane (nav bars, status bars, toasts)
Z-Layer 7: Emergency plane (alerts, critical overlays)
```

Each layer deeper = more blur + higher opacity fill + stronger shadow.

### 6.2 Parallax Implementation (CSS-only, 60fps)

```css
/* Parallax container — NO JS scroll listeners */
.parallax-scene {
  transform-style: preserve-3d;
  perspective: 1000px;
}

.layer-back { transform: translateZ(-200px) scale(1.2); }
.layer-mid  { transform: translateZ(-100px) scale(1.1); }
.layer-fore { transform: translateZ(0px); }

/* Hover parallax — use CSS custom properties + @property */
@property --mouse-x { syntax: '<number>'; inherits: true; initial-value: 0; }
@property --mouse-y { syntax: '<number>'; inherits: true; initial-value: 0; }
```

### 6.3 Specular Highlight System

```css
/* Moving light reflection on glass — the signature effect */
.glass-specular {
  position: relative;
  overflow: hidden;
}
.glass-specular::after {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(
    135deg,
    rgba(255, 255, 255, 0.15) 0%,
    transparent 40%,
    transparent 60%,
    rgba(255, 255, 255, 0.05) 100%
  );
  pointer-events: none;
  transition: opacity 0.3s;
}
```

---

## 7. MOTION PHYSICS ENGINE (MOTION_PHYSICS-driven)

### 7.1 Spring Config Library

```js
// iOS-calibrated spring presets
export const springs = {
  // iOS default — used for most UI transitions
  ios: { type: "spring", stiffness: 300, damping: 30 },
  // Snappy — buttons, toggles
  snappy: { type: "spring", stiffness: 500, damping: 35 },
  // Bouncy — playful elements, notifications
  bouncy: { type: "spring", stiffness: 400, damping: 20, mass: 0.8 },
  // Gentle — large panels, sheets
  gentle: { type: "spring", stiffness: 120, damping: 25 },
  // Magnetic — cursor-following elements
  magnetic: { type: "spring", stiffness: 150, damping: 15, mass: 0.3 },
  // visionOS — slow, weighted spatial movement
  spatial: { type: "spring", stiffness: 80, damping: 20, mass: 1.2 },
};
```

### 7.2 Magnetic Glass Button

```jsx
// The signature glass button with magnetic pull
// CRITICAL: use useMotionValue — never useState for mouse position
const MagneticGlassButton = ({ children }) => {
  const x = useMotionValue(0);
  const y = useMotionValue(0);
  const rotateX = useTransform(y, [-0.5, 0.5], [8, -8]);
  const rotateY = useTransform(x, [-0.5, 0.5], [-8, 8]);

  const handleMove = (e) => {
    const rect = e.currentTarget.getBoundingClientRect();
    const centerX = rect.left + rect.width / 2;
    const centerY = rect.top + rect.height / 2;
    x.set((e.clientX - centerX) / rect.width);
    y.set((e.clientY - centerY) / rect.height);
  };

  return (
    <motion.button
      style={{ x: useTransform(x, v => v * 12), y: useTransform(y, v => v * 12), rotateX, rotateY }}
      onMouseMove={handleMove}
      onMouseLeave={() => { x.set(0); y.set(0); }}
      className="glass-panel px-6 py-3 relative overflow-hidden"
      whileTap={{ scale: 0.97 }}
    >
      {/* Inner specular on hover */}
      <motion.div className="absolute inset-0 bg-gradient-to-br from-white/20 to-transparent opacity-0 hover:opacity-100 transition-opacity" />
      {children}
    </motion.button>
  );
};
```

### 7.3 Page Transition System

```jsx
// Frosted glass page transitions
const pageVariants = {
  initial: { opacity: 0, y: 20, filter: "blur(8px)" },
  enter: { opacity: 1, y: 0, filter: "blur(0px)", transition: springs.gentle },
  exit: { opacity: 0, y: -10, filter: "blur(4px)", transition: { duration: 0.2 } },
};
// Wrap pages in <AnimatePresence mode="wait">
```

### 7.4 Glass Panel Entrance

```jsx
// Staggered glass panel reveal
const containerVariants = {
  hidden: {},
  visible: { transition: { staggerChildren: 0.08 } },
};
const panelVariants = {
  hidden: { opacity: 0, y: 24, filter: "blur(12px)", scale: 0.97 },
  visible: { opacity: 1, y: 0, filter: "blur(0px)", scale: 1, transition: springs.ios },
};
```

---

## 8. COMPONENT LIBRARY — GLASS PATTERNS

See `references/glass-components.md` for full code. Summary:

### 8.1 The Glass Navigation Bar
- Frosted, 100% width, 60px tall (iOS standard)
- `backdrop-filter: blur(40px) saturate(200%)`
- Separator: 0.5px line at bottom with `rgba(255,255,255,0.1)`
- Extend into safe area: `padding-top: env(safe-area-inset-top)`

### 8.2 The Glass Card System
Four card types: `GlassCard`, `GlassCardElevated`, `GlassCardAccent`, `GlassCardDark`
All inherit base glass recipe. Elevation communicated purely via shadow and blur intensity.

### 8.3 The Glass Input
```css
input.glass-input {
  backdrop-filter: blur(16px);
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(255, 255, 255, 0.12);
  border-radius: 12px;
  /* On focus: increase border opacity to 0.3, add subtle glow */
  box-shadow: 0 0 0 3px rgba(0, 122, 255, 0.25);
}
```

### 8.4 The Glass Toast / Notification
- Float-in from bottom with spring physics
- `backdrop-filter: blur(32px) saturate(180%)`
- Max width: 360px, centered
- Icon + short text + dismiss — Apple-style brevity

### 8.5 The Segmented Control (iOS native feel)
- Glass pill container with animated sliding indicator
- Indicator uses Framer `layoutId` for seamless slide
- Never use border-based tab indicators — use background fill

---

## 9. AWWWARDS CHECKLIST — THE QUALITY GATES

Every output must pass ALL of these before shipping:

### Visual
- [ ] Minimum 3 distinct depth planes visible
- [ ] Background is designed (not flat color), glass makes sense contextually
- [ ] All glass panels have correct inner top highlight (`inset 0 1px 0 rgba(255,255,255,...)`)
- [ ] No flat/generic shadows — all shadows are tinted and layered
- [ ] Noise texture overlay applied for tactile depth
- [ ] Typography uses negative tracking for large headings
- [ ] Max 2 font families used. Zero Inter.
- [ ] Color palette: max 1 accent + neutrals. Zero AI purple gradients.

### Interaction
- [ ] Hover states on ALL interactive elements
- [ ] At least one magnetic/physics-driven interaction (MOTION_PHYSICS > 5)
- [ ] Page/section entrance animation implemented
- [ ] No linear easing anywhere — all spring physics
- [ ] Touch targets minimum 44x44px (iOS HIG)

### Technical
- [ ] `backdrop-filter` paired with `-webkit-backdrop-filter` for Safari
- [ ] `will-change: transform` only on actively animating elements, removed after
- [ ] No animations on `top`, `left`, `width`, `height` — only `transform` and `opacity`
- [ ] Noise overlay is `pointer-events: none, fixed, z-index: 9999`
- [ ] Perpetual animations isolated in their own Client Component (React)
- [ ] `min-h-[100dvh]` never `h-screen`
- [ ] All glass panels: `overflow: hidden` to clip content properly
- [ ] Safari tested: blur values above 80px may cause performance issues on mobile Safari

### Copy & Content
- [ ] Zero filler words: "elevate", "seamless", "unleash", "next-gen" BANNED
- [ ] No generic placeholder names (John Doe, Jane Smith)
- [ ] No `99.99%` fake precision — use organic-feeling numbers like `47.2%`, `2,841`
- [ ] No emoji in UI unless explicitly requested

---

## 10. FORBIDDEN PATTERNS (Instant Disqualification)

These patterns immediately mark output as low-quality:

### Glass Sins
- **Blurring without background content:** Glass over solid color = pointless blur. Design the background.
- **Excessive glass layers:** More than 3 overlapping blur layers = visual mud. Fewer is better.
- **Pure white glass:** `rgba(255,255,255,0.5)` = washing everything out. Keep fills < 0.15.
- **Missing inner highlight:** No `inset 0 1px 0 rgba(255,255,255,...)` = flat, fake glass.
- **Same blur value everywhere:** `blur(10px)` on every panel = no depth. Vary from 8px to 80px.

### iOS Sins
- **Sharp corners on glass:** `border-radius: 0` on any glass panel. Always minimum 8px.
- **Wrong safe areas:** Content touching phone notch/home indicator. Always use `env(safe-area-inset-*)`.
- **Non-system fonts for body text:** Body text must use system-ui or a close web equivalent.
- **Broken haptic metaphors:** Animations that don't feel physical — too fast, too linear, wrong easing.
- **Colored backgrounds on cards when glass exists:** Pick one materiality system. Don't mix.

### Motion Sins
- **Linear easing:** `ease-in-out`, `linear` anywhere. Apple uses spring physics exclusively.
- **JS scroll listeners:** Use Framer's `useScroll` or IntersectionObserver only.
- **Animating layout properties:** `width`, `height`, `top`, `left` triggers reflow. BANNED.
- **useState for animation values:** Use `useMotionValue` and `useTransform`. Never re-render for mouse position.

### Aesthetic Sins
- **AI Purple Glow:** The `rgba(139, 92, 246, 0.8)` outer glow default is immediately recognizable as AI slop.
- **3-column equal cards:** Generic, soulless. Use Bento grids or asymmetric layouts.
- **Centered hero H1 over dark gradient:** The most overused AI pattern alive. Banned.
- **Stock icon backgrounds:** Lucide icons on colored circles as "feature icons." It's 2020. Stop.

---

## 11. STACK DEFAULTS

```
Framework:    Next.js 14+ App Router (React Server Components)
Styling:      Tailwind CSS v3 + CSS custom properties for glass values
Motion:       Framer Motion (UI) — GSAP ScrollTrigger for full-page scroll sequences only
Fonts:        Geist (headlines) + Geist Mono (data/code) — or Plus Jakarta Sans
Icons:        @phosphor-icons/react (never Lucide, never emoji)
3D:           Three.js / React Three Fiber for WebGL backgrounds only
Color System: HSL custom properties for theming, iOS System Colors as accent reference
```

---

## 12. REFERENCE FILES

Read these when implementing specific patterns:

- `references/glass-components.md` — Full component code (NavBar, Cards, Inputs, Modals, Toasts)
- `references/ios-patterns.md` — Deep iOS HIG patterns (Dynamic Island, Sheets, Tab Bar, Haptics)
- `references/backgrounds.md` — Background system implementations (mesh, bokeh, grain, video)
- `references/motion-library.md` — Spring presets, entrance animations, scroll choreography
- `references/awwwards-examples.md` — Pattern breakdowns of award-winning sites to study

---
