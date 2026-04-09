# Lynx Combinator Electric Scroll Redesign — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Redesign `index.html` into a dark electric mobile-first landing page with bottom app nav, animated hero, glowing project cards, snap-scroll social proof carousel, merged About/Why section, and urgency marquee ticker.

**Architecture:** Single `index.html` with embedded CSS and JS. Full replacement of styles, HTML structure, and scripts. Chart.js and Google Sheets code removed. Space Grotesk + Inter added via Google Fonts.

**Tech Stack:** HTML5, CSS3 (`clip-path`, `backdrop-filter`, `scroll-snap`, CSS keyframes), vanilla JS, Space Grotesk + Inter (Google Fonts)

---

### Task 1: Global CSS Foundation + Fonts

**Files:**
- Modify: `index.html` — `<head>`, `:root`, body, shared utility classes

- [ ] **Step 1: Replace `<head>` and opening CSS block**

Replace the existing `<head>` through the first `body { ... }` block with:

```html
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <meta name="description" content="Kyle Tran - Founder of Lynx Combinator, SoCal's #1 youth AI bootcamp." />
  <title>Kyle Tran | Lynx Combinator</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;500;600;700&family=Inter:wght@400;500;600&display=swap" rel="stylesheet">
  <style>
    :root {
      --bg: #050508;
      --card: rgba(255,255,255,0.04);
      --card-border: rgba(59,130,246,0.2);
      --text: #ffffff;
      --muted: #94a3b8;
      --accent: #3b82f6;
      --cyan: #06b6d4;
      --gradient: linear-gradient(135deg, #3b82f6, #06b6d4);
      --glow-sm: 0 0 16px rgba(59,130,246,0.35);
      --glow-md: 0 0 32px rgba(59,130,246,0.45);
      --max: 1120px;
      --bottom-nav-h: 60px;
    }
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    html { scroll-behavior: smooth; }
    body {
      font-family: 'Inter', -apple-system, sans-serif;
      background: var(--bg);
      color: var(--text);
      line-height: 1.6;
      overflow-x: hidden;
    }
    .container { width: min(92%, var(--max)); margin: 0 auto; }
    h1, h2, h3, h4 { font-family: 'Space Grotesk', sans-serif; letter-spacing: -0.02em; }
    section {
      padding: 96px 0;
      opacity: 0;
      transform: translateY(24px);
      transition: opacity 600ms ease, transform 600ms ease;
    }
    section.visible { opacity: 1; transform: translateY(0); }
    .label {
      display: inline-block;
      font-size: 0.7rem;
      font-weight: 700;
      letter-spacing: 0.2em;
      text-transform: uppercase;
      color: var(--cyan);
      margin-bottom: 14px;
    }
    .gradient-text {
      background: var(--gradient);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
    }
    .section-title {
      font-size: clamp(1.9rem, 4vw, 2.8rem);
      line-height: 1.1;
      margin-bottom: 14px;
    }
    .section-intro {
      color: var(--muted);
      font-size: 1.05rem;
      max-width: 640px;
      margin-bottom: 40px;
    }
    .btn {
      display: inline-flex;
      align-items: center;
      gap: 8px;
      background: var(--gradient);
      color: #fff;
      text-decoration: none;
      padding: 14px 28px;
      border-radius: 12px;
      font-family: 'Space Grotesk', sans-serif;
      font-weight: 700;
      font-size: 1rem;
      transition: transform 200ms ease, box-shadow 200ms ease;
      box-shadow: var(--glow-sm);
      border: none;
      cursor: pointer;
    }
    .btn:hover, .btn:focus { transform: translateY(-2px); box-shadow: var(--glow-md); }
    .btn-full { width: 100%; justify-content: center; }
    body.no-scroll { overflow: hidden; }
  </style>
```

- [ ] **Step 2: Verify in browser**

Open `index.html` in Chrome. Background should be near-black `#050508`, headings Space Grotesk, body Inter. All existing sections visible (they'll be unstyled — that's fine).

- [ ] **Step 3: Commit**
```bash
cd "/Users/kyletran/Desktop/Projects I Built/ls-portfolio-page"
git add index.html
git commit -m "feat: global CSS foundation — electric palette + Space Grotesk/Inter fonts"
```

---

### Task 2: Desktop Sticky Nav + Mobile Bottom App Bar

**Files:**
- Modify: `index.html` — add `<nav class="top-nav">` after `<body>`, add `<nav class="bottom-nav">` before `</body>`, add CSS for both navs

- [ ] **Step 1: Add top nav HTML after `<body>` opening tag**

```html
<nav class="top-nav" id="top-nav">
  <div class="container top-nav-inner">
    <a href="#top" class="top-nav-logo">
      <span class="gradient-text">Lynx</span> Combinator
    </a>
    <div class="top-nav-links">
      <a href="#top" class="top-nav-link">Home</a>
      <a href="#projects" class="top-nav-link">Program</a>
      <a href="#proof" class="top-nav-link">Proof</a>
      <a href="#about-kyle" class="top-nav-link">About</a>
      <a href="#contact" class="btn" style="padding:10px 20px;font-size:0.9rem;">Apply Now →</a>
    </div>
  </div>
</nav>
```

- [ ] **Step 2: Add bottom nav HTML before `</body>`**

```html
<nav class="bottom-nav" aria-label="Site navigation">
  <a href="#top" class="bnav-item active" data-target="top">
    <svg width="22" height="22" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M3 9l9-7 9 7v11a2 2 0 01-2 2H5a2 2 0 01-2-2z"/><polyline points="9 22 9 12 15 12 15 22"/></svg>
    <span>Home</span>
  </a>
  <a href="#projects" class="bnav-item" data-target="projects">
    <svg width="22" height="22" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><rect x="2" y="3" width="20" height="14" rx="2"/><path d="M8 21h8M12 17v4"/></svg>
    <span>Program</span>
  </a>
  <a href="#proof" class="bnav-item" data-target="proof">
    <svg width="22" height="22" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M12 2l3.09 6.26L22 9.27l-5 4.87 1.18 6.88L12 17.77l-6.18 3.25L7 14.14 2 9.27l6.91-1.01z"/></svg>
    <span>Proof</span>
  </a>
  <a href="#contact" class="bnav-item" data-target="contact">
    <svg width="22" height="22" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M22 16.92v3a2 2 0 01-2.18 2 19.79 19.79 0 01-8.63-3.07 19.5 19.5 0 01-6-6 19.79 19.79 0 01-3.07-8.67A2 2 0 014.11 2h3a2 2 0 012 1.72 12.84 12.84 0 00.7 2.81 2 2 0 01-.45 2.11L8.09 9.91a16 16 0 006 6l1.27-1.27a2 2 0 012.11-.45 12.84 12.84 0 002.81.7A2 2 0 0122 16.92z"/></svg>
    <span>Apply</span>
  </a>
</nav>
```

- [ ] **Step 3: Add nav CSS (inside the `<style>` tag)**

```css
/* ── TOP NAV ── */
.top-nav {
  position: fixed;
  top: 0; left: 0; right: 0;
  z-index: 100;
  transition: background 300ms ease, backdrop-filter 300ms ease;
  padding: 0 0;
}
.top-nav.scrolled {
  background: rgba(5,5,8,0.85);
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  border-bottom: 1px solid rgba(255,255,255,0.06);
}
.top-nav-inner {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 64px;
}
.top-nav-logo {
  font-family: 'Space Grotesk', sans-serif;
  font-weight: 700;
  font-size: 1.15rem;
  color: #fff;
  text-decoration: none;
}
.top-nav-links {
  display: flex;
  align-items: center;
  gap: 28px;
}
.top-nav-link {
  color: var(--muted);
  text-decoration: none;
  font-size: 0.9rem;
  font-weight: 500;
  transition: color 200ms;
}
.top-nav-link:hover { color: #fff; }

/* ── BOTTOM NAV (mobile only) ── */
.bottom-nav {
  display: none;
  position: fixed;
  bottom: 0; left: 0; right: 0;
  z-index: 100;
  height: calc(var(--bottom-nav-h) + env(safe-area-inset-bottom, 0px));
  padding-bottom: env(safe-area-inset-bottom, 0px);
  background: rgba(5,5,8,0.9);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  border-top: 1px solid rgba(255,255,255,0.07);
  align-items: stretch;
  justify-content: space-around;
}
.bnav-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 3px;
  flex: 1;
  color: var(--muted);
  text-decoration: none;
  font-size: 0.65rem;
  font-weight: 600;
  letter-spacing: 0.05em;
  text-transform: uppercase;
  transition: color 200ms;
  position: relative;
}
.bnav-item.active { color: var(--cyan); }
.bnav-item.active svg { filter: drop-shadow(0 0 6px rgba(6,182,212,0.7)); }
.bnav-item::after {
  content: '';
  position: absolute;
  bottom: 6px;
  width: 18px;
  height: 2px;
  border-radius: 1px;
  background: var(--gradient);
  opacity: 0;
  transition: opacity 200ms;
}
.bnav-item.active::after { opacity: 1; }

/* Ensure content clears both navs */
body { padding-top: 64px; }

@media (max-width: 768px) {
  .bottom-nav { display: flex; }
  .top-nav-links { display: none; }
  body { padding-bottom: calc(var(--bottom-nav-h) + env(safe-area-inset-bottom, 0px)); }
}
```

- [ ] **Step 4: Add nav JS (inside the `<script>` tag at bottom)**

```javascript
// Top nav: add .scrolled class on scroll
window.addEventListener('scroll', () => {
  document.getElementById('top-nav').classList.toggle('scrolled', window.scrollY > 40);
}, { passive: true });

// Bottom nav: highlight active section
const navSections = ['top', 'projects', 'proof', 'about-kyle', 'contact'];
const bnavItems = document.querySelectorAll('.bnav-item');
const updateBnav = () => {
  let current = 'top';
  navSections.forEach(id => {
    const el = document.getElementById(id);
    if (el && window.scrollY >= el.offsetTop - 160) current = id;
  });
  bnavItems.forEach(item => {
    item.classList.toggle('active', item.dataset.target === current);
  });
};
window.addEventListener('scroll', updateBnav, { passive: true });
updateBnav();
```

- [ ] **Step 5: Verify in browser**

Resize to 375px (iPhone). Bottom nav should appear with 4 icons. On desktop (> 768px), top nav with links should appear. Scroll down — top nav gets frosted glass. Active bottom nav icon glows cyan.

- [ ] **Step 6: Commit**
```bash
git add index.html
git commit -m "feat: sticky top nav + mobile bottom app bar with active state"
```

---

### Task 3: Hero Section Redesign

**Files:**
- Modify: `index.html` — `<header class="hero">` HTML + CSS

- [ ] **Step 1: Replace hero HTML**

Replace the existing `<header class="hero" id="top">` block with:

```html
<header class="hero" id="top">
  <div class="orb orb-1"></div>
  <div class="orb orb-2"></div>
  <div class="container hero-inner">
    <span class="label">SoCal's #1 Youth AI Bootcamp</span>
    <h1 class="hero-title">I turn youth leaders<br>into <span class="gradient-text">AI builders.</span></h1>
    <p class="hero-sub">6 weeks. 3 real AI products. Portfolio pieces that open doors.</p>
    <a class="btn btn-full-mobile" href="#projects">See What Students Build →</a>
    <div class="hero-microbar">
      <span class="microbar-dot"></span>
      8 spots
      <span class="microbar-dot"></span>
      Spring 2026
      <span class="microbar-dot"></span>
      Irvine, CA
    </div>
  </div>
  <div class="scroll-hint" aria-hidden="true">
    <svg width="24" height="24" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><polyline points="6 9 12 15 18 9"/></svg>
  </div>
</header>
```

- [ ] **Step 2: Add hero CSS**

```css
/* ── HERO ── */
.hero {
  position: relative;
  min-height: 100svh;
  display: flex;
  align-items: center;
  overflow: hidden;
  padding: 80px 0 100px;
}
.hero-inner { position: relative; z-index: 2; }
.hero-title {
  font-size: clamp(2.6rem, 8vw, 5.5rem);
  line-height: 1.05;
  margin-bottom: 20px;
  max-width: 800px;
}
.hero-sub {
  color: var(--muted);
  font-size: clamp(1rem, 2.5vw, 1.25rem);
  max-width: 560px;
  margin-bottom: 32px;
}
.btn-full-mobile { display: inline-flex; }
.hero-microbar {
  display: flex;
  align-items: center;
  gap: 10px;
  margin-top: 20px;
  font-size: 0.82rem;
  color: var(--muted);
  font-weight: 500;
  flex-wrap: wrap;
}
.microbar-dot {
  width: 5px;
  height: 5px;
  border-radius: 50%;
  background: var(--cyan);
  box-shadow: 0 0 8px var(--cyan);
  flex-shrink: 0;
}

/* Orbs */
.orb {
  position: absolute;
  border-radius: 50%;
  filter: blur(90px);
  pointer-events: none;
  z-index: 1;
}
.orb-1 {
  width: 520px; height: 520px;
  background: radial-gradient(circle, rgba(59,130,246,0.45) 0%, transparent 70%);
  top: -160px; left: -140px;
  animation: orbFloat 10s ease-in-out infinite;
}
.orb-2 {
  width: 420px; height: 420px;
  background: radial-gradient(circle, rgba(6,182,212,0.4) 0%, transparent 70%);
  top: 60px; right: -120px;
  animation: orbFloat 13s ease-in-out infinite reverse;
}
@keyframes orbFloat {
  0%, 100% { transform: translateY(0) scale(1); }
  50% { transform: translateY(-36px) scale(1.06); }
}

/* Scroll hint */
.scroll-hint {
  position: absolute;
  bottom: 28px;
  left: 50%;
  transform: translateX(-50%);
  color: var(--muted);
  animation: bounce 2s ease-in-out infinite;
  z-index: 2;
  opacity: 1;
  transition: opacity 400ms;
}
.scroll-hint.hidden { opacity: 0; }
@keyframes bounce {
  0%, 100% { transform: translateX(-50%) translateY(0); }
  50% { transform: translateX(-50%) translateY(8px); }
}

@media (max-width: 600px) {
  .btn-full-mobile { width: 100%; justify-content: center; }
}
```

- [ ] **Step 3: Add scroll-hint hide JS**

```javascript
// Hide scroll hint after user scrolls
const scrollHint = document.querySelector('.scroll-hint');
window.addEventListener('scroll', () => {
  if (window.scrollY > 80) scrollHint?.classList.add('hidden');
}, { passive: true, once: true });
```

- [ ] **Step 4: Verify in browser**

Hero should be near full-screen height. Two glowing orbs drift slowly behind the headline. "AI builders." glows with blue→cyan gradient. CTA is full-width on mobile. Micro-bar shows 3 items with glowing cyan dots.

- [ ] **Step 5: Commit**
```bash
git add index.html
git commit -m "feat: animated hero — orbs, gradient headline, social proof micro-bar"
```

---

### Task 4: Projects Section Redesign

**Files:**
- Modify: `index.html` — `<section id="projects">` HTML + CSS, lightbox CSS update

- [ ] **Step 1: Replace projects section HTML**

Replace the existing `<section id="projects" class="reveal">` block with:

```html
<section id="projects" class="reveal">
  <div class="container">
    <span class="label">What You'll Ship</span>
    <h2 class="section-title">3 real AI products.<br><span class="gradient-text">6 weeks. Zero fluff.</span></h2>
    <p class="section-intro">Students don't just learn concepts — they ship real AI products they can demo, improve, and put in college applications.</p>
    <div class="projects-stack">
      <article class="proj-card">
        <div class="proj-week-tag">Week 1–2</div>
        <video class="product-shot" src="assets/videos/ai-study-buddy-demo.mov" aria-label="AI Chatbot project demo" autoplay loop muted playsinline preload="metadata" tabindex="0"></video>
        <div class="proj-card-body">
          <div class="proj-icon" aria-hidden="true">💬</div>
          <h3>AI Chatbot</h3>
          <p>A custom chatbot students deploy and own, built to solve a real problem they care about.</p>
        </div>
      </article>
      <article class="proj-card">
        <div class="proj-week-tag">Week 3–4</div>
        <video class="product-shot" src="assets/videos/voice-agent-demo.mov" aria-label="Voice Agent project demo" autoplay loop muted playsinline preload="metadata" tabindex="0"></video>
        <div class="proj-card-body">
          <div class="proj-icon" aria-hidden="true">🎙️</div>
          <h3>Voice Agent</h3>
          <p>A voice AI students can actually talk to — language practice, interview prep, or study coaching.</p>
        </div>
      </article>
      <article class="proj-card">
        <div class="proj-week-tag">Week 5–6</div>
        <video class="product-shot" src="assets/videos/customer-support-video.mov" aria-label="Customer Support Agent project demo" autoplay loop muted playsinline preload="metadata" tabindex="0"></video>
        <div class="proj-card-body">
          <div class="proj-icon" aria-hidden="true">⚙️</div>
          <h3>Customer Support Agent</h3>
          <p>An AI support agent that connects real tools students already use — saving time on scheduling, homework, and personal projects.</p>
        </div>
      </article>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Add projects CSS**

```css
/* ── PROJECTS ── */
.projects-stack {
  display: flex;
  flex-direction: column;
  gap: 20px;
}
.proj-card {
  position: relative;
  background: var(--card);
  border: 1px solid var(--card-border);
  border-radius: 18px;
  overflow: hidden;
  transition: border-color 250ms ease, box-shadow 250ms ease, transform 250ms ease;
}
.proj-card:hover, .proj-card:focus-within {
  border-color: var(--cyan);
  box-shadow: 0 0 28px rgba(6,182,212,0.2), 0 0 0 1px rgba(6,182,212,0.15);
  transform: translateY(-3px);
}
.proj-week-tag {
  position: absolute;
  top: 14px;
  left: 14px;
  z-index: 3;
  background: rgba(5,5,8,0.8);
  border: 1px solid var(--cyan);
  color: var(--cyan);
  font-size: 0.68rem;
  font-weight: 700;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  padding: 4px 10px;
  border-radius: 6px;
  backdrop-filter: blur(8px);
}
.product-shot {
  width: 100%;
  aspect-ratio: 16 / 10;
  object-fit: cover;
  display: block;
  cursor: zoom-in;
  background: #0a0a10;
}
.proj-card-body {
  padding: 20px 22px 24px;
  display: flex;
  flex-direction: column;
  gap: 6px;
}
.proj-icon {
  font-size: 1.4rem;
  margin-bottom: 4px;
}
.proj-card-body h3 {
  font-size: 1.2rem;
  font-weight: 700;
}
.proj-card-body p { color: var(--muted); font-size: 0.95rem; }

@media (min-width: 900px) {
  .projects-stack {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 20px;
  }
}
```

- [ ] **Step 3: Update lightbox CSS for dark electric style**

Find the existing `.lightbox` CSS and replace with:

```css
.lightbox {
  position: fixed;
  inset: 0;
  z-index: 9999;
  display: none;
  align-items: center;
  justify-content: center;
  padding: 12px;
  background: rgba(0,0,0,0.97);
  backdrop-filter: blur(4px);
}
.lightbox.open { display: flex; }
.lightbox img, .lightbox video {
  width: 100%;
  height: 100%;
  max-width: 100vw;
  max-height: 100vh;
  object-fit: contain;
  border-radius: 12px;
  z-index: 1;
  border: 1px solid rgba(255,255,255,0.07);
}
.is-hidden { display: none !important; }
.lightbox-close {
  position: absolute;
  top: calc(env(safe-area-inset-top, 0px) + 16px);
  right: calc(env(safe-area-inset-right, 0px) + 16px);
  width: 48px;
  height: 48px;
  border: 1px solid rgba(255,255,255,0.2);
  border-radius: 50%;
  background: rgba(5,5,8,0.8);
  color: #fff;
  font-size: 1.4rem;
  cursor: pointer;
  z-index: 3;
  display: grid;
  place-items: center;
  backdrop-filter: blur(8px);
  transition: border-color 200ms, box-shadow 200ms;
}
.lightbox-close:hover { border-color: var(--cyan); box-shadow: var(--glow-sm); }
```

- [ ] **Step 4: Verify in browser on mobile (375px)**

Cards stack vertically, each full width. Week tag visible top-left of video. Tap video — lightbox opens full screen. On desktop, 3-column grid.

- [ ] **Step 5: Commit**
```bash
git add index.html
git commit -m "feat: projects section — glass cards, glow borders, week tags"
```

---

### Task 5: Social Proof Wall (replaces Customer Discovery)

**Files:**
- Modify: `index.html` — replace `<section id="insights">` entirely, remove Chart.js script tag and Google Sheets fetch block

- [ ] **Step 1: Replace insights section HTML with social proof**

Replace the entire `<section id="insights" ...>` block with:

```html
<section id="proof" class="reveal">
  <div class="container">
    <span class="label">What People Are Saying</span>
    <h2 class="section-title">Real parents.<br><span class="gradient-text">Real results.</span></h2>

    <!-- Featured hero quote -->
    <div class="proof-hero-quote">
      <blockquote>
        "Tech and AI are moving fast, but helping kids build discernment, judgment, and confidence takes time, repetition, and trust. The program and your personal brand are tied together right now. Projects that show real-world application, consistency, and follow-through."
      </blockquote>
      <cite>— KV, SoCal Parent</cite>
    </div>

    <!-- Snap carousel -->
    <div class="proof-carousel-wrap">
      <div class="proof-carousel" id="proof-carousel">
        <div class="proof-card">
          <div class="proof-avatar">KV</div>
          <p class="proof-quote">"Tech and AI are moving fast, but helping kids build discernment, judgment, and confidence takes time, repetition, and trust."</p>
          <span class="proof-name">— KV, SoCal Parent</span>
        </div>
        <div class="proof-card proof-placeholder">
          <div class="proof-avatar">?</div>
          <p class="proof-quote">[Add testimonial — student or parent quote here]</p>
          <span class="proof-name">— Name, Role</span>
        </div>
        <div class="proof-card proof-placeholder">
          <div class="proof-avatar">?</div>
          <p class="proof-quote">[Add testimonial — student or parent quote here]</p>
          <span class="proof-name">— Name, Role</span>
        </div>
      </div>
      <div class="proof-progress-wrap">
        <div class="proof-progress-bar" id="proof-progress"></div>
      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Add social proof CSS**

```css
/* ── SOCIAL PROOF ── */
.proof-hero-quote {
  background: rgba(59,130,246,0.06);
  border-left: 3px solid var(--accent);
  border-radius: 0 14px 14px 0;
  padding: 28px 28px 24px;
  margin-bottom: 36px;
}
.proof-hero-quote blockquote {
  font-size: clamp(1rem, 2.2vw, 1.2rem);
  color: #e2e8f0;
  line-height: 1.7;
  font-style: italic;
  margin-bottom: 12px;
}
.proof-hero-quote cite {
  font-size: 0.82rem;
  color: var(--cyan);
  font-style: normal;
  font-weight: 700;
  letter-spacing: 0.1em;
  text-transform: uppercase;
}

.proof-carousel-wrap { position: relative; }
.proof-carousel {
  display: flex;
  gap: 16px;
  overflow-x: auto;
  scroll-snap-type: x mandatory;
  -webkit-overflow-scrolling: touch;
  padding-bottom: 4px;
  scrollbar-width: none;
}
.proof-carousel::-webkit-scrollbar { display: none; }
.proof-card {
  flex: 0 0 min(85vw, 340px);
  scroll-snap-align: start;
  background: var(--card);
  border: 1px solid var(--card-border);
  border-radius: 16px;
  padding: 24px;
  display: flex;
  flex-direction: column;
  gap: 14px;
}
.proof-placeholder { opacity: 0.4; border-style: dashed; }
.proof-avatar {
  width: 42px;
  height: 42px;
  border-radius: 50%;
  background: var(--gradient);
  display: grid;
  place-items: center;
  font-family: 'Space Grotesk', sans-serif;
  font-weight: 700;
  font-size: 0.9rem;
  color: #fff;
  flex-shrink: 0;
}
.proof-quote {
  color: #e2e8f0;
  font-size: 0.95rem;
  line-height: 1.65;
  font-style: italic;
  flex: 1;
}
.proof-name {
  font-size: 0.78rem;
  color: var(--cyan);
  font-weight: 700;
  letter-spacing: 0.08em;
  text-transform: uppercase;
}
.proof-progress-wrap {
  height: 3px;
  background: rgba(255,255,255,0.08);
  border-radius: 2px;
  margin-top: 16px;
  overflow: hidden;
}
.proof-progress-bar {
  height: 100%;
  background: var(--gradient);
  border-radius: 2px;
  width: 33%;
  transition: width 200ms ease;
}

@media (min-width: 900px) {
  .proof-card { flex: 0 0 320px; }
}
```

- [ ] **Step 3: Add carousel progress JS**

```javascript
// Proof carousel progress bar
const carousel = document.getElementById('proof-carousel');
const progressBar = document.getElementById('proof-progress');
if (carousel && progressBar) {
  carousel.addEventListener('scroll', () => {
    const max = carousel.scrollWidth - carousel.clientWidth;
    const pct = max > 0 ? (carousel.scrollLeft / max) * 100 : 0;
    progressBar.style.width = `${Math.max(10, pct)}%`;
  }, { passive: true });
}
```

- [ ] **Step 4: Remove Chart.js script tag and Google Sheets fetch block**

Delete the `<script src="https://cdn.jsdelivr.net/npm/chart.js...">` tag from `<head>`.

Delete the entire `(async () => { ... })();` block from the `<script>` at the bottom.

- [ ] **Step 5: Verify in browser**

Section shows KV hero quote with blue left border. Below it, 3 cards in horizontal scroll carousel. On mobile, cards snap one at a time. Progress bar updates as you swipe. Placeholder cards show dashed borders.

- [ ] **Step 6: Commit**
```bash
git add index.html
git commit -m "feat: social proof wall — hero quote + snap carousel, remove Chart.js"
```

---

### Task 6: About Kyle + Why AI Merged Section

**Files:**
- Modify: `index.html` — replace `<section id="about">`, `<section id="why-ai-matters">`, and `<section id="about-kyle">` with one merged section

- [ ] **Step 1: Replace all three sections with one merged section**

Delete sections `#about`, `#why-ai-matters`, and `#about-kyle`, replacing with:

```html
<section id="about-kyle" class="reveal">
  <div class="container">
    <span class="label">The Founder</span>
    <div class="about-grid">
      <div class="about-photo-col">
        <a href="https://www.linkedin.com/in/kyletran01/" target="_blank" rel="noopener noreferrer">
          <img
            src="assets/images/KT%20professional%20photo.JPEG"
            alt="Kyle Tran professional headshot"
            class="headshot-image"
            loading="lazy"
          />
        </a>
        <div class="stat-pills">
          <div class="stat-pill"><span>6</span>Weeks</div>
          <div class="stat-pill"><span>3</span>Products</div>
          <div class="stat-pill"><span>∞</span>Community</div>
        </div>
      </div>
      <div class="about-text-col">
        <h2 class="section-title">About <span class="gradient-text">Kyle</span></h2>
        <div class="about-story">
          <p>i didn't go to school for this. i taught myself — chatbots, voice agents, customer support agents, websites shipped on vercel. zapier led to chatgpt led to claude code led to realizing i could build <em class="gradient-text">real things that worked.</em></p>
          <p>then i met a family. their kids were half my age — curious, energetic, asking questions nonstop. something clicked.</p>
          <p>i thought about who i was at 16. junior year. AP classes. track and field. already racing against time without knowing where i was running. nobody handed me a roadmap. i had to find that years later, alone.</p>
          <p><strong>those kids didn't have to wait that long.</strong></p>
        </div>
        <div class="why-cards">
          <div class="why-card">
            <span class="why-icon">⚡</span>
            <div>
              <strong>Technical Initiative</strong>
              <p>You didn't wait to be taught — you built something real.</p>
            </div>
          </div>
          <div class="why-card">
            <span class="why-icon">🧠</span>
            <div>
              <strong>Problem-Solving Ability</strong>
              <p>Real AI projects prove you can think, not just code.</p>
            </div>
          </div>
          <div class="why-card">
            <span class="why-icon">🚀</span>
            <div>
              <strong>Future Readiness</strong>
              <p>Whether college apps or your own startup — builders stand out.</p>
            </div>
          </div>
        </div>
        <div class="starter-line">Founder, Lynx Combinator · Irvine, CA</div>
      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Add about section CSS**

```css
/* ── ABOUT KYLE ── */
.about-grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 40px;
}
.about-photo-col { display: flex; flex-direction: column; gap: 20px; }
.headshot-image {
  width: 100%;
  max-width: 360px;
  aspect-ratio: 4 / 5;
  border-radius: 18px;
  object-fit: cover;
  object-position: 60% center;
  border: 1px solid rgba(59,130,246,0.3);
  box-shadow: 0 0 40px rgba(59,130,246,0.2), 0 20px 40px rgba(0,0,0,0.5);
  display: block;
}
.stat-pills {
  display: flex;
  gap: 10px;
  flex-wrap: wrap;
}
.stat-pill {
  display: flex;
  flex-direction: column;
  align-items: center;
  background: var(--card);
  border: 1px solid var(--card-border);
  border-radius: 12px;
  padding: 12px 18px;
  font-size: 0.72rem;
  font-weight: 600;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  color: var(--muted);
  flex: 1;
  min-width: 80px;
}
.stat-pill span {
  font-family: 'Space Grotesk', sans-serif;
  font-size: 1.6rem;
  font-weight: 700;
  background: var(--gradient);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  line-height: 1.1;
  margin-bottom: 2px;
}
.about-story {
  display: flex;
  flex-direction: column;
  gap: 14px;
  margin-bottom: 28px;
  color: #c8d0e0;
  font-size: 1rem;
  line-height: 1.75;
}
.about-story strong { color: #fff; }
.why-cards {
  display: flex;
  flex-direction: column;
  gap: 12px;
  margin-bottom: 24px;
}
.why-card {
  display: flex;
  align-items: flex-start;
  gap: 14px;
  background: var(--card);
  border: 1px solid var(--card-border);
  border-radius: 12px;
  padding: 16px 18px;
  transition: border-color 200ms, box-shadow 200ms;
}
.why-card:hover { border-color: var(--cyan); box-shadow: 0 0 16px rgba(6,182,212,0.12); }
.why-icon { font-size: 1.4rem; flex-shrink: 0; margin-top: 2px; }
.why-card strong { display: block; color: #fff; font-size: 0.95rem; margin-bottom: 3px; }
.why-card p { color: var(--muted); font-size: 0.88rem; margin: 0; }
.starter-line {
  font-size: 0.78rem;
  font-weight: 700;
  letter-spacing: 0.14em;
  text-transform: uppercase;
  color: var(--cyan);
}

@media (min-width: 900px) {
  .about-grid {
    grid-template-columns: 280px 1fr;
    gap: 56px;
    align-items: start;
  }
}
```

- [ ] **Step 3: Verify in browser**

On mobile: headshot full width, stat pills below, then story + why cards stacked. On desktop: headshot + pills on left, story + cards on right. Headshot has blue glow. "real things that worked." highlights in gradient.

- [ ] **Step 4: Commit**
```bash
git add index.html
git commit -m "feat: merged about + why-ai section — headshot glow, stat pills, why cards"
```

---

### Task 7: Contact Section + Urgency Marquee + Footer

**Files:**
- Modify: `index.html` — `<section id="contact">`, marquee banner, `<footer>`

- [ ] **Step 1: Replace contact section HTML**

Replace the existing `<section id="contact" ...>` with:

```html
<section id="contact" class="reveal">
  <div class="container contact-inner">
    <span class="label">Join the Cohort</span>
    <h2 class="section-title">Ready to <span class="gradient-text">build?</span></h2>
    <p class="section-intro">Spring 2026 · 8 spots · Beta pricing for early applicants through March 31, 2026.</p>
    <a href="mailto:kyle7tran@gmail.com" class="btn btn-full-mobile contact-cta-btn">Apply Now — Email Kyle →</a>
    <div class="contact-links">
      <a href="https://www.linkedin.com/in/kyletran01/" target="_blank" rel="noopener noreferrer" class="contact-pill">LinkedIn</a>
      <a href="https://x.com/kyle_trxn" target="_blank" rel="noopener noreferrer" class="contact-pill">Twitter / X</a>
      <a href="mailto:kyle7tran@gmail.com" class="contact-pill">kyle7tran@gmail.com</a>
    </div>
    <p class="contact-note">Interested in bringing Lynx Combinator to your school or community? <a href="mailto:kyle7tran@gmail.com">Let's talk.</a></p>
  </div>
</section>
```

- [ ] **Step 2: Add marquee banner HTML before `<footer>`**

```html
<div class="marquee-wrap" aria-hidden="true">
  <div class="marquee-track">
    <span class="marquee-content">✦ 8 SPOTS REMAINING &nbsp;&nbsp;&nbsp; APPLY BY MARCH 31 &nbsp;&nbsp;&nbsp; IRVINE, CA &nbsp;&nbsp;&nbsp; SPRING 2026 &nbsp;&nbsp;&nbsp; LYNX COMBINATOR &nbsp;&nbsp;&nbsp;</span>
    <span class="marquee-content" aria-hidden="true">✦ 8 SPOTS REMAINING &nbsp;&nbsp;&nbsp; APPLY BY MARCH 31 &nbsp;&nbsp;&nbsp; IRVINE, CA &nbsp;&nbsp;&nbsp; SPRING 2026 &nbsp;&nbsp;&nbsp; LYNX COMBINATOR &nbsp;&nbsp;&nbsp;</span>
  </div>
</div>
```

- [ ] **Step 3: Replace footer HTML**

```html
<footer>
  <div class="container">© <span id="year"></span> Kyle Tran · Lynx Combinator</div>
</footer>
```

- [ ] **Step 4: Add contact + marquee CSS**

```css
/* ── CONTACT ── */
.contact-inner { max-width: 600px; }
.contact-cta-btn { margin-bottom: 28px; font-size: 1.05rem; padding: 16px 32px; }
.contact-links {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  margin-bottom: 24px;
}
.contact-pill {
  display: inline-flex;
  align-items: center;
  padding: 9px 18px;
  border-radius: 999px;
  border: 1px solid var(--card-border);
  color: var(--cyan);
  text-decoration: none;
  font-size: 0.88rem;
  font-weight: 600;
  background: var(--card);
  transition: border-color 200ms, box-shadow 200ms, color 200ms;
}
.contact-pill:hover { border-color: var(--cyan); box-shadow: 0 0 12px rgba(6,182,212,0.25); color: #fff; }
.contact-note { color: var(--muted); font-size: 0.9rem; }
.contact-note a { color: var(--cyan); text-decoration: none; border-bottom: 1px solid transparent; transition: border-color 200ms; }
.contact-note a:hover { border-color: var(--cyan); }

/* ── MARQUEE ── */
.marquee-wrap {
  overflow: hidden;
  border-top: 1px solid rgba(255,255,255,0.06);
  border-bottom: 1px solid rgba(255,255,255,0.06);
  padding: 12px 0;
  background: rgba(59,130,246,0.04);
}
.marquee-track {
  display: flex;
  width: max-content;
  animation: marquee 22s linear infinite;
}
.marquee-content {
  font-size: 0.72rem;
  font-weight: 700;
  letter-spacing: 0.2em;
  color: var(--cyan);
  white-space: nowrap;
  padding-right: 40px;
}
@keyframes marquee {
  0% { transform: translateX(0); }
  100% { transform: translateX(-50%); }
}

/* ── FOOTER ── */
footer {
  padding: 28px 0 20px;
  text-align: center;
  color: #4a5568;
  font-size: 0.85rem;
}

@media (max-width: 600px) {
  .contact-cta-btn { width: 100%; }
}
```

- [ ] **Step 5: Verify in browser**

Contact section has glowing CTA button. Below: 3 pill links (LinkedIn, Twitter, Email) with cyan glow on hover. Marquee scrolls continuously. Footer is clean and minimal. On mobile, CTA is full-width.

- [ ] **Step 6: Commit**
```bash
git add index.html
git commit -m "feat: contact section, urgency marquee ticker, updated footer"
```

---

### Task 8: Final Mobile Polish + Section Diagonal Cuts

**Files:**
- Modify: `index.html` — diagonal clip-path dividers, mobile spacing, safe area fixes

- [ ] **Step 1: Add diagonal section dividers via CSS**

Add to the CSS:

```css
/* ── SECTION DIAGONAL CUTS ── */
#projects {
  clip-path: polygon(0 0, 100% 0, 100% 95%, 0 100%);
  margin-bottom: -40px;
  background: linear-gradient(180deg, #050508 0%, #07080f 100%);
}
#proof {
  clip-path: polygon(0 5%, 100% 0, 100% 95%, 0 100%);
  margin-bottom: -40px;
  padding-top: 120px;
  background: linear-gradient(180deg, #07080f 0%, #050508 100%);
}
#about-kyle {
  clip-path: polygon(0 5%, 100% 0, 100% 100%, 0 100%);
  padding-top: 120px;
}
```

- [ ] **Step 2: Add mobile spacing fixes**

```css
@media (max-width: 600px) {
  section { padding: 72px 0; }
  #projects, #proof, #about-kyle { padding-top: 100px; }
  .hero { padding: 60px 0 80px; }
  .hero-title { font-size: clamp(2.4rem, 11vw, 3.2rem); }
  .proof-hero-quote { padding: 20px; }
  .about-grid { gap: 28px; }
  .stat-pills { justify-content: space-between; }
  .stat-pill { min-width: 0; flex: 1; padding: 10px 12px; }
}
@media (max-width: 380px) {
  .hero-title { font-size: 2.2rem; }
  .btn { font-size: 0.95rem; padding: 13px 20px; }
}
```

- [ ] **Step 3: Verify full mobile experience at 375px and 390px**

Test checklist:
- [ ] Bottom nav visible, never covers content
- [ ] Hero orbs visible but not overwhelming
- [ ] Project cards full-width, tap to expand lightbox
- [ ] Social proof carousel swipe-snaps between cards
- [ ] About section: photo + pills stacked, story readable
- [ ] Contact CTA button full-width, easy to tap
- [ ] Marquee scrolls without jank
- [ ] No horizontal scroll on any section

- [ ] **Step 4: Final commit**
```bash
git add index.html
git commit -m "feat: diagonal section dividers + mobile polish — complete electric scroll redesign"
```
