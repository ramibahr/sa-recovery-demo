# SA Recovery Group — Demo Website Design Spec

**Date:** 2026-05-05  
**Project:** SA Recovery Group demo website  
**Stack:** Plain HTML / CSS / JS (no build tools)

---

## Overview

A static multi-page demo website for SA Recovery Group, a car recovery business. Four pages with a shared navbar, footer, and stylesheet. Images sourced from Unsplash via URL. Logo files already present in the project root.

---

## File Structure

```
sa-recovery-demo/
├── index.html
├── services.html
├── about.html
├── contact.html
├── styles.css
├── main.js
├── white-black logo.png
└── black logo.png
```

---

## Design Tokens

| Token | Value |
|---|---|
| Primary dark | `#1a1a2e` |
| Accent amber | `#f59e0b` |
| Amber hover | `#d97706` |
| Page background | `#f9fafb` |
| Card background | `#ffffff` |
| Body text | `#374151` |
| Muted text | `#6b7280` |
| Font | Inter (Google Fonts) |

---

## Shared Components

### Navbar
- Background: `#1a1a2e`
- Logo: `white-black logo.png` on the left, links to `index.html`
- Nav links right-aligned: Home · Services · About · Contact
- Active link: amber underline (`#f59e0b`)
- Mobile: hamburger icon toggles a vertical dropdown via `main.js`

### Footer
- Background: `#1a1a2e`, white text
- Left: logo (`white-black logo.png`) + tagline
- Center: nav links
- Right: placeholder phone, email
- Bottom bar: copyright © SA Recovery Group 2026

### Page Hero (inner pages)
- Height: ~280px
- Background: `#1a1a2e` with a subtle truck Unsplash image overlay
- Centered white page title + short breadcrumb

---

## Pages

### 1. Home (`index.html`)

**Hero section**
- Full viewport height (`100vh`)
- Background: Unsplash recovery truck photo (`https://images.unsplash.com/photo-1558618666-fcd25c85cd64?w=1600`) with `rgba(26,26,46,0.72)` overlay
- Centered content:
  - Headline: *"24/7 Vehicle Recovery You Can Count On"* (white, 3rem+)
  - Subline: *"Fast, reliable roadside assistance across the region"* (light gray, 1.2rem)
  - CTA button: **"Get Help Now"** → `contact.html`, amber background, dark text, rounded

**Services Preview**
- Section title: "Our Services"
- 3 cards: Towing · Roadside Assistance · Accident Recovery
- Each card: icon (emoji or SVG), bold title, one-line description
- "See All Services →" link below cards

**Why Choose Us**
- 3 stat blocks: "24/7 Available" · "30-Min Response" · "Fully Licensed & Insured"
- Dark charcoal background, amber icon accents

**CTA Banner**
- Amber background, dark text: *"Stranded? We're on our way."*
- Button: **"Contact Us Now"** → `contact.html`

---

### 2. Services (`services.html`)

**Page Hero**
- Title: "Our Services"

**Service Cards Grid**
- 7 cards in a responsive grid (3 columns desktop, 2 tablet, 1 mobile)
- Services:
  1. Towing
  2. Roadside Assistance
  3. Jump Starts
  4. Flat Tyre Changes
  5. Fuel Delivery
  6. Accident Recovery
  7. Long-Distance Towing
- Each card: icon, bold title, 2-line description, amber accent border-top

**Bottom CTA Banner**
- Same amber CTA banner as home, linking to `contact.html`

---

### 3. About Us (`about.html`)

**Page Hero**
- Title: "About SA Recovery Group"

**Story Section**
- Two-column layout (desktop): left = text, right = Unsplash truck image
- Text covers: company background (placeholder copy), mission statement, years of service
- Responsive: stacks to single column on mobile

**Values Section**
- 3 pill/card items: Fast · Reliable · Professional
- Dark background with amber icons

**Truck Image Strip**
- Full-width Unsplash recovery truck image (decorative, `object-fit: cover`, fixed height 300px)

---

### 4. Contact (`contact.html`)

**Page Hero**
- Title: "Contact Us"

**Two-Column Layout**
- Left column — Contact Form:
  - Fields: Full Name (text), Phone Number (tel), Email (email), Service Required (select dropdown with all 7 services), Message (textarea)
  - Submit button: amber, full-width on mobile
  - On submit: JS `alert()` confirmation — *"Thank you! We'll be in touch shortly."* — form resets
- Right column — Contact Info:
  - Phone: +27 XX XXX XXXX (placeholder)
  - Email: info@sarecoverygroup.co.za (placeholder)
  - Address: placeholder address, South Africa
  - Operating hours: 24/7

---

## Responsive Behaviour

- Breakpoints: 768px (tablet), 480px (mobile)
- Navbar collapses to hamburger below 768px
- All grids collapse to single column on mobile
- Hero text scales down on mobile

---

## Assets

- **Logo:** `white-black logo.png` — navbar and footer (on dark backgrounds); `black logo.png` — not used (dark-on-dark would be invisible)
- **Images:** Unsplash URLs embedded directly, no local downloads required. Exact photo IDs to be confirmed as valid during implementation; swap for any working Unsplash recovery/truck photo if a URL returns a 404.
  - Hero truck: recovery truck / tow truck search
  - About image: roadside / vehicle recovery scene
  - Inner page hero: same hero truck image, darker overlay

---

## JS (`main.js`)

- Mobile nav toggle (hamburger open/close)
- Contact form submit handler (prevent default, show alert, reset form)
- Active nav link highlighting based on current page filename

---

## Out of Scope

- Backend / form email delivery
- CMS or dynamic content
- Animations beyond CSS transitions
- SEO meta tags beyond basic title/description
