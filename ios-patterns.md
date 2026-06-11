# iOS / Apple HIG Deep Patterns

## Core HIG Principles to Internalize
1. **Hierarchy through weight, not size alone** — Use `font-weight: 600` vs `font-weight: 300` to create contrast. Don't just make things bigger.
2. **Negative space is content** — Breathing room communicates quality. Don't fill every pixel.
3. **Translucency creates context** — Glass tells the user where they are in the hierarchy. More opaque = higher in the stack.
4. **Consistent motion = trust** — When animations are predictable and physical, the app feels trustworthy.

---

## 1. Dynamic Island Component

```tsx
'use client'
import { motion, AnimatePresence } from 'framer-motion'
import { useState } from 'react'

type IslandState = 'compact' | 'expanded' | 'notification'

const islandGeometry = {
  compact:      { width: 126, height: 37, borderRadius: 20 },
  notification: { width: 240, height: 40, borderRadius: 22 },
  expanded:     { width: 352, height: 100, borderRadius: 44 },
}

export function DynamicIsland({ children }) {
  const [state, setState] = useState<IslandState>('compact')
  const geo = islandGeometry[state]

  return (
    <div className="flex flex-col items-center gap-4">
      <motion.div
        layout
        className="overflow-hidden flex items-center justify-center"
        style={{
          background: '#000',
          width: geo.width,
          height: geo.height,
          borderRadius: geo.borderRadius,
          boxShadow: '0 0 0 1px rgba(255,255,255,0.05)',
        }}
        transition={{ type: 'spring', stiffness: 300, damping: 30 }}
      >
        <AnimatePresence mode="wait">
          <motion.div
            key={state}
            initial={{ opacity: 0, scale: 0.8 }}
            animate={{ opacity: 1, scale: 1, transition: { type: 'spring', stiffness: 400, damping: 30, delay: 0.05 } }}
            exit={{ opacity: 0, scale: 0.9, transition: { duration: 0.1 } }}
            className="flex items-center gap-2 px-4"
          >
            {children?.[state]}
          </motion.div>
        </AnimatePresence>
      </motion.div>

      {/* Debug controls */}
      <div className="flex gap-2">
        {(Object.keys(islandGeometry) as IslandState[]).map(s => (
          <button key={s} onClick={() => setState(s)}
            className="px-3 py-1 text-xs text-white/60 border border-white/10 rounded-full hover:bg-white/05">
            {s}
          </button>
        ))}
      </div>
    </div>
  )
}
```

---

## 2. iOS Tab Bar

```tsx
'use client'
import { motion } from 'framer-motion'
import { useState } from 'react'

const tabs = [
  { id: 'home', label: 'Home', icon: 'M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6' },
  { id: 'search', label: 'Search', icon: 'M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z' },
  { id: 'profile', label: 'Profile', icon: 'M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z' },
]

export function IOSTabBar() {
  const [active, setActive] = useState('home')

  return (
    <div
      className="fixed bottom-0 inset-x-0"
      style={{
        paddingBottom: 'env(safe-area-inset-bottom)',
        backdropFilter: 'blur(40px) saturate(200%)',
        WebkitBackdropFilter: 'blur(40px) saturate(200%)',
        background: 'rgba(18, 18, 26, 0.88)',
        borderTop: '0.5px solid rgba(255,255,255,0.08)',
      }}
    >
      <div className="flex justify-around items-center pt-2 pb-1">
        {tabs.map(tab => {
          const isActive = active === tab.id
          return (
            <button
              key={tab.id}
              onClick={() => setActive(tab.id)}
              className="flex flex-col items-center gap-1 min-w-[44px] min-h-[44px] justify-center"
            >
              <motion.div
                animate={{ scale: isActive ? 1 : 1 }}
                whileTap={{ scale: 0.85 }}
                transition={{ type: 'spring', stiffness: 500, damping: 30 }}
              >
                <svg
                  className="w-[26px] h-[26px] transition-colors duration-150"
                  fill="none"
                  stroke={isActive ? '#007AFF' : 'rgba(255,255,255,0.35)'}
                  strokeWidth={isActive ? 2 : 1.5}
                  viewBox="0 0 24 24"
                >
                  <path strokeLinecap="round" strokeLinejoin="round" d={tab.icon} />
                </svg>
              </motion.div>
              <span
                className="text-[10px] font-medium transition-colors duration-150"
                style={{ color: isActive ? '#007AFF' : 'rgba(255,255,255,0.35)' }}
              >
                {tab.label}
              </span>
            </button>
          )
        })}
      </div>
    </div>
  )
}
```

---

## 3. iOS List / Table View

```tsx
// The Apple-style grouped list — used in Settings, Mail, etc.
export function IOSListGroup({ title, items }) {
  return (
    <div className="px-4">
      {title && (
        <p className="text-[13px] font-medium text-white/35 uppercase tracking-wider px-3 pb-2">{title}</p>
      )}
      <div
        className="rounded-[12px] overflow-hidden"
        style={{
          backdropFilter: 'blur(20px) saturate(160%)',
          background: 'rgba(28, 28, 30, 0.8)',
          border: '0.5px solid rgba(255,255,255,0.06)',
        }}
      >
        {items.map((item, i) => (
          <div key={i}>
            <motion.div
              className="flex items-center justify-between px-4 py-[14px] cursor-pointer"
              whileTap={{ background: 'rgba(255,255,255,0.05)' }}
              transition={{ duration: 0.1 }}
            >
              <div className="flex items-center gap-3">
                {item.icon && (
                  <div className="w-8 h-8 rounded-[8px] flex items-center justify-center" style={{ background: item.iconBg || 'rgba(255,255,255,0.1)' }}>
                    {item.icon}
                  </div>
                )}
                <span className="text-[17px] text-white">{item.label}</span>
              </div>
              <div className="flex items-center gap-2">
                {item.value && <span className="text-[17px] text-white/35">{item.value}</span>}
                <svg className="w-4 h-4 text-white/20" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path strokeLinecap="round" d="M9 18l6-6-6-6" />
                </svg>
              </div>
            </motion.div>
            {i < items.length - 1 && (
              <div className="h-px ml-4" style={{ background: 'rgba(255,255,255,0.06)' }} />
            )}
          </div>
        ))}
      </div>
    </div>
  )
}
```

---

## 4. iOS Toggle Switch

```tsx
'use client'
import { motion } from 'framer-motion'
import { useState } from 'react'

export function IOSToggle({ defaultOn = false, onChange, label, description }) {
  const [on, setOn] = useState(defaultOn)

  const handleToggle = () => {
    const next = !on
    setOn(next)
    onChange?.(next)
    // Haptic feedback simulation via CSS (visual only)
  }

  return (
    <div className="flex items-center justify-between py-3">
      <div>
        <p className="text-[17px] text-white">{label}</p>
        {description && <p className="text-[13px] text-white/35 mt-0.5">{description}</p>}
      </div>
      <motion.button
        onClick={handleToggle}
        className="relative flex-shrink-0 w-[51px] h-[31px] rounded-full p-[2px] transition-colors duration-200"
        style={{ background: on ? '#34C759' : 'rgba(120, 120, 128, 0.32)' }}
        whileTap={{ scale: 0.95 }}
        transition={{ type: 'spring', stiffness: 500, damping: 35 }}
      >
        <motion.div
          className="w-[27px] h-[27px] rounded-full bg-white"
          style={{ boxShadow: '0 2px 4px rgba(0,0,0,0.3)' }}
          animate={{ x: on ? 20 : 0 }}
          transition={{ type: 'spring', stiffness: 500, damping: 35 }}
        />
      </motion.button>
    </div>
  )
}
```

---

## 5. iOS Context Menu

```tsx
'use client'
import { motion, AnimatePresence } from 'framer-motion'
import { useState, useRef } from 'react'

export function IOSContextMenu({ trigger, items }) {
  const [open, setOpen] = useState(false)

  return (
    <div className="relative inline-block">
      <div onContextMenu={(e) => { e.preventDefault(); setOpen(true) }}>
        {trigger}
      </div>

      <AnimatePresence>
        {open && (
          <>
            <div className="fixed inset-0 z-50" onClick={() => setOpen(false)} />
            <motion.div
              className="absolute z-50 min-w-[200px] rounded-[14px] overflow-hidden"
              style={{
                top: '100%', left: 0, marginTop: 8,
                backdropFilter: 'blur(40px) saturate(200%)',
                background: 'rgba(28, 28, 30, 0.92)',
                border: '0.5px solid rgba(255,255,255,0.10)',
                boxShadow: '0 20px 40px rgba(0,0,0,0.5), 0 0 0 0.5px rgba(0,0,0,0.2)',
              }}
              initial={{ opacity: 0, scale: 0.85, y: -8 }}
              animate={{ opacity: 1, scale: 1, y: 0, transition: { type: 'spring', stiffness: 400, damping: 28 } }}
              exit={{ opacity: 0, scale: 0.9, y: -4, transition: { duration: 0.12 } }}
            >
              {items.map((item, i) => (
                <div key={i}>
                  <motion.button
                    className="flex items-center justify-between w-full px-4 py-[13px] text-[17px]"
                    style={{ color: item.destructive ? '#FF3B30' : 'white' }}
                    whileTap={{ background: 'rgba(255,255,255,0.08)' }}
                    onClick={() => { item.onPress?.(); setOpen(false) }}
                  >
                    <span>{item.label}</span>
                    {item.icon && <span className="text-white/40">{item.icon}</span>}
                  </motion.button>
                  {i < items.length - 1 && <div className="h-px" style={{ background: 'rgba(255,255,255,0.06)' }} />}
                </div>
              ))}
            </motion.div>
          </>
        )}
      </AnimatePresence>
    </div>
  )
}
```

---

## 6. Apple-Style Typography Usage

```tsx
// Headline hierarchy — Apple-style
export function AppleHeadline({ eyebrow, title, subtitle }) {
  return (
    <div className="flex flex-col gap-4">
      {eyebrow && (
        <p className="text-[15px] font-semibold tracking-widest uppercase" style={{ color: '#007AFF' }}>
          {eyebrow}
        </p>
      )}
      <h2 className="text-[clamp(2.5rem,7vw,5rem)] font-semibold tracking-[-0.04em] leading-[1.05] text-white">
        {title}
      </h2>
      {subtitle && (
        <p className="text-[clamp(1rem,2vw,1.25rem)] text-white/50 leading-relaxed max-w-[54ch]">
          {subtitle}
        </p>
      )}
    </div>
  )
}
```

---

## 7. Safe Area System (Critical for Mobile)

```css
/* Always use in app shells */
.app-container {
  padding-top: env(safe-area-inset-top);
  padding-bottom: env(safe-area-inset-bottom);
  padding-left: env(safe-area-inset-left);
  padding-right: env(safe-area-inset-right);
}

/* iOS status bar overlay */
.status-bar-overlay {
  height: calc(44px + env(safe-area-inset-top));
  padding-top: env(safe-area-inset-top);
}

/* Home indicator zone */
.bottom-bar {
  padding-bottom: max(16px, env(safe-area-inset-bottom));
}
```
