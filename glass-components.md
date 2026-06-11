# Glass Components Reference

## Table of Contents
1. [Glass Navigation Bar](#glass-nav)
2. [Glass Card System](#glass-cards)
3. [Glass Inputs](#glass-inputs)
4. [Glass Modal / Sheet](#glass-modal)
5. [Glass Toast](#glass-toast)
6. [iOS Segmented Control](#segmented-control)
7. [Glass Button Variants](#glass-buttons)
8. [Glass Sidebar / Drawer](#glass-sidebar)
9. [Glass Stat Cards](#glass-stats)
10. [Glass Image Cards (Car inspection style)](#glass-media)

---

## 1. Glass Navigation Bar {#glass-nav}

```tsx
// app/components/GlassNav.tsx
'use client'
import { motion, useScroll, useTransform } from 'framer-motion'

export function GlassNav() {
  const { scrollY } = useScroll()
  // Intensify glass on scroll
  const blur = useTransform(scrollY, [0, 80], [0, 40])
  const bgOpacity = useTransform(scrollY, [0, 80], [0, 0.8])
  const borderOpacity = useTransform(scrollY, [0, 80], [0, 0.12])

  return (
    <motion.nav
      className="fixed top-0 inset-x-0 z-50 flex items-center justify-between px-6"
      style={{
        paddingTop: 'max(16px, env(safe-area-inset-top))',
        height: 'calc(60px + env(safe-area-inset-top))',
        backdropFilter: useTransform(blur, v => `blur(${v}px) saturate(180%)`),
        WebkitBackdropFilter: useTransform(blur, v => `blur(${v}px) saturate(180%)`),
        background: useTransform(bgOpacity, v => `rgba(0, 0, 0, ${v})`),
        borderBottom: `1px solid`,
        borderColor: useTransform(borderOpacity, v => `rgba(255, 255, 255, ${v})`),
      }}
    >
      {/* Logo */}
      <span className="text-white font-semibold tracking-tight text-base">Brand</span>

      {/* Nav Links */}
      <div className="flex items-center gap-8">
        {['Product', 'Pricing', 'About'].map(link => (
          <a key={link} href="#" className="text-[15px] text-white/60 hover:text-white transition-colors">
            {link}
          </a>
        ))}
      </div>

      {/* CTA */}
      <button className="px-4 py-2 text-sm font-medium text-white rounded-full
        bg-white/10 border border-white/15 hover:bg-white/15 transition-colors
        backdrop-blur-sm" style={{ boxShadow: 'inset 0 1px 0 rgba(255,255,255,0.2)' }}>
        Get Started
      </button>
    </motion.nav>
  )
}
```

---

## 2. Glass Card System {#glass-cards}

```tsx
// Four card tiers

// Base Glass Card
export function GlassCard({ children, className = '' }) {
  return (
    <div
      className={`relative overflow-hidden rounded-[20px] p-6 ${className}`}
      style={{
        backdropFilter: 'blur(20px) saturate(180%)',
        WebkitBackdropFilter: 'blur(20px) saturate(180%)',
        background: 'rgba(255, 255, 255, 0.08)',
        border: '1px solid rgba(255, 255, 255, 0.15)',
        boxShadow: `
          inset 0 1px 0 rgba(255, 255, 255, 0.25),
          inset 0 -1px 0 rgba(0, 0, 0, 0.1),
          0 8px 32px rgba(0, 0, 0, 0.15),
          0 2px 8px rgba(0, 0, 0, 0.1)
        `,
      }}
    >
      {/* Inner specular highlight */}
      <div className="absolute inset-0 pointer-events-none"
        style={{ background: 'linear-gradient(135deg, rgba(255,255,255,0.12) 0%, transparent 50%)' }} />
      <div className="relative z-10">{children}</div>
    </div>
  )
}

// Elevated Glass Card (deeper, more opaque)
export function GlassCardElevated({ children, className = '' }) {
  return (
    <div
      className={`relative overflow-hidden rounded-[24px] p-8 ${className}`}
      style={{
        backdropFilter: 'blur(40px) saturate(200%) brightness(110%)',
        WebkitBackdropFilter: 'blur(40px) saturate(200%) brightness(110%)',
        background: 'rgba(255, 255, 255, 0.12)',
        border: '1px solid rgba(255, 255, 255, 0.22)',
        boxShadow: `
          inset 0 2px 0 rgba(255, 255, 255, 0.35),
          inset 0 -1px 0 rgba(0, 0, 0, 0.15),
          0 24px 48px rgba(0, 0, 0, 0.2),
          0 4px 16px rgba(0, 0, 0, 0.12)
        `,
      }}
    >
      <div className="absolute inset-0 pointer-events-none"
        style={{ background: 'linear-gradient(135deg, rgba(255,255,255,0.15) 0%, transparent 45%)' }} />
      <div className="relative z-10">{children}</div>
    </div>
  )
}

// Accent Glass Card (colored tint)
export function GlassCardAccent({ children, color = '0, 122, 255', className = '' }) {
  return (
    <div
      className={`relative overflow-hidden rounded-[20px] p-6 ${className}`}
      style={{
        backdropFilter: 'blur(24px) saturate(200%)',
        WebkitBackdropFilter: 'blur(24px) saturate(200%)',
        background: `rgba(${color}, 0.10)`,
        border: `1px solid rgba(${color}, 0.30)`,
        boxShadow: `
          inset 0 1px 0 rgba(${color}, 0.40),
          0 8px 32px rgba(${color}, 0.20)
        `,
      }}
    >
      <div className="relative z-10">{children}</div>
    </div>
  )
}

// Dark Glass Card
export function GlassCardDark({ children, className = '' }) {
  return (
    <div
      className={`relative overflow-hidden rounded-[20px] p-6 ${className}`}
      style={{
        backdropFilter: 'blur(32px) saturate(180%) brightness(0.9)',
        WebkitBackdropFilter: 'blur(32px) saturate(180%) brightness(0.9)',
        background: 'rgba(12, 12, 20, 0.70)',
        border: '1px solid rgba(255, 255, 255, 0.06)',
        boxShadow: `
          inset 0 1px 0 rgba(255, 255, 255, 0.08),
          inset 0 -1px 0 rgba(0, 0, 0, 0.4),
          0 20px 40px rgba(0, 0, 0, 0.5)
        `,
      }}
    >
      <div className="relative z-10">{children}</div>
    </div>
  )
}
```

---

## 3. Glass Inputs {#glass-inputs}

```tsx
'use client'
import { useState } from 'react'

export function GlassInput({ label, placeholder, type = 'text' }) {
  const [focused, setFocused] = useState(false)
  const [value, setValue] = useState('')

  return (
    <div className="flex flex-col gap-1.5">
      <label className="text-[13px] font-medium text-white/50 uppercase tracking-wider">
        {label}
      </label>
      <div className="relative">
        <input
          type={type}
          value={value}
          placeholder={placeholder}
          onFocus={() => setFocused(true)}
          onBlur={() => setFocused(false)}
          onChange={e => setValue(e.target.value)}
          className="w-full px-4 py-3 text-[15px] text-white placeholder-white/25 rounded-[12px] outline-none transition-all duration-200"
          style={{
            backdropFilter: 'blur(16px) saturate(150%)',
            WebkitBackdropFilter: 'blur(16px) saturate(150%)',
            background: focused ? 'rgba(255,255,255,0.08)' : 'rgba(255,255,255,0.04)',
            border: `1px solid ${focused ? 'rgba(0, 122, 255, 0.6)' : 'rgba(255, 255, 255, 0.10)'}`,
            boxShadow: focused
              ? '0 0 0 3px rgba(0, 122, 255, 0.20), inset 0 1px 0 rgba(255,255,255,0.10)'
              : 'inset 0 1px 0 rgba(255,255,255,0.05)',
          }}
        />
      </div>
    </div>
  )
}

// Search Input with icon
export function GlassSearch({ placeholder = 'Search...' }) {
  return (
    <div className="relative flex items-center">
      {/* Search icon */}
      <svg className="absolute left-3.5 w-4 h-4 text-white/30" fill="none" stroke="currentColor" viewBox="0 0 24 24">
        <circle cx="11" cy="11" r="8"/><path d="m21 21-4.35-4.35"/>
      </svg>
      <input
        placeholder={placeholder}
        className="w-full pl-10 pr-4 py-2.5 text-[15px] text-white placeholder-white/25 rounded-full outline-none"
        style={{
          backdropFilter: 'blur(20px) saturate(180%)',
          background: 'rgba(255, 255, 255, 0.08)',
          border: '1px solid rgba(255, 255, 255, 0.12)',
          boxShadow: 'inset 0 1px 0 rgba(255,255,255,0.10)',
        }}
      />
    </div>
  )
}
```

---

## 4. Glass Modal / Sheet {#glass-modal}

```tsx
'use client'
import { motion, AnimatePresence } from 'framer-motion'

export function GlassModal({ isOpen, onClose, children, title }) {
  return (
    <AnimatePresence>
      {isOpen && (
        <>
          {/* Backdrop */}
          <motion.div
            className="fixed inset-0 z-50"
            style={{ backdropFilter: 'blur(4px)', background: 'rgba(0,0,0,0.4)' }}
            initial={{ opacity: 0 }}
            animate={{ opacity: 1 }}
            exit={{ opacity: 0 }}
            onClick={onClose}
          />

          {/* Modal */}
          <motion.div
            className="fixed inset-x-4 top-1/2 -translate-y-1/2 z-50 rounded-[28px] p-8 max-w-lg mx-auto"
            style={{
              backdropFilter: 'blur(60px) saturate(200%) brightness(110%)',
              WebkitBackdropFilter: 'blur(60px) saturate(200%) brightness(110%)',
              background: 'rgba(20, 20, 28, 0.85)',
              border: '1px solid rgba(255, 255, 255, 0.12)',
              boxShadow: `
                inset 0 1px 0 rgba(255,255,255,0.15),
                0 40px 80px rgba(0,0,0,0.5),
                0 0 0 0.5px rgba(0,0,0,0.2)
              `,
            }}
            initial={{ opacity: 0, scale: 0.92, y: '-48%' }}
            animate={{ opacity: 1, scale: 1, y: '-50%', transition: { type: 'spring', stiffness: 300, damping: 30 } }}
            exit={{ opacity: 0, scale: 0.95, y: '-48%', transition: { duration: 0.15 } }}
          >
            <div className="absolute inset-0 rounded-[28px] pointer-events-none overflow-hidden">
              <div style={{ background: 'linear-gradient(135deg, rgba(255,255,255,0.08) 0%, transparent 50%)' }} className="absolute inset-0" />
            </div>
            <div className="relative z-10">
              <div className="flex items-center justify-between mb-6">
                <h2 className="text-xl font-semibold text-white tracking-tight">{title}</h2>
                <button onClick={onClose} className="w-8 h-8 rounded-full flex items-center justify-center text-white/40 hover:text-white hover:bg-white/10 transition-all">
                  <svg className="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path d="M18 6 6 18M6 6l12 12"/></svg>
                </button>
              </div>
              {children}
            </div>
          </motion.div>
        </>
      )}
    </AnimatePresence>
  )
}

// iOS Bottom Sheet
export function IOSBottomSheet({ isOpen, onClose, children, title }) {
  return (
    <AnimatePresence>
      {isOpen && (
        <>
          <motion.div className="fixed inset-0 z-40" style={{ background: 'rgba(0,0,0,0.4)' }}
            initial={{ opacity: 0 }} animate={{ opacity: 1 }} exit={{ opacity: 0 }} onClick={onClose} />

          <motion.div
            className="fixed bottom-0 inset-x-0 z-50 rounded-t-[28px] overflow-hidden"
            style={{
              backdropFilter: 'blur(40px) saturate(200%)',
              background: 'rgba(20, 20, 28, 0.92)',
              border: '1px solid rgba(255, 255, 255, 0.10)',
              borderBottom: 'none',
              paddingBottom: 'env(safe-area-inset-bottom)',
              boxShadow: 'inset 0 1px 0 rgba(255,255,255,0.12), 0 -20px 40px rgba(0,0,0,0.3)',
            }}
            initial={{ y: '100%' }}
            animate={{ y: 0, transition: { type: 'spring', stiffness: 300, damping: 35 } }}
            exit={{ y: '100%', transition: { duration: 0.25 } }}
          >
            {/* Drag Handle */}
            <div className="flex justify-center pt-3 pb-2">
              <div className="w-9 h-1 rounded-full bg-white/20" />
            </div>
            {title && <h3 className="text-center text-[17px] font-semibold text-white pb-3 border-b border-white/08">{title}</h3>}
            <div className="p-6">{children}</div>
          </motion.div>
        </>
      )}
    </AnimatePresence>
  )
}
```

---

## 5. Glass Toast {#glass-toast}

```tsx
'use client'
import { motion, AnimatePresence } from 'framer-motion'
import { useEffect } from 'react'

export function GlassToast({ message, type = 'info', visible, onDismiss }) {
  useEffect(() => {
    if (visible) {
      const t = setTimeout(onDismiss, 3000)
      return () => clearTimeout(t)
    }
  }, [visible, onDismiss])

  const icons = {
    success: <div className="w-5 h-5 rounded-full bg-[#34C759] flex items-center justify-center"><svg className="w-3 h-3 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path strokeLinecap="round" d="M5 13l4 4L19 7"/></svg></div>,
    error: <div className="w-5 h-5 rounded-full bg-[#FF3B30] flex items-center justify-center"><svg className="w-3 h-3 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path strokeLinecap="round" d="M18 6 6 18M6 6l12 12"/></svg></div>,
    info: <div className="w-5 h-5 rounded-full bg-[#007AFF] flex items-center justify-center"><svg className="w-3 h-3 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24"><circle cx="12" cy="12" r="10"/><path d="M12 8v4m0 4h.01"/></svg></div>,
  }

  return (
    <AnimatePresence>
      {visible && (
        <motion.div
          className="fixed bottom-6 inset-x-0 z-[100] flex justify-center"
          style={{ paddingBottom: 'env(safe-area-inset-bottom)' }}
          initial={{ opacity: 0, y: 16, scale: 0.9, filter: 'blur(4px)' }}
          animate={{ opacity: 1, y: 0, scale: 1, filter: 'blur(0px)', transition: { type: 'spring', stiffness: 400, damping: 28 } }}
          exit={{ opacity: 0, y: 8, scale: 0.95, transition: { duration: 0.15 } }}
        >
          <div
            className="flex items-center gap-3 px-5 py-3.5 rounded-full"
            style={{
              backdropFilter: 'blur(32px) saturate(200%)',
              background: 'rgba(28, 28, 30, 0.88)',
              border: '1px solid rgba(255,255,255,0.08)',
              boxShadow: 'inset 0 1px 0 rgba(255,255,255,0.10), 0 16px 32px rgba(0,0,0,0.4)',
            }}
          >
            {icons[type]}
            <span className="text-[15px] font-medium text-white">{message}</span>
          </div>
        </motion.div>
      )}
    </AnimatePresence>
  )
}
```

---

## 6. iOS Segmented Control {#segmented-control}

```tsx
'use client'
import { useState } from 'react'
import { motion } from 'framer-motion'

export function GlassSegmentedControl({ options, defaultIndex = 0, onChange }) {
  const [selected, setSelected] = useState(defaultIndex)

  return (
    <div
      className="relative flex p-1 rounded-[12px]"
      style={{
        backdropFilter: 'blur(20px) saturate(160%)',
        background: 'rgba(255, 255, 255, 0.06)',
        border: '1px solid rgba(255, 255, 255, 0.08)',
      }}
    >
      {/* Sliding indicator */}
      <motion.div
        className="absolute top-1 bottom-1 rounded-[9px]"
        style={{
          width: `calc(${100 / options.length}% - 4px)`,
          left: `calc(${(selected / options.length) * 100}% + 4px)`,
          backdropFilter: 'blur(12px)',
          background: 'rgba(255, 255, 255, 0.15)',
          border: '1px solid rgba(255,255,255,0.18)',
          boxShadow: 'inset 0 1px 0 rgba(255,255,255,0.25), 0 2px 8px rgba(0,0,0,0.15)',
        }}
        layout
        transition={{ type: 'spring', stiffness: 400, damping: 35 }}
      />

      {options.map((option, i) => (
        <button
          key={option}
          className="relative z-10 flex-1 py-1.5 text-[13px] font-medium transition-colors duration-150"
          style={{ color: selected === i ? 'rgba(255,255,255,0.95)' : 'rgba(255,255,255,0.4)' }}
          onClick={() => { setSelected(i); onChange?.(i, option) }}
        >
          {option}
        </button>
      ))}
    </div>
  )
}
```

---

## 7. Glass Button Variants {#glass-buttons}

```tsx
// Primary Glass Button
export function GlassButton({ children, onClick, variant = 'default', size = 'md' }) {
  const variants = {
    default: {
      background: 'rgba(255, 255, 255, 0.10)',
      border: '1px solid rgba(255, 255, 255, 0.18)',
      shadow: 'inset 0 1px 0 rgba(255,255,255,0.25), 0 4px 12px rgba(0,0,0,0.15)',
      color: 'white',
    },
    primary: {
      background: 'rgba(0, 122, 255, 0.85)',
      border: '1px solid rgba(0, 122, 255, 0.9)',
      shadow: 'inset 0 1px 0 rgba(255,255,255,0.3), 0 4px 16px rgba(0,122,255,0.4)',
      color: 'white',
    },
    ghost: {
      background: 'transparent',
      border: '1px solid rgba(255, 255, 255, 0.12)',
      shadow: 'none',
      color: 'rgba(255,255,255,0.7)',
    },
  }

  const sizes = {
    sm: 'px-3 py-1.5 text-[13px] rounded-[9px]',
    md: 'px-5 py-2.5 text-[15px] rounded-[12px]',
    lg: 'px-7 py-3.5 text-[17px] rounded-[14px]',
    pill: 'px-5 py-2.5 text-[15px] rounded-full',
  }

  const v = variants[variant]

  return (
    <motion.button
      onClick={onClick}
      className={`relative font-medium transition-colors overflow-hidden ${sizes[size]}`}
      style={{
        background: v.background,
        border: v.border,
        boxShadow: v.shadow,
        color: v.color,
        backdropFilter: variant === 'default' ? 'blur(12px)' : undefined,
      }}
      whileTap={{ scale: 0.97 }}
      whileHover={{ scale: 1.02 }}
      transition={{ type: 'spring', stiffness: 400, damping: 25 }}
    >
      {/* Specular on hover */}
      <motion.div
        className="absolute inset-0 pointer-events-none"
        style={{ background: 'linear-gradient(135deg, rgba(255,255,255,0.15) 0%, transparent 60%)' }}
        initial={{ opacity: 0 }}
        whileHover={{ opacity: 1 }}
        transition={{ duration: 0.2 }}
      />
      <span className="relative z-10">{children}</span>
    </motion.button>
  )
}
```

---

## 8. Glass Stat Cards (like the car inspection app) {#glass-stats}

```tsx
export function GlassStatCard({ label, value, unit, change, accentColor = '0, 122, 255' }) {
  const isPositive = change >= 0

  return (
    <GlassCard className="flex flex-col gap-3">
      <p className="text-[13px] font-medium text-white/40 uppercase tracking-wider">{label}</p>
      <div className="flex items-end gap-1.5">
        <span className="text-[36px] font-semibold text-white tracking-tight leading-none">{value}</span>
        {unit && <span className="text-[15px] text-white/40 pb-1">{unit}</span>}
      </div>
      {change !== undefined && (
        <div className="flex items-center gap-1.5">
          <div
            className="flex items-center gap-1 px-2 py-0.5 rounded-full text-[12px] font-medium"
            style={{
              background: isPositive ? 'rgba(52, 199, 89, 0.15)' : 'rgba(255, 59, 48, 0.15)',
              color: isPositive ? '#34C759' : '#FF3B30',
            }}
          >
            <svg className="w-3 h-3" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path strokeLinecap="round" d={isPositive ? 'M5 15l7-7 7 7' : 'M19 9l-7 7-7-7'} />
            </svg>
            {Math.abs(change)}%
          </div>
          <span className="text-[12px] text-white/25">vs last period</span>
        </div>
      )}
      {/* Progress bar */}
      <div className="h-1 rounded-full overflow-hidden" style={{ background: 'rgba(255,255,255,0.06)' }}>
        <motion.div
          className="h-full rounded-full"
          style={{ background: `rgba(${accentColor}, 0.8)` }}
          initial={{ width: 0 }}
          animate={{ width: `${Math.min(100, Math.abs(Number(value)))}%` }}
          transition={{ type: 'spring', stiffness: 100, damping: 20, delay: 0.2 }}
        />
      </div>
    </GlassCard>
  )
}
```

---

## 9. Glass Media / Product Card (like Colbo product page) {#glass-media}

```tsx
export function GlassProductCard({ name, price, description, imageSrc }) {
  return (
    <motion.div
      className="group relative overflow-hidden rounded-[28px] aspect-[4/5]"
      whileHover={{ scale: 1.02 }}
      transition={{ type: 'spring', stiffness: 300, damping: 25 }}
    >
      {/* Background image */}
      <img src={imageSrc} alt={name} className="absolute inset-0 w-full h-full object-cover transition-transform duration-700 group-hover:scale-105" />

      {/* Dark vignette */}
      <div className="absolute inset-0" style={{ background: 'linear-gradient(to top, rgba(0,0,0,0.9) 0%, rgba(0,0,0,0.2) 50%, transparent 100%)' }} />

      {/* Content glass panel — bottom */}
      <div
        className="absolute bottom-4 inset-x-4 p-5 rounded-[20px]"
        style={{
          backdropFilter: 'blur(32px) saturate(180%)',
          background: 'rgba(10, 10, 15, 0.75)',
          border: '1px solid rgba(255,255,255,0.08)',
          boxShadow: 'inset 0 1px 0 rgba(255,255,255,0.10)',
        }}
      >
        <div className="flex items-start justify-between gap-3">
          <div>
            <p className="text-[11px] font-medium text-white/40 uppercase tracking-widest mb-1">{description}</p>
            <h3 className="text-[18px] font-semibold text-white tracking-tight">{name}</h3>
          </div>
          <div className="text-right">
            <p className="text-[11px] text-white/30">From</p>
            <p className="text-[18px] font-semibold text-white">{price}</p>
          </div>
        </div>

        {/* CTA */}
        <motion.button
          className="mt-4 w-full py-2.5 rounded-[12px] text-[15px] font-medium text-white"
          style={{
            background: 'rgba(255,255,255,0.12)',
            border: '1px solid rgba(255,255,255,0.15)',
            boxShadow: 'inset 0 1px 0 rgba(255,255,255,0.2)',
          }}
          whileTap={{ scale: 0.98 }}
        >
          Add to Cart
        </motion.button>
      </div>
    </motion.div>
  )
}
```
