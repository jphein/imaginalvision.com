# imaginalvision.com Landing Page Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build the imaginalvision.com landing page as a single HTML file with embedded CSS, dark/light theme support, scroll animations, and deploy to Cloudflare Pages.

**Architecture:** Single `index.html` with embedded `<style>` and minimal `<script>`. CSS custom properties for theming, `@media (prefers-color-scheme)` for dark/light switch. Vanilla JS `IntersectionObserver` for scroll fade-ins and sticky nav. No build step, no dependencies.

**Tech Stack:** HTML, CSS (custom properties, Grid, Flexbox), vanilla JS, Google Fonts (Cormorant Garamond + Inter), Cloudflare Pages.

**Spec:** `docs/superpowers/specs/2026-04-03-landing-page-design.md`

**Reference:** `imaginal-vision-precision.html` — the domain proposal page built on the Precision laptop. Reuse its gradient, font imports, and overall tone.

---

## File Structure

```
imaginalvision.com/
├── index.html          # Landing page (create — single file, all CSS/JS embedded)
├── favicon.svg         # SVG favicon (create)
└── .gitignore          # Ignore .superpowers/, node_modules, etc. (create)
```

One file to build (`index.html`), one asset (`favicon.svg`), one config (`.gitignore`). Everything else already exists.

---

### Task 1: Project Setup — .gitignore and Git Init

**Files:**
- Create: `imaginalvision.com/.gitignore`

- [ ] **Step 1: Initialize git repo**

```bash
cd /home/jp/Projects/imaginalvision.com
git init
```

- [ ] **Step 2: Create .gitignore**

```gitignore
.superpowers/
node_modules/
.env
*.swp
*~
.DS_Store
```

- [ ] **Step 3: Commit**

```bash
git add .gitignore
git commit -m "chore: init repo with .gitignore"
```

---

### Task 2: Favicon

**Files:**
- Create: `imaginalvision.com/favicon.svg`

- [ ] **Step 1: Create SVG favicon**

An abstract eye/lens shape in earth tones. Must be legible at 16x16 and 32x32.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 32 32">
  <defs>
    <linearGradient id="g" x1="0" y1="0" x2="1" y2="1">
      <stop offset="0%" stop-color="#c9b8a8"/>
      <stop offset="100%" stop-color="#5a4a3a"/>
    </linearGradient>
  </defs>
  <!-- Eye/lens outer shape -->
  <path d="M2 16 Q16 4 30 16 Q16 28 2 16Z" fill="none" stroke="url(#g)" stroke-width="2"/>
  <!-- Iris -->
  <circle cx="16" cy="16" r="5" fill="url(#g)"/>
  <!-- Pupil -->
  <circle cx="16" cy="16" r="2" fill="#3a3028"/>
</svg>
```

- [ ] **Step 2: Verify favicon renders**

Open in browser: `xdg-open /home/jp/Projects/imaginalvision.com/favicon.svg`

- [ ] **Step 3: Commit**

```bash
git add favicon.svg
git commit -m "feat: add SVG favicon — abstract eye/lens in earth tones"
```

---

### Task 3: HTML Skeleton + Hero Section

**Files:**
- Create: `imaginalvision.com/index.html`

Build the document structure, CSS custom properties for both themes, Google Fonts import, hero section, and drift animation. This is the foundation everything else builds on.

- [ ] **Step 1: Write index.html with full CSS foundation + hero**

The file should contain:

1. `<!DOCTYPE html>` with `lang="en"`, charset, viewport meta
2. `<title>Imaginal Vision — Expressive Art Therapy & Digital Tools</title>`
3. Open Graph meta tags: `og:title`, `og:description`, `og:type` (website)
4. Favicon link: `<link rel="icon" href="favicon.svg" type="image/svg+xml">`
5. `<style>` block with:
   - Google Fonts `@import` for Cormorant Garamond (400, 600, 400i) and Inter (300, 400, 500)
   - `:root` with all light mode CSS custom properties from spec
   - `@media (prefers-color-scheme: dark)` with all dark mode overrides
   - `@media (prefers-reduced-motion: reduce)` disabling all animations
   - CSS reset (`* { margin: 0; padding: 0; box-sizing: border-box; }`)
   - Base body styles: `font-family: 'Inter', sans-serif; font-weight: 300; color: var(--text-body); background: var(--bg); line-height: 1.7;`
   - `.hero` styles: full viewport height, centered flex, gradient background using `var(--bg-gradient-start)` and `var(--bg-gradient-end)`, `position: relative; overflow: hidden;`
   - `.hero::before` pseudo-element for drift animation (radial gradients, 20s `drift` keyframes — copy pattern from `imaginal-vision-precision.html`)
   - `.hero-content` with `position: relative; z-index: 1; max-width: 700px;`
   - `h1` style: Cormorant Garamond, 400 weight, italic, `clamp(3rem, 8vw, 5.5rem)`, color `var(--text-primary)`
   - `.subtitle` style: Inter, 400 weight, 1.1rem, letter-spacing 0.15em, uppercase, color `var(--text-muted)`
   - `.tagline` style: Cormorant Garamond, italic, 1.4rem, color `var(--text-secondary)`
   - `.scroll-hint` style: absolute bottom, small uppercase, pulse animation
   - `@keyframes drift` and `@keyframes pulse`
   - Section base styles: `max-width: 760px; margin: 0 auto; padding: 5rem 2rem;`
   - Responsive: `@media (max-width: 768px)` reducing hero font sizes, section padding
6. `<body>` with hero section HTML:
   - `<div class="hero">` containing `.hero-content` with `<h1>`, `.subtitle`, `.tagline`
   - `.scroll-hint` at bottom

Light mode CSS custom properties (from spec):
```css
:root {
  --bg: #faf9f7;
  --bg-warm: #f5f0eb;
  --bg-gradient-start: #f5f0eb;
  --bg-gradient-end: #c9b8a8;
  --text-primary: #3a3028;
  --text-body: #4a4a4a;
  --text-secondary: #5a4a3a;
  --text-muted: #8a7a6a;
  --accent-earth: #c9b8a8;
  --accent-gold: #c9a84c;
  --accent-lavender: #a78bfa;
  --border: #ebe6e0;
}
```

Dark mode overrides (from spec):
```css
@media (prefers-color-scheme: dark) {
  :root {
    --bg: #0f0a12;
    --bg-warm: #1a1320;
    --bg-gradient-start: #1a1320;
    --bg-gradient-end: #251a30;
    --text-primary: #f5f0eb;
    --text-body: #d4c8bb;
    --text-secondary: #c9b8a8;
    --text-muted: #8a7a6a;
    --accent-earth: #c9b8a8;
    --accent-gold: #c9a84c;
    --accent-lavender: #c4b5fd;
    --border: rgba(255, 255, 255, 0.08);
  }
}
```

Hero HTML:
```html
<div class="hero">
  <div class="hero-content">
    <h1><em>Imaginal</em> Vision</h1>
    <div class="subtitle">Expressive Art Therapy & Digital Tools</div>
    <div class="tagline">Where creative expression meets therapeutic insight</div>
  </div>
  <div class="scroll-hint">scroll to explore</div>
</div>
```

- [ ] **Step 2: Open in browser, verify both themes**

```bash
xdg-open /home/jp/Projects/imaginalvision.com/index.html
```

Verify: hero fills viewport, gradient renders, drift animation runs, text is readable in both light and dark mode (toggle system theme to check). Favicon shows in browser tab.

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: landing page skeleton with hero section, dual theme, drift animation"
```

---

### Task 4: Sticky Nav

**Files:**
- Modify: `imaginalvision.com/index.html`

Add the sticky nav that appears after scrolling past the hero. Uses CSS for styling, JS `IntersectionObserver` for show/hide.

- [ ] **Step 1: Add sticky nav HTML after the hero div**

```html
<nav class="sticky-nav" id="sticky-nav">
  <a href="#tools">Art Cards</a>
  <a href="#tools">Dreamspace</a>
  <a href="#about">About</a>
</nav>
```

- [ ] **Step 2: Add sticky nav CSS**

```css
.sticky-nav {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  display: flex;
  justify-content: center;
  gap: 2rem;
  padding: 0.75rem 2rem;
  background: var(--bg);
  border-bottom: 1px solid var(--border);
  z-index: 100;
  transform: translateY(-100%);
  transition: transform 0.3s ease;
}

.sticky-nav.visible {
  transform: translateY(0);
}

.sticky-nav a {
  font-family: 'Inter', sans-serif;
  font-weight: 400;
  font-size: 0.85rem;
  color: var(--text-muted);
  text-decoration: none;
  letter-spacing: 0.05em;
  transition: color 0.2s;
}

.sticky-nav a:hover {
  color: var(--text-primary);
}
```

- [ ] **Step 3: Add JS at bottom of body for sticky nav**

```html
<script>
// Sticky nav — appears after scrolling past hero
const nav = document.getElementById('sticky-nav');
const hero = document.querySelector('.hero');
const observer = new IntersectionObserver(([entry]) => {
  nav.classList.toggle('visible', !entry.isIntersecting);
}, { threshold: 0 });
observer.observe(hero);
</script>
```

- [ ] **Step 4: Verify sticky nav appears/disappears on scroll**

Refresh browser, scroll past hero — nav should slide in from top. Scroll back up — nav should hide.

- [ ] **Step 5: Commit**

```bash
git add index.html
git commit -m "feat: sticky nav with IntersectionObserver show/hide"
```

---

### Task 5: Tools Section

**Files:**
- Modify: `imaginalvision.com/index.html`

Two side-by-side cards for Art Cards and Dreamspace with themed hover glows.

- [ ] **Step 1: Add tools section HTML after the sticky nav**

```html
<section id="tools" class="tools">
  <h2>The Tools</h2>
  <div class="tool-cards">
    <a href="https://artcards.imaginalvision.com" class="tool-card tool-card--gold">
      <div class="tool-card__preview tool-card__preview--gold">
        <span class="tool-card__icon">✦</span>
      </div>
      <h3>Art Cards</h3>
      <p>Expressive art card deck for therapeutic exploration, dreamwork, and clinical training.</p>
      <span class="tool-card__credential">Used at CIIS for intake training</span>
      <span class="tool-card__cta">Explore →</span>
    </a>
    <a href="https://dreamspace.imaginalvision.com" class="tool-card tool-card--lavender">
      <div class="tool-card__preview tool-card__preview--lavender">
        <span class="tool-card__icon">◐</span>
      </div>
      <h3>Dreamspace</h3>
      <p>Digital collage tool for dreamwork and creative self-exploration.</p>
      <span class="tool-card__credential">Self-guided or therapist-facilitated</span>
      <span class="tool-card__cta">Create →</span>
    </a>
  </div>
</section>
```

- [ ] **Step 2: Add tools CSS**

```css
.tools { text-align: center; }

.tools h2 {
  font-family: 'Cormorant Garamond', serif;
  font-weight: 600;
  font-size: 2rem;
  color: var(--text-primary);
  margin-bottom: 2rem;
}

.tool-cards {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 2rem;
  max-width: 760px;
  margin: 0 auto;
  padding: 0 2rem;
}

@media (max-width: 768px) {
  .tool-cards { grid-template-columns: 1fr; }
}

.tool-card {
  background: var(--bg-warm);
  border: 1px solid var(--border);
  border-radius: 12px;
  padding: 0;
  text-decoration: none;
  color: var(--text-body);
  transition: box-shadow 0.3s ease, transform 0.3s ease;
  overflow: hidden;
  display: flex;
  flex-direction: column;
}

.tool-card:hover {
  transform: translateY(-2px);
}

.tool-card--gold:hover {
  box-shadow: 0 4px 24px rgba(201, 168, 76, 0.25);
}

.tool-card--lavender:hover {
  box-shadow: 0 4px 24px rgba(167, 139, 250, 0.25);
}

.tool-card__preview {
  height: 160px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 3rem;
}

.tool-card__preview--gold {
  background: linear-gradient(135deg, #1a1000, #2a1a00);
  color: #c9a84c;
}

.tool-card__preview--lavender {
  background: linear-gradient(135deg, #0f0a1a, #1a1025);
  color: #c4b5fd;
}

.tool-card h3 {
  font-family: 'Cormorant Garamond', serif;
  font-weight: 600;
  font-size: 1.4rem;
  color: var(--text-primary);
  padding: 1.25rem 1.5rem 0;
}

.tool-card p {
  padding: 0.5rem 1.5rem;
  font-size: 0.9rem;
  line-height: 1.6;
  flex: 1;
}

.tool-card__credential {
  display: block;
  padding: 0 1.5rem;
  font-size: 0.8rem;
  font-style: italic;
  color: var(--text-muted);
}

.tool-card__cta {
  display: block;
  padding: 1.25rem 1.5rem;
  font-weight: 500;
  font-size: 0.9rem;
  color: var(--text-primary);
  letter-spacing: 0.02em;
}
```

- [ ] **Step 3: Verify cards render side-by-side on desktop, stacked on mobile**

Refresh browser. Check hover glows (gold on Art Cards, lavender on Dreamspace). Resize to <768px and verify stacking.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: tools section with Art Cards and Dreamspace cards"
```

---

### Task 6: "What is the Imaginal?" Section

**Files:**
- Modify: `imaginalvision.com/index.html`

- [ ] **Step 1: Add imaginal section HTML after tools section**

```html
<section id="imaginal">
  <h2>What is the Imaginal?</h2>
  <p>The word <em>imaginal</em> was coined by the philosopher Henry Corbin to describe a genuine mode of perception — a way of knowing through images that is as real as sight or reason. Not <em>imaginary</em>, meaning unreal, but <em>imaginal</em>: the capacity to see with the soul's eye.</p>
  <div class="quote">
    <p>"An image is not what one sees but the way in which one sees."</p>
    <cite>— Edward Casey</cite>
  </div>
  <p>James Hillman brought this idea to the center of psychology, and Shaun McNiff built it into the foundation of expressive arts therapy — the practice of using drawing, collage, movement, and writing as pathways to self-understanding. The tools on this site carry that tradition forward into digital form.</p>
</section>
```

- [ ] **Step 2: Add quote block CSS**

```css
.quote {
  border-left: 3px solid var(--accent-earth);
  padding: 1rem 1.5rem;
  margin: 2rem 0;
  background: var(--bg-warm);
  border-radius: 0 8px 8px 0;
}

.quote p {
  font-family: 'Cormorant Garamond', serif;
  font-size: 1.2rem;
  font-style: italic;
  color: var(--text-secondary);
  margin-bottom: 0.5rem;
}

.quote cite {
  font-family: 'Inter', sans-serif;
  font-size: 0.8rem;
  font-style: normal;
  color: var(--text-muted);
  letter-spacing: 0.05em;
}

section h2 {
  font-family: 'Cormorant Garamond', serif;
  font-weight: 600;
  font-size: 2rem;
  color: var(--text-primary);
  margin-bottom: 1.5rem;
}

section p {
  margin-bottom: 1.2rem;
  color: var(--text-body);
}
```

- [ ] **Step 3: Verify section renders with quote styled correctly**

Refresh browser. Check light and dark mode.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: 'What is the Imaginal?' section with Casey quote"
```

---

### Task 7: "Who It's For" Section

**Files:**
- Modify: `imaginalvision.com/index.html`

- [ ] **Step 1: Add audience section HTML after imaginal section**

```html
<section id="audience">
  <h2>Who It's For</h2>
  <div class="audience-grid">
    <div class="audience-block">
      <h3>Clients</h3>
      <p>Use Art Cards and Dreamspace between sessions or during telehealth to deepen your expressive arts work.</p>
    </div>
    <div class="audience-block">
      <h3>Students & Educators</h3>
      <p>A training tool for expressive arts programs. Currently used at CIIS for intake training.</p>
    </div>
    <div class="audience-block">
      <h3>Therapists</h3>
      <p>Integrate these tools into your own practice, whether you work in-person or remotely.</p>
    </div>
    <div class="audience-block">
      <h3>Creative Explorers</h3>
      <p>No therapy background needed. Browse the card deck, create a collage, see what emerges.</p>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Add audience grid CSS**

```css
.audience-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1.5rem;
}

@media (max-width: 768px) {
  .audience-grid { grid-template-columns: 1fr; }
}

.audience-block {
  background: var(--bg-warm);
  padding: 1.5rem;
  border-radius: 10px;
  border: 1px solid var(--border);
}

.audience-block h3 {
  font-family: 'Cormorant Garamond', serif;
  font-weight: 600;
  font-size: 1.2rem;
  color: var(--text-primary);
  margin-bottom: 0.5rem;
}

.audience-block p {
  font-size: 0.9rem;
  margin-bottom: 0;
}
```

- [ ] **Step 3: Verify 2x2 grid on desktop, single column on mobile**

Refresh browser. Check both themes.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: 'Who It's For' section with four audience blocks"
```

---

### Task 8: About Cassandra + Creative Sight Counseling Sections

**Files:**
- Modify: `imaginalvision.com/index.html`

- [ ] **Step 1: Add About section HTML**

```html
<section id="about">
  <h2>About</h2>
  <div class="about-content">
    <div class="about-photo">
      <!-- Photo placeholder — will be replaced with actual photo -->
      <div class="photo-placeholder"></div>
    </div>
    <div class="about-text">
      <p><strong>Cassandra Clark, LMFT #116676</strong>, is a Licensed Marriage and Family Therapist specializing in expressive arts therapy. She holds a degree from the California Institute of Integral Studies (CIIS) in San Francisco and brings over nine years of clinical experience to her practice.</p>
      <p>Rooted in Jungian and transpersonal psychology, her work integrates drawing, painting, collage, writing, music, guided imagery, dreamwork, and sandtray therapy — all within a trauma-informed, mindfulness-based framework.</p>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Add Creative Sight Counseling section HTML**

```html
<section id="practice" class="practice-section">
  <h2>Creative Sight Counseling</h2>
  <p>Cassandra offers individual therapy in Nevada City, California, and online for all California residents. Sessions integrate expressive arts with evidence-based approaches including mindfulness-based cognitive behavioral therapy.</p>
  <div class="practice-details">
    <div class="practice-detail">
      <h4>Areas of Focus</h4>
      <p>Anxiety, grief, trauma & PTSD, women's issues, LGBTQ+ concerns, self-esteem, spirituality</p>
    </div>
    <div class="practice-detail">
      <h4>Investment</h4>
      <p>Private-pay sliding scale, $132–200 per session. Insurance accepted.</p>
    </div>
    <div class="practice-detail">
      <h4>Groups & Workshops</h4>
      <p>Expressive arts workshop offerings coming in 2026.</p>
    </div>
  </div>
  <a href="https://creativesightcounseling.com" class="practice-cta">Learn more at Creative Sight Counseling →</a>
</section>
```

- [ ] **Step 3: Add CSS for both sections**

```css
.about-content {
  display: flex;
  gap: 2rem;
  align-items: flex-start;
}

@media (max-width: 768px) {
  .about-content { flex-direction: column; align-items: center; text-align: center; }
}

.photo-placeholder {
  width: 160px;
  height: 160px;
  border-radius: 50%;
  background: var(--bg-warm);
  border: 2px solid var(--border);
  flex-shrink: 0;
}

.about-text strong {
  color: var(--text-primary);
}

.practice-section {
  background: var(--bg-warm);
  border-radius: 16px;
  padding: 3rem 2rem;
  max-width: 760px;
  margin: 0 auto 5rem;
}

.practice-details {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  gap: 1.5rem;
  margin: 1.5rem 0;
}

@media (max-width: 768px) {
  .practice-details { grid-template-columns: 1fr; }
}

.practice-detail h4 {
  font-family: 'Inter', sans-serif;
  font-weight: 500;
  font-size: 0.85rem;
  color: var(--text-primary);
  margin-bottom: 0.3rem;
  letter-spacing: 0.02em;
}

.practice-detail p {
  font-size: 0.85rem;
  margin-bottom: 0;
}

.practice-cta {
  display: inline-block;
  margin-top: 1rem;
  font-family: 'Inter', sans-serif;
  font-weight: 500;
  font-size: 0.9rem;
  color: var(--text-primary);
  text-decoration: none;
  padding: 0.6rem 1.5rem;
  border: 1px solid var(--border);
  border-radius: 8px;
  transition: background 0.2s, border-color 0.2s;
}

.practice-cta:hover {
  background: var(--bg);
  border-color: var(--accent-earth);
}
```

- [ ] **Step 4: Verify both sections render, check responsive layout**

Refresh browser. Verify photo placeholder circle, practice details 3-col on desktop / 1-col on mobile, CTA link works.

- [ ] **Step 5: Commit**

```bash
git add index.html
git commit -m "feat: About Cassandra and Creative Sight Counseling sections"
```

---

### Task 9: Footer

**Files:**
- Modify: `imaginalvision.com/index.html`

- [ ] **Step 1: Add footer HTML before closing `</body>`**

```html
<footer>
  <div class="footer-links">
    <a href="https://www.instagram.com/creative.sight.counseling/" target="_blank" rel="noopener">Instagram</a>
    <a href="https://creativesightcounseling.com" target="_blank" rel="noopener">Creative Sight Counseling</a>
    <a href="https://creativesightcounseling.theranext.com" target="_blank" rel="noopener">Client Portal</a>
    <span>LMFT #116676</span>
  </div>
  <p>&copy; 2026 Imaginal Vision. All rights reserved.</p>
</footer>
```

- [ ] **Step 2: Add footer CSS**

```css
footer {
  text-align: center;
  padding: 3rem 2rem;
  border-top: 1px solid var(--border);
}

.footer-links {
  display: flex;
  justify-content: center;
  gap: 2rem;
  flex-wrap: wrap;
  margin-bottom: 1rem;
}

.footer-links a {
  color: var(--text-muted);
  text-decoration: none;
  font-size: 0.85rem;
  transition: color 0.2s;
}

.footer-links a:hover {
  color: var(--text-primary);
}

.footer-links span {
  color: var(--text-muted);
  font-size: 0.85rem;
}

footer p {
  font-size: 0.75rem;
  color: var(--text-muted);
}
```

- [ ] **Step 3: Verify footer renders**

Refresh browser. Check links work (Instagram opens in new tab).

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: footer with links, license number, copyright"
```

---

### Task 10: Scroll Fade-In Animations

**Files:**
- Modify: `imaginalvision.com/index.html`

Add the IntersectionObserver-based fade-in for all sections, and the `prefers-reduced-motion` disable.

- [ ] **Step 1: Add `.fade-in` class to all sections**

Add `class="fade-in"` to each `<section>` element (tools, imaginal, audience, about, practice).

- [ ] **Step 2: Add fade-in CSS**

```css
.fade-in {
  opacity: 0;
  transform: translateY(20px);
  transition: opacity 0.6s ease, transform 0.6s ease;
}

.fade-in.visible {
  opacity: 1;
  transform: translateY(0);
}

@media (prefers-reduced-motion: reduce) {
  .hero::before { animation: none; }
  .scroll-hint { animation: none; opacity: 0.7; }
  .sticky-nav { transition: none; }
  .fade-in {
    opacity: 1;
    transform: none;
    transition: none;
  }
}
```

- [ ] **Step 3: Add IntersectionObserver JS for fade-ins**

Append to the existing `<script>` block:

```javascript
// Scroll fade-in for sections
document.querySelectorAll('.fade-in').forEach(el => {
  const sectionObserver = new IntersectionObserver(([entry]) => {
    if (entry.isIntersecting) {
      el.classList.add('visible');
      sectionObserver.unobserve(el);
    }
  }, { threshold: 0.1 });
  sectionObserver.observe(el);
});
```

- [ ] **Step 4: Verify animations**

Refresh browser. Scroll down — each section should fade in as it enters the viewport. Toggle system `prefers-reduced-motion` and verify all animations are disabled.

- [ ] **Step 5: Commit**

```bash
git add index.html
git commit -m "feat: scroll fade-in animations with reduced-motion support"
```

---

### Task 11: Final Polish and Visual QA

**Files:**
- Modify: `imaginalvision.com/index.html`

- [ ] **Step 1: Full visual QA pass**

Open in browser and check:
- [ ] Light mode: all sections readable, gradients correct, hover glows visible
- [ ] Dark mode: toggle system theme, verify all colors swap correctly
- [ ] Mobile: resize to <768px, verify all grids stack, text sizes are readable
- [ ] Sticky nav: scrolls in/out correctly, links jump to sections
- [ ] Scroll animations: each section fades in once, no repeat
- [ ] Reduced motion: all animations disabled
- [ ] Favicon: visible in browser tab
- [ ] Links: all external links work (Instagram, Creative Sight Counseling)
- [ ] Content: no typos, proper em dashes, correct license number

- [ ] **Step 2: Fix any issues found in QA**

Apply fixes as needed.

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "fix: visual QA polish pass"
```

---

### Task 12: Deploy to Cloudflare Pages

**Files:** None (infrastructure setup)

- [ ] **Step 1: Create GitHub repo**

```bash
cd /home/jp/Projects/imaginalvision.com
gh repo create jphein/imaginalvision.com --public --source=. --push
```

- [ ] **Step 2: Set up Cloudflare Pages**

Connect the GitHub repo to Cloudflare Pages via the Cloudflare dashboard:
- Project name: `imaginalvision`
- Production branch: `main`
- Build command: (none — static site)
- Build output directory: `/` (root)
- Custom domain: `imaginalvision.com`

This step requires the Cloudflare dashboard — open it for JP:
```bash
xdg-open "https://dash.cloudflare.com"
```

- [ ] **Step 3: Verify deployment**

After Cloudflare Pages deploys, verify:
```bash
curl -sI https://imaginalvision.com | head -5
```

- [ ] **Step 4: Commit any deployment config if needed**

If Cloudflare requires a `_headers` or `_redirects` file, add and commit them.
