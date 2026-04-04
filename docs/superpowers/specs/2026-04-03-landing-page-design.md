# imaginalvision.com Landing Page — Design Spec

**Date:** 2026-04-03
**Status:** Approved
**Approach:** Narrative Scroll (single-page)

## Overview

imaginalvision.com is the professional identity site for Cassandra Clark (LMFT #116676), serving as the front door to her expressive arts therapy practice and the digital tools she's built. The landing page is a narrative scroll that tells the story of the Imaginal Vision brand, presents the tools, identifies who they're for, and connects to her counseling practice.

## Audiences (priority order)

1. **Existing therapy clients** — using Art Cards and Dreamspace as part of their therapeutic work
2. **Expressive arts students/educators** — her master's class and CIIS program using Art Cards for intake training
3. **Fellow therapists** — evaluating the tools for use with their own clients (in-person or telehealth)
4. **Creative explorers** — laypersons who want to make art, explore collage, or browse the card deck — no therapy context, just curiosity
5. **Potential new clients** — discovering Cassandra through search or referral

## Architecture

### Hosting & Deployment

- **Landing page + Art Cards static build** → Cloudflare Pages (free), deployed from the `imaginalvision.com` repo
- **Dreamspace** → Stays on Fly.io (`dreamspace.fly.dev`), CNAME'd as `dreamspace.imaginalvision.com`
- **Art Cards API** → Migrated from Vercel into the Dreamspace Go server on Fly.io (endpoints: `/api/artcards/*`)
- **Creative Sight Counseling** → Stays on Canva for now, linked from landing page. Will be rebuilt under this project in a later phase.
- **DNS** → Cloudflare (domain already registered there)

### Domain Structure

| URL | What | Hosting |
|-----|------|---------|
| `imaginalvision.com` | Landing page (this spec) | Cloudflare Pages |
| `artcards.imaginalvision.com` | Art Cards React SPA | Cloudflare Pages (subpath or subdomain) |
| `dreamspace.imaginalvision.com` | Dreamspace collage tool | Fly.io (CNAME) |
| `creativesightcounseling.com` | Counseling practice | Canva (for now) |

### Repository Structure

```
imaginalvision.com/
├── index.html              # Landing page (single file, embedded CSS)
├── favicon.svg             # SVG favicon
├── imaginal-vision-precision.html  # Domain proposal page (reference)
└── docs/
    └── superpowers/
        └── specs/
            └── 2026-04-03-landing-page-design.md  # This file
```

## Page Sections

### 1. Hero

Full-viewport hero with the Imaginal Vision brand.

- **Title:** "Imaginal Vision" in Cormorant Garamond italic
- **Subtitle:** "EXPRESSIVE ART THERAPY & DIGITAL TOOLS" in Inter, small caps, letter-spaced
- **Tagline:** "Where creative expression meets therapeutic insight"
- **Background:** Warm gradient (light mode: `#f5f0eb → #e8e0d8 → #d4c8bb → #c9b8a8`; dark mode: `#0f0a12 → #1a1320 → #251a30`) with subtle drift animation
- **Scroll hint:** "scroll to explore" with pulse animation at bottom
- **Sticky nav:** Minimal anchor links (Art Cards | Dreamspace | About) that appear after scrolling past the hero, so returning users can jump straight to what they need

### 2. The Tools

Two side-by-side cards presenting Art Cards and Dreamspace. Tools first — get people clicking immediately.

- **Art Cards card:**
  - Screenshot/preview area (dark background with gold tint, referencing Art Cards' aesthetic)
  - Title: "Art Cards"
  - Description: Expressive art card deck for therapeutic exploration, dreamwork, and clinical training
  - Credential: "Used at CIIS for intake training"
  - CTA button: "Explore →" linking to `artcards.imaginalvision.com`
  - Hover: Gold glow (`#c9a84c` shadow)

- **Dreamspace card:**
  - Screenshot/preview area (dark background with lavender tint, referencing Dreamspace's aesthetic)
  - Title: "Dreamspace"
  - Description: Digital collage tool for dreamwork and creative self-exploration
  - Note: "Self-guided or therapist-facilitated"
  - CTA button: "Create →" linking to `dreamspace.imaginalvision.com`
  - Hover: Lavender glow (`#a78bfa` shadow)

- Cards are responsive: side-by-side on desktop, stacked on mobile.

### 3. What is the Imaginal?

Brief, accessible explanation of the imaginal tradition — for those who scroll past the tools, this rewards their curiosity. Not the full academic treatment from the domain proposal.

- 2-3 paragraphs: Corbin coined the term → Hillman made it central to psychology → McNiff brought it to expressive arts therapy
- One featured quote (Hillman or Casey)
- Warm, inviting tone — not academic

### 4. Who It's For

Four blocks addressing each audience directly:

- **Clients** — "Use Art Cards and Dreamspace between sessions or during telehealth to deepen your expressive arts work."
- **Students & Educators** — "A training tool for expressive arts programs. Currently used at CIIS for intake training."
- **Therapists** — "Integrate these tools into your own practice, whether you work in-person or remotely."
- **Creative Explorers** — "No therapy background needed. Browse the card deck, create a collage, see what emerges."

### 5. About Cassandra

Brief professional bio:

- Name: Cassandra Clark
- Credentials: LMFT #116676
- Education: California Institute of Integral Studies (CIIS), San Francisco
- Experience: 9+ years clinical experience
- Orientation: Jungian and transpersonal psychology, expressive arts therapy
- Photo: Placeholder (to be provided)
- Link to Creative Sight Counseling practice

### 6. Creative Sight Counseling

Compact practice information:

- Modalities: Expressive arts (drawing, painting, collage, writing, music, dance), guided imagery, meditation, mindfulness-based CBT, dreamwork, sandtray, ritual work
- Populations: Anxiety, grief, trauma, PTSD, women's issues, LGBTQ+, self-esteem, spirituality
- Pricing: Private-pay sliding scale $132-200/session, plus insurance
- Location: Nevada City, CA — in-person and online for California residents
- CTA: "Learn more" → creativesightcounseling.com
- Note: Groups & workshops section coming in 2026

### 7. Footer

- Contact method (email or form — TBD with Cassandra)
- Instagram: @creative.sight.counseling
- Client portal link (TheraNext)
- License: LMFT #116676
- Copyright

## Visual Design

### Typography

| Role | Font | Weight | Usage |
|------|------|--------|-------|
| Display/brand | Cormorant Garamond | 400 italic | Hero title, section headers, quotes |
| Section headers | Cormorant Garamond | 600 | H2 elements |
| Body text | Inter | 300 | Paragraphs, descriptions |
| UI/labels | Inter | 400-500 | Buttons, navigation, small caps labels |

Google Fonts import: `Cormorant+Garamond:ital,wght@0,400;0,600;1,400` and `Inter:wght@300;400;500`.

### Color — Light Mode (default, `prefers-color-scheme: light`)

| Token | Value | Usage |
|-------|-------|-------|
| `--bg` | `#faf9f7` | Page background |
| `--bg-warm` | `#f5f0eb` | Section backgrounds, quote blocks |
| `--bg-gradient-start` | `#f5f0eb` | Hero gradient start |
| `--bg-gradient-end` | `#c9b8a8` | Hero gradient end |
| `--text-primary` | `#3a3028` | Headlines, strong text |
| `--text-body` | `#4a4a4a` | Body paragraphs |
| `--text-secondary` | `#5a4a3a` | Taglines, quotes |
| `--text-muted` | `#8a7a6a` | Labels, captions |
| `--accent-earth` | `#c9b8a8` | Dividers, decorative lines |
| `--accent-gold` | `#c9a84c` | Art Cards hover glow, accents |
| `--accent-lavender` | `#a78bfa` | Dreamspace hover glow, accents |
| `--border` | `#ebe6e0` | Card borders, section dividers |

### Color — Dark Mode (`prefers-color-scheme: dark`)

| Token | Value | Usage |
|-------|-------|-------|
| `--bg` | `#0f0a12` | Page background (violet-black, bridging Dreamspace) |
| `--bg-warm` | `#1a1320` | Section backgrounds |
| `--bg-gradient-start` | `#1a1320` | Hero gradient start |
| `--bg-gradient-end` | `#251a30` | Hero gradient end |
| `--text-primary` | `#f5f0eb` | Headlines (warm cream) |
| `--text-body` | `#d4c8bb` | Body paragraphs |
| `--text-secondary` | `#c9b8a8` | Taglines, quotes |
| `--text-muted` | `#8a7a6a` | Labels, captions |
| `--accent-earth` | `#c9b8a8` | Dividers, decorative lines |
| `--accent-gold` | `#c9a84c` | Art Cards hover glow |
| `--accent-lavender` | `#c4b5fd` | Dreamspace hover glow |
| `--border` | `rgba(255, 255, 255, 0.08)` | Card borders |

### Motion

- **Hero drift:** Slow background gradient shift (20s cycle), same as proposal page
- **Scroll fade-in:** Sections fade in with slight upward translate on scroll (`IntersectionObserver`, no library)
- **Tool card hover:** Soft glow — gold for Art Cards, lavender for Dreamspace
- **Scroll hint pulse:** Gentle opacity animation at hero bottom
- **`prefers-reduced-motion`:** All animations disabled; content appears immediately

### Responsive Breakpoints

| Breakpoint | Behavior |
|------------|----------|
| ≥768px | Desktop: tool cards side-by-side, wider content column (760px max) |
| <768px | Mobile: tool cards stacked, full-width padding, smaller hero text |

### Favicon

SVG favicon. Simple mark that works at small sizes — suggest an abstract eye or lens shape in earth tones, referencing "vision" in the brand name.

## Technical Implementation

- **Single HTML file** with embedded `<style>` — no build step, no dependencies
- **CSS custom properties** for all theme colors, switched via `@media (prefers-color-scheme: dark)`
- **Google Fonts** loaded via `@import` in CSS
- **Scroll animations** via vanilla JS `IntersectionObserver` (no library)
- **No JavaScript framework** — pure HTML/CSS with minimal JS for scroll effects
- **Cloudflare Pages** deployment — connect GitHub repo, auto-deploy on push to `main`

## Future Phases (out of scope for this spec)

1. **Migrate Art Cards API** from Vercel to Dreamspace Fly.io server
2. **Art Cards subdomain** — deploy static React build to `artcards.imaginalvision.com` via Cloudflare Pages
3. **Dreamspace subdomain** — CNAME `dreamspace.imaginalvision.com` to Fly.io
4. **Rebuild Creative Sight Counseling** — replace Canva site with a purpose-built page under this project
5. **Content from Cassandra** — professional photo, refined bio text, workshop announcements
