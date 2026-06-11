# Background Systems Reference

## The Fundamental Rule
Glass without a designed background is amateur. The background is 50% of the glassmorphism effect. Every glass project MUST have an intentionally engineered background.

---

## 1. Animated Mesh Gradient (Primary Recommendation)

```tsx
// MeshBackground.tsx — isolated Client Component
'use client'
import { useEffect, useRef } from 'react'

export function MeshBackground() {
  return (
    <div
      className="fixed inset-0 -z-10"
      style={{
        background: `
          radial-gradient(ellipse 80% 60% at 20% 20%, rgba(120, 40, 200, 0.45) 0%, transparent 60%),
          radial-gradient(ellipse 60% 70% at 80% 80%, rgba(0, 180, 255, 0.35) 0%, transparent 60%),
          radial-gradient(ellipse 50% 50% at 50% 50%, rgba(255, 80, 50, 0.20) 0%, transparent 70%),
          radial-gradient(ellipse 70% 40% at 70% 20%, rgba(0, 200, 150, 0.25) 0%, transparent 55%),
          linear-gradient(135deg, #060610 0%, #0d0d1e 40%, #080d1a 100%)
        `,
        animation: 'meshPulse 16s ease-in-out infinite alternate',
      }}
    >
      <style>{`
        @keyframes meshPulse {
          0%   { filter: hue-rotate(0deg) brightness(1.0); }
          50%  { filter: hue-rotate(15deg) brightness(1.05); }
          100% { filter: hue-rotate(-10deg) brightness(0.95); }
        }
      `}</style>
    </div>
  )
}
```

---

## 2. Bokeh Orb System (Animated Depth Blobs)

```tsx
'use client'
import { motion } from 'framer-motion'

const orbs = [
  { x: '15%', y: '25%', size: 500, color: 'rgba(99, 40, 220, 0.35)', duration: 18 },
  { x: '75%', y: '65%', size: 600, color: 'rgba(0, 150, 255, 0.30)', duration: 22 },
  { x: '55%', y: '15%', size: 400, color: 'rgba(16, 185, 129, 0.25)', duration: 14 },
  { x: '85%', y: '30%', size: 350, color: 'rgba(255, 100, 50, 0.20)', duration: 26 },
]

export function BokehBackground() {
  return (
    <div className="fixed inset-0 -z-10 overflow-hidden" style={{ background: '#060610' }}>
      {orbs.map((orb, i) => (
        <motion.div
          key={i}
          className="absolute rounded-full"
          style={{
            left: orb.x,
            top: orb.y,
            width: orb.size,
            height: orb.size,
            background: `radial-gradient(circle, ${orb.color} 0%, transparent 70%)`,
            transform: 'translate(-50%, -50%)',
            filter: 'blur(40px)',
            willChange: 'transform',
          }}
          animate={{
            x: [0, 40, -20, 30, 0],
            y: [0, -30, 20, -10, 0],
            scale: [1, 1.1, 0.95, 1.05, 1],
          }}
          transition={{
            duration: orb.duration,
            repeat: Infinity,
            ease: 'easeInOut',
            delay: i * 2,
          }}
        />
      ))}
    </div>
  )
}
```

---

## 3. CSS-only Noise Texture (Always Layer on Top)

```tsx
// Add this to your root layout — always present for tactile depth
export function NoiseOverlay() {
  return (
    <div
      className="fixed inset-0 pointer-events-none z-[9999]"
      style={{
        opacity: 0.035,
        backgroundImage: `url("data:image/svg+xml,%3Csvg viewBox='0 0 512 512' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.75' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E")`,
        backgroundRepeat: 'repeat',
        backgroundSize: '256px 256px',
        mixBlendMode: 'overlay',
      }}
    />
  )
}
```

---

## 4. Aurora / Northern Lights (Dramatic Hero Background)

```css
.aurora-bg {
  background: #030308;
  position: relative;
  overflow: hidden;
}

.aurora-bg::before,
.aurora-bg::after {
  content: '';
  position: absolute;
  border-radius: 50%;
  filter: blur(80px);
  animation: aurora 12s ease-in-out infinite alternate;
}

.aurora-bg::before {
  width: 800px;
  height: 500px;
  background: linear-gradient(135deg, rgba(0, 200, 180, 0.4), rgba(0, 100, 255, 0.3));
  top: -200px;
  left: -200px;
}

.aurora-bg::after {
  width: 600px;
  height: 600px;
  background: linear-gradient(135deg, rgba(150, 0, 255, 0.35), rgba(255, 50, 100, 0.2));
  bottom: -200px;
  right: -200px;
  animation-delay: 4s;
}

@keyframes aurora {
  0%   { transform: rotate(0deg) scale(1); }
  100% { transform: rotate(20deg) scale(1.2); }
}
```

---

## 5. Subtle Grid / Dot Pattern (Tech / Dashboard Background)

```css
/* Fine dot grid — elegant for dashboard glass */
.dot-grid-bg {
  background-color: #08080f;
  background-image: radial-gradient(rgba(255,255,255,0.08) 1px, transparent 1px);
  background-size: 28px 28px;
}

/* Line grid */
.line-grid-bg {
  background-color: #08080f;
  background-image:
    linear-gradient(rgba(255,255,255,0.03) 1px, transparent 1px),
    linear-gradient(90deg, rgba(255,255,255,0.03) 1px, transparent 1px);
  background-size: 40px 40px;
}

/* Faded edge */
.line-grid-bg::after {
  content: '';
  position: fixed;
  inset: 0;
  background: radial-gradient(ellipse at center, transparent 40%, #08080f 100%);
  pointer-events: none;
}
```

---

## 6. Video Background with Glass Overlay

```tsx
export function VideoBackground({ src }) {
  return (
    <div className="fixed inset-0 -z-10 overflow-hidden">
      <video
        autoPlay
        muted
        loop
        playsInline
        className="absolute inset-0 w-full h-full object-cover"
        style={{ filter: 'brightness(0.4) saturate(1.3)' }}
      >
        <source src={src} type="video/mp4" />
      </video>
      {/* Dark overlay for glass readability */}
      <div className="absolute inset-0" style={{ background: 'rgba(4, 4, 12, 0.6)' }} />
    </div>
  )
}
```

---

## 7. Background Composition Rules

1. **Dark-first:** Glass reads best on dark backgrounds (85% of the time). Keep base darker than `#121220`.
2. **Color placement:** Put warm tones (orange, red) in one corner, cool tones (blue, purple) opposite. Natural tension.
3. **Blur radius:** Background orbs should use `filter: blur(60-120px)` — too sharp and they compete with glass. Too blurred and they disappear.
4. **Animation speed:** Max 20s for background animation. Faster = distracting.
5. **Noise always:** Always layer noise texture. It makes the glass feel physical, not digital.
6. **Saturation:** `filter: saturate(120-150%)` on `backdrop-filter` enhances the colors showing through glass.
