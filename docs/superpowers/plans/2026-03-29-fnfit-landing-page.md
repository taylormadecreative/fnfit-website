# FnFit Landing Page Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a production-quality, single-page landing page for FnFit (faith-based personal training) with no images, mailto contact, and deploy to GitHub Pages.

**Architecture:** Single HTML file with inlined CSS and JS. No build tools, no frameworks, no external dependencies except Google Fonts. SVG icons inline. Deployed as static site to GitHub Pages.

**Tech Stack:** HTML5, CSS3 (custom properties, grid, flexbox, animations), vanilla JS (IntersectionObserver, event listeners), Google Fonts (Fraunces + Plus Jakarta Sans), GitHub Pages.

**Spec:** `docs/superpowers/specs/2026-03-29-fnfit-landing-page-design.md`

---

## File Structure

```
fnfit-website/
├── index.html          # Complete single-file site (CSS + JS inlined)
├── docs/
│   └── superpowers/
│       ├── specs/      # Design spec
│       └── plans/      # This plan
└── README.md           # GitHub repo description (auto-generated)
```

Only one file to create/modify: `index.html`. The existing draft at this path will be **completely rewritten** to incorporate all spec requirements and 4-agent review fixes.

---

### Task 1: Initialize Git Repo & Scaffold HTML Shell

**Files:**
- Modify: `index.html` (rewrite from scratch)

- [ ] **Step 1: Initialize git repo**

```bash
cd /Users/nelsontaylor/Documents/fnfit-website
git init
```

- [ ] **Step 2: Write the HTML shell with `<head>` section**

Rewrite `index.html` with the complete `<head>` including:
- Charset, viewport, title, meta description
- OG tags (`og:title`, `og:description`, `og:type`, `og:url`)
- Twitter card meta (`twitter:card` summary)
- Optimized Google Fonts load (preload critical weights, reduced weight set)
- Opening `<style>` tag with CSS reset, custom properties, and utility classes
- `<noscript>` fallback for `.reveal` elements

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>FnFit — Transform Lives One Smile at a Time</title>
  <meta name="description" content="FnFit is a faith-based personal training program offering online and in-person fitness coaching in the DFW area. Transform your body, mind, and spirit.">

  <!-- Open Graph -->
  <meta property="og:title" content="FnFit — Transform Lives One Smile at a Time">
  <meta property="og:description" content="Faith-based personal training in the DFW area. Online and in-person coaching for body, mind, and spirit.">
  <meta property="og:type" content="website">
  <meta name="twitter:card" content="summary">

  <!-- Fonts: preload critical, then load full set -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link rel="preload" href="https://fonts.googleapis.com/css2?family=Fraunces:opsz,wght@9..144,700&family=Plus+Jakarta+Sans:wght@400;600&display=swap" as="style">
  <link href="https://fonts.googleapis.com/css2?family=Fraunces:ital,opsz,wght@0,9..144,700;0,9..144,800;1,9..144,400&family=Plus+Jakarta+Sans:wght@300;400;500;600;700&display=swap" rel="stylesheet">

  <!-- No-JS fallback -->
  <noscript><style>.reveal { opacity: 1 !important; transform: none !important; }</style></noscript>

  <style>
    *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }

    :root {
      --forest: #2B4A3E;
      --forest-deep: #1A3329;
      --gold: #C8963E;
      --gold-light: #E8C06A;
      --gold-glow: #F5DFA0;
      --cream: #FBF5EB;
      --cream-dark: #F0E6D4;
      --sage: #A8B5A0;
      --sage-light: #D4DDD0;
      --white: #FFFFFF;
      --text: #2A2118;
      --text-light: #6B5F54;
    }

    html { scroll-behavior: smooth; }

    body {
      font-family: 'Plus Jakarta Sans', sans-serif;
      color: var(--text);
      background: var(--cream);
      overflow-x: hidden;
      -webkit-font-smoothing: antialiased;
    }

    .container { max-width: 1200px; margin: 0 auto; padding: 0 24px; }
    .sr-only { position: absolute; width: 1px; height: 1px; overflow: hidden; clip: rect(0,0,0,0); }

    /* Reveal animations */
    .reveal {
      opacity: 0;
      transform: translateY(40px);
      transition: opacity 0.8s cubic-bezier(0.16, 1, 0.3, 1), transform 0.8s cubic-bezier(0.16, 1, 0.3, 1);
    }
    .reveal.visible { opacity: 1; transform: translateY(0); }
    .reveal-delay-1 { transition-delay: 0.1s; }
    .reveal-delay-2 { transition-delay: 0.2s; }
    .reveal-delay-3 { transition-delay: 0.3s; }
    .reveal-delay-4 { transition-delay: 0.4s; }
  </style>
</head>
```

- [ ] **Step 3: Verify HTML validates**

Open in browser, check that fonts load and no console errors appear.

```bash
open /Users/nelsontaylor/Documents/fnfit-website/index.html
```

- [ ] **Step 4: Commit**

```bash
cd /Users/nelsontaylor/Documents/fnfit-website
git add index.html
git commit -m "feat: scaffold HTML shell with head, fonts, OG tags, noscript fallback"
```

---

### Task 2: Navigation CSS & HTML

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add navigation CSS**

Add after the reveal animation CSS, inside the `<style>` block. Uses `.nav-links .nav-cta` specificity instead of `!important` (fix from review).

```css
/* ─── NAVIGATION ─── */
nav {
  position: fixed; top: 0; left: 0; right: 0;
  z-index: 100; padding: 20px 0;
  transition: all 0.4s ease;
}
nav.scrolled {
  background: rgba(251, 245, 235, 0.95);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  padding: 14px 0;
  box-shadow: 0 1px 30px rgba(43, 74, 62, 0.08);
}
nav .container {
  display: flex; align-items: center; justify-content: space-between;
}
.nav-logo {
  font-family: 'Fraunces', serif; font-weight: 800; font-size: 28px;
  color: var(--forest); text-decoration: none; letter-spacing: -0.5px;
}
.nav-logo span { color: var(--gold); }
.nav-links {
  display: flex; align-items: center; gap: 36px; list-style: none;
}
.nav-links a {
  font-size: 14px; font-weight: 500; color: var(--forest);
  text-decoration: none; letter-spacing: 0.3px; transition: color 0.3s;
}
.nav-links a:hover { color: var(--gold); }
.nav-links .nav-cta {
  background: var(--forest); color: var(--cream);
  padding: 12px 28px; border-radius: 100px;
  font-weight: 600; transition: all 0.3s;
}
.nav-links .nav-cta:hover {
  background: var(--gold); color: var(--forest);
  transform: translateY(-1px);
}
.mobile-toggle {
  display: none; background: none; border: none; cursor: pointer;
  width: 32px; height: 24px; position: relative; z-index: 110;
}
.mobile-toggle span {
  display: block; width: 100%; height: 2px; background: var(--forest);
  border-radius: 2px; transition: all 0.3s; position: absolute; left: 0;
}
.mobile-toggle span:nth-child(1) { top: 0; }
.mobile-toggle span:nth-child(2) { top: 11px; }
.mobile-toggle span:nth-child(3) { top: 22px; }
.mobile-toggle.active span:nth-child(1) { top: 11px; transform: rotate(45deg); }
.mobile-toggle.active span:nth-child(2) { opacity: 0; }
.mobile-toggle.active span:nth-child(3) { top: 11px; transform: rotate(-45deg); }
```

- [ ] **Step 2: Add navigation HTML**

Add after the opening `<body>` tag. Nav links point to section IDs: `#about`, `#programs`, `#expect`, `#contact`. The "Free Consultation" CTA links to `mailto:chiquitawhite@icloud.com?subject=Free%20Consultation%20Request`.

```html
<body>
  <nav>
    <div class="container">
      <a href="#" class="nav-logo">Fn<span>Fit</span></a>
      <ul class="nav-links" id="navLinks">
        <li><a href="#about">About</a></li>
        <li><a href="#programs">Programs</a></li>
        <li><a href="#expect">What to Expect</a></li>
        <li><a href="#contact" class="nav-cta">Free Consultation</a></li>
      </ul>
      <button class="mobile-toggle" id="mobileToggle" aria-label="Toggle menu">
        <span></span><span></span><span></span>
      </button>
    </div>
  </nav>
```

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add sticky navigation with mobile hamburger"
```

---

### Task 3: Hero Section

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add hero CSS**

Add to `<style>` block. Includes the morphing organic shape (desktop only), hero badge with pulsing dot, headline with italic emphasis, stat pills, and two CTA buttons.

```css
/* ─── SHARED ─── */
section { padding: 120px 0; }
.section-label {
  font-size: 12px; font-weight: 700; letter-spacing: 2.5px;
  text-transform: uppercase; color: var(--gold); margin-bottom: 16px;
}
.section-heading {
  font-family: 'Fraunces', serif;
  font-size: clamp(36px, 5vw, 52px); font-weight: 700;
  line-height: 1.15; color: var(--forest-deep);
  letter-spacing: -0.5px; margin-bottom: 20px;
}
.section-heading em { font-style: italic; color: var(--gold); font-weight: 400; }
.section-sub {
  font-size: 17px; line-height: 1.7; color: var(--text-light); max-width: 560px;
}
.btn {
  display: inline-flex; align-items: center; gap: 10px;
  padding: 18px 36px; border-radius: 100px;
  font-size: 15px; font-weight: 600; text-decoration: none;
  transition: all 0.35s cubic-bezier(0.16, 1, 0.3, 1);
  cursor: pointer; border: none; letter-spacing: 0.3px;
}
.btn-primary { background: var(--gold); color: var(--forest-deep); }
.btn-primary:hover {
  background: var(--gold-light); transform: translateY(-2px);
  box-shadow: 0 12px 40px rgba(200, 150, 62, 0.35);
}
.btn-outline {
  background: transparent; color: var(--cream);
  border: 1.5px solid rgba(251, 245, 235, 0.3);
}
.btn-outline:hover {
  border-color: var(--gold-light); color: var(--gold-light);
  transform: translateY(-2px);
}

/* ─── HERO ─── */
.hero {
  min-height: 100vh; display: flex; align-items: center;
  position: relative; overflow: hidden;
  background: linear-gradient(165deg, var(--forest-deep) 0%, var(--forest) 40%, #3A6B56 100%);
}
.hero::before {
  content: ''; position: absolute; inset: 0;
  background:
    radial-gradient(ellipse 80% 60% at 70% 20%, rgba(200, 150, 62, 0.15) 0%, transparent 60%),
    radial-gradient(ellipse 60% 80% at 20% 80%, rgba(168, 181, 160, 0.1) 0%, transparent 50%);
}
.hero::after {
  content: ''; position: absolute; bottom: -2px; left: 0; right: 0;
  height: 120px; background: var(--cream);
  clip-path: ellipse(55% 100% at 50% 100%);
}
.hero-pattern {
  position: absolute; inset: 0; opacity: 0.04;
  background-image:
    radial-gradient(circle at 20% 50%, var(--gold) 1px, transparent 1px),
    radial-gradient(circle at 80% 20%, var(--gold) 1px, transparent 1px),
    radial-gradient(circle at 60% 80%, var(--gold) 1px, transparent 1px);
  background-size: 80px 80px, 120px 120px, 100px 100px;
}
.hero .container { position: relative; z-index: 2; padding-top: 120px; padding-bottom: 80px; }
.hero-content { max-width: 720px; }
.hero-badge {
  display: inline-flex; align-items: center; gap: 8px;
  background: rgba(200, 150, 62, 0.15);
  border: 1px solid rgba(200, 150, 62, 0.3);
  color: var(--gold-light); padding: 8px 20px; border-radius: 100px;
  font-size: 13px; font-weight: 600; letter-spacing: 1.5px;
  text-transform: uppercase; margin-bottom: 32px;
}
.hero-badge::before {
  content: ''; width: 8px; height: 8px; border-radius: 50%;
  background: var(--gold); animation: pulse-dot 2s ease-in-out infinite;
}
@keyframes pulse-dot {
  0%, 100% { opacity: 1; transform: scale(1); }
  50% { opacity: 0.5; transform: scale(1.5); }
}
.hero h1 {
  font-family: 'Fraunces', serif;
  font-size: clamp(48px, 7vw, 80px); font-weight: 700;
  line-height: 1.05; color: var(--cream); margin-bottom: 28px; letter-spacing: -1.5px;
}
.hero h1 em { font-style: italic; color: var(--gold-light); font-weight: 400; }
.hero-sub {
  font-size: 18px; line-height: 1.7; color: rgba(251, 245, 235, 0.75);
  max-width: 540px; margin-bottom: 48px; font-weight: 300;
}
.hero-buttons { display: flex; gap: 16px; flex-wrap: wrap; }
.hero-stats {
  display: flex; gap: 48px; margin-top: 64px; padding-top: 40px;
  border-top: 1px solid rgba(251, 245, 235, 0.1);
}
.hero-stat h3 {
  font-family: 'Fraunces', serif; font-size: 36px; font-weight: 700;
  color: var(--gold-light);
}
.hero-stat p {
  font-size: 13px; color: rgba(251, 245, 235, 0.5);
  text-transform: uppercase; letter-spacing: 1px; margin-top: 4px;
}

/* Decorative shape (desktop only) */
.hero-shape {
  position: absolute; right: -5%; top: 50%; transform: translateY(-50%);
  width: 500px; height: 500px;
  border-radius: 30% 70% 70% 30% / 30% 30% 70% 70%;
  background: linear-gradient(135deg, rgba(200, 150, 62, 0.12), rgba(168, 181, 160, 0.08));
  border: 1px solid rgba(200, 150, 62, 0.1);
  animation: morph 15s ease-in-out infinite; z-index: 1;
}
@keyframes morph {
  0% { border-radius: 30% 70% 70% 30% / 30% 30% 70% 70%; }
  25% { border-radius: 58% 42% 36% 64% / 54% 62% 38% 46%; }
  50% { border-radius: 50% 50% 34% 66% / 56% 68% 32% 44%; }
  75% { border-radius: 42% 58% 64% 36% / 48% 32% 68% 52%; }
  100% { border-radius: 30% 70% 70% 30% / 30% 30% 70% 70%; }
}
.hero-shape-inner {
  position: absolute; inset: 40px; border-radius: inherit;
  border: 1px solid rgba(200, 150, 62, 0.08);
}
```

- [ ] **Step 2: Add hero HTML**

After the `</nav>`, add the hero section. "Start Your Journey" button links to `mailto:chiquitawhite@icloud.com?subject=Free%20Consultation%20Request`. "View Programs" scrolls to `#programs`. Stats row uses "Free / First Consultation" instead of "DFW / Texas Based" (review fix).

```html
<section class="hero">
  <div class="hero-pattern"></div>
  <div class="hero-shape"><div class="hero-shape-inner"></div></div>
  <div class="container">
    <div class="hero-content">
      <div class="hero-badge reveal">Faith + Fitness + Purpose</div>
      <h1 class="reveal reveal-delay-1">Transform Lives,<br>One <em>Smile</em> at a Time</h1>
      <p class="hero-sub reveal reveal-delay-2">Faith-based personal training that meets you where you are. Build strength in body, mind, and spirit — with a coach who believes in your purpose.</p>
      <div class="hero-buttons reveal reveal-delay-3">
        <a href="mailto:chiquitawhite@icloud.com?subject=Free%20Consultation%20Request" class="btn btn-primary">Start Your Journey</a>
        <a href="#programs" class="btn btn-outline">View Programs</a>
      </div>
      <div class="hero-stats reveal reveal-delay-4">
        <div class="hero-stat">
          <h3>1:1</h3>
          <p>Personalized Coaching</p>
        </div>
        <div class="hero-stat">
          <h3>Flexible</h3>
          <p>Online or In-Person</p>
        </div>
        <div class="hero-stat">
          <h3>Free</h3>
          <p>First Consultation</p>
        </div>
      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 3: Verify hero renders correctly**

```bash
open /Users/nelsontaylor/Documents/fnfit-website/index.html
```

Check: gradient background, badge with pulsing dot, headline with gold italic "Smile", two buttons, stats row, morphing shape on right side, elliptical cream bottom edge.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add hero section with badge, CTAs, stats, morphing shape"
```

---

### Task 4: About / Mission Section with SVG Icons

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add about section CSS**

```css
/* ─── ABOUT ─── */
.about { background: var(--cream); position: relative; }
.about-grid {
  display: grid; grid-template-columns: 1fr 1fr; gap: 80px; align-items: center;
}
.about-visual {
  position: relative; height: 520px; border-radius: 24px; overflow: hidden;
  background: linear-gradient(145deg, var(--forest), var(--forest-deep));
}
.about-visual-pattern {
  position: absolute; inset: 0; opacity: 0.06;
  background-image: repeating-linear-gradient(45deg, transparent, transparent 20px, var(--gold) 20px, var(--gold) 21px);
}
.about-visual-content {
  position: absolute; inset: 0; display: flex; flex-direction: column;
  justify-content: center; align-items: center; text-align: center; padding: 48px;
}
.about-visual-icon {
  width: 80px; height: 80px; border-radius: 50%;
  background: rgba(200, 150, 62, 0.15); border: 1px solid rgba(200, 150, 62, 0.3);
  display: flex; align-items: center; justify-content: center; margin-bottom: 32px;
}
.about-visual-quote {
  font-family: 'Fraunces', serif; font-size: 28px; font-style: italic;
  color: var(--cream); line-height: 1.4; max-width: 360px; font-weight: 400;
}
.about-visual-ref {
  margin-top: 20px; font-size: 14px; color: var(--gold-light); font-weight: 500;
}
.about-text .section-sub { margin-bottom: 32px; }
.about-values { display: flex; flex-direction: column; gap: 20px; margin-top: 40px; }
.about-value { display: flex; align-items: flex-start; gap: 16px; }
.about-value-icon {
  flex-shrink: 0; width: 44px; height: 44px; border-radius: 12px;
  background: var(--sage-light); display: flex; align-items: center;
  justify-content: center;
}
.about-value-icon svg { width: 22px; height: 22px; stroke: var(--forest); }
.about-value h4 { font-size: 16px; font-weight: 700; color: var(--forest); margin-bottom: 4px; }
.about-value p { font-size: 14px; color: var(--text-light); line-height: 1.6; }
```

- [ ] **Step 2: Add about section HTML with inline SVG icons**

All icons are Lucide SVGs. The dove icon is replaced with a heart-handshake concept. Value prop icons: heart (faith), users (community), sparkles (wellness).

```html
<section class="about" id="about">
  <div class="container">
    <div class="about-grid">
      <div class="about-visual reveal">
        <div class="about-visual-pattern"></div>
        <div class="about-visual-content">
          <div class="about-visual-icon">
            <svg width="36" height="36" viewBox="0 0 24 24" fill="none" stroke="var(--gold-light)" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><path d="M19 14c1.49-1.46 3-3.21 3-5.5A5.5 5.5 0 0 0 16.5 3c-1.76 0-3 .5-4.5 2-1.5-1.5-2.74-2-4.5-2A5.5 5.5 0 0 0 2 8.5c0 2.3 1.5 4.05 3 5.5l7 7Z"/></svg>
          </div>
          <p class="about-visual-quote">"For physical training is of some value, but godliness has value for all things."</p>
          <p class="about-visual-ref">— 1 Timothy 4:8</p>
        </div>
      </div>
      <div class="about-text">
        <p class="section-label reveal">Our Mission</p>
        <h2 class="section-heading reveal reveal-delay-1">More Than Fitness.<br>It's a <em>Calling</em></h2>
        <p class="section-sub reveal reveal-delay-2">FnFit is a faith-based health and wellness program built on the belief that your body is a temple. We don't just count reps — we build confidence, restore joy, and help you step into your God-given purpose through movement.</p>
        <div class="about-values reveal reveal-delay-3">
          <div class="about-value">
            <div class="about-value-icon">
              <svg viewBox="0 0 24 24" fill="none" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M19 14c1.49-1.46 3-3.21 3-5.5A5.5 5.5 0 0 0 16.5 3c-1.76 0-3 .5-4.5 2-1.5-1.5-2.74-2-4.5-2A5.5 5.5 0 0 0 2 8.5c0 2.3 1.5 4.05 3 5.5l7 7Z"/></svg>
            </div>
            <div>
              <h4>Faith-Centered Approach</h4>
              <p>Every session is rooted in encouragement, scripture, and the belief that wellness is a form of worship.</p>
            </div>
          </div>
          <div class="about-value">
            <div class="about-value-icon">
              <svg viewBox="0 0 24 24" fill="none" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M16 21v-2a4 4 0 0 0-4-4H6a4 4 0 0 0-4 4v2"/><circle cx="9" cy="7" r="4"/><path d="M22 21v-2a4 4 0 0 0-3-3.87"/><path d="M16 3.13a4 4 0 0 1 0 7.75"/></svg>
            </div>
            <div>
              <h4>Meet You Where You Are</h4>
              <p>No judgment, no intimidation. Whether you're just starting or getting back on track — you belong here.</p>
            </div>
          </div>
          <div class="about-value">
            <div class="about-value-icon">
              <svg viewBox="0 0 24 24" fill="none" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="m12 3-1.912 5.813a2 2 0 0 1-1.275 1.275L3 12l5.813 1.912a2 2 0 0 1 1.275 1.275L12 21l1.912-5.813a2 2 0 0 1 1.275-1.275L21 12l-5.813-1.912a2 2 0 0 1-1.275-1.275L12 3Z"/></svg>
            </div>
            <div>
              <h4>Whole-Person Wellness</h4>
              <p>We train the body, nourish the mind, and strengthen the spirit. Transformation starts from within.</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 3: Verify about section renders**

Check: scripture card on left with heart SVG, diagonal line pattern, heading with gold "Calling" italic, three value props with SVG icons on sage backgrounds.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add about/mission section with SVG icons and scripture card"
```

---

### Task 5: Programs Section (Dark)

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add programs CSS**

```css
/* ─── PROGRAMS ─── */
.services { background: var(--forest-deep); position: relative; overflow: hidden; }
.services::before {
  content: ''; position: absolute; inset: 0;
  background: radial-gradient(ellipse 50% 50% at 80% 20%, rgba(200, 150, 62, 0.06) 0%, transparent 70%);
}
.services .section-label { color: var(--gold-light); }
.services .section-heading { color: var(--cream); }
.services .section-heading em { color: var(--gold-light); }
.services .section-sub { color: rgba(251, 245, 235, 0.6); }
.services-header { text-align: center; margin-bottom: 72px; }
.services-header .section-sub { margin: 0 auto; }
.services-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 24px; }
.service-card {
  background: rgba(251, 245, 235, 0.04); border: 1px solid rgba(251, 245, 235, 0.08);
  border-radius: 20px; padding: 44px 36px;
  transition: all 0.4s cubic-bezier(0.16, 1, 0.3, 1); position: relative; overflow: hidden;
}
.service-card::before {
  content: ''; position: absolute; top: 0; left: 0; right: 0; height: 3px;
  background: linear-gradient(90deg, var(--gold), var(--gold-light));
  opacity: 0; transition: opacity 0.4s;
}
.service-card:hover {
  background: rgba(251, 245, 235, 0.08);
  border-color: rgba(200, 150, 62, 0.2); transform: translateY(-4px);
}
.service-card:hover::before { opacity: 1; }
.service-icon {
  width: 56px; height: 56px; border-radius: 16px;
  background: rgba(200, 150, 62, 0.12); display: flex;
  align-items: center; justify-content: center; margin-bottom: 28px;
}
.service-icon svg { width: 28px; height: 28px; stroke: var(--gold-light); }
.service-card h3 {
  font-family: 'Fraunces', serif; font-size: 24px; font-weight: 600;
  color: var(--cream); margin-bottom: 14px;
}
.service-card p { font-size: 15px; line-height: 1.7; color: rgba(251, 245, 235, 0.55); }
.service-features {
  list-style: none; margin-top: 24px; display: flex; flex-direction: column; gap: 10px;
}
.service-features li {
  display: flex; align-items: center; gap: 10px;
  font-size: 14px; color: rgba(251, 245, 235, 0.65);
}
.service-features li::before {
  content: '\2713'; color: var(--gold); font-weight: 700; font-size: 13px;
}
```

- [ ] **Step 2: Add programs HTML with SVG icons**

Three cards: Online Training (monitor icon), In-Person Training (dumbbell icon), Faith & Wellness (sun icon). No pricing on any card.

```html
<section class="services" id="programs">
  <div class="container">
    <div class="services-header">
      <p class="section-label reveal">Programs</p>
      <h2 class="section-heading reveal reveal-delay-1">Train Your Way,<br>On <em>Your Terms</em></h2>
      <p class="section-sub reveal reveal-delay-2">Whether you prefer to train from home or face-to-face, FnFit offers flexible coaching that fits your life and goals.</p>
    </div>
    <div class="services-grid">
      <div class="service-card reveal">
        <div class="service-icon">
          <svg viewBox="0 0 24 24" fill="none" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect width="20" height="14" x="2" y="3" rx="2"/><line x1="8" x2="16" y1="21" y2="21"/><line x1="12" x2="12" y1="17" y2="21"/></svg>
        </div>
        <h3>Online Training</h3>
        <p>Personalized workout plans and virtual coaching sessions from the comfort of your home — anywhere, anytime.</p>
        <ul class="service-features">
          <li>Custom workout plans</li>
          <li>Video call coaching sessions</li>
          <li>Weekly check-ins & accountability</li>
          <li>Nutrition guidance</li>
        </ul>
      </div>
      <div class="service-card reveal reveal-delay-1">
        <div class="service-icon">
          <svg viewBox="0 0 24 24" fill="none" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M6.5 6.5h11"/><path d="M6.5 17.5h11"/><path d="M2 12h2"/><path d="M20 12h2"/><path d="M7 12h10"/><rect x="4" y="9" width="3" height="6" rx="1"/><rect x="17" y="9" width="3" height="6" rx="1"/></svg>
        </div>
        <h3>In-Person Training</h3>
        <p>One-on-one sessions in the DFW area with hands-on guidance, form correction, and real-time motivation.</p>
        <ul class="service-features">
          <li>1-on-1 personal sessions</li>
          <li>Form & technique coaching</li>
          <li>Customized to your fitness level</li>
          <li>DFW metroplex locations</li>
        </ul>
      </div>
      <div class="service-card reveal reveal-delay-2">
        <div class="service-icon">
          <svg viewBox="0 0 24 24" fill="none" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="4"/><path d="M12 2v2"/><path d="M12 20v2"/><path d="m4.93 4.93 1.41 1.41"/><path d="m17.66 17.66 1.41 1.41"/><path d="M2 12h2"/><path d="M20 12h2"/><path d="m6.34 17.66-1.41 1.41"/><path d="m19.07 4.93-1.41 1.41"/></svg>
        </div>
        <h3>Faith & Wellness</h3>
        <p>A holistic program combining physical fitness with spiritual growth — because your best self is the whole self.</p>
        <ul class="service-features">
          <li>Devotional-led sessions</li>
          <li>Mindset & motivation coaching</li>
          <li>Community & group support</li>
          <li>Goal-setting with purpose</li>
        </ul>
      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 3: Verify programs section**

Check: dark forest background, subtle gold radial, 3 cards with SVG icons, gold top-line on hover, checkmark bullets, no pricing visible.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add programs section with three service cards and SVG icons"
```

---

### Task 6: What to Expect Section (Replaces Testimonials)

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add "What to Expect" CSS**

```css
/* ─── WHAT TO EXPECT ─── */
.expect { background: var(--cream); position: relative; }
.expect-header { text-align: center; margin-bottom: 72px; }
.expect-header .section-sub { margin: 0 auto; }
.expect-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 32px; }
.expect-card {
  background: var(--white); border-radius: 20px; padding: 44px 36px;
  border: 1px solid rgba(43, 74, 62, 0.06); transition: all 0.3s;
}
.expect-card:hover {
  box-shadow: 0 20px 60px rgba(43, 74, 62, 0.08); transform: translateY(-4px);
}
.expect-card-header {
  display: flex; align-items: center; gap: 16px; margin-bottom: 32px;
  padding-bottom: 24px; border-bottom: 1px solid rgba(43, 74, 62, 0.08);
}
.expect-card-icon {
  width: 52px; height: 52px; border-radius: 14px;
  background: var(--sage-light); display: flex;
  align-items: center; justify-content: center;
}
.expect-card-icon svg { width: 24px; height: 24px; stroke: var(--forest); }
.expect-card-header h3 {
  font-family: 'Fraunces', serif; font-size: 22px; font-weight: 700; color: var(--forest);
}
.expect-card-header p { font-size: 13px; color: var(--text-light); margin-top: 2px; }
.expect-steps { display: flex; flex-direction: column; gap: 20px; }
.expect-step { display: flex; align-items: flex-start; gap: 16px; }
.expect-step-num {
  flex-shrink: 0; width: 32px; height: 32px; border-radius: 50%;
  background: var(--forest); color: var(--cream);
  display: flex; align-items: center; justify-content: center;
  font-size: 14px; font-weight: 700;
}
.expect-step h4 { font-size: 15px; font-weight: 700; color: var(--forest); margin-bottom: 4px; }
.expect-step p { font-size: 14px; color: var(--text-light); line-height: 1.6; }
```

- [ ] **Step 2: Add "What to Expect" HTML**

Two cards: In-Person (map-pin icon) and Online (monitor icon). Each has 5 numbered steps describing the first session experience.

```html
<section class="expect" id="expect">
  <div class="container">
    <div class="expect-header">
      <p class="section-label reveal">Your First Session</p>
      <h2 class="section-heading reveal reveal-delay-1">What to <em>Expect</em></h2>
      <p class="section-sub reveal reveal-delay-2">Not sure what a session looks like? Here's a step-by-step walkthrough so you know exactly what you're signing up for.</p>
    </div>
    <div class="expect-grid">
      <div class="expect-card reveal">
        <div class="expect-card-header">
          <div class="expect-card-icon">
            <svg viewBox="0 0 24 24" fill="none" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M20 10c0 6-8 12-8 12s-8-6-8-12a8 8 0 0 1 16 0Z"/><circle cx="12" cy="10" r="3"/></svg>
          </div>
          <div>
            <h3>In-Person Training</h3>
            <p>DFW Metroplex</p>
          </div>
        </div>
        <div class="expect-steps">
          <div class="expect-step">
            <div class="expect-step-num">1</div>
            <div>
              <h4>Welcome & Goal Discussion</h4>
              <p>We sit down, get to know each other, and talk about what you want to achieve — body, mind, and spirit.</p>
            </div>
          </div>
          <div class="expect-step">
            <div class="expect-step-num">2</div>
            <div>
              <h4>Movement Assessment</h4>
              <p>A simple walkthrough of basic movements to see where you're at. No judgment — just understanding your starting point.</p>
            </div>
          </div>
          <div class="expect-step">
            <div class="expect-step-num">3</div>
            <div>
              <h4>Customized Workout</h4>
              <p>We jump into a session tailored to your level. You'll leave knowing exactly what training with FnFit feels like.</p>
            </div>
          </div>
          <div class="expect-step">
            <div class="expect-step-num">4</div>
            <div>
              <h4>Cool-Down & Reflection</h4>
              <p>We close with stretching and a moment of prayer or reflection — grounding the work you just put in.</p>
            </div>
          </div>
          <div class="expect-step">
            <div class="expect-step-num">5</div>
            <div>
              <h4>Your Game Plan</h4>
              <p>You leave with a clear picture of what's next — your plan, your pace, your path forward.</p>
            </div>
          </div>
        </div>
      </div>
      <div class="expect-card reveal reveal-delay-1">
        <div class="expect-card-header">
          <div class="expect-card-icon">
            <svg viewBox="0 0 24 24" fill="none" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect width="20" height="14" x="2" y="3" rx="2"/><line x1="8" x2="16" y1="21" y2="21"/><line x1="12" x2="12" y1="17" y2="21"/></svg>
          </div>
          <div>
            <h3>Online Training</h3>
            <p>Train from Anywhere</p>
          </div>
        </div>
        <div class="expect-steps">
          <div class="expect-step">
            <div class="expect-step-num">1</div>
            <div>
              <h4>Video Intro Call</h4>
              <p>We connect face-to-face on video to meet, vibe, and make sure we're a great fit for each other.</p>
            </div>
          </div>
          <div class="expect-step">
            <div class="expect-step-num">2</div>
            <div>
              <h4>Fitness Goals & History</h4>
              <p>We dig into your goals, past experience, schedule, and any limitations so your plan is built around your real life.</p>
            </div>
          </div>
          <div class="expect-step">
            <div class="expect-step-num">3</div>
            <div>
              <h4>Custom Plan Delivered</h4>
              <p>You receive a personalized workout plan designed for your goals, equipment access, and fitness level.</p>
            </div>
          </div>
          <div class="expect-step">
            <div class="expect-step-num">4</div>
            <div>
              <h4>First Guided Session</h4>
              <p>We walk through the first workout together on video — real-time coaching, form checks, and encouragement.</p>
            </div>
          </div>
          <div class="expect-step">
            <div class="expect-step-num">5</div>
            <div>
              <h4>Weekly Accountability</h4>
              <p>Ongoing check-ins to track progress, adjust the plan, and keep you motivated and on track.</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 3: Verify What to Expect section**

Check: two white cards side by side, numbered steps with forest green circles, card headers with SVG icons, hover lift effect.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add What to Expect section replacing testimonials"
```

---

### Task 7: Contact Section with Mailto Form

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add contact section CSS**

```css
/* ─── CONTACT ─── */
.contact { background: var(--cream-dark); position: relative; overflow: hidden; }
.contact::before {
  content: ''; position: absolute; inset: 0;
  background:
    radial-gradient(ellipse 40% 50% at 10% 50%, rgba(43, 74, 62, 0.03), transparent),
    radial-gradient(ellipse 40% 50% at 90% 50%, rgba(200, 150, 62, 0.04), transparent);
}
.contact-wrapper {
  position: relative; display: grid; grid-template-columns: 1fr 1fr;
  gap: 80px; align-items: start;
}
.contact-info { padding-top: 20px; }
.contact-info .section-sub { margin-bottom: 48px; }
.contact-methods { display: flex; flex-direction: column; gap: 24px; }
.contact-method { display: flex; align-items: center; gap: 18px; }
.contact-method-icon {
  width: 52px; height: 52px; border-radius: 14px; background: var(--white);
  display: flex; align-items: center; justify-content: center;
  border: 1px solid rgba(43, 74, 62, 0.06); flex-shrink: 0;
}
.contact-method-icon svg { width: 22px; height: 22px; stroke: var(--gold); }
.contact-method-label {
  font-size: 13px; color: var(--text-light); text-transform: uppercase;
  letter-spacing: 1px; font-weight: 600;
}
.contact-method-value { font-size: 16px; color: var(--forest); font-weight: 600; margin-top: 2px; }
.contact-method-value a { color: inherit; text-decoration: none; }
.contact-method-value a:hover { color: var(--gold); }
.contact-form-card {
  background: var(--white); border-radius: 24px; padding: 48px;
  box-shadow: 0 20px 80px rgba(43, 74, 62, 0.06);
  border: 1px solid rgba(43, 74, 62, 0.05);
}
.contact-form-card h3 {
  font-family: 'Fraunces', serif; font-size: 26px; font-weight: 700;
  color: var(--forest); margin-bottom: 8px;
}
.contact-form-card > p { font-size: 14px; color: var(--text-light); margin-bottom: 32px; }
.form-group { margin-bottom: 20px; }
.form-group label {
  display: block; font-size: 13px; font-weight: 600;
  color: var(--forest); margin-bottom: 8px; letter-spacing: 0.3px;
}
.form-group input,
.form-group select,
.form-group textarea {
  width: 100%; padding: 14px 18px;
  border: 1.5px solid rgba(43, 74, 62, 0.12); border-radius: 12px;
  font-family: 'Plus Jakarta Sans', sans-serif; font-size: 15px;
  color: var(--text); background: var(--cream); transition: all 0.3s; outline: none;
}
.form-group input:focus,
.form-group select:focus,
.form-group textarea:focus {
  border-color: var(--gold);
  box-shadow: 0 0 0 4px rgba(200, 150, 62, 0.1); background: var(--white);
}
.form-group textarea { resize: vertical; min-height: 100px; }
.form-group select {
  cursor: pointer; appearance: none;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='12' viewBox='0 0 12 12'%3E%3Cpath d='M6 8L1 3h10z' fill='%232B4A3E'/%3E%3C/svg%3E");
  background-repeat: no-repeat; background-position: right 16px center;
}
.form-row { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; }
.btn-submit {
  width: 100%; padding: 18px; background: var(--forest); color: var(--cream);
  border: none; border-radius: 14px;
  font-family: 'Plus Jakarta Sans', sans-serif; font-size: 16px; font-weight: 700;
  cursor: pointer; transition: all 0.35s; margin-top: 8px; letter-spacing: 0.3px;
}
.btn-submit:hover {
  background: var(--gold); color: var(--forest-deep);
  transform: translateY(-2px); box-shadow: 0 12px 40px rgba(200, 150, 62, 0.3);
}
```

- [ ] **Step 2: Add contact section HTML with SVG icons and mailto form**

The form submit handler builds a mailto link with the form data in the body. SVG icons for phone, mail, and map-pin replace emoji.

```html
<section class="contact" id="contact">
  <div class="container">
    <div class="contact-wrapper">
      <div class="contact-info">
        <p class="section-label reveal">Get Started</p>
        <h2 class="section-heading reveal reveal-delay-1">Your Journey<br>Begins <em>Today</em></h2>
        <p class="section-sub reveal reveal-delay-2">Book a free consultation and let's talk about your goals, your vision, and how FnFit can help you get there — body, mind, and spirit.</p>
        <div class="contact-methods reveal reveal-delay-3">
          <div class="contact-method">
            <div class="contact-method-icon">
              <svg viewBox="0 0 24 24" fill="none" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07 19.5 19.5 0 0 1-6-6 19.79 19.79 0 0 1-3.07-8.67A2 2 0 0 1 4.11 2h3a2 2 0 0 1 2 1.72 12.84 12.84 0 0 0 .7 2.81 2 2 0 0 1-.45 2.11L8.09 9.91a16 16 0 0 0 6 6l1.27-1.27a2 2 0 0 1 2.11-.45 12.84 12.84 0 0 0 2.81.7A2 2 0 0 1 22 16.92z"/></svg>
            </div>
            <div>
              <div class="contact-method-label">Phone</div>
              <div class="contact-method-value"><a href="tel:6823064875">(682) 306-4875</a></div>
            </div>
          </div>
          <div class="contact-method">
            <div class="contact-method-icon">
              <svg viewBox="0 0 24 24" fill="none" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect width="20" height="16" x="2" y="4" rx="2"/><path d="m22 7-8.97 5.7a1.94 1.94 0 0 1-2.06 0L2 7"/></svg>
            </div>
            <div>
              <div class="contact-method-label">Email</div>
              <div class="contact-method-value"><a href="mailto:chiquitawhite@icloud.com">chiquitawhite@icloud.com</a></div>
            </div>
          </div>
          <div class="contact-method">
            <div class="contact-method-icon">
              <svg viewBox="0 0 24 24" fill="none" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M20 10c0 6-8 12-8 12s-8-6-8-12a8 8 0 0 1 16 0Z"/><circle cx="12" cy="10" r="3"/></svg>
            </div>
            <div>
              <div class="contact-method-label">Location</div>
              <div class="contact-method-value">DFW Metroplex, TX</div>
            </div>
          </div>
        </div>
      </div>
      <div class="contact-form-card reveal reveal-delay-2">
        <h3>Book a Free Consultation</h3>
        <p>Fill out the form and Chiquita will reach out within 24 hours.</p>
        <form id="contactForm">
          <div class="form-row">
            <div class="form-group">
              <label for="firstName">First Name</label>
              <input type="text" id="firstName" name="firstName" placeholder="Your first name" required>
            </div>
            <div class="form-group">
              <label for="lastName">Last Name</label>
              <input type="text" id="lastName" name="lastName" placeholder="Your last name" required>
            </div>
          </div>
          <div class="form-group">
            <label for="email">Email</label>
            <input type="email" id="email" name="email" placeholder="your@email.com" required>
          </div>
          <div class="form-group">
            <label for="phone">Phone</label>
            <input type="tel" id="phone" name="phone" placeholder="(xxx) xxx-xxxx">
          </div>
          <div class="form-group">
            <label for="interest">I'm Interested In</label>
            <select id="interest" name="interest">
              <option value="" disabled selected>Select a program</option>
              <option value="Online Training">Online Training</option>
              <option value="In-Person Training (DFW)">In-Person Training (DFW)</option>
              <option value="Faith & Wellness Program">Faith & Wellness Program</option>
              <option value="Not Sure Yet">Not Sure Yet — Let's Talk</option>
            </select>
          </div>
          <div class="form-group">
            <label for="message">Tell Us About Your Goals</label>
            <textarea id="message" name="message" placeholder="What are you hoping to achieve?"></textarea>
          </div>
          <button type="submit" class="btn-submit">Book My Free Consultation</button>
        </form>
      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add contact section with SVG icons and mailto form"
```

---

### Task 8: Footer

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add footer CSS**

```css
/* ─── FOOTER ─── */
footer { background: var(--forest-deep); padding: 64px 0 32px; }
.footer-top {
  display: flex; justify-content: space-between; align-items: start;
  padding-bottom: 48px; border-bottom: 1px solid rgba(251, 245, 235, 0.08);
  gap: 48px; flex-wrap: wrap;
}
.footer-brand .nav-logo { display: inline-block; margin-bottom: 16px; font-size: 32px; }
.footer-tagline {
  font-size: 14px; color: rgba(251, 245, 235, 0.45);
  max-width: 280px; line-height: 1.6;
}
.footer-links { display: flex; gap: 64px; }
.footer-links h4 {
  font-size: 13px; font-weight: 700; text-transform: uppercase;
  letter-spacing: 1.5px; color: rgba(251, 245, 235, 0.4); margin-bottom: 20px;
}
.footer-links ul { list-style: none; display: flex; flex-direction: column; gap: 12px; }
.footer-links a {
  font-size: 15px; color: rgba(251, 245, 235, 0.65);
  text-decoration: none; transition: color 0.3s;
}
.footer-links a:hover { color: var(--gold-light); }
.footer-bottom {
  padding-top: 32px; display: flex; justify-content: space-between; align-items: center;
}
.footer-bottom p { font-size: 13px; color: rgba(251, 245, 235, 0.3); }
.footer-bottom a { color: rgba(251, 245, 235, 0.4); text-decoration: none; }
.footer-bottom a:hover { color: var(--gold-light); }
```

- [ ] **Step 2: Add footer HTML**

No social links (she doesn't have active accounts yet). Just brand, nav, and credit.

```html
<footer>
  <div class="container">
    <div class="footer-top">
      <div class="footer-brand">
        <a href="#" class="nav-logo">Fn<span>Fit</span></a>
        <p class="footer-tagline">Transform lives one smile at a time through health and wellness. Faith-based fitness in the DFW metroplex.</p>
      </div>
      <div class="footer-links">
        <div>
          <h4>Navigate</h4>
          <ul>
            <li><a href="#about">About</a></li>
            <li><a href="#programs">Programs</a></li>
            <li><a href="#expect">What to Expect</a></li>
            <li><a href="#contact">Contact</a></li>
          </ul>
        </div>
        <div>
          <h4>Contact</h4>
          <ul>
            <li><a href="tel:6823064875">(682) 306-4875</a></li>
            <li><a href="mailto:chiquitawhite@icloud.com">chiquitawhite@icloud.com</a></li>
          </ul>
        </div>
      </div>
    </div>
    <div class="footer-bottom">
      <p>&copy; 2026 FnFit. All rights reserved.</p>
      <p>Website by <a href="https://www.taylormadecreative.net" target="_blank" rel="noopener">Taylormade Creative</a></p>
    </div>
  </div>
</footer>
```

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add footer with brand, nav, and TC credit"
```

---

### Task 9: Responsive Breakpoints

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add responsive CSS**

Add before the closing `</style>` tag.

```css
/* ─── RESPONSIVE ─── */
@media (max-width: 1024px) {
  .services-grid { grid-template-columns: 1fr; max-width: 480px; margin: 0 auto; }
  .expect-grid { grid-template-columns: 1fr; }
  .about-grid { grid-template-columns: 1fr; gap: 48px; }
  .about-visual { height: 380px; }
  .contact-wrapper { grid-template-columns: 1fr; gap: 48px; }
  .hero-shape { display: none; }
  .hero-stats { gap: 32px; }
  .footer-links { gap: 40px; }
}
@media (max-width: 768px) {
  section { padding: 80px 0; }
  .nav-links {
    display: none; position: fixed; top: 0; left: 0; right: 0; bottom: 0;
    background: var(--cream); flex-direction: column;
    justify-content: center; align-items: center; gap: 28px; z-index: 105;
  }
  .nav-links.open { display: flex; }
  .nav-links a { font-size: 20px; }
  .nav-links .nav-cta { padding: 16px 36px; font-size: 18px; }
  .mobile-toggle { display: block; }
  .hero .container { padding-top: 100px; }
  .hero-stats { flex-direction: column; gap: 20px; }
  .form-row { grid-template-columns: 1fr; }
  .contact-form-card { padding: 32px 24px; }
  .footer-top { flex-direction: column; }
  .footer-links { flex-direction: column; gap: 32px; }
  .footer-bottom { flex-direction: column; gap: 12px; text-align: center; }
}
```

- [ ] **Step 2: Verify mobile layout**

Open in browser, use DevTools responsive mode at 375px and 768px widths. Check: hamburger visible, single-column layouts, hero stats stack vertically, form fields full-width.

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add responsive breakpoints for tablet and mobile"
```

---

### Task 10: JavaScript (Scroll Reveal, Nav, Mobile Menu, Mailto Form)

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add JavaScript before closing `</body>`**

Fixes from review: smooth scroll excludes bare `href="#"` links. Form submit builds a mailto link with form data in the body.

```html
<script>
  // Scroll reveal
  const reveals = document.querySelectorAll('.reveal');
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) entry.target.classList.add('visible');
    });
  }, { threshold: 0.15, rootMargin: '0px 0px -40px 0px' });
  reveals.forEach(el => observer.observe(el));

  // Nav scroll
  const nav = document.querySelector('nav');
  window.addEventListener('scroll', () => {
    nav.classList.toggle('scrolled', window.scrollY > 60);
  });

  // Mobile menu
  const toggle = document.getElementById('mobileToggle');
  const navLinks = document.getElementById('navLinks');
  toggle.addEventListener('click', () => {
    toggle.classList.toggle('active');
    navLinks.classList.toggle('open');
  });
  navLinks.querySelectorAll('a').forEach(link => {
    link.addEventListener('click', () => {
      toggle.classList.remove('active');
      navLinks.classList.remove('open');
    });
  });

  // Smooth scroll (excludes bare # links)
  document.querySelectorAll('a[href^="#"]:not([href="#"])').forEach(anchor => {
    anchor.addEventListener('click', function(e) {
      e.preventDefault();
      const target = document.querySelector(this.getAttribute('href'));
      if (target) target.scrollIntoView({ behavior: 'smooth', block: 'start' });
    });
  });

  // Mailto form handler
  document.getElementById('contactForm').addEventListener('submit', function(e) {
    e.preventDefault();
    const f = Object.fromEntries(new FormData(this));
    const subject = encodeURIComponent('Free Consultation Request from ' + (f.firstName || '') + ' ' + (f.lastName || ''));
    const body = encodeURIComponent(
      'Name: ' + (f.firstName || '') + ' ' + (f.lastName || '') + '\n' +
      'Email: ' + (f.email || '') + '\n' +
      'Phone: ' + (f.phone || '') + '\n' +
      'Interested In: ' + (f.interest || 'Not specified') + '\n\n' +
      'Goals:\n' + (f.message || 'No message provided')
    );
    window.location.href = 'mailto:chiquitawhite@icloud.com?subject=' + subject + '&body=' + body;
  });
</script>
</body>
</html>
```

- [ ] **Step 2: Test all interactions**

1. Scroll down — nav gets blur background
2. Click "View Programs" — smooth scrolls to programs
3. Click hamburger on mobile — overlay opens, link click closes it
4. Fill out contact form, submit — mailto opens with form data in email body
5. Verify logo click (bare `#`) does NOT preventDefault

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add JS - scroll reveal, nav, mobile menu, mailto form handler"
```

---

### Task 11: Deploy to GitHub Pages

**Files:**
- Modify: repository setup

- [ ] **Step 1: Create GitHub repo**

```bash
cd /Users/nelsontaylor/Documents/fnfit-website
gh repo create fnfit-website --public --source=. --push
```

- [ ] **Step 2: Enable GitHub Pages**

```bash
gh api repos/nelsontaylor/fnfit-website/pages -X POST -f source.branch=main -f source.path=/
```

If that fails (Pages API can be finicky), enable manually: repo Settings > Pages > Source: main branch, root folder.

- [ ] **Step 3: Verify deployment**

Wait 1-2 minutes, then check the live URL:

```bash
gh api repos/nelsontaylor/fnfit-website/pages --jq '.html_url'
```

Expected: `https://nelsontaylor.github.io/fnfit-website/`

- [ ] **Step 4: Commit any final changes**

```bash
git add -A
git commit -m "chore: deploy to GitHub Pages"
git push
```

---

### Task 12: 4-Agent Review Panel

After deployment, run the mandatory 4-agent review panel (Senior Web Developer, Senior Art Director, Senior Marketing Director, Senior UI/UX Designer) against the final `index.html`.

- [ ] **Step 1: Deploy all 4 reviewers in a single agent dispatch**

Each reviewer grades A-F, lists top 3 strengths, top 3 issues with line references and specific fixes.

- [ ] **Step 2: Compile combined priority fix list ranked by impact**

- [ ] **Step 3: Fix ALL issues before marking complete**

- [ ] **Step 4: Final commit and push**

```bash
git add index.html
git commit -m "fix: address 4-agent review feedback"
git push
```
