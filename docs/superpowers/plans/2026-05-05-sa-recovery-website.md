# SA Recovery Group Website — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a 4-page static demo website for SA Recovery Group using plain HTML, CSS, and JS.

**Architecture:** One shared `styles.css` and `main.js` included by all four HTML pages. No build tools, no frameworks — open `index.html` directly in a browser to run.

**Tech Stack:** HTML5, CSS3 (custom properties), vanilla JS, Google Fonts (Inter), Unsplash image URLs.

---

## File Map

| File | Responsibility |
|---|---|
| `styles.css` | All styling — design tokens, reset, navbar, footer, hero variants, cards, grid, responsive |
| `main.js` | Mobile nav toggle, active link highlight, contact form submit handler |
| `index.html` | Home page — full hero, services preview, why-us, CTA banner |
| `services.html` | Services page — page hero, 7 service cards, CTA banner |
| `about.html` | About page — page hero, story section, values, image strip |
| `contact.html` | Contact page — page hero, form + contact info columns |

---

## Task 1: Shared CSS (`styles.css`)

**Files:**
- Create: `styles.css`

- [ ] **Step 1: Create `styles.css` with this full content**

```css
/* ── Design Tokens ─────────────────────────────────────── */
:root {
  --dark:        #1a1a2e;
  --amber:       #f59e0b;
  --amber-hover: #d97706;
  --bg:          #f9fafb;
  --card-bg:     #ffffff;
  --text:        #374151;
  --muted:       #6b7280;
  --white:       #ffffff;
  --radius:      8px;
  --shadow:      0 2px 12px rgba(0,0,0,0.08);
  --transition:  0.2s ease;
}

/* ── Reset ─────────────────────────────────────────────── */
*, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }
html { scroll-behavior: smooth; }
body {
  font-family: 'Inter', sans-serif;
  color: var(--text);
  background: var(--bg);
  line-height: 1.6;
}
img { max-width: 100%; display: block; }
a { text-decoration: none; color: inherit; }
ul { list-style: none; }

/* ── Navbar ────────────────────────────────────────────── */
.navbar {
  position: sticky;
  top: 0;
  z-index: 100;
  background: var(--dark);
  padding: 0 2rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 68px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.3);
}
.navbar-logo img { height: 44px; object-fit: contain; }
.navbar-links {
  display: flex;
  gap: 2rem;
  align-items: center;
}
.navbar-links a {
  color: var(--white);
  font-weight: 500;
  font-size: 0.95rem;
  padding-bottom: 4px;
  border-bottom: 2px solid transparent;
  transition: border-color var(--transition), color var(--transition);
}
.navbar-links a:hover,
.navbar-links a.active {
  color: var(--amber);
  border-bottom-color: var(--amber);
}
.hamburger {
  display: none;
  flex-direction: column;
  gap: 5px;
  cursor: pointer;
  background: none;
  border: none;
  padding: 4px;
}
.hamburger span {
  display: block;
  width: 24px;
  height: 2px;
  background: var(--white);
  border-radius: 2px;
  transition: transform var(--transition), opacity var(--transition);
}
.mobile-menu {
  display: none;
  flex-direction: column;
  background: var(--dark);
  padding: 1rem 2rem 1.5rem;
  border-top: 1px solid rgba(255,255,255,0.08);
}
.mobile-menu a {
  color: var(--white);
  font-weight: 500;
  padding: 0.6rem 0;
  border-bottom: 1px solid rgba(255,255,255,0.06);
  transition: color var(--transition);
}
.mobile-menu a:hover,
.mobile-menu a.active { color: var(--amber); }
.mobile-menu.open { display: flex; }

/* ── Buttons ───────────────────────────────────────────── */
.btn {
  display: inline-block;
  padding: 0.8rem 2rem;
  border-radius: var(--radius);
  font-weight: 600;
  font-size: 1rem;
  cursor: pointer;
  border: none;
  transition: background var(--transition), transform var(--transition);
}
.btn:hover { transform: translateY(-1px); }
.btn-primary {
  background: var(--amber);
  color: var(--dark);
}
.btn-primary:hover { background: var(--amber-hover); }
.btn-dark {
  background: var(--dark);
  color: var(--white);
}
.btn-dark:hover { background: #2a2a4e; }

/* ── Hero (Home) ───────────────────────────────────────── */
.hero {
  min-height: 100vh;
  background:
    linear-gradient(rgba(26,26,46,0.75), rgba(26,26,46,0.75)),
    url('https://images.unsplash.com/photo-1527786356703-4b100091cd2c?w=1600&auto=format&fit=crop') center/cover no-repeat;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  padding: 2rem;
}
.hero-content { max-width: 760px; }
.hero-content h1 {
  font-size: clamp(2rem, 5vw, 3.5rem);
  font-weight: 800;
  color: var(--white);
  line-height: 1.15;
  margin-bottom: 1.2rem;
}
.hero-content p {
  font-size: clamp(1rem, 2.5vw, 1.25rem);
  color: rgba(255,255,255,0.82);
  margin-bottom: 2rem;
}

/* ── Page Hero (inner pages) ───────────────────────────── */
.page-hero {
  height: 280px;
  background:
    linear-gradient(rgba(26,26,46,0.82), rgba(26,26,46,0.82)),
    url('https://images.unsplash.com/photo-1527786356703-4b100091cd2c?w=1600&auto=format&fit=crop') center/cover no-repeat;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  text-align: center;
  padding: 1rem;
}
.page-hero h1 {
  font-size: clamp(1.8rem, 4vw, 2.8rem);
  font-weight: 800;
  color: var(--white);
  margin-bottom: 0.5rem;
}
.page-hero .breadcrumb {
  font-size: 0.9rem;
  color: rgba(255,255,255,0.6);
}
.page-hero .breadcrumb span { color: var(--amber); }

/* ── Section wrapper ───────────────────────────────────── */
.section { padding: 5rem 2rem; }
.section-dark { background: var(--dark); }
.section-title {
  text-align: center;
  font-size: clamp(1.6rem, 3vw, 2.2rem);
  font-weight: 700;
  color: var(--dark);
  margin-bottom: 0.5rem;
}
.section-title.light { color: var(--white); }
.section-subtitle {
  text-align: center;
  color: var(--muted);
  margin-bottom: 3rem;
  font-size: 1rem;
}
.section-subtitle.light { color: rgba(255,255,255,0.65); }
.container { max-width: 1100px; margin: 0 auto; }

/* ── Cards grid ────────────────────────────────────────── */
.cards-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1.5rem;
}
.card {
  background: var(--card-bg);
  border-radius: var(--radius);
  padding: 2rem 1.5rem;
  box-shadow: var(--shadow);
  border-top: 4px solid var(--amber);
  transition: transform var(--transition), box-shadow var(--transition);
}
.card:hover {
  transform: translateY(-4px);
  box-shadow: 0 8px 24px rgba(0,0,0,0.12);
}
.card-icon {
  font-size: 2.2rem;
  margin-bottom: 1rem;
}
.card h3 {
  font-size: 1.15rem;
  font-weight: 700;
  color: var(--dark);
  margin-bottom: 0.5rem;
}
.card p {
  font-size: 0.92rem;
  color: var(--muted);
  line-height: 1.6;
}

/* ── Why-Us stats ──────────────────────────────────────── */
.stats-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 2rem;
  text-align: center;
}
.stat-item .stat-icon {
  font-size: 2.5rem;
  color: var(--amber);
  margin-bottom: 0.75rem;
}
.stat-item h3 {
  font-size: 1.3rem;
  font-weight: 700;
  color: var(--white);
  margin-bottom: 0.3rem;
}
.stat-item p {
  font-size: 0.9rem;
  color: rgba(255,255,255,0.6);
}

/* ── CTA Banner ────────────────────────────────────────── */
.cta-banner {
  background: var(--amber);
  padding: 3.5rem 2rem;
  text-align: center;
}
.cta-banner h2 {
  font-size: clamp(1.5rem, 3vw, 2rem);
  font-weight: 800;
  color: var(--dark);
  margin-bottom: 1.2rem;
}
.cta-banner .cta-sub {
  color: rgba(26,26,46,0.75);
  margin-bottom: 1.8rem;
  font-size: 1rem;
}

/* ── See All link ──────────────────────────────────────── */
.see-all {
  text-align: center;
  margin-top: 2.5rem;
}
.see-all a {
  color: var(--amber);
  font-weight: 600;
  font-size: 1rem;
  border-bottom: 2px solid transparent;
  transition: border-color var(--transition);
}
.see-all a:hover { border-bottom-color: var(--amber); }

/* ── About: two-column story ───────────────────────────── */
.two-col {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: center;
}
.two-col img {
  width: 100%;
  height: 380px;
  object-fit: cover;
  border-radius: var(--radius);
  box-shadow: var(--shadow);
}
.story-text h2 {
  font-size: clamp(1.5rem, 2.5vw, 2rem);
  font-weight: 700;
  color: var(--dark);
  margin-bottom: 1rem;
}
.story-text p {
  color: var(--muted);
  margin-bottom: 1rem;
  font-size: 0.97rem;
}
.story-text .highlight {
  color: var(--amber);
  font-weight: 600;
}

/* ── Values pills ──────────────────────────────────────── */
.values-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1.5rem;
  text-align: center;
}
.value-card {
  padding: 2rem 1.5rem;
  border-radius: var(--radius);
  background: rgba(255,255,255,0.05);
  border: 1px solid rgba(255,255,255,0.1);
}
.value-card .val-icon {
  font-size: 2.2rem;
  color: var(--amber);
  margin-bottom: 0.75rem;
}
.value-card h3 {
  font-size: 1.1rem;
  font-weight: 700;
  color: var(--white);
  margin-bottom: 0.4rem;
}
.value-card p {
  font-size: 0.88rem;
  color: rgba(255,255,255,0.6);
}

/* ── Image strip ───────────────────────────────────────── */
.img-strip {
  height: 300px;
  background: url('https://images.unsplash.com/photo-1591768575198-88dac53fbd0a?w=1600&auto=format&fit=crop') center/cover no-repeat;
}

/* ── Contact layout ────────────────────────────────────── */
.contact-grid {
  display: grid;
  grid-template-columns: 1.4fr 1fr;
  gap: 4rem;
  align-items: start;
}
.contact-form h2,
.contact-info h2 {
  font-size: 1.4rem;
  font-weight: 700;
  color: var(--dark);
  margin-bottom: 1.5rem;
}
.form-group {
  margin-bottom: 1.2rem;
}
.form-group label {
  display: block;
  font-size: 0.88rem;
  font-weight: 600;
  color: var(--dark);
  margin-bottom: 0.4rem;
}
.form-group input,
.form-group select,
.form-group textarea {
  width: 100%;
  padding: 0.75rem 1rem;
  border: 1.5px solid #e5e7eb;
  border-radius: var(--radius);
  font-family: 'Inter', sans-serif;
  font-size: 0.95rem;
  color: var(--text);
  background: var(--white);
  transition: border-color var(--transition);
}
.form-group input:focus,
.form-group select:focus,
.form-group textarea:focus {
  outline: none;
  border-color: var(--amber);
}
.form-group textarea { resize: vertical; min-height: 130px; }
.btn-submit {
  width: 100%;
  padding: 0.9rem;
  font-size: 1rem;
  font-weight: 700;
}

/* ── Contact info ──────────────────────────────────────── */
.info-item {
  display: flex;
  gap: 1rem;
  align-items: flex-start;
  margin-bottom: 1.5rem;
}
.info-icon {
  font-size: 1.5rem;
  color: var(--amber);
  flex-shrink: 0;
  margin-top: 2px;
}
.info-item h4 {
  font-size: 0.88rem;
  font-weight: 600;
  color: var(--muted);
  text-transform: uppercase;
  letter-spacing: 0.05em;
  margin-bottom: 0.2rem;
}
.info-item p {
  font-size: 0.97rem;
  color: var(--dark);
  font-weight: 500;
}

/* ── Footer ────────────────────────────────────────────── */
.footer {
  background: var(--dark);
  color: var(--white);
  padding: 3.5rem 2rem 0;
}
.footer-grid {
  display: grid;
  grid-template-columns: 1.5fr 1fr 1fr;
  gap: 3rem;
  max-width: 1100px;
  margin: 0 auto;
  padding-bottom: 3rem;
  border-bottom: 1px solid rgba(255,255,255,0.08);
}
.footer-brand img { height: 44px; margin-bottom: 0.75rem; }
.footer-brand p {
  font-size: 0.88rem;
  color: rgba(255,255,255,0.55);
  line-height: 1.7;
  max-width: 260px;
}
.footer-col h4 {
  font-size: 0.85rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  color: var(--amber);
  margin-bottom: 1rem;
}
.footer-col a,
.footer-col p {
  display: block;
  font-size: 0.92rem;
  color: rgba(255,255,255,0.6);
  margin-bottom: 0.5rem;
  transition: color var(--transition);
}
.footer-col a:hover { color: var(--amber); }
.footer-bottom {
  max-width: 1100px;
  margin: 0 auto;
  padding: 1.2rem 0;
  font-size: 0.82rem;
  color: rgba(255,255,255,0.35);
  text-align: center;
}

/* ── Responsive ────────────────────────────────────────── */
@media (max-width: 768px) {
  .navbar-links { display: none; }
  .hamburger { display: flex; }
  .cards-grid { grid-template-columns: repeat(2, 1fr); }
  .stats-grid { grid-template-columns: 1fr; gap: 1.5rem; }
  .two-col { grid-template-columns: 1fr; gap: 2rem; }
  .values-grid { grid-template-columns: 1fr; }
  .contact-grid { grid-template-columns: 1fr; gap: 2.5rem; }
  .footer-grid { grid-template-columns: 1fr; gap: 2rem; }
}

@media (max-width: 480px) {
  .section { padding: 3.5rem 1rem; }
  .navbar { padding: 0 1rem; }
  .mobile-menu { padding: 1rem 1rem 1.5rem; }
  .cards-grid { grid-template-columns: 1fr; }
  .card { padding: 1.5rem 1.2rem; }
}
```

- [ ] **Step 2: Open any `.html` file in a browser once the later pages are built to confirm styles load (no errors in DevTools console).**

---

## Task 2: Shared JS (`main.js`)

**Files:**
- Create: `main.js`

- [ ] **Step 1: Create `main.js` with this full content**

```js
document.addEventListener('DOMContentLoaded', () => {

  // ── Active nav link ──────────────────────────────────
  const currentPage = location.pathname.split('/').pop() || 'index.html';
  document.querySelectorAll('.navbar-links a, .mobile-menu a').forEach(link => {
    const href = link.getAttribute('href');
    if (href === currentPage || (currentPage === '' && href === 'index.html')) {
      link.classList.add('active');
    }
  });

  // ── Mobile nav toggle ────────────────────────────────
  const hamburger = document.querySelector('.hamburger');
  const mobileMenu = document.querySelector('.mobile-menu');
  if (hamburger && mobileMenu) {
    hamburger.addEventListener('click', () => {
      mobileMenu.classList.toggle('open');
      const isOpen = mobileMenu.classList.contains('open');
      hamburger.setAttribute('aria-expanded', isOpen);
    });
    // Close on outside click
    document.addEventListener('click', e => {
      if (!hamburger.contains(e.target) && !mobileMenu.contains(e.target)) {
        mobileMenu.classList.remove('open');
        hamburger.setAttribute('aria-expanded', false);
      }
    });
  }

  // ── Contact form ─────────────────────────────────────
  const form = document.getElementById('contact-form');
  if (form) {
    form.addEventListener('submit', e => {
      e.preventDefault();
      alert("Thank you! We'll be in touch shortly.");
      form.reset();
    });
  }

});
```

- [ ] **Step 2: Commit what we have so far**

```bash
git init
git add styles.css main.js
git commit -m "feat: add shared CSS and JS"
```

---

## Task 3: Home page (`index.html`)

**Files:**
- Create: `index.html`

- [ ] **Step 1: Create `index.html` with this full content**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>SA Recovery Group — 24/7 Vehicle Recovery</title>
  <meta name="description" content="Fast, reliable vehicle recovery and roadside assistance. SA Recovery Group is available 24/7.">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="styles.css">
</head>
<body>

  <!-- Navbar -->
  <nav class="navbar">
    <a href="index.html" class="navbar-logo">
      <img src="white-black logo.png" alt="SA Recovery Group">
    </a>
    <ul class="navbar-links">
      <li><a href="index.html">Home</a></li>
      <li><a href="services.html">Services</a></li>
      <li><a href="about.html">About</a></li>
      <li><a href="contact.html">Contact</a></li>
    </ul>
    <button class="hamburger" aria-label="Toggle menu" aria-expanded="false">
      <span></span><span></span><span></span>
    </button>
  </nav>
  <div class="mobile-menu">
    <a href="index.html">Home</a>
    <a href="services.html">Services</a>
    <a href="about.html">About</a>
    <a href="contact.html">Contact</a>
  </div>

  <!-- Hero -->
  <section class="hero">
    <div class="hero-content">
      <h1>24/7 Vehicle Recovery<br>You Can Count On</h1>
      <p>Fast, reliable roadside assistance across the region.<br>We get you moving again — day or night.</p>
      <a href="contact.html" class="btn btn-primary">Get Help Now</a>
    </div>
  </section>

  <!-- Services Preview -->
  <section class="section">
    <div class="container">
      <h2 class="section-title">Our Services</h2>
      <p class="section-subtitle">Whatever the breakdown, we've got you covered.</p>
      <div class="cards-grid">
        <div class="card">
          <div class="card-icon">🚛</div>
          <h3>Towing</h3>
          <p>Safe and secure towing for all vehicle types, from compact cars to larger vehicles.</p>
        </div>
        <div class="card">
          <div class="card-icon">🛟</div>
          <h3>Roadside Assistance</h3>
          <p>Stuck on the side of the road? Our team arrives fast to get you back on your way.</p>
        </div>
        <div class="card">
          <div class="card-icon">🚑</div>
          <h3>Accident Recovery</h3>
          <p>Professional accident recovery handled with care, speed, and precision.</p>
        </div>
      </div>
      <div class="see-all">
        <a href="services.html">See All Services &rarr;</a>
      </div>
    </div>
  </section>

  <!-- Why Us -->
  <section class="section section-dark">
    <div class="container">
      <h2 class="section-title light">Why Choose SA Recovery Group?</h2>
      <p class="section-subtitle light">Trusted by thousands of drivers across the region.</p>
      <div class="stats-grid">
        <div class="stat-item">
          <div class="stat-icon">🕐</div>
          <h3>24/7 Available</h3>
          <p>We never close. Breakdowns don't keep business hours — neither do we.</p>
        </div>
        <div class="stat-item">
          <div class="stat-icon">⚡</div>
          <h3>30-Min Response</h3>
          <p>Our fleet is strategically positioned to reach you in under 30 minutes.</p>
        </div>
        <div class="stat-item">
          <div class="stat-icon">✅</div>
          <h3>Fully Licensed & Insured</h3>
          <p>Certified operators, insured vehicles, and professional equipment every time.</p>
        </div>
      </div>
    </div>
  </section>

  <!-- CTA Banner -->
  <div class="cta-banner">
    <h2>Stranded? We're on our way.</h2>
    <p class="cta-sub">Don't wait — contact us now and we'll dispatch a recovery unit immediately.</p>
    <a href="contact.html" class="btn btn-dark">Contact Us Now</a>
  </div>

  <!-- Footer -->
  <footer class="footer">
    <div class="footer-grid">
      <div class="footer-brand">
        <img src="white-black logo.png" alt="SA Recovery Group">
        <p>Professional vehicle recovery and roadside assistance, available around the clock.</p>
      </div>
      <div class="footer-col">
        <h4>Quick Links</h4>
        <a href="index.html">Home</a>
        <a href="services.html">Services</a>
        <a href="about.html">About Us</a>
        <a href="contact.html">Contact</a>
      </div>
      <div class="footer-col">
        <h4>Contact</h4>
        <p>📞 +27 XX XXX XXXX</p>
        <p>✉️ info@sarecoverygroup.co.za</p>
        <p>📍 South Africa</p>
        <p>🕐 24/7 Operations</p>
      </div>
    </div>
    <div class="footer-bottom">
      &copy; 2026 SA Recovery Group. All rights reserved.
    </div>
  </footer>

  <script src="main.js"></script>
</body>
</html>
```

- [ ] **Step 2: Open `index.html` in a browser. Verify:**
  - Hero image loads with dark overlay and centered text
  - "Get Help Now" button is amber and links to `contact.html`
  - 3 service cards display in a row
  - Stats row displays on dark background
  - Amber CTA banner appears
  - Footer shows logo + links + contact info
  - Resize to mobile: hamburger appears, nav links hide

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add home page"
```

---

## Task 4: Services page (`services.html`)

**Files:**
- Create: `services.html`

- [ ] **Step 1: Create `services.html` with this full content**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Our Services — SA Recovery Group</title>
  <meta name="description" content="Full range of vehicle recovery services including towing, roadside assistance, jump starts, and more.">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="styles.css">
</head>
<body>

  <!-- Navbar -->
  <nav class="navbar">
    <a href="index.html" class="navbar-logo">
      <img src="white-black logo.png" alt="SA Recovery Group">
    </a>
    <ul class="navbar-links">
      <li><a href="index.html">Home</a></li>
      <li><a href="services.html">Services</a></li>
      <li><a href="about.html">About</a></li>
      <li><a href="contact.html">Contact</a></li>
    </ul>
    <button class="hamburger" aria-label="Toggle menu" aria-expanded="false">
      <span></span><span></span><span></span>
    </button>
  </nav>
  <div class="mobile-menu">
    <a href="index.html">Home</a>
    <a href="services.html">Services</a>
    <a href="about.html">About</a>
    <a href="contact.html">Contact</a>
  </div>

  <!-- Page Hero -->
  <div class="page-hero">
    <h1>Our Services</h1>
    <p class="breadcrumb">Home &rsaquo; <span>Services</span></p>
  </div>

  <!-- Services Grid -->
  <section class="section">
    <div class="container">
      <h2 class="section-title">Everything You Need on the Road</h2>
      <p class="section-subtitle">From a flat tyre to a full vehicle recovery — we handle it all.</p>
      <div class="cards-grid" style="grid-template-columns: repeat(3, 1fr);">
        <div class="card">
          <div class="card-icon">🚛</div>
          <h3>Towing</h3>
          <p>Safe and secure towing for all vehicle types. We handle your car with care from pickup to drop-off.</p>
        </div>
        <div class="card">
          <div class="card-icon">🛟</div>
          <h3>Roadside Assistance</h3>
          <p>Stuck on the side of the road? We dispatch quickly and resolve most issues on the spot.</p>
        </div>
        <div class="card">
          <div class="card-icon">⚡</div>
          <h3>Jump Starts</h3>
          <p>Dead battery? Our team will jump-start your vehicle and get you back on the road in minutes.</p>
        </div>
        <div class="card">
          <div class="card-icon">🔧</div>
          <h3>Flat Tyre Changes</h3>
          <p>We'll fit your spare or help arrange a replacement if you don't have one available.</p>
        </div>
        <div class="card">
          <div class="card-icon">⛽</div>
          <h3>Fuel Delivery</h3>
          <p>Run out of fuel? We'll bring enough to get you to the nearest filling station safely.</p>
        </div>
        <div class="card">
          <div class="card-icon">🚑</div>
          <h3>Accident Recovery</h3>
          <p>Post-accident recovery handled professionally — we prioritise safety and minimise further damage.</p>
        </div>
        <div class="card">
          <div class="card-icon">🛣️</div>
          <h3>Long-Distance Towing</h3>
          <p>Need your vehicle moved across the country? We offer reliable long-distance towing solutions.</p>
        </div>
      </div>
    </div>
  </section>

  <!-- CTA Banner -->
  <div class="cta-banner">
    <h2>Need a Recovery Right Now?</h2>
    <p class="cta-sub">Call us or fill in the contact form — we'll have someone with you fast.</p>
    <a href="contact.html" class="btn btn-dark">Contact Us Now</a>
  </div>

  <!-- Footer -->
  <footer class="footer">
    <div class="footer-grid">
      <div class="footer-brand">
        <img src="white-black logo.png" alt="SA Recovery Group">
        <p>Professional vehicle recovery and roadside assistance, available around the clock.</p>
      </div>
      <div class="footer-col">
        <h4>Quick Links</h4>
        <a href="index.html">Home</a>
        <a href="services.html">Services</a>
        <a href="about.html">About Us</a>
        <a href="contact.html">Contact</a>
      </div>
      <div class="footer-col">
        <h4>Contact</h4>
        <p>📞 +27 XX XXX XXXX</p>
        <p>✉️ info@sarecoverygroup.co.za</p>
        <p>📍 South Africa</p>
        <p>🕐 24/7 Operations</p>
      </div>
    </div>
    <div class="footer-bottom">
      &copy; 2026 SA Recovery Group. All rights reserved.
    </div>
  </footer>

  <script src="main.js"></script>
</body>
</html>
```

- [ ] **Step 2: Open `services.html` in a browser. Verify:**
  - "Services" nav link is underlined in amber (active state)
  - Page hero shows with title and breadcrumb
  - All 7 service cards display (last row has 1 card centred or left-aligned — acceptable)
  - Amber CTA banner at bottom links to contact page

- [ ] **Step 3: Commit**

```bash
git add services.html
git commit -m "feat: add services page"
```

---

## Task 5: About page (`about.html`)

**Files:**
- Create: `about.html`

- [ ] **Step 1: Create `about.html` with this full content**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>About Us — SA Recovery Group</title>
  <meta name="description" content="Learn more about SA Recovery Group — who we are, our mission, and what drives us.">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="styles.css">
</head>
<body>

  <!-- Navbar -->
  <nav class="navbar">
    <a href="index.html" class="navbar-logo">
      <img src="white-black logo.png" alt="SA Recovery Group">
    </a>
    <ul class="navbar-links">
      <li><a href="index.html">Home</a></li>
      <li><a href="services.html">Services</a></li>
      <li><a href="about.html">About</a></li>
      <li><a href="contact.html">Contact</a></li>
    </ul>
    <button class="hamburger" aria-label="Toggle menu" aria-expanded="false">
      <span></span><span></span><span></span>
    </button>
  </nav>
  <div class="mobile-menu">
    <a href="index.html">Home</a>
    <a href="services.html">Services</a>
    <a href="about.html">About</a>
    <a href="contact.html">Contact</a>
  </div>

  <!-- Page Hero -->
  <div class="page-hero">
    <h1>About SA Recovery Group</h1>
    <p class="breadcrumb">Home &rsaquo; <span>About Us</span></p>
  </div>

  <!-- Story Section -->
  <section class="section">
    <div class="container">
      <div class="two-col">
        <div class="story-text">
          <h2>Who We Are</h2>
          <p>SA Recovery Group was founded with a single purpose: to make sure no driver is ever left stranded on the side of the road. With years of experience in the vehicle recovery industry, our team of certified professionals has helped thousands of motorists across the region.</p>
          <p>We operate a modern fleet of recovery vehicles, equipped with the latest tools and technology to handle any situation — from a simple flat tyre to a complex accident recovery.</p>
          <p>Our commitment is simple: <span class="highlight">fast response, professional service, and peace of mind</span> — every single time.</p>
          <br>
          <a href="contact.html" class="btn btn-primary">Get in Touch</a>
        </div>
        <img
          src="https://images.unsplash.com/photo-1449965408869-eaa3f722e40d?w=800&auto=format&fit=crop"
          alt="SA Recovery Group truck on the road"
        >
      </div>
    </div>
  </section>

  <!-- Values Section -->
  <section class="section section-dark">
    <div class="container">
      <h2 class="section-title light">What Drives Us</h2>
      <p class="section-subtitle light">Three core values behind everything we do.</p>
      <div class="values-grid">
        <div class="value-card">
          <div class="val-icon">⚡</div>
          <h3>Fast</h3>
          <p>Speed matters when you're stranded. We aim to reach you within 30 minutes, no excuses.</p>
        </div>
        <div class="value-card">
          <div class="val-icon">🤝</div>
          <h3>Reliable</h3>
          <p>When you call, we answer. 24/7, 365 days a year. You can count on us to show up.</p>
        </div>
        <div class="value-card">
          <div class="val-icon">🏆</div>
          <h3>Professional</h3>
          <p>Certified operators, insured vehicles, and a team that treats your car like their own.</p>
        </div>
      </div>
    </div>
  </section>

  <!-- Image Strip -->
  <div class="img-strip"></div>

  <!-- Footer -->
  <footer class="footer">
    <div class="footer-grid">
      <div class="footer-brand">
        <img src="white-black logo.png" alt="SA Recovery Group">
        <p>Professional vehicle recovery and roadside assistance, available around the clock.</p>
      </div>
      <div class="footer-col">
        <h4>Quick Links</h4>
        <a href="index.html">Home</a>
        <a href="services.html">Services</a>
        <a href="about.html">About Us</a>
        <a href="contact.html">Contact</a>
      </div>
      <div class="footer-col">
        <h4>Contact</h4>
        <p>📞 +27 XX XXX XXXX</p>
        <p>✉️ info@sarecoverygroup.co.za</p>
        <p>📍 South Africa</p>
        <p>🕐 24/7 Operations</p>
      </div>
    </div>
    <div class="footer-bottom">
      &copy; 2026 SA Recovery Group. All rights reserved.
    </div>
  </footer>

  <script src="main.js"></script>
</body>
</html>
```

- [ ] **Step 2: Open `about.html` in a browser. Verify:**
  - "About" nav link is active (amber underline)
  - Two-column story section: text left, image right
  - Image loads from Unsplash (if URL 404s, swap to any working Unsplash automotive photo)
  - Dark values section with 3 cards
  - Full-width image strip visible below values

- [ ] **Step 3: Commit**

```bash
git add about.html
git commit -m "feat: add about page"
```

---

## Task 6: Contact page (`contact.html`)

**Files:**
- Create: `contact.html`

- [ ] **Step 1: Create `contact.html` with this full content**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Contact Us — SA Recovery Group</title>
  <meta name="description" content="Contact SA Recovery Group for 24/7 vehicle recovery and roadside assistance.">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="styles.css">
</head>
<body>

  <!-- Navbar -->
  <nav class="navbar">
    <a href="index.html" class="navbar-logo">
      <img src="white-black logo.png" alt="SA Recovery Group">
    </a>
    <ul class="navbar-links">
      <li><a href="index.html">Home</a></li>
      <li><a href="services.html">Services</a></li>
      <li><a href="about.html">About</a></li>
      <li><a href="contact.html">Contact</a></li>
    </ul>
    <button class="hamburger" aria-label="Toggle menu" aria-expanded="false">
      <span></span><span></span><span></span>
    </button>
  </nav>
  <div class="mobile-menu">
    <a href="index.html">Home</a>
    <a href="services.html">Services</a>
    <a href="about.html">About</a>
    <a href="contact.html">Contact</a>
  </div>

  <!-- Page Hero -->
  <div class="page-hero">
    <h1>Contact Us</h1>
    <p class="breadcrumb">Home &rsaquo; <span>Contact</span></p>
  </div>

  <!-- Contact Section -->
  <section class="section">
    <div class="container">
      <div class="contact-grid">

        <!-- Form -->
        <div class="contact-form">
          <h2>Send Us a Message</h2>
          <form id="contact-form" novalidate>
            <div class="form-group">
              <label for="name">Full Name</label>
              <input type="text" id="name" name="name" placeholder="John Smith" required>
            </div>
            <div class="form-group">
              <label for="phone">Phone Number</label>
              <input type="tel" id="phone" name="phone" placeholder="+27 XX XXX XXXX" required>
            </div>
            <div class="form-group">
              <label for="email">Email Address</label>
              <input type="email" id="email" name="email" placeholder="john@example.com" required>
            </div>
            <div class="form-group">
              <label for="service">Service Required</label>
              <select id="service" name="service" required>
                <option value="" disabled selected>Select a service...</option>
                <option value="towing">Towing</option>
                <option value="roadside">Roadside Assistance</option>
                <option value="jumpstart">Jump Start</option>
                <option value="tyre">Flat Tyre Change</option>
                <option value="fuel">Fuel Delivery</option>
                <option value="accident">Accident Recovery</option>
                <option value="longdistance">Long-Distance Towing</option>
              </select>
            </div>
            <div class="form-group">
              <label for="message">Message</label>
              <textarea id="message" name="message" placeholder="Describe your situation or leave a message..."></textarea>
            </div>
            <button type="submit" class="btn btn-primary btn-submit">Send Message</button>
          </form>
        </div>

        <!-- Info -->
        <div class="contact-info">
          <h2>Get In Touch</h2>
          <div class="info-item">
            <div class="info-icon">📞</div>
            <div>
              <h4>Phone</h4>
              <p>+27 XX XXX XXXX</p>
            </div>
          </div>
          <div class="info-item">
            <div class="info-icon">✉️</div>
            <div>
              <h4>Email</h4>
              <p>info@sarecoverygroup.co.za</p>
            </div>
          </div>
          <div class="info-item">
            <div class="info-icon">📍</div>
            <div>
              <h4>Based In</h4>
              <p>South Africa</p>
            </div>
          </div>
          <div class="info-item">
            <div class="info-icon">🕐</div>
            <div>
              <h4>Operating Hours</h4>
              <p>24/7 — Every Day of the Year</p>
            </div>
          </div>
        </div>

      </div>
    </div>
  </section>

  <!-- Footer -->
  <footer class="footer">
    <div class="footer-grid">
      <div class="footer-brand">
        <img src="white-black logo.png" alt="SA Recovery Group">
        <p>Professional vehicle recovery and roadside assistance, available around the clock.</p>
      </div>
      <div class="footer-col">
        <h4>Quick Links</h4>
        <a href="index.html">Home</a>
        <a href="services.html">Services</a>
        <a href="about.html">About Us</a>
        <a href="contact.html">Contact</a>
      </div>
      <div class="footer-col">
        <h4>Contact</h4>
        <p>📞 +27 XX XXX XXXX</p>
        <p>✉️ info@sarecoverygroup.co.za</p>
        <p>📍 South Africa</p>
        <p>🕐 24/7 Operations</p>
      </div>
    </div>
    <div class="footer-bottom">
      &copy; 2026 SA Recovery Group. All rights reserved.
    </div>
  </footer>

  <script src="main.js"></script>
</body>
</html>
```

- [ ] **Step 2: Open `contact.html` in a browser. Verify:**
  - "Contact" nav link is active
  - Form fields all render: name, phone, email, service dropdown (7 options), message textarea
  - Submit button is amber, full width
  - Submit shows alert "Thank you! We'll be in touch shortly." and resets form
  - Right column shows 4 info items with amber icons
  - On mobile: columns stack vertically

- [ ] **Step 3: Final commit**

```bash
git add contact.html
git commit -m "feat: add contact page"
```

---

## Task 7: Final cross-page verification

- [ ] **Step 1: Open `index.html` — click every nav link and confirm each page loads and active link highlights correctly**

- [ ] **Step 2: Resize browser to 375px width (mobile). On every page verify:**
  - Hamburger icon visible, nav links hidden
  - Tap hamburger — dropdown opens with all 4 links
  - Tap outside — dropdown closes
  - Cards stack to single column
  - Hero text readable and not overflowing

- [ ] **Step 3: On `index.html`, click "Get Help Now" — confirm it navigates to `contact.html`**

- [ ] **Step 4: On `index.html`, click "See All Services" — confirm it navigates to `services.html`**

- [ ] **Step 5: Check all Unsplash images load. If any return a broken image:**
  - Hero/page-hero background: replace the URL in `.hero` and `.page-hero` in `styles.css` with `https://images.unsplash.com/photo-1502877338535-766e1452684a?w=1600&auto=format&fit=crop`
  - About image: replace `src` in `about.html` with `https://images.unsplash.com/photo-1486262715619-67b85e0b08d3?w=800&auto=format&fit=crop`
  - Image strip: replace URL in `.img-strip` in `styles.css` with `https://images.unsplash.com/photo-1502877338535-766e1452684a?w=1600&auto=format&fit=crop`

- [ ] **Step 6: Final commit**

```bash
git add -A
git commit -m "feat: complete SA Recovery Group demo website"
```
