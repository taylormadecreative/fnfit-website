# FnFit Landing Page — Design Spec

**Date:** 2026-03-29
**Client:** Chiquita White — FnFit (Faith & Fitness)
**Built by:** Taylormade Creative (Nelson Taylor)
**Deploy:** GitHub Pages

---

## Overview

Single-page landing page for FnFit, a faith-based personal training brand in DFW, Texas. Chiquita offers online and in-person training. She is just starting out with no brand assets, no logo, no photos, and no established pricing. The page must stand entirely on typography, color, and layout — no images.

The goal is lead generation via free consultation requests (mailto link).

## Brand Context

- **Name:** FnFit (Faith & Fitness)
- **Tagline:** "Transform lives one smile at a time through health and wellness"
- **Services:** Online personal training, in-person personal training (DFW), faith & wellness coaching
- **USP:** Faith-based approach — no intimidation, wellness + empowerment, "your body is a temple"
- **Stage:** Brand new. No clients, no testimonials, no brand assets.
- **Contact:** chiquitawhite@icloud.com / (682) 306-4875
- **Location:** DFW Metroplex, Texas
- **Referred by:** Elliot Taylor

## Design Direction

**Approach: Warm Editorial** — Typography-forward, no images. Large Fraunces serif headings paired with Plus Jakarta Sans body text. The page should feel like a wellness magazine editorial: elevated, warm, approachable. Fitness energy without gym-bro intensity. Faith-inspired without being churchy.

### Color Palette

| Token | Hex | Usage |
|---|---|---|
| `--forest` | `#2B4A3E` | Primary brand color, nav, buttons, headings |
| `--forest-deep` | `#1A3329` | Dark section backgrounds (programs) |
| `--gold` | `#C8963E` | Accent, CTAs, icons, emphasis |
| `--gold-light` | `#E8C06A` | Light gold for dark backgrounds |
| `--cream` | `#FBF5EB` | Page background |
| `--cream-dark` | `#F0E6D4` | Alternate section background |
| `--sage` | `#A8B5A0` | Subtle accents, value prop icon backgrounds |
| `--sage-light` | `#D4DDD0` | Light sage fills |
| `--text` | `#2A2118` | Body text |
| `--text-light` | `#6B5F54` | Secondary text |

### Typography

- **Display:** Fraunces (Google Fonts) — weights: 400 italic, 700 regular
- **Body:** Plus Jakarta Sans (Google Fonts) — weights: 300, 400, 500, 600, 700
- **Load strategy:** Preload critical weights, `display=swap`, reduce total weights loaded

### Icons

All icons are inline SVGs from Lucide icon set. No emoji anywhere on the page. SVGs are styled with `stroke` or `fill` using CSS custom properties to match the palette.

## Page Sections

### 1. Navigation (sticky)

- **Left:** "FnFit" wordmark in Fraunces 800, `Fn` in forest, `Fit` in gold
- **Right:** Text links (About, Programs, What to Expect, Contact) + "Free Consultation" pill button (forest background, cream text, gold on hover)
- **Scroll behavior:** Transparent initially, blur glass background + shadow on scroll (60px threshold)
- **Mobile:** Hamburger toggle, full-screen overlay menu, auto-close on link click

### 2. Hero

- **Background:** Forest-deep to forest gradient (165deg) with subtle radial gold highlights
- **Bottom edge:** Cream elliptical clip-path for organic transition
- **Badge:** "Faith + Fitness + Purpose" pill with pulsing gold dot
- **Headline:** Fraunces 700, clamp(48px, 7vw, 80px). Text: `Transform Lives, One Smile at a Time` with "Smile" in gold italic
- **Subtext:** Plus Jakarta 300, 18px. Describes faith-based personal training.
- **CTAs:** Two buttons:
  - "Start Your Journey" — gold fill, links to `mailto:chiquitawhite@icloud.com`
  - "View Programs" — outline, scrolls to programs section
- **Stats row:** Three items below CTAs, separated by top border:
  - "1:1 / Personalized Coaching"
  - "Flexible / Online or In-Person"
  - "Free / First Consultation"
- **Desktop decorative element:** Morphing organic shape with subtle gold tint (hidden on mobile). No image, no text content — purely atmospheric.

### 3. About / Mission

- **Layout:** Two-column grid (1fr 1fr), 80px gap
- **Left column:** Dark green card (forest gradient), diagonal line pattern overlay at 6% opacity
  - SVG dove/heart icon in gold-tinted circle
  - Scripture quote: "For physical training is of some value, but godliness has value for all things." — 1 Timothy 4:8
  - Fraunces italic, cream text
- **Right column:**
  - Section label: "OUR MISSION" (gold, 12px, tracked)
  - Heading: "More Than Fitness. It's a *Calling*" (Calling in gold italic)
  - Body copy: Explains faith-based approach, body as temple, building confidence
  - Three value props with SVG icons on sage-light backgrounds:
    1. **Faith-Centered Approach** — sessions rooted in encouragement and scripture
    2. **Meet You Where You Are** — no judgment, no intimidation
    3. **Whole-Person Wellness** — body, mind, spirit

### 4. Programs (dark section)

- **Background:** Forest-deep with subtle radial gold highlight (top-right, 6% opacity)
- **Header:** Centered. "PROGRAMS" label + "Train Your Way, On *Your Terms*" heading + subtext
- **Cards:** 3-column grid (stacks to 1 column on mobile), max-width 480px centered when stacked
  - Each card: dark glass background (cream 4% opacity), 1px border, 20px radius
  - Gold top-line accent on hover
  - SVG icon (not emoji) in gold-tinted square
  - Fraunces heading, description paragraph, feature checklist with gold checkmarks
  - **No pricing** on any card
  - Card 1: **Online Training** — custom plans, video coaching, weekly check-ins, nutrition guidance
  - Card 2: **In-Person Training** — 1-on-1 sessions, form coaching, customized to level, DFW locations
  - Card 3: **Faith & Wellness** — devotional-led, mindset coaching, community support, goal-setting with purpose

### 5. What to Expect (replaces testimonials)

- **Background:** Cream
- **Header:** Centered. "YOUR FIRST SESSION" label + "What to Expect" heading + subtext about removing anxiety
- **Layout:** Two-column card layout
  - **Card 1: In-Person Training**
    - Step-by-step walkthrough of first session
    - Steps: Welcome & goal discussion, movement assessment, customized workout, cool-down & prayer/reflection, game plan for next session
  - **Card 2: Online Training**
    - Step-by-step walkthrough of first virtual session
    - Steps: Video intro call, fitness goals & history, custom plan delivered, first guided session, weekly accountability check-in
- **Card style:** White cards on cream background, subtle border, rounded corners, hover lift

### 6. Contact

- **Background:** Cream-dark
- **Layout:** Two-column grid
- **Left column:**
  - "GET STARTED" label + "Your Journey Begins *Today*" heading
  - Body copy about booking free consultation
  - Contact methods with SVG icons:
    - Phone: (682) 306-4875 (tel: link)
    - Email: chiquitawhite@icloud.com (mailto: link)
    - Location: DFW Metroplex, TX
- **Right column:** Contact form card (white, rounded, shadow)
  - Heading: "Book a Free Consultation"
  - Subtext: "Fill out the form and Chiquita will reach out within 24 hours."
  - Fields: First Name + Last Name (2-col), Email, Phone, Interest (select dropdown: Online / In-Person / Faith & Wellness / Not Sure), Message (textarea)
  - **Submit behavior:** `mailto:chiquitawhite@icloud.com` with form data formatted in the email body. Button text: "Book My Free Consultation"
  - Focus states: gold border + gold glow shadow

### 7. Footer

- **Background:** Forest-deep
- **Top row:** Three-column flex
  - FnFit wordmark + tagline
  - Navigate links (About, Programs, What to Expect, Contact)
  - Connect links (only if she has active social accounts — otherwise omit)
- **Bottom row:** Copyright 2026 FnFit + "Website by Taylormade Creative" (linked)

## Technical Requirements

### Performance
- Single HTML file, no external dependencies except Google Fonts
- Optimized font load: preload critical weights, reduce from 12 weights to essential 6-7
- No images to optimize (none used)
- Inline CSS and JS — zero additional network requests

### Accessibility
- Semantic HTML: `<nav>`, `<section>`, `<footer>`, proper heading hierarchy
- All form inputs have associated `<label>` elements
- `aria-label` on mobile toggle button
- Color contrast ratios meet WCAG AA (forest on cream, gold on forest-deep)
- `<noscript>` fallback for reveal animations — all content visible without JS
- Keyboard-navigable menu and form

### SEO / Social
- `<title>`: "FnFit — Transform Lives One Smile at a Time"
- `<meta name="description">`: Faith-based personal training, DFW area
- Open Graph tags: `og:title`, `og:description`, `og:type`
- Twitter card: `twitter:card` summary

### Animations
- Scroll-reveal: opacity 0 → 1, translateY(40px → 0), 0.8s cubic-bezier easing
- Staggered delays: 0.1s increments (reveal-delay-1 through reveal-delay-4)
- IntersectionObserver: threshold 0.15, rootMargin -40px bottom
- Nav: background transition on scroll (transparent → blur glass)
- Morphing organic shape in hero (CSS animation, 15s loop, desktop only)
- Button hover: translateY(-2px) + box-shadow
- Form focus: border-color + box-shadow transition

### Code Quality (fixes from 4-agent review)
- No `!important` — use proper CSS specificity
- Smooth scroll selector excludes bare `href="#"` links
- `<noscript>` fallback for `.reveal` elements
- SVG icons replace all emoji throughout

## What This Page Does NOT Include

- Images or photo placeholders (by client request)
- Pricing (client has not set pricing yet)
- Testimonials (brand new, no clients yet)
- Blog or content section
- Booking/scheduling integration
- Payment processing
- Analytics tracking (can be added later)
- Logo mark (text wordmark only)

## Deployment

- **Host:** GitHub Pages
- **Repo:** To be created (fnfit-website or similar)
- **Structure:** `index.html` at repo root
- **Domain:** GitHub Pages default URL initially; custom domain later if needed
