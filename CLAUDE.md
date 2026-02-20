# Uridle (우리들) — AI Project Instructions

## Project Overview
A two-page brand website for Uridle — a language and culture exchange platform starting with Korean tutoring, evolving into a global understanding community.

- **Page 1** (`src/index.html`): The Story — horizontal storybook + vertical scroll sections
- **Page 2** (`src/packages.html`): The System — packages, pricing, booking

## Architecture
Pure HTML/CSS/JS. No build tools. Single-file per page. CDN libraries only.

### Libraries (CDN)
- **Swiper.js 11**: Horizontal storybook slides
- **GSAP 3 + ScrollTrigger**: Scroll-driven animations, parallax, background transitions

### Deployment
- GitHub Pages: `g4jy.github.io/uridle/`
- Push `src/` contents to `gh-pages` branch

## Design System

### Colors (Campfire Palette)
```css
:root {
  --midnight:   #1B2438;  /* Deep backgrounds */
  --amber:      #E8983E;  /* Primary accent, CTAs */
  --terracotta: #C4654A;  /* Secondary accent */
  --sage:       #6B9080;  /* Balance, calm */
  --lavender:   #8B7EB8;  /* Special moments */
  --rice:       #F7F3ED;  /* Light backgrounds */
  --ink:        #2A2A2A;  /* Text */
}
```

### Typography
- Headings: `Playfair Display` (serif)
- Body: `Inter` (sans-serif)
- Storybook captions: `Caveat` or `Patrick Hand` (handwritten)

### Animation Rules
- Easing: `cubic-bezier(.25,1,.5,1)` (fast start, gentle landing)
- GPU-only: `transform` and `opacity` only — NEVER animate width/height/margin/padding
- Duration: 600-800ms transitions, 300-400ms micro-interactions
- Stagger: 50-100ms between sequential reveals

### Illustration Style
- Hand-drawn SVG with warm fills from palette
- feTurbulence filter for paper texture
- stroke-dasharray animation for drawing-in effect
- Simple, expressive, rounded character shapes

## Key Files

| File | Purpose |
|------|---------|
| `docs/PROJECT_PLAN.md` | Full concept, narrative, tasks, decisions |
| `src/index.html` | Page 1: The Story |
| `src/packages.html` | Page 2: The System |
| `assets/illustrations/` | SVG storybook illustrations |

## Brand Context

### Who is Jay?
- "The Soft & Reliable Mentor" — wise, gentle Korean hyung/oppa
- Former learning center owner, top 0.03% tutor in Korea
- Burnt out from caring too much about students and parents
- Discovered his calling while traveling the world
- Mission: Protect real Korean culture, help people understand each other

### Core Values
- **Reliability (신뢰)**: Systems, preparation, consistency
- **Context (맥락)**: The "why" behind everything
- **Care (정성)**: Going the extra mile because you genuinely want them to succeed

### Ultimate Vision
1:1 tutoring → Group learning → Community → Global cultural exchange platform

## Rules

1. **Check PROJECT_PLAN.md first** — All narrative content, slide descriptions, and design specs are there
2. **Single-file pages** — Each HTML page is self-contained (inline CSS + JS). No separate CSS/JS files.
3. **CDN only** — No npm, no build tools. Swiper and GSAP from CDN.
4. **GPU animations** — Never animate layout properties. Transform + opacity only.
5. **Mobile-first** — Design for mobile viewport first, enhance for desktop
6. **Accessibility** — Keyboard navigation for storybook, ARIA labels, sufficient contrast
7. **Performance** — Lazy-load illustrations, preload fonts, inline critical CSS
8. **Illustration placeholders** — Use CSS gradient placeholders until SVGs are ready
9. **Test with Playwright** — Preview pages in browser automation before committing

## Related Projects
- **flykorean** (`G:\내 드라이브\Preply\flykorean\`): Current Preply landing page. Separate project. Do not modify.
- **Preply workspace** (`G:\내 드라이브\Preply\`): Student management, lessons. Separate project.
- **Self-Branding** (`G:\내 드라이브\Self-Branding\`): Brand strategy documents. Read-only reference.
