# Lynx Combinator — Electric Scroll Redesign
**Date:** 2026-04-09  
**Status:** Approved  

---

## Overview
Redesign `index.html` from a minimal dark developer portfolio into a high-energy, mobile-first landing page for Lynx Combinator — SoCal's #1 youth AI bootcamp. Inspired by vibecodingacademy.ai but darker, more electric, and more premium. Primary users are on mobile.

---

## Visual Foundation
- **Background:** `#050508` (near-black with blue tint)
- **Accent 1:** `#3b82f6` (electric blue)
- **Accent 2:** `#06b6d4` (cyan)
- **Glow:** Both accents used as `box-shadow` / `text-shadow` on key elements
- **Gradient:** `linear-gradient(135deg, #3b82f6, #06b6d4)` for CTAs, borders, highlights
- **Fonts:** `Space Grotesk` (headings) + `Inter` (body) via Google Fonts
- **Section dividers:** Diagonal `clip-path` cuts between sections

---

## Navigation

### Mobile (fixed bottom app bar)
- 4 icons: Home · Program · Proof · Apply
- Active icon: cyan glow + gradient underline dot
- Frosted glass background (`backdrop-filter: blur`)
- 60px tall + safe area inset for iPhone home bar

### Desktop (sticky top nav)
- Left: "Lynx Combinator" wordmark, "Lynx" in cyan gradient
- Right: Home · Program · Proof · About · Apply (Apply = glowing CTA button)
- Frosted glass on scroll, transparent at top

---

## Sections

### 1. Hero
- Small cyan label above headline: `SOCAL'S #1 YOUTH AI BOOTCAMP` (letter-spaced uppercase)
- Massive headline: "I turn youth leaders into AI builders." (~52px mobile)
- Two animated gradient orbs (blue + cyan) floating in background via CSS keyframes
- CTA button: full-width on mobile, gradient border + glow — "See What Students Build →"
- Social proof micro-bar under CTA: `✦ 8 spots · Spring 2026 · Irvine, CA`
- Animated bouncing scroll chevron at bottom, fades on scroll

### 2. What Students Build
- Section label: `WHAT YOU'LL SHIP`
- Headline: "3 real AI products. 6 weeks. Zero fluff."
- Cards: full-width stacked on mobile, 3-column grid on desktop
- Card: dark glass (`rgba(255,255,255,0.04)`) + cyan/blue gradient border that glows on tap/hover
- Each card: video demo (autoplay muted) + bold project name + one-liner + week tag (`WEEK 1–2` etc.)
- Tap video → opens redesigned lightbox (full dark overlay, swipe-to-dismiss on mobile)

### 3. Social Proof Wall
- Section label: `WHAT PEOPLE ARE SAYING`
- Headline: "Real parents. Real students. Real results."
- Featured hero quote (full-width card, gradient left border, large font): KV parent quote
- Horizontal snap carousel on mobile, 2-column masonry on desktop
- Carousel progress bar (thin cyan line below cards)
- Placeholder cards labeled clearly for future testimonials

**KV Quote:**
> "Tech and AI are moving fast, but helping kids build discernment, judgment, and confidence takes time, repetition, and trust. The program and your personal brand are tied together right now. Projects that show real-world application, consistency, and follow-through."
> — KV, SoCal Parent

### 4. About Kyle + Why AI Matters (merged)
- Kyle's headshot: right side on desktop (cyan glow halo), full-width cinematic crop on mobile
- Story: existing raw voice, key phrases highlighted in cyan gradient text
- 3 stat pills: `6 Weeks` · `3 Real Products` · `Lifetime Community`
- Why AI bullets converted to 3 icon cards: ✓ Technical initiative · ✓ Problem-solving · ✓ Future readiness

### 5. Contact / Apply
- Headline: "Ready to build?"
- Subhead: "Spring 2026 · 8 spots · Beta pricing for early applicants"
- Primary CTA: full-width glowing gradient button → `mailto:kyle7tran@gmail.com`
- Secondary links: LinkedIn · Twitter · Email as glowing pill tags
- Urgency marquee ticker above footer: `✦ 8 SPOTS REMAINING · APPLY BY MARCH 31 · IRVINE, CA · ✦`

### Footer
- `© 2026 Kyle Tran · Lynx Combinator` centered, muted
- Padded above mobile bottom nav bar

---

## Mobile-First Constraints
- All tap targets minimum 44px
- Bottom nav always visible, content never hidden behind it
- Horizontal carousel uses `scroll-snap-type: x mandatory`
- Videos: autoplay muted, pause when off-screen via IntersectionObserver
- Lightbox: swipe-down gesture to dismiss
- Safe area insets respected throughout (`env(safe-area-inset-*)`)

---

## What's Removed
- Customer Discovery Insights section (charts/Google Sheets data) — replaced by Social Proof Wall
- "Why AI Skills Matter" as a standalone section — merged into About Kyle
