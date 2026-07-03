# Kingswell & Partners — Website

A 7-page corporate/NRI law firm website: dark navy + gold theme, a real
Parliament House background image in the hero (matching the reference
screenshot you shared), scroll reveals, animated counters, a mobile
slide-in menu, an FAQ accordion, and a validated consultation form.

## What's inside

```
kingswell-legal/
├── index.html            Home
├── about.html
├── practice-areas.html   8 practice areas
├── nri.html
├── team.html
├── insights.html         Articles grid + FAQ accordion
├── contact.html          Consultation form + map
├── css/style.css
├── js/script.js          Nav, scroll reveal, counters, FAQ, form validation
└── php/contact-handler.php   Optional — see "About the PHP request" below
```

No build step. No framework. Open `index.html` directly in a browser to preview.

## About the motion effects

The animations were built directly in CSS + vanilla JavaScript, matching what
you liked on the reference site:

- **Sticky header** that gains a blur/background on scroll (`initHeaderScroll`)
- **Scroll-triggered reveals** — sections fade/slide in as you scroll, using
  `IntersectionObserver` (`initScrollReveal`), staggered with `.reveal-delay-1/2/3`
- **Animated counters** that count up when they enter view (`initCounters`)
- **Mobile slide-in menu** with a scrim overlay
- **FAQ accordion** with animated height + rotating "+" icon
- **Hover micro-interactions** on cards, buttons, and nav links
- **Ambient hero motion** — a slow Ken Burns drift on the Parliament House
  background, and a gentle float on the photo placeholder

## About the PHP request

You asked to "add these motion effects using PHP." Worth clarifying so you
don't spend time on the wrong thing: **animation and motion effects are a
front-end concern — they run in the browser via CSS/JavaScript, not on a
PHP server.** PHP runs *before* the page is even sent to the visitor, so it
has no way to control what happens after the page loads (scrolling, hover,
clicks). This isn't a limitation of this build — it's true of every website.

What PHP *is* actually useful for here is the **contact form backend**
(receiving the enquiry and emailing it to you), which is a separate concern
from the animations. I've included `php/contact-handler.php` for that.
Two honest options, pick one:

### Option A — Static hosting + Formspree (recommended, easiest)
GitHub Pages (free) only serves static files — it cannot run PHP at all.
Use [Formspree](https://formspree.io) (free tier available) to receive form
submissions by email with zero backend code:

1. Create a free Formspree account, create a form, copy your form ID.
2. In `contact.html`, replace `YOUR_FORM_ID` in:
   ```html
   <form id="consultation-form" data-endpoint="https://formspree.io/f/YOUR_FORM_ID">
   ```
3. Done — submissions land in your inbox. No PHP needed.

### Option B — Real PHP hosting
If you specifically want your own PHP backend (e.g. you're moving off
GitHub Pages to a host like Hostinger, cPanel, or a VPS):

1. Upload the whole `kingswell-legal/` folder including `php/contact-handler.php`.
2. Open `php/contact-handler.php` and set `$to_email` to your real address.
3. In `contact.html`, change the form's endpoint to:
   ```html
   <form id="consultation-form" data-endpoint="php/contact-handler.php">
   ```
4. Note: GitHub Pages **cannot** run this file — it will just download as
   text if you try. PHP requires actual PHP-capable hosting.

## Deploying to GitHub

```bash
cd kingswell-legal
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO.git
git push -u origin main
```

Then on GitHub: **Settings → Pages → Deploy from branch → main → / (root)**.
Your site will be live at `https://YOUR_USERNAME.github.io/YOUR_REPO/`
within a couple of minutes.

## Before you launch — swap these placeholders

- Phone/email/address: search for `+91 98765 43210`, `info@kingswelllegal.in`,
  and the office address in `contact.html`.
- Hero and about-page photo placeholders — replace the placeholder `<div>`
  blocks in `index.html`, `about.html`, `nri.html`, and the SVG silhouettes
  in `team.html` with real photography.
- Team member names/roles in `team.html`.
- `data-endpoint` in `contact.html` (see Option A/B above).
- Google Map: the `contact.html` map iframe currently points at "New Delhi,
  India" generally — replace the query string with your exact office address.

## The most efficient path from here

1. Preview locally by opening `index.html` in a browser (or use the
   "Live Server" extension in VS Code for auto-reload while editing).
2. Swap the placeholders above.
3. Push to GitHub and enable Pages (5 minutes).
4. Wire up Formspree (Option A) — takes about 3 minutes, no code.
5. Optional: point a custom domain at GitHub Pages via a CNAME record.

That gets you a fully live, animated site with a working contact form,
without needing to manage a server at all.
