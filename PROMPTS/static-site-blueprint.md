# A Minimal Single-Page Static Site Blueprint

This is a blueprint for building a single page website with best of web standards. 
The example here is for site/domain called "VibeOnRails"

**Seven files. No framework. No build step.** The entire site is `index.html`, `base.css`, `style.css`, `app.js`, `sitemap.xml`, `robots.txt`, and `llms.txt` — served as static files.

## Architecture

A single `index.html` file holds all content in semantic `<section>` elements, each with an `id` for anchor-link navigation. The nav bar references these anchors (`#thesis`, `#voices`, `#essays`, etc.), making it a smooth-scrolling single-page site with no routing, no JS framework, and no bundler. The header is sticky with a backdrop-blur glass effect.

## Typography — The Entire Design System

Typography is the design. Not decorative — structural. The right type choices eliminate the need for illustrations, heavy imagery, or complex layouts. Two reference points inform this approach: the editorial card layout of VibeOnRails, and the prose-first manifesto style of 37signals' ONCE page.

### The ONCE Principle: Let Big Serif Text Breathe

The ONCE page (once.com by 37signals) is a masterclass in typographic confidence. It uses a single serif font ("Family") at a large responsive size — `clamp(1.375rem, 2.225vw, 2rem)` — with a tight line-height of `1.3` and slightly negative letter-spacing (`-0.0015em`). The content container is narrow (`min(100%, 34.5em)`) so lines stay comfortably within 50–70 characters. Paragraphs are separated by `1.3em` of margin — roughly one full line-height — creating a rhythm where each paragraph feels like its own thought, with room to land before the next begins.

The result: text that reads like a letter, not a website. No cards, no grids, no badges — just words on a page with enough space to command attention.

Key techniques from ONCE worth adopting:

- **Responsive serif body text**: `font-size: clamp(1.375rem, 2.225vw, 2rem)` — big enough to feel confident, fluid enough to work everywhere
- **Tight line-height**: `1.3` instead of the typical `1.5–1.6` — pulls lines closer together so paragraphs read as cohesive blocks
- **Negative letter-spacing**: `-0.0015em` — subtle tightening that makes serif text feel more composed at large sizes
- **Narrow content width**: `min(100%, 34.5em)` — roughly 55–65 characters per line, the optimal reading measure
- **Generous paragraph spacing**: `margin-top: 1.3em` — one full line-height of air between paragraphs, so each thought breathes
- **Font feature settings**: `font-feature-settings: "liga", "dlig"` — enables standard and discretionary ligatures for polished typesetting
- **Antialiased rendering**: `-webkit-font-smoothing: antialiased` — cleaner glyph edges, especially on macOS

### The VibeOnRails Approach: Serif + Sans Pairing for Editorial Layouts

VibeOnRails uses two Google Fonts: **Fraunces** (a variable optical-size serif) for display headings and stat numbers, and **DM Sans** (a clean geometric sans-serif) for body text, card titles, and UI elements. The contrast between a warm, slightly quirky serif and a neutral sans creates editorial character without imagery.

A fluid type scale using `clamp()` handles responsive sizing — no breakpoint-based font changes needed:

```css
--text-xs:   clamp(0.75rem,  0.7rem  + 0.25vw, 0.875rem);
--text-sm:   clamp(0.875rem, 0.8rem  + 0.35vw, 1rem);
--text-base: clamp(1rem,     0.95rem + 0.25vw, 1.125rem);
--text-lg:   clamp(1.125rem, 1rem    + 0.75vw, 1.5rem);
--text-xl:   clamp(1.5rem,   1.2rem  + 1.25vw, 2.25rem);
--text-2xl:  clamp(2rem,     1.2rem  + 2.5vw,  3.5rem);
--text-3xl:  clamp(2.5rem,   1rem    + 4vw,    5rem);
```

### When to Use Which Approach

| Content Type | Typography Approach | Example |
|---|---|---|
| Long-form prose, manifestos, open letters | ONCE-style: single large serif, narrow measure, generous spacing | once.com, product announcements |
| Curated collections, resource lists, card grids | VibeOnRails-style: serif/sans pairing, wider container, structured cards | vibeonrails.com, reading lists, portfolios |
| Mixed (prose intro + structured content) | ONCE-style for the narrative sections, VibeOnRails-style for the grid sections | Landing pages with both story and catalog |

### Typographic Principles Both Share

1. **`clamp()` for everything** — font sizes, spacing, section padding. One declaration works from 320px to 2560px.
2. **`text-wrap: balance` on headings** — prevents orphaned words on the last line of a heading.
3. **`text-wrap: pretty` on paragraphs** — avoids single-word last lines in body text.
4. **`max-width` in `ch` or `em`** — constrain line length to readable measures (50–72 characters), not arbitrary pixel values.
5. **Antialiased rendering** — `-webkit-font-smoothing: antialiased` and `-moz-osx-font-smoothing: grayscale` for cleaner glyphs.
6. **`hanging-punctuation: first last`** — optically aligns quotes and punctuation outside the text block.

## Content Spacing — The Invisible Architecture

The ONCE page teaches that spacing between content blocks matters more than the content styling itself. When paragraphs have `1.3em` of vertical separation — equal to one full line of text — each paragraph becomes a self-contained thought. The reader's eye gets a natural pause before the next idea.

Apply this principle at every level:

```css
/* Paragraph-level: one line-height of breathing room */
p + p {
  margin-top: 1.3em;
}

/* Section-level: generous, fluid padding */
.section {
  padding-block: clamp(3rem, 8vw, 8rem);
}

/* Card-level: consistent interior padding */
.card {
  padding: var(--space-6); /* 1.5rem */
}

/* Grid-level: enough gap that cards don't crowd */
.articles-grid {
  gap: var(--space-6); /* 1.5rem */
}
```

The rule of thumb: when in doubt, add more space, not more styling.

## CSS Design Tokens, Not Hardcoded Values

Every color, spacing unit, font size, radius, and shadow is a CSS custom property defined in `:root`. Dark mode and light mode are toggled by swapping a single `data-theme` attribute — both palettes use the same variable names, so components never need theme-specific overrides.

The palette is warm (dark charcoal `#141414`, cream-white `#f5f0e8`) with a single Ruby Red accent (`#CC0000`). One accent color used sparingly is more effective than a multi-color palette.

```css
/* Dark mode (default) */
:root, [data-theme="dark"] {
  --color-bg:         #141414;
  --color-surface:    #1a1a1a;
  --color-text:       #ede8e0;
  --color-text-muted: #9a9590;
  --color-primary:    #e63939;
}

/* Light mode — same variable names, different values */
[data-theme="light"] {
  --color-bg:         #f5f0e8;
  --color-surface:    #faf7f2;
  --color-text:       #1a1714;
  --color-text-muted: #6b6560;
  --color-primary:    #cc0000;
}
```

Spacing follows a 4px-based scale (`--space-1` through `--space-32`), keeping vertical rhythm consistent without guesswork.

## The Card Pattern

Every piece of content is an `<a>` wrapping an `<article class="card">`. Cards have a type badge (Tweet, Essay, Tool, Framework), a title, author info, a pull-quote, and a subtle arrow icon. A `card--featured` variant adds a red border and tinted background using `color-mix()`. This single pattern scales from 3 to 30 items without new CSS.

```html
<a href="..." target="_blank" rel="noopener noreferrer" class="card-link fade-in">
  <article class="card">
    <div>
      <span class="type-badge">Essay</span>
      <span class="card-date">Feb 2026</span>
    </div>
    <h3 class="card-title">Article Title Here</h3>
    <div>
      <span class="author-name">Author Name</span>
      <span class="author-role"> · Publication</span>
    </div>
    <p class="article-quote">"A representative quote from the piece."</p>
  </article>
</a>
```

The featured variant is just one class addition:

```css
.card--featured {
  border-color: var(--color-primary);
  border-width: 2px;
  background: color-mix(in oklab, var(--color-surface) 94%, var(--color-primary) 6%);
}
```

## Grid Layout

Content grids use `auto-fill` with `minmax()`, so they're responsive without media queries:

```css
.articles-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(min(340px, 100%), 1fr));
  gap: var(--space-6);
}
```

This creates 3 columns on wide screens, 2 on medium, and 1 on mobile — automatically.

## JavaScript: ~170 Lines, Vanilla

No jQuery, no React, no dependencies. Just an IIFE with six features:

- **Dynamic year injection** — so "The framework from 2005 is the AI framework of [year]" stays current
- **Theme toggle** with icon swap (sun/moon SVGs)
- **Mobile hamburger menu** — simple display toggle with close-on-link-click
- **Animated counters** using `requestAnimationFrame` with cubic ease-out
- **Scroll-triggered fade-ins** — CSS-native `animation-timeline: view()` where supported, `IntersectionObserver` fallback elsewhere
- **Sticky header shadow** on scroll via classList toggle

## SEO Optimization

### In `<head>`

```html
<!-- Descriptive title with primary keyword -->
<title>VibeOnRails — Why Ruby on Rails Is the Best Framework for AI and LLM Development</title>

<!-- Meta description summarizing content and resource count -->
<meta name="description" content="A curated collection of 28+ articles, essays, talks...">

<!-- Keywords -->
<meta name="keywords" content="Ruby on Rails, AI, LLM, vibe coding...">

<!-- Canonical URL -->
<link rel="canonical" href="https://vibeonrails.com">

<!-- Sitemap reference -->
<link rel="sitemap" type="application/xml" href="./sitemap.xml">

<!-- Author attribution -->
<meta name="author" content="Abhishek Parolkar">
<link rel="author" href="https://github.com/parolkar">
```

### Open Graph (Facebook, LinkedIn)

```html
<meta property="og:title" content="VibeOnRails — Why Ruby on Rails Is the Best Framework for AI">
<meta property="og:description" content="28+ curated articles, essays, frameworks...">
<meta property="og:type" content="website">
<meta property="og:url" content="https://vibeonrails.com">
<meta property="og:site_name" content="VibeOnRails">
```

### Twitter Card

```html
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:title" content="...">
<meta name="twitter:description" content="...">
<meta name="twitter:creator" content="@parolkar">
```

### JSON-LD Structured Data

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "CollectionPage",
  "name": "VibeOnRails",
  "description": "...",
  "author": {
    "@type": "Person",
    "name": "Abhishek Parolkar",
    "url": "https://github.com/parolkar",
    "sameAs": [
      "https://x.com/parolkar",
      "https://github.com/parolkar",
      "https://www.linkedin.com/in/search4abhi"
    ]
  },
  "url": "https://vibeonrails.com",
  "inLanguage": "en"
}
</script>
```

### Semantic HTML

Use `<main>`, `<section>`, `<article>`, `<nav>`, `<header>`, `<footer>` with proper heading hierarchy (`h1` once in hero, `h2` per section, `h3` per card).

## Machine Readability — The Three Files

### `sitemap.xml`

Standard XML sitemap with `<lastmod>`, `<changefreq>`, and `<priority>`. Referenced in both `<head>` (via `<link rel="sitemap">`) and in `robots.txt`.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>https://vibeonrails.com/</loc>
    <lastmod>2026-03-08</lastmod>
    <changefreq>weekly</changefreq>
    <priority>1.0</priority>
  </url>
</urlset>
```

### `robots.txt`

Allow all crawlers, point to the sitemap:

```
User-agent: *
Allow: /

Sitemap: https://vibeonrails.com/sitemap.xml
```

### `llms.txt`

A structured plaintext summary of the entire site's content, organized by section, with key quotes and URLs. This helps LLM-based search engines (Perplexity, ChatGPT search, Google AI Overviews) understand and cite the page correctly. Think of it as a human-readable site manifest specifically for AI crawlers.

Structure it with Markdown-style headings:

```
# Site Name

> One-line description

## About
Summary paragraph with resource count and creator info.

## The Thesis
Core arguments, numbered.

## Key Voices Featured
Bullet list with names, roles, and representative quotes.

## Categories of Content
### Section Name (N pieces)
Description + bullet list of every item with author.

## Key Concepts
Definitions of domain-specific terms.

## Creator
Name + links (Twitter, GitHub, LinkedIn).

## URL
Production URL.
```

## Accessibility

- Skip-to-content link (`<a href="#main" class="skip-link">`)
- `aria-label` on interactive elements (theme toggle, logo link, stats)
- `aria-labelledby` on every section pointing to its heading
- `role="list"` on `<ul>` elements (Safari VoiceOver fix)
- `:focus-visible` outlines with `outline-offset: 3px`
- `prefers-reduced-motion` media query that disables all animations
- Sufficient color contrast in both themes

## Base Reset (`base.css`)

A minimal ~65-line reset that sets `box-sizing: border-box`, font smoothing, `text-wrap: balance` on headings, `text-wrap: pretty` on paragraphs, `100dvh` body height, smooth scroll with `scroll-padding-top` for the sticky header, `::selection` styling, and `prefers-reduced-motion` support. No library needed.

```css
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

html {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-rendering: optimizeLegibility;
  scroll-behavior: smooth;
  hanging-punctuation: first last;
  scroll-padding-top: var(--space-16);
}

body {
  min-height: 100dvh;
  line-height: 1.6;
  font-family: var(--font-body, sans-serif);
  font-size: var(--text-base);
  color: var(--color-text);
  background-color: var(--color-bg);
}

h1, h2, h3, h4, h5, h6 { text-wrap: balance; line-height: 1.15; }
p, li, figcaption { text-wrap: pretty; max-width: 72ch; }

::selection {
  background: oklch(from var(--color-primary) l c h / 0.25);
  color: var(--color-text);
}

@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
}
```

## File Structure

```
vibeonrails/
├── index.html      # All content, semantic sections, SEO tags
├── base.css        # Reset, accessibility, reduced-motion
├── style.css       # Design tokens, components, dark/light themes
├── app.js          # Theme toggle, counters, scroll animations
├── sitemap.xml     # XML sitemap for search engines
├── robots.txt      # Crawler permissions + sitemap reference
└── llms.txt        # Structured plaintext for LLM crawlers
```

## The Takeaway

The entire static site should weighs under 50 to 100 KB (excluding fonts). No npm, no build, no deploy pipeline — just files on a CDN.

The two typography approaches — ONCE-style prose (large serif, narrow measure, generous paragraph spacing) and VibeOnRails-style editorial (serif/sans pairing, card grids, structured metadata) — are complementary. Use the first when the writing is the product. Use the second when you're curating and organizing other people's work. Combine them when a page needs both narrative and catalog.

Either way, the formula is the same: start with a good typeface, define your tokens, constrain your line length, give your content room to breathe, and let semantic HTML and CSS do the rest. The less you add, the more the words come through.
