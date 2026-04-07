# BabyAndPalm Website Design Spec
**Date:** 2026-04-07  
**Business:** Baby & Palm (babyandpalm.co.uk — domain not yet purchased)  
**Instructor:** Katherine Rivers  
**Location:** Petersfield, Hampshire — serving the South Downs area

---

## Overview

A single-page static website for BabyAndPalm, a baby massage business run by Katherine Rivers. The site is inspired by redkitepilates.co.uk: clean, elegant, single scrollable page with sticky navigation anchoring to sections. Built as a single `index.html` file with all CSS embedded, hosted on GitHub Pages initially.

---

## Technology

- **Stack:** Plain HTML + CSS + minimal vanilla JS (no frameworks, no build tools)
- **File structure:** Single `index.html`
- **Hosting:** GitHub Pages (initially), migrate to babyandpalm.co.uk when domain is purchased
- **Fonts:** Google Fonts — Cormorant Garamond (serif, headings) + Lato (sans-serif, body)
- **Images:** `logo.png` (hands/heart icon), `background.heic` → converted to `background.jpg`, placeholder images from Unsplash (free to use) for About Me and Baby Massage sections

---

## Editability

The top of the `<style>` block contains a clearly marked `/* === EDIT ME === */` section with CSS custom properties:

```css
/* === EDIT ME: Colors === */
--accent: #7a9e7e;         /* sage green — change this to update all accent colors */
--accent-dark: #5a7d5e;
--text: #3a3a3a;
--bg: #ffffff;

/* === EDIT ME: Fonts === */
--font-heading: 'Cormorant Garamond', serif;
--font-body: 'Lato', sans-serif;
```

Every piece of body copy is preceded by an HTML comment: `<!-- EDIT: [description] -->`.  
Every image `src` attribute has an inline comment marking it as replaceable.

---

## Navigation

**Desktop:** Sticky top bar. Logo (hands/heart icon) on the left. Nav links on the right, separated by thin sage-green vertical dividers:

> Welcome | About Me | Baby Massage | Courses | Contact

Each link is a smooth-scroll anchor (`#welcome`, `#about`, `#massage`, `#courses`, `#contact`).

**Mobile:** Nav bar collapses. Hamburger icon (three lines, top right). Tapping opens a full-width dropdown overlay with the same links stacked vertically. Implemented with a CSS class toggle via ~10 lines of vanilla JS.

---

## Sections

### 1. Welcome (Hero)
- Full-width background: `background.jpg` with a dark overlay for text legibility
- Semi-transparent white content box (matching mobile reference screenshot)
- **Heading:** "Welcome" in Cormorant Garamond, sage green
- **Body copy (placeholder):** ~3 short paragraphs introducing Baby & Palm and the South Downs/Petersfield setting

### 2. About Me
- Two-column layout: text left, image right (stacks vertically on mobile)
- **Heading:** "About Me"
- **Body copy (placeholder):** ~3 paragraphs. Key facts to include:
  - Katherine Rivers, registered paediatric nurse with many years' experience
  - IAIM (International Association of Infant Massage) certified instructor
  - Trained by Baby & Child Massage (babyandchildmassage.co.uk)
  - Personal warmth, connection to local community
- **Image:** Placeholder for Katherine's photo (clearly marked)

### 3. Baby Massage
- Two-column layout: image left, text right (reversed from About Me)
- **Heading:** "Baby Massage"
- **Body copy (placeholder):** What baby massage is, the techniques used (drawing from IAIM: Indian massage, Swedish massage, reflexology, yoga), benefits: bonding, attachment, postnatal wellbeing, early development
- **Image:** Placeholder Unsplash image (baby massage scene)

### 4. Courses
- Single wide column or simple card layout
- **Heading:** "Courses"
- **Body copy (placeholder):** 
  - 5-week course: 5 × 90-minute sessions
  - Small friendly groups — a chance to meet other local parents
  - 1:1 sessions also available
  - Contact prompt: "Get in touch to find out more" linking to `#contact`
- No pricing listed (to be confirmed by Katherine)

### 5. Contact
- Full-width section with `background.jpg` overlay (semi-transparent, matching reference footer style)
- **Heading:** "Contact Me" in sage green
- **Email:** `contact@babyandpalm.co.uk` as a `mailto:` link
- **Location:** Petersfield, Hampshire
- Small footer line below: "Terms & Conditions" (placeholder — links to a `#` for now)

---

## Responsive Behaviour

- Desktop (>768px): Two-column layouts, horizontal sticky nav
- Mobile (≤768px): Single column, hamburger nav, hero text box full width

---

## Assets

| File | Purpose |
|------|---------|
| `logo.png` | Hands/heart line-art icon — used in nav bar |
| `background.jpg` | Converted from `background.heic` — hero + contact overlay |
| `images/katherine.jpg` | Placeholder marker — to be supplied by Katherine |
| Unsplash URLs | Placeholder images for Baby Massage section |

---

## Out of Scope

- Booking system (contact via email only)
- Google Reviews widget (present on reference site — not included)
- Social media links (none confirmed)
- Terms & Conditions page content (placeholder link only)
- Pricing (to be confirmed)
