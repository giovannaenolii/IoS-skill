# Motion Library Reference

## Core Principle
Every motion in this system must feel physical — like real objects with weight, friction, and spring energy. No linear easing. No `ease-in-out`. Pure spring physics at all times.

---

## 1. Spring Preset Library

```ts
// springs.ts — import from here everywhere
export const springs = {
  // iOS System — universal default for most transitions
  ios: { type: 'spring', stiffness: 300, damping: 30 } as const,

  // Snappy — quick UI responses (toggles, tabs, buttons)
  snappy: { type: 'spring', stiffness: 500, damping: 38 } as const,

  // Bouncy — playful (notifications, success states, badges)
  bouncy: { type: 'spring', stiffness: 380, damping: 20, mass: 0.8 } as const,

  // Gentle — large panels, page transitions
  gentle: { type: 'spring', stiffness: 100, damping: 22 } as const,

  // Magnetic — cursor-following, hover effects
  magnetic: { type: 'spring', stiffness: 150, damping: 12, mass: 0.3 } as const,

  // Spatial — visionOS-style weighted movement
  spatial: { type: 'spring', stiffness: 70, damping: 18, mass: 1.5 } as const,

  // Wobbly — fun/playful interfaces
  wobbly: { type: 'spring', stiffness: 260, damping: 16 } as const,

  // Stiff — nearly instant, UI-critical
  stiff: { type: 'spring', stiffness: 700, damping: 45 } as const,
}
```

---

## 2. Entrance Animation Variants

```ts
// variants.ts

// Standard glass panel entrance
export const glassPanelVariants = {
  hidden: { opacity: 0, y: 20, filter: 'blur(8px)', scale: 0.98 },
  visible: {
    opacity: 1, y: 0, filter: 'blur(0px)', scale: 1,
    transition: springs.ios,
  },
}

// Staggered container
export const staggerContainer = {
  hidden: {},
  visible: { transition: { staggerChildren: 0.07, delayChildren: 0.1 } },
}

// Card from below
export const cardFromBelow = {
  hidden: { opacity: 0, y: 32, scale: 0.96 },
  visible: { opacity: 1, y: 0, scale: 1, transition: springs.ios },
}

// Fade in from left
export const fromLeft = {
  hidden: { opacity: 0, x: -24, filter: 'blur(4px)' },
  visible: { opacity: 1, x: 0, filter: 'blur(0px)', transition: springs.gentle },
}

// Scale pop (for modals, alerts, badges)
export const scalePop = {
  hidden: { opacity: 0, scale: 0.85 },
  visible: { opacity: 1, scale: 1, transition: springs.bouncy },
}

// Page transition
export const pageTransition = {
  initial: { opacity: 0, y: 16, filter: 'blur(6px)' },
  animate: { opacity: 1, y: 0, filter: 'blur(0px)', transition: springs.gentle },
  exit: { opacity: 0, y: -8, filter: 'blur(3px)', transition: { duration: 0.15 } },
}
```

---

## 3. Scroll-Triggered Animations

```tsx
// Use Framer's useInView — NEVER window.addEventListener('scroll')
import { useInView } from 'framer-motion'
import { useRef } from 'react'

export function ScrollReveal({ children, delay = 0 }) {
  const ref = useRef(null)
  const inView = useInView(ref, { once: true, margin: '-80px 0px' })

  return (
    <motion.div
      ref={ref}
      initial={{ opacity: 0, y: 28, filter: 'blur(8px)' }}
      animate={inView ? { opacity: 1, y: 0, filter: 'blur(0px)' } : {}}
      transition={{ ...springs.ios, delay }}
    >
      {children}
    </motion.div>
  )
}

// Parallax scroll (Framer's useScroll)
import { useScroll, useTransform } from 'framer-motion'

export function ParallaxLayer({ children, speed = 0.3, className = '' }) {
  const { scrollY } = useScroll()
  const y = useTransform(scrollY, [0, 1000], [0, 1000 * speed])

  return (
    <motion.div style={{ y }} className={className}>
      {children}
    </motion.div>
  )
}
```

---

## 4. Hover Interaction Library

```tsx
// Tilt card — 3D perspective on hover
export function TiltCard({ children }) {
  const x = useMotionValue(0)
  const y = useMotionValue(0)
  const rotateX = useTransform(y, [-0.5, 0.5], [12, -12])
  const rotateY = useTransform(x, [-0.5, 0.5], [-12, 12])
  const glare = useTransform(x, [-0.5, 0.5], ['rgba(255,255,255,0.05)', 'rgba(255,255,255,0.20)'])

  const handleMove = (e) => {
    const rect = e.currentTarget.getBoundingClientRect()
    x.set((e.clientX - rect.left - rect.width / 2) / rect.width)
    y.set((e.clientY - rect.top - rect.height / 2) / rect.height)
  }

  return (
    <motion.div
      style={{ rotateX, rotateY, transformStyle: 'preserve-3d', perspective: 1000 }}
      onMouseMove={handleMove}
      onMouseLeave={() => { x.set(0); y.set(0) }}
      transition={springs.magnetic}
    >
      {/* Specular glare */}
      <motion.div
        className="absolute inset-0 rounded-[inherit] pointer-events-none z-10"
        style={{ background: useTransform(x, v => `linear-gradient(${135 + v * 60}deg, ${glare.get()} 0%, transparent 60%)`) }}
      />
      {children}
    </motion.div>
  )
}

// Spotlight card border
export function SpotlightCard({ children }) {
  const spotX = useMotionValue(-100)
  const spotY = useMotionValue(-100)

  return (
    <motion.div
      className="relative overflow-hidden"
      onMouseMove={(e) => {
        const rect = e.currentTarget.getBoundingClientRect()
        spotX.set(e.clientX - rect.left)
        spotY.set(e.clientY - rect.top)
      }}
      onMouseLeave={() => { spotX.set(-100); spotY.set(-100) }}
    >
      {/* Spotlight border */}
      <motion.div
        className="pointer-events-none absolute inset-0 rounded-[inherit] opacity-0 hover:opacity-100"
        style={{
          background: useMotionTemplate`
            radial-gradient(200px circle at ${spotX}px ${spotY}px, rgba(255,255,255,0.12), transparent 60%)
          `,
          transition: 'opacity 0.3s',
        }}
      />
      {children}
    </motion.div>
  )
}
```

---

## 5. Perpetual Micro-Animations (Performance-Safe)

```tsx
// Pulse indicator (status dot)
// MUST be isolated in its own React.memo component
export const PulseDot = React.memo(({ color = '#34C759' }) => (
  <div className="relative w-2.5 h-2.5">
    <motion.div
      className="absolute inset-0 rounded-full opacity-40"
      style={{ background: color }}
      animate={{ scale: [1, 2.5, 1], opacity: [0.4, 0, 0.4] }}
      transition={{ duration: 2.5, repeat: Infinity, ease: 'easeInOut' }}
    />
    <div className="absolute inset-0 rounded-full" style={{ background: color }} />
  </div>
))

// Shimmer loader
export const ShimmerLine = React.memo(({ width = '100%', height = 16, radius = 8 }) => (
  <div
    className="relative overflow-hidden"
    style={{ width, height, borderRadius: radius, background: 'rgba(255,255,255,0.05)' }}
  >
    <motion.div
      className="absolute inset-0"
      style={{ background: 'linear-gradient(90deg, transparent 0%, rgba(255,255,255,0.08) 50%, transparent 100%)' }}
      animate={{ x: ['-100%', '100%'] }}
      transition={{ duration: 1.8, repeat: Infinity, ease: 'linear' }}
    />
  </div>
))

// Float animation
export const FloatWrapper = React.memo(({ children, amplitude = 8, duration = 4 }) => (
  <motion.div
    animate={{ y: [0, -amplitude, 0] }}
    transition={{ duration, repeat: Infinity, ease: 'easeInOut' }}
  >
    {children}
  </motion.div>
))
```

---

## 6. useMotionTemplate Usage (Dynamic Glass Interactions)

```tsx
import { motion, useMotionTemplate, useMotionValue, useSpring } from 'framer-motion'

// Dynamic glow that follows cursor inside a container
export function GlowCard({ children }) {
  const mouseX = useMotionValue(0)
  const mouseY = useMotionValue(0)

  const glowX = useSpring(mouseX, { stiffness: 150, damping: 20 })
  const glowY = useSpring(mouseY, { stiffness: 150, damping: 20 })

  const background = useMotionTemplate`
    radial-gradient(250px circle at ${glowX}px ${glowY}px,
      rgba(0, 122, 255, 0.08) 0%,
      transparent 70%
    )
  `

  return (
    <motion.div
      className="relative rounded-[20px] overflow-hidden"
      onMouseMove={(e) => {
        const rect = e.currentTarget.getBoundingClientRect()
        mouseX.set(e.clientX - rect.left)
        mouseY.set(e.clientY - rect.top)
      }}
      style={{ background }}
    >
      {children}
    </motion.div>
  )
}
```

---

## 7. Performance Rules

- `will-change: transform` — add on animation start via JS, remove on end. NEVER set it statically in CSS permanently.
- Perpetual animations must be in their own `React.memo` component. Never inside a parent that re-renders.
- `AnimatePresence` — always wrap conditionally rendered elements. Enables exit animations.
- `layout` prop — use for elements that change position/size. Framer handles the FLIP animation automatically.
- Blur animations — blurring/unblurring is expensive. Keep `filter: blur()` animations short (under 0.3s).
- Background orbs — always `pointer-events: none`. Never animate `top/left`, use `transform: translate()`.
