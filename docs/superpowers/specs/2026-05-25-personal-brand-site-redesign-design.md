# Personal Brand Site Redesign — Design Spec

**Date:** 2026-05-25
**Owner:** Sandeep Sundaram
**Repo:** `sandeepsundaram.github.io` (GitHub Pages)
**Status:** Draft — pending user review

## 1. Goal

Transform the current single-page resume (`index.html`) into a **bold, modern personal brand site** that works for four audiences in priority order:

1. Potential clients/customers (Data Equity prospects, advisory)
2. Investors/partners (founder credibility)
3. Recruiters/employers (clean experience + PDF)
4. Fellow engineers/network (writing, depth)

**Primary CTA:** Connect on LinkedIn.

**Constraints:**
- Stay on GitHub Pages — no backend, no build step in v1.
- Single `index.html` file remains the source. Existing print/PDF flow must keep working.
- Existing GitHub Actions deploy (`aws.yml`) must keep working.

## 2. Approach

**Approach A: Single-page evolution.** Restructure `index.html` into a landing experience with sticky nav, hero, refreshed sections, Medium feed via RSS, expandable case studies. Dark by default with a light toggle. No SSG, no framework, no build step.

Rejected alternatives:
- *Approach B (Multi-page Jekyll/11ty):* Better long-term scaling but bigger upfront refactor. Revisit once content stabilises.
- *Approach C (Single-page + modal case studies):* Modals weaken SEO and don't add enough value over inline expansion.

## 3. Information architecture

Page reads top-to-bottom; sticky nav anchors to each section.

1. **Sticky top nav** — wordmark "Sandeep", anchor links (`Work`, `Projects`, `Writing`, `About`), primary `Connect` button (LinkedIn), theme toggle.
2. **Hero** — full-viewport. Typographic statement + subline + three headline metrics + CTA pair (LinkedIn primary, "See my work" secondary).
3. **About / Now** — 3–4 sentence narrative about current focus at Data Equity. Photo aside.
4. **Work** — vertical timeline of roles. Most recent at top. Oracle + Accenture collapse into "Earlier roles" block.
5. **Featured projects** — three expandable case study cards: Data Equity AI Schema Builder, DE API Developer Portal, DE Peppol Access Point.
6. **Writing** — 3–4 most recent Medium posts pulled at runtime via RSS.
7. **Skills** — tightened tag grid (kept from current site).
8. **Contact footer** — final CTA block, LinkedIn primary, secondary email/phone/location.
9. **Floating PDF download** — kept; print stylesheet renders clean resume.

## 4. Visual system

### Palette

| Role | Dark (default) | Light |
|---|---|---|
| Background | `#0a0a0b` | `#ffffff` |
| Surface (cards) | `#1f1f23` | `#f5f5f7` |
| Border | `#2a2a30` | `#e5e5ea` |
| Text primary | `#ededed` | `#111114` |
| Text muted | `#9999a3` | `#5e5e66` |
| Accent | `#6366f1` (indigo) → `#a855f7` (violet) gradient | same |

### Typography

- **Display + body:** Geist Sans (CDN), Inter fallback. Weights 400 / 600 / 700 / 800.
- **Mono accents:** JetBrains Mono for metrics, tags, dates.
- **Scale:** hero headline `clamp(2.5rem, 8vw, 6rem)`. Section headings ~2rem. Body 1rem with 1.65 leading.
- `font-display: swap` to avoid blocking.

### Layout & motion

- Content max-width 1200px. Section vertical rhythm ~120px desktop / ~64px mobile.
- Subtle noise/grain overlay at 3% opacity on dark mode.
- Hero background: animated indigo→violet gradient orb (existing pattern, refined).
- Scroll reveal via IntersectionObserver (existing — keep, tighten timing).
- Card hover: 4px lift + accent-color glow (not generic shadow).
- All non-essential motion disabled under `prefers-reduced-motion`.

### Iconography

- Replace Font Awesome with **Lucide icons** (CDN: `https://unpkg.com/lucide@latest`).

### Components

- **Cards:** 1px tinted-gray border, no heavy shadow, subtle top-edge highlight.
- **Buttons:** primary = solid accent fill; secondary = 1px outlined. Radius 6px. Not pill-shaped.
- **Tags:** mono, smaller, lowercase, faint border, accent text color. No gradient fills.

## 5. Component specifications

### 5.1 Hero

- Left-aligned, full-viewport on desktop.
- Headline: **"I build engineering teams that ship."** — accent gradient on "teams that ship".
- Subline: "21 years across energy, utilities, ERP, and AI. Cofounder, architect, and people-first leader."
- Metric row (mono): `21 yrs experience` · `£140M delivered` · `25 engineers led`.
- CTAs: `Connect on LinkedIn →` (primary) and `See my work` (secondary, anchor to `#work`).
- Avatar (existing `static/img/sandeep.jpeg`) floats top-right at smaller size.

### 5.2 Work timeline

- Single column. Vertical accent line on left.
- Each role card: title (large), company (accent), dates (mono, right). 2–3 outcome-led bullets max. Optional inline mono tags for stack/scope.
- Roles to show in full:
  - Cofounder & Director of AI — Data Equity Ltd (Mar 2023 – Present)
  - Ex-Cofounder & CTO — Perse Technologies Ltd (Feb 2020 – Feb 2023)
  - Principal Architect — Enzen Global UK (Jan 2014 – Feb 2020)
  - Solutions Architect — Apigee Technologies / Google (Nov 2011 – Jan 2014)
- Collapsed into "Earlier roles" block:
  - Principal Software Engineer — Oracle India (Jun 2005 – Nov 2011)
  - Software Engineer — Accenture (Jan 2004 – Jun 2005)

### 5.3 Featured project case studies

Three cards. Each collapsed by default:
- Project name (large) + company + year (right).
- One-line value statement.
- Headline outcome metric in big mono text.
- Toggle: `Read case study ↓`.

Expanded inline content per card:
- **Problem** (2–3 sentences)
- **Approach** (3–5 bullets)
- **Impact** (outcome metrics, qualitative wins)
- **Stack** (mono tag row)
- **Link out** (external project page if applicable)

Card content:

**1. AI-Powered API Schema Builder — Data Equity, 2023**
- Value: Generative AI schema builder trained on 16,000+ API definitions; RAG-based enterprise contract generator.
- Headline metric: `60% automation lift`.
- Stack: Python, PyTorch, RAG, ReactJS, Azure, Docker.

**2. DE API Developer Portal — Data Equity, 2024**
- Value: Unified portal for API discovery, integration, and monetisation. Swagger/Redoc/GraphQL docs; flexible pricing (subscription, PAYG, freemium); pre-built onboarding workflows; analytics.
- Headline metric: `faster API time-to-market` (replace with quantified metric if available).
- Stack: ReactJS, Python/FastAPI, Azure.
- Link: https://www.dataequity.io/products/de-marketplace

**3. DE Peppol Access Point — Data Equity, 2024–25**
- Value: Certified Peppol gateway for cross-border eInvoicing across 20+ jurisdictions. Single REST API, AS4 over TLS 1.3, BIS 3.0 + country-specific XML validation, multi-tenant RBAC, ISO 27001, tamper-evident archiving.
- Headline metric: `99.95% uptime SLA`.
- Stack: Python, AS4, UBL/PINT, Azure.
- Link: https://www.dataequity.io/products/de-peppol-access-point

### 5.4 Writing (Medium feed)

- Source: `https://medium.com/feed/@dataequity` via `api.rss2json.com` proxy.
- Render up to 4 most recent posts: title (link), relative date (`Intl.RelativeTimeFormat`), 120-char excerpt with HTML stripped, link to canonical Medium URL.
- "View all on Medium →" link at the bottom.
- Loading state: 3 skeleton rows.
- Failure / empty / parse error → replace with a single "Read all posts on Medium →" link. Section never shows broken state.

### 5.5 Skills

- Keep existing 6 categories (Programming Languages, Frontend, Cloud, API & Integration, Databases, Domain Expertise).
- Render as compact tag grid using new mono tag style. Lose the heavy gradient fills.
- Drop the duplicated "Core Leadership Strengths" tag grid — fold those points into hero metrics + work bullets where they're already implied.

### 5.6 Contact footer

- Final CTA block: large "Let's talk." heading.
- Primary: `Connect on LinkedIn →` button.
- Secondary inline links: email, phone, location, Medium, GitHub.
- Small print: "© 2026 Sandeep Sundaram · Built with care · Last updated 2026-05-25".

### 5.7 Sticky top nav

- Always visible from page load, so `Connect` is reachable from any scroll position (especially on mobile).
- Background transparent over the hero; switches to a frosted-blur opaque background once the user scrolls past the hero.
- Active section highlighted as user scrolls (IntersectionObserver).
- Mobile: collapses to a hamburger that opens a full-screen overlay menu.

### 5.8 Theme toggle

- Sun/moon Lucide icon button in top nav.
- Default: dark. First visit respects `prefers-color-scheme` if user hasn't chosen.
- Persists choice in `localStorage` key `theme`.
- Applied via `data-theme="light"` attribute on `<html>`; CSS reads `[data-theme="light"]` overrides.
- `aria-pressed` reflects state.

### 5.9 Floating PDF download

- Kept. Print stylesheet:
  - Hides nav, theme toggle, animations, gradient orb, hover states.
  - Forces light theme.
  - Auto-expands all case studies for print.
  - One clean A4 layout. Links rendered as accent-color text (URL not appended).

## 6. Data flow

### 6.1 Medium RSS

- **Endpoint:** `https://api.rss2json.com/v1/api.json?rss_url=https%3A%2F%2Fmedium.com%2Ffeed%2F%40dataequity`
- **Fetch:** on `DOMContentLoaded`, wrapped in `Promise.race` against a 5-second timeout.
- **Caching:** parsed result stored in `localStorage` key `medium-feed-v1` with 30-minute TTL. On subsequent loads, render cache instantly; revalidate in background; swap DOM if newer.
- **Per post:** title, ISO date → "5 days ago" via `Intl.RelativeTimeFormat`, excerpt from `description` (strip HTML, truncate ~120 chars), canonical Medium link.
- **Fallbacks (in this order):**
  - Proxy down / 4xx / 5xx / timeout → replace skeletons with single `<a>` to `https://dataequity.medium.com/`.
  - Empty feed → same fallback.
  - Parse error → `console.warn`, same fallback.
- **No analytics in v1.** Add later if desired.

### 6.2 Theme persistence

- Read `localStorage.theme` synchronously in a `<head>` inline script before paint to prevent flash of incorrect theme.
- If absent, check `window.matchMedia('(prefers-color-scheme: light)')`.
- Set `document.documentElement.dataset.theme`.

## 7. Accessibility

- Semantic landmarks (`<header>`, `<nav>`, `<main>`, `<section aria-labelledby>`, `<footer>`).
- All interactive controls are real `<button>` or `<a>` elements; keyboard-accessible; visible focus rings (`outline: 2px solid <accent>` with offset).
- Case study toggles use `aria-expanded`; theme toggle uses `aria-pressed`.
- Color contrast: WCAG AA verified for both themes (indigo accent passes against both bgs).
- `prefers-reduced-motion` honored: kills gradient orb, fade-ins, hover lifts.
- Skip-to-main link at the top for screen readers.

## 8. SEO / metadata

Additions to `<head>`:
- `<meta name="description">` — one-line professional summary.
- `<meta name="keywords">` — engineering leader, CTO, cofounder, API, Peppol, energy, AI.
- `<link rel="canonical">` to `https://sandeepsundaram.github.io/`.
- OpenGraph: `og:title`, `og:description`, `og:url`, `og:image` (1200×630 PNG with hero headline + photo, committed to `static/img/og.png` — to be produced separately).
- Twitter card: `summary_large_image` with the same image.
- `<meta name="theme-color">` for browser chrome (set to `#0a0a0b` for dark, `#ffffff` for light via media query).

## 9. File layout

Everything stays in `index.html` for v1. New file added:
- `static/img/og.png` — 1200×630 OpenGraph image (separate task; can ship without it and add later).

No new dependencies installed locally. CDN-loaded assets:
- Geist Sans + JetBrains Mono via Google Fonts or `vercel/geist-font` CDN.
- Lucide icons via `https://unpkg.com/lucide@latest`.

## 10. Verification checklist

Run in browser before merging to `main`:

1. **Layout / responsive** — DevTools widths: 1440, 1024, 768, 414, 360. No overflow, no overlap, hero readable everywhere.
2. **Cross-browser** — Spot-check Safari + Firefox (backdrop-filter, gradients can differ).
3. **Theme toggle** — Dark default; toggle to light; reload; persists. Clear `localStorage`, OS = light → respects `prefers-color-scheme`.
4. **Reduced motion** — OS "Reduce motion" on → orb, fade-ins, lifts all disabled.
5. **Medium feed:**
   - Happy path: posts render correctly.
   - Failure: block `api.rss2json.com` in DevTools → fallback link-out shows.
   - Cache: second load renders feed before network completes.
6. **Case study expand/collapse** — Click + keyboard (`Tab` → `Enter`/`Space`); multiple open simultaneously; screen reader announces state.
7. **Navigation** — Sticky nav visible on scroll; anchor links smooth-scroll; active section highlighted.
8. **Print/PDF** — `Cmd-P`: clean A4, no nav/toggle/orb, case studies expanded, light theme forced.
9. **Lighthouse Accessibility** — Target ≥95.
10. **Lighthouse Performance** — Target ≥90 desktop.
11. **Keyboard-only walkthrough** — Tab through page top to bottom; every interactive element reachable; focus visible.

## 11. Rollout

- Branch: `redesign-v2`.
- Single squashed commit when ready.
- Pre-merge: walk the checklist above; capture before/after screenshots in PR description.
- Push to `main` triggers existing GitHub Actions deploy.
- No automated tests in v1. If the page grows beyond a single file later, that's when we add Playwright smoke tests.

## 12. Open items / explicit non-goals

**Open items (decide during implementation):**
- Exact quantified metric for DE API Developer Portal headline (currently placeholder "faster API time-to-market"). If none available by ship, headline metric will be replaced with a count-based fact like `Swagger · Redoc · GraphQL`.
- Whether OG image ships in v1 or as a follow-up. Default: ship as follow-up; site works without it.

**Non-goals for v1:**
- Multi-page architecture / static site generator.
- Per-project deep-dive pages.
- Testimonials section.
- Analytics integration.
- Contact form (LinkedIn is the CTA).
- Speaking/writing index beyond the Medium feed.
- Animated illustrations or 3D effects.
