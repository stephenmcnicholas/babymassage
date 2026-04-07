# BabyAndPalm Website Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a single-page static website for BabyAndPalm (baby massage business, Petersfield, Hampshire) as one `index.html` file with embedded CSS and minimal JS, ready to host on GitHub Pages.

**Architecture:** Everything lives in `index.html` — a clearly commented `/* === EDIT ME === */` CSS variables block at the top controls all colours/fonts, followed by layout CSS, then semantic HTML sections. A small inline `<script>` handles the mobile hamburger toggle. Images live in an `images/` folder alongside the file.

**Tech Stack:** Plain HTML5, CSS3 (custom properties, flexbox, media queries), vanilla JS (~15 lines), Google Fonts (Cormorant Garamond + Lato).

---

## File Map

| File | Action | Responsibility |
|------|--------|---------------|
| `index.html` | Create | Entire site — HTML, CSS, JS |
| `images/background.jpg` | Create (convert from `background.heic`) | Hero + contact section overlay |
| `logo.png` | Existing | Nav bar logo icon |
| `images/katherine-placeholder.jpg` | Unsplash URL reference | About Me section (marked for replacement) |
| `images/baby-massage-placeholder.jpg` | Unsplash URL reference | Baby Massage section (marked for replacement) |

---

## Task 1: Convert background image and set up folder structure

**Files:**
- Create: `images/` directory
- Create: `images/background.jpg` (converted from `background.heic`)

- [ ] **Step 1: Convert background.heic to JPEG**

```bash
sips -s format jpeg background.heic --out images/background.jpg
```

Expected output: `images/background.jpg` created. Verify with `ls -lh images/`.

- [ ] **Step 2: Verify the image looks correct**

Open the file to confirm it's a valid landscape photo:
```bash
open images/background.jpg
```

- [ ] **Step 3: Commit**

```bash
git add images/background.jpg logo.png
git commit -m "chore: add converted background image and logo asset"
```

---

## Task 2: HTML skeleton + CSS variables block

**Files:**
- Create: `index.html`

- [ ] **Step 1: Create `index.html` with skeleton, Google Fonts, and the full CSS variables block**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Baby &amp; Palm | Infant Massage — Petersfield</title>
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:wght@400;600&family=Lato:wght@300;400;700&display=swap" rel="stylesheet" />
  <style>
    /* ============================================================
       === EDIT ME: Brand colours — change --accent to update   ===
       === the sage green across the entire site at once.       ===
       ============================================================ */
    :root {
      --accent:       #7a9e7e;   /* sage green */
      --accent-dark:  #5a7d5e;   /* darker shade for hover states */
      --accent-light: #e8f0e9;   /* very light tint for backgrounds */
      --text:         #3a3a3a;   /* main body text */
      --text-light:   #ffffff;   /* text on dark/image backgrounds */
      --bg:           #ffffff;   /* page background */
      --divider:      #7a9e7e;   /* nav separator colour */

      /* ============================================================
         === EDIT ME: Fonts                                       ===
         === heading font: elegant serif for titles              ===
         === body font: clean sans-serif for paragraphs          ===
         ============================================================ */
      --font-heading: 'Cormorant Garamond', Georgia, serif;
      --font-body:    'Lato', Arial, sans-serif;

      /* Spacing & sizing — safe to leave as-is */
      --nav-height:   70px;
      --section-pad:  80px;
      --max-width:    1100px;
    }

    /* === Reset & base === */
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    html { scroll-behavior: smooth; }
    body {
      font-family: var(--font-body);
      color: var(--text);
      background: var(--bg);
      font-size: 17px;
      line-height: 1.7;
    }
    img { max-width: 100%; display: block; }
    a { color: var(--accent-dark); text-decoration: underline; }
    a:hover { color: var(--accent); }
  </style>
</head>
<body>

  <!-- NAVIGATION -->
  <header id="site-nav"><!-- Task 3 --></header>

  <!-- SECTIONS -->
  <main>
    <section id="welcome"><!-- Task 4 --></section>
    <section id="about"><!-- Task 5 --></section>
    <section id="massage"><!-- Task 6 --></section>
    <section id="courses"><!-- Task 7 --></section>
    <section id="contact"><!-- Task 8 --></section>
  </main>

  <script>/* Task 9 */</script>
</body>
</html>
```

- [ ] **Step 2: Open in browser to verify it loads without errors**

```bash
open index.html
```

Expected: blank white page, no console errors.

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add HTML skeleton with CSS variables block"
```

---

## Task 3: Sticky navigation bar (desktop)

**Files:**
- Modify: `index.html` — replace `<header id="site-nav">` content and add nav CSS inside `<style>`

- [ ] **Step 1: Add nav CSS inside the `<style>` block (after the base styles)**

```css
/* === Navigation === */
#site-nav {
  position: sticky;
  top: 0;
  z-index: 100;
  background: var(--bg);
  height: var(--nav-height);
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 40px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.06);
}

.nav-logo {
  display: flex;
  align-items: center;
  gap: 12px;
  text-decoration: none;
}
.nav-logo img {
  height: 44px;
  width: auto;
}
.nav-logo span {
  font-family: var(--font-heading);
  font-size: 1.4rem;
  font-weight: 600;
  color: var(--accent-dark);
  letter-spacing: 0.03em;
}

.nav-links {
  display: flex;
  align-items: center;
  list-style: none;
  gap: 0;
}
.nav-links li {
  display: flex;
  align-items: center;
}
.nav-links li + li::before {
  content: '';
  display: inline-block;
  width: 1px;
  height: 18px;
  background: var(--divider);
  margin: 0 18px;
}
.nav-links a {
  font-family: var(--font-body);
  font-size: 0.95rem;
  font-weight: 400;
  color: var(--text);
  text-decoration: none;
  letter-spacing: 0.02em;
  transition: color 0.2s;
}
.nav-links a:hover { color: var(--accent); }

/* Hamburger — hidden on desktop */
.nav-hamburger {
  display: none;
  flex-direction: column;
  gap: 5px;
  cursor: pointer;
  background: none;
  border: none;
  padding: 8px;
}
.nav-hamburger span {
  display: block;
  width: 24px;
  height: 2px;
  background: var(--accent-dark);
  transition: all 0.3s;
}

/* Mobile nav overlay — hidden by default */
.nav-mobile {
  display: none;
}
```

- [ ] **Step 2: Replace the `<header>` placeholder with the nav HTML**

```html
<header id="site-nav">
  <a class="nav-logo" href="#welcome">
    <img src="logo.png" alt="Baby &amp; Palm logo" />
    <!-- EDIT: change the text below to update the site name in the nav -->
    <span>Baby &amp; Palm</span>
  </a>

  <ul class="nav-links" id="nav-links-desktop">
    <li><a href="#welcome">Welcome</a></li>
    <li><a href="#about">About Me</a></li>
    <li><a href="#massage">Baby Massage</a></li>
    <li><a href="#courses">Courses</a></li>
    <li><a href="#contact">Contact</a></li>
  </ul>

  <button class="nav-hamburger" id="nav-hamburger" aria-label="Open menu">
    <span></span><span></span><span></span>
  </button>
</header>

<!-- Mobile dropdown nav — toggled by JS -->
<nav class="nav-mobile" id="nav-mobile">
  <ul>
    <li><a href="#welcome" onclick="closeMobileNav()">Welcome</a></li>
    <li><a href="#about" onclick="closeMobileNav()">About Me</a></li>
    <li><a href="#massage" onclick="closeMobileNav()">Baby Massage</a></li>
    <li><a href="#courses" onclick="closeMobileNav()">Courses</a></li>
    <li><a href="#contact" onclick="closeMobileNav()">Contact</a></li>
  </ul>
</nav>
```

- [ ] **Step 3: Open in browser and verify**

```bash
open index.html
```

Expected: sticky nav bar with logo left, five links right, separated by thin sage-green lines.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add sticky desktop navigation bar"
```

---

## Task 4: Welcome / hero section

**Files:**
- Modify: `index.html` — replace `<section id="welcome">` content and add hero CSS

- [ ] **Step 1: Add hero CSS inside `<style>`**

```css
/* === Welcome / Hero === */
#welcome {
  position: relative;
  min-height: 90vh;
  display: flex;
  align-items: center;
  justify-content: center;
  background: url('images/background.jpg') center center / cover no-repeat;
}
#welcome::before {
  content: '';
  position: absolute;
  inset: 0;
  background: rgba(0,0,0,0.35);
}
.welcome-box {
  position: relative;
  z-index: 1;
  background: rgba(255,255,255,0.18);
  backdrop-filter: blur(2px);
  max-width: 620px;
  margin: 0 auto;
  padding: 50px 50px;
  text-align: center;
}
.welcome-box h1 {
  font-family: var(--font-heading);
  font-size: 3.5rem;
  font-weight: 600;
  color: var(--accent-light);
  margin-bottom: 24px;
  letter-spacing: 0.04em;
}
.welcome-box p {
  color: var(--text-light);
  font-size: 1.05rem;
  margin-bottom: 14px;
  line-height: 1.75;
}
```

- [ ] **Step 2: Replace the `<section id="welcome">` placeholder**

```html
<section id="welcome">
  <div class="welcome-box">
    <!-- EDIT: Welcome heading -->
    <h1>Welcome</h1>
    <!-- EDIT: Welcome paragraph 1 — introduce the business and location -->
    <p>At Baby &amp; Palm I offer warm, nurturing baby massage classes in the heart of the beautiful South Downs town of Petersfield, and across the surrounding Hampshire countryside.</p>
    <!-- EDIT: Welcome paragraph 2 — who is welcome / what to expect -->
    <p>Whether you are a first-time parent finding your feet, or looking to deepen the bond with your growing baby, you are very welcome here. Classes are small, friendly, and designed to fit around the reality of early parenthood.</p>
    <!-- EDIT: Welcome paragraph 3 — warmth / invitation -->
    <p>My aim is to give you and your baby a calm, joyful space — a little pocket of time each week that is just for the two of you.</p>
  </div>
</section>
```

- [ ] **Step 3: Verify in browser**

```bash
open index.html
```

Expected: full-height hero with background landscape photo, dark overlay, semi-transparent white box with text centred.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add welcome hero section"
```

---

## Task 5: About Me section

**Files:**
- Modify: `index.html` — replace `<section id="about">` content and add About CSS

- [ ] **Step 1: Add About Me CSS inside `<style>`**

```css
/* === Shared two-column layout === */
.two-col {
  max-width: var(--max-width);
  margin: 0 auto;
  display: flex;
  align-items: center;
  gap: 60px;
}
.two-col .col-text { flex: 1; }
.two-col .col-img  { flex: 1; }
.two-col .col-img img {
  width: 100%;
  height: 420px;
  object-fit: cover;
  border-radius: 2px;
}

/* === Section shared styles === */
.section-inner {
  padding: var(--section-pad) 40px;
}
.section-inner h2 {
  font-family: var(--font-heading);
  font-size: 2.4rem;
  font-weight: 600;
  color: var(--accent);
  margin-bottom: 28px;
  letter-spacing: 0.03em;
}
.section-inner p {
  margin-bottom: 16px;
  color: var(--text);
}

/* === About Me specifics === */
#about { background: var(--bg); }
```

- [ ] **Step 2: Replace the `<section id="about">` placeholder**

```html
<section id="about">
  <div class="section-inner">
    <div class="two-col">
      <div class="col-text">
        <!-- EDIT: About Me heading -->
        <h2>About Me</h2>
        <!-- EDIT: Bio paragraph 1 — introduce Katherine, paediatric nurse background -->
        <p>Hello, I'm Katherine Rivers — a registered paediatric nurse with many years of clinical experience caring for babies and young children. That background has given me a deep understanding of infant development, and an even deeper appreciation of how much the early weeks and months matter for both baby and parent.</p>
        <!-- EDIT: Bio paragraph 2 — IAIM certification and training -->
        <p>I am a certified Infant Massage Instructor, trained and accredited by the International Association of Infant Massage (IAIM). My training was completed through Baby &amp; Child Massage, one of the UK's leading centres for infant massage instructor education.</p>
        <!-- EDIT: Bio paragraph 3 — personal warmth / local connection -->
        <p>I live locally and know how precious — and how exhausting — the early days can be. My classes are designed to be a genuinely restful, sociable, and restorative part of your week: for your baby, and for you.</p>
      </div>
      <div class="col-img">
        <!-- EDIT: replace the src below with Katherine's photo path, e.g. src="images/katherine.jpg" -->
        <img
          src="https://images.unsplash.com/photo-1524863479829-916d8e77f114?w=600&q=80"
          alt="Katherine Rivers — Baby &amp; Palm instructor"
        />
        <!-- NOTE: the Unsplash URL above is a free placeholder. Replace with Katherine's actual photo. -->
      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 3: Verify in browser**

```bash
open index.html
```

Expected: two-column layout, text left, photo right, "About Me" heading in sage green.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add About Me section"
```

---

## Task 6: Baby Massage section

**Files:**
- Modify: `index.html` — replace `<section id="massage">` content and add section CSS

- [ ] **Step 1: Add Baby Massage CSS inside `<style>`**

```css
/* === Baby Massage section === */
#massage { background: var(--accent-light); }
/* Image appears on the LEFT — reverse the column order */
#massage .two-col { flex-direction: row-reverse; }
```

- [ ] **Step 2: Replace the `<section id="massage">` placeholder**

```html
<section id="massage">
  <div class="section-inner">
    <div class="two-col">
      <div class="col-text">
        <!-- EDIT: Baby Massage heading -->
        <h2>Baby Massage</h2>
        <!-- EDIT: What baby massage is -->
        <p>Baby massage is a simple, loving practice of using gentle touch to communicate with your baby. Drawing on techniques from Indian massage, Swedish massage, reflexology, and baby yoga, it is specifically designed for babies from birth up to around twelve months old.</p>
        <!-- EDIT: Benefits paragraph -->
        <p>Research consistently shows that regular massage helps to strengthen the bond between parent and baby, supports healthy physical development, aids digestion and sleep, and can be a meaningful source of comfort for babies experiencing colic or overstimulation. For parents, the quiet ritual of massage can ease the emotional challenges of the postnatal period and build confidence in reading your baby's cues.</p>
        <!-- EDIT: Encouraging closing line -->
        <p>You do not need any prior experience — just a willingness to be present with your baby. I will guide you through every stroke, every step of the way.</p>
      </div>
      <div class="col-img">
        <!-- EDIT: replace with a suitable baby massage image, e.g. src="images/baby-massage.jpg" -->
        <img
          src="https://images.unsplash.com/photo-1544717305-2782549b5136?w=600&q=80"
          alt="Parent giving baby a gentle massage"
        />
        <!-- NOTE: Unsplash placeholder — replace with a preferred image. -->
      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 3: Verify in browser**

```bash
open index.html
```

Expected: light sage-green background, image on the LEFT, text on the right, columns reversed from About Me.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add Baby Massage section"
```

---

## Task 7: Courses section

**Files:**
- Modify: `index.html` — replace `<section id="courses">` content and add CSS

- [ ] **Step 1: Add Courses CSS inside `<style>`**

```css
/* === Courses section === */
#courses { background: var(--bg); }
.courses-inner {
  max-width: 780px;
  margin: 0 auto;
}
.course-card {
  border-left: 3px solid var(--accent);
  padding: 24px 32px;
  margin-bottom: 32px;
  background: var(--accent-light);
  border-radius: 0 4px 4px 0;
}
.course-card h3 {
  font-family: var(--font-heading);
  font-size: 1.6rem;
  color: var(--accent-dark);
  margin-bottom: 12px;
}
.course-card p { margin-bottom: 10px; }
.cta-link {
  display: inline-block;
  margin-top: 8px;
  color: var(--accent-dark);
  font-weight: 700;
  text-decoration: underline;
  font-size: 0.95rem;
  letter-spacing: 0.02em;
}
.cta-link:hover { color: var(--accent); }
```

- [ ] **Step 2: Replace the `<section id="courses">` placeholder**

```html
<section id="courses">
  <div class="section-inner">
    <!-- EDIT: Courses heading -->
    <h2>Courses</h2>
    <div class="courses-inner">

      <div class="course-card">
        <!-- EDIT: Group course heading -->
        <h3>5-Week Group Course</h3>
        <!-- EDIT: Group course description -->
        <p>My signature course runs across five weekly sessions, each lasting 90 minutes. Together we work through a complete sequence of baby massage techniques at a gentle, unhurried pace — so that by the end you feel confident and at ease practising at home.</p>
        <!-- EDIT: Group / social element -->
        <p>Groups are kept intentionally small, creating a warm and relaxed atmosphere. Many parents find the course becomes a highlight of their week — a chance to slow down, connect with their baby, and meet other local families at the same stage of the journey.</p>
        <!-- EDIT: Contact prompt for group course -->
        <a class="cta-link" href="#contact">Get in touch to find out about upcoming dates &rarr;</a>
      </div>

      <div class="course-card">
        <!-- EDIT: 1:1 heading -->
        <h3>One-to-One Sessions</h3>
        <!-- EDIT: 1:1 description -->
        <p>Prefer a more personalised experience? I also offer one-to-one instruction, tailored entirely around you and your baby. This is a wonderful option if group settings feel overwhelming, if your baby has specific needs, or if you simply prefer the flexibility of a private session.</p>
        <!-- EDIT: Contact prompt for 1:1 -->
        <a class="cta-link" href="#contact">Contact me to arrange a session &rarr;</a>
      </div>

    </div>
  </div>
</section>
```

- [ ] **Step 3: Verify in browser**

```bash
open index.html
```

Expected: two left-bordered sage-green cards, centred column, clear call-to-action links.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add Courses section"
```

---

## Task 8: Contact section + footer

**Files:**
- Modify: `index.html` — replace `<section id="contact">` and add CSS

- [ ] **Step 1: Add Contact CSS inside `<style>`**

```css
/* === Contact section === */
#contact {
  position: relative;
  padding: var(--section-pad) 40px;
  background: url('images/background.jpg') center center / cover no-repeat;
  text-align: center;
}
#contact::before {
  content: '';
  position: absolute;
  inset: 0;
  background: rgba(255,255,255,0.78);
}
.contact-inner {
  position: relative;
  z-index: 1;
  max-width: 500px;
  margin: 0 auto;
}
#contact h2 {
  font-family: var(--font-heading);
  font-size: 2.4rem;
  color: var(--accent);
  margin-bottom: 24px;
  letter-spacing: 0.03em;
}
.contact-detail {
  font-size: 1rem;
  color: var(--text);
  margin-bottom: 10px;
}
.contact-detail a {
  color: var(--accent-dark);
  font-weight: 700;
  text-decoration: underline;
}
.contact-detail a:hover { color: var(--accent); }
.contact-footer {
  margin-top: 40px;
  font-size: 0.82rem;
  color: #888;
}
.contact-footer a {
  color: #888;
  text-decoration: underline;
}
```

- [ ] **Step 2: Replace the `<section id="contact">` placeholder**

```html
<section id="contact">
  <div class="contact-inner">
    <!-- EDIT: Contact heading -->
    <h2>Contact Me</h2>
    <!-- EDIT: Instructor name -->
    <p class="contact-detail">Katherine Rivers</p>
    <!-- EDIT: update email address when domain is live -->
    <p class="contact-detail">
      <a href="mailto:contact@babyandpalm.co.uk">contact@babyandpalm.co.uk</a>
    </p>
    <!-- EDIT: location line -->
    <p class="contact-detail">Petersfield, Hampshire</p>

    <!-- Footer line -->
    <div class="contact-footer">
      <!-- EDIT: update href when Terms page is created -->
      <a href="#">Terms &amp; Conditions</a>
      &nbsp;&middot;&nbsp;
      &copy; <span id="year"></span> Baby &amp; Palm
    </div>
  </div>
</section>
```

- [ ] **Step 3: Add the auto-year script — replace `<script>/* Task 9 */</script>` temporarily to verify year renders**

```html
<script>
  document.getElementById('year').textContent = new Date().getFullYear();
</script>
```

- [ ] **Step 4: Verify in browser**

```bash
open index.html
```

Expected: contact section with background photo, light overlay, sage green "Contact Me" heading, email as clickable link, current year in footer.

- [ ] **Step 5: Commit**

```bash
git add index.html
git commit -m "feat: add Contact section and footer"
```

---

## Task 9: Mobile responsiveness + hamburger menu

**Files:**
- Modify: `index.html` — add responsive CSS and hamburger JS

- [ ] **Step 1: Add mobile CSS inside `<style>` (after all desktop styles)**

```css
/* ============================================================
   === Mobile / responsive styles (max-width: 768px)        ===
   ============================================================ */
@media (max-width: 768px) {

  /* Nav: hide desktop links, show hamburger */
  .nav-links { display: none; }
  .nav-hamburger { display: flex; }

  #site-nav { padding: 0 20px; }

  /* Mobile nav overlay */
  .nav-mobile {
    position: fixed;
    top: var(--nav-height);
    left: 0;
    right: 0;
    background: var(--bg);
    z-index: 99;
    box-shadow: 0 4px 12px rgba(0,0,0,0.1);
    padding: 20px 0;
    /* hidden by default — JS adds .open to show */
    max-height: 0;
    overflow: hidden;
    transition: max-height 0.3s ease;
  }
  .nav-mobile.open {
    max-height: 340px;
  }
  .nav-mobile ul {
    list-style: none;
    text-align: center;
  }
  .nav-mobile ul li {
    padding: 14px 0;
    border-bottom: 1px solid var(--accent-light);
  }
  .nav-mobile ul li:last-child { border-bottom: none; }
  .nav-mobile ul li a {
    font-family: var(--font-body);
    font-size: 1.05rem;
    color: var(--text);
    text-decoration: none;
    letter-spacing: 0.02em;
  }
  .nav-mobile ul li a:hover { color: var(--accent); }

  /* Hero */
  .welcome-box {
    padding: 36px 24px;
    margin: 20px;
  }
  .welcome-box h1 { font-size: 2.6rem; }

  /* Two-column sections stack vertically */
  .two-col {
    flex-direction: column !important;
    gap: 30px;
  }
  .two-col .col-img img {
    height: 260px;
  }

  /* Sections padding */
  .section-inner { padding: 50px 20px; }
  #contact { padding: 50px 20px; }

  /* Course cards */
  .course-card { padding: 20px; }
}
```

- [ ] **Step 2: Replace the `<script>` block with the hamburger toggle + year script**

```html
<script>
  // Auto-update copyright year
  document.getElementById('year').textContent = new Date().getFullYear();

  // Hamburger menu toggle
  const hamburger = document.getElementById('nav-hamburger');
  const mobileNav = document.getElementById('nav-mobile');

  hamburger.addEventListener('click', function () {
    mobileNav.classList.toggle('open');
  });

  // Close mobile nav when a link is clicked
  function closeMobileNav() {
    mobileNav.classList.remove('open');
  }

  // Close mobile nav if user clicks outside it
  document.addEventListener('click', function (e) {
    if (!mobileNav.contains(e.target) && !hamburger.contains(e.target)) {
      mobileNav.classList.remove('open');
    }
  });
</script>
```

- [ ] **Step 3: Test mobile layout using browser DevTools**

```bash
open index.html
```

In Chrome/Safari: open DevTools → toggle device toolbar → select iPhone or similar. Verify:
- Desktop links hidden, hamburger (three lines) visible top right
- Tapping hamburger slides down the mobile nav
- Tapping a nav link scrolls to section and closes the menu
- All sections stack to single column
- Hero text box fills width with readable text

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add mobile responsive layout and hamburger nav"
```

---

## Task 10: GitHub Pages setup

**Files:**
- Create: `.github/workflows/` (not needed — GitHub Pages serves from root directly)
- Create: `.nojekyll` (prevents Jekyll processing)

- [ ] **Step 1: Add `.nojekyll` file so GitHub Pages serves plain HTML**

```bash
touch .nojekyll
```

- [ ] **Step 2: Create `README.md` with hosting instructions**

```bash
cat > README.md << 'EOF'
# Baby & Palm — Website

Single-page static website for [Baby & Palm](https://babyandpalm.co.uk).

## Editing the site

Open `index.html` in any text editor. The `/* === EDIT ME === */` block near the top of
the `<style>` section controls all colours and fonts. Every piece of copy and every image
path is marked with an `<!-- EDIT: ... -->` comment.

## Hosting

This site is hosted on GitHub Pages. Push to `main` to deploy.

## Images to replace

- `images/background.jpg` — landscape background photo
- About Me section: Unsplash placeholder → replace with `images/katherine.jpg`
- Baby Massage section: Unsplash placeholder → replace with preferred image
EOF
```

- [ ] **Step 3: Commit everything**

```bash
git add .nojekyll README.md docs/
git commit -m "chore: add GitHub Pages config and README"
```

- [ ] **Step 4: Create GitHub repo and push**

Go to github.com → New repository → name it `babyandpalm` (or `babymassage`) → do NOT initialise with README.

Then run:
```bash
git remote add origin https://github.com/YOUR_USERNAME/babyandpalm.git
git branch -M main
git push -u origin main
```

Replace `YOUR_USERNAME` with your GitHub username.

- [ ] **Step 5: Enable GitHub Pages**

On GitHub: Settings → Pages → Source → Deploy from branch → `main` → `/ (root)` → Save.

Site will be live at: `https://YOUR_USERNAME.github.io/babyandpalm/`

---

## Self-Review Checklist

| Spec requirement | Covered in task |
|-----------------|----------------|
| Single `index.html`, everything embedded | Task 2 |
| CSS variables block (`/* === EDIT ME === */`) | Task 2 |
| Sticky nav, logo left, links right with dividers | Task 3 |
| Hamburger on mobile (top right) | Task 9 |
| Welcome hero with background.jpg + overlay | Task 4 |
| About Me: two-col, text left, image right | Task 5 |
| About Me: paediatric nurse, IAIM credentials | Task 5 |
| Baby Massage: two-col reversed, techniques, benefits | Task 6 |
| Courses: 5-week group + 1:1 cards | Task 7 |
| Contact: background overlay, email mailto, location | Task 8 |
| Footer: Terms & Conditions link, copyright year | Task 8 |
| All copy marked `<!-- EDIT: -->` | Tasks 4–8 |
| All image paths marked for replacement | Tasks 5–6 |
| Mobile single-column stacking | Task 9 |
| GitHub Pages deploy | Task 10 |
