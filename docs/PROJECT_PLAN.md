# Uridle (우리들) — Project Plan & Workflow

> **Last Updated**: 2026-02-21
> **Status**: Phase 0-3 DONE → Phase 4 (Illustrations & Polish) next
> **Repository**: `G:\내 드라이브\uridle\`

---

## 1. Vision & Identity

### What is Uridle?
**Uridle (우리들)** = "All of us" in Korean. A language and culture exchange platform where people learn to understand each other — starting with Korean, expanding to global cultural exchange.

### Brand Core (from Self-Branding docs)
- **Persona**: "The Soft & Reliable Mentor" — a wise, gentle Korean hyung/oppa who reads books, enjoys silence, and genuinely cares about your growth
- **Mission**: "Protect the Brand Value of Korea" — show what real quality looks like
- **Core Values**: Reliability (신뢰), Context (맥락), Care (정성)
- **Educational Philosophy**: "I Teach Systems, Not Just Words" — build independence, not dependence
- **Ultimate Goal**: Not just tutoring, but a comprehensive platform: Education (Online/Offline) + Tourism (Local Guide/Program) + Community (Global Understanding)

### Why "Uridle"?
- 우리들 = "all of us" — inclusive, community-first
- Represents the ultimate vision: people understanding each other
- Gentle, warm sound that matches the brand persona
- Works internationally — easy to pronounce, memorable

---

## 2. Architecture: Two Separate Pages

### Why Two Pages?
Based on cultural design research (see Section 3), Western audiences prefer shorter, focused pages. But Jay's story requires deep emotional context. Solution: **separate the storytelling from the transaction**.

| | Page 1: The Story | Page 2: The System |
|---|---|---|
| **File** | `src/index.html` | `src/packages.html` |
| **Purpose** | Brand storytelling, emotional connection | Service details, pricing, booking |
| **Tone** | Warm, personal, hand-drawn | Professional, clear, systematic |
| **Scroll** | Horizontal storybook → Vertical sections | Vertical with continuous thread |
| **CTA** | "See What I've Built" → Page 2 | "Book a Trial Lesson" |
| **Length** | Medium (storybook feels short despite depth) | Short-medium (focused on conversion) |

### Relationship to Existing Sites
- **flykorean** (`g4jy.github.io/flykorean`): Stays as-is. Current landing page for Preply students.
- **uridle**: New brand website. Eventually replaces flykorean as the primary web presence.
- **Student review hubs** (`g4jy.github.io/korean-practice-*`): Separate, per-student apps.

---

## 3. Cultural Design Insight

### From @goojeon.insight (Instagram, 2026-02-20)
Korean vs Western product page design differs fundamentally:

| Aspect | Western (US) | East Asian (KR) |
|---|---|---|
| **Length** | Short, focused | Long, detailed |
| **Info Style** | Key message only | Context-rich, relationship-based |
| **Structure** | Template-based (Amazon) | Seller expression freedom (Naver) |
| **Cognitive Model** | Product as independent object | Product as contextual element |
| **Design** | Extension-suppressed | Expansion-allowed |

### Application to Uridle
- **Target audience is global/Western** → prefer shorter, result-focused design
- **Content is deeply contextual** (Korean culture) → needs depth
- **Solution**: The horizontal storybook format delivers deep context in bite-sized, engaging slides. It *feels* short even though it communicates deeply. After storybook, vertical sections are focused and conversion-oriented.
- **Key principle**: "Short pages win for conversion (13.5% better), but complex services need more persuasion" → our two-page split is the answer

### 2026 Landing Page Trends (from research)
- Scroll storytelling is a top 2026 web design trend
- Micro-interactions demonstrate functionality, not just decoration
- AI-powered personalization and mobile-first are essential
- Video increases conversions 86% (relevant for future YouTube integration)
- One page = one job (validates our two-page split)

---

## 4. Reference Website Analysis

### Reference A: Pencils of Promise — Storybook
**URL**: https://pencilsofpromise.org/book/?lang=en&book=slide-13
- **Tech**: Swiper.js horizontal scroll, warm beige (#f5ebd6), slide-type variants
- **What we use**: Horizontal scroll format for Jay's personal story
- **Adaptation**: Hand-drawn SVG illustrations instead of photos. More slides (24+). Deeper emotional arc.

### Reference B: Planetono — Smooth Scroll Animations
**URL**: https://www.planetono.space/
- **Tech**: Nuxt.js + Vue 3 + Rive animations, cubic-bezier(.25,1,.5,1), 700svh scroll containers
- **What we use**: Background color transitions, buttery smooth animations, GPU-only transforms
- **Adaptation**: CSS custom properties for color transitions. GSAP ScrollTrigger for scroll-driven animations. Applied to post-storybook vertical sections.

### Reference C: Optikka — Continuous Design Thread
**URL**: https://optikka.com/
- **Tech**: Astro + View Transition API, persistent elements across pages
- **What we use**: One continuous SVG path/line connecting all sections on Page 2
- **Adaptation**: SVG thread animated with stroke-dashoffset on scroll. Connects "How It Works" waypoints through packages to booking form.

---

## 5. Design System

### Color Palette: "Campfire"
| Name | Hex | Usage |
|---|---|---|
| Midnight Navy | `#1B2438` | Backgrounds, deep sections |
| Campfire Amber | `#E8983E` | Primary accent, CTAs, warmth |
| Terracotta | `#C4654A` | Secondary accent, emphasis |
| Forest Sage | `#6B9080` | Balance, nature, calm sections |
| Twilight Lavender | `#8B7EB8` | Special moments, vision sections |
| Rice Paper | `#F7F3ED` | Light backgrounds, text areas |
| Brush Ink | `#2A2A2A` | Text, dark elements |

### Background Color Transitions (Planetono-style)
Each major section has its own background color that transitions smoothly on scroll:
- **Storybook**: Rice Paper → Midnight Navy (as story deepens)
- **Pyramid**: Midnight Navy
- **Persona Comparison**: Rice Paper
- **Philosophy**: Forest Sage (faded)
- **System**: Campfire Amber (faded)
- **CTA**: Midnight Navy

### Typography
- **Headings**: Playfair Display (serif, elegant, warm)
- **Body**: Inter (clean, readable, modern)
- **Storybook captions**: Caveat or Patrick Hand (handwritten feel)

### Illustration Style
- **Hand-drawn SVG** — warm, attractive, adorable like a Korean 동화책 (children's storybook)
- **Techniques**: feTurbulence filter for paper texture, stroke-dasharray animation for drawing effect, warm color fills from palette
- **Character style**: Simple, expressive, rounded shapes. Jay as a recognizable character throughout.
- **Tools for generation**: AI SVG generators (Recraft, SVGStorm, Kittl) → manual cleanup → SVG optimization

### Animation Principles
- **Easing**: `cubic-bezier(.25,1,.5,1)` (Planetono-style — fast start, gentle landing)
- **GPU-only**: `transform` and `opacity` only — never animate layout properties
- **Scroll-driven**: IntersectionObserver + GSAP ScrollTrigger for reveal animations
- **Stagger**: Elements appear in sequence (50-100ms gaps) for natural feel
- **Duration**: 600-800ms for transitions, 300-400ms for micro-interactions

---

## 6. Page 1: The Story (`src/index.html`)

### Section A: Horizontal Storybook

**Tech**: Swiper.js with `direction: 'horizontal'`, `mousewheel: true`, full-viewport slides.

#### Act 1: The Care That Broke You (Slides 1-5)

**Slide 1 — Opening**
- Visual: Warm classroom scene, small figure (Jay) surrounded by many students
- Text: "This is a story about a teacher..."
- Mood: Warm, inviting

**Slide 2 — The Coach**
- Visual: Jay at desk, planning boards, messy notes, coffee cups
- Text: "In Korea, I ran a learning center. Ranked 170th out of 450,000 tutors — top 0.03%."
- Detail: Not bragging. Setting up what comes next.

**Slide 3 — The Extra Mile**
- Visual: Jay on phone late at night, worried parent on other end, clock showing 11pm
- Text: "I didn't just teach grammar. I talked to parents about their children's health, their worries, their fears. I convinced anxious mothers that rankings weren't everything."
- Emotion: This is the CARE (정성) that defines Jay

**Slide 4 — The Weight**
- Visual: Jay carrying weight on shoulders, student problems floating as thought bubbles
- Text: "I cared about every student's mentality, concerns, worries. More than just a tutor should."
- Emotion: Building toward burnout

**Slide 5 — The Break**
- Visual: Broken desk, scattered papers, Jay sitting alone. March 2025.
- Text: "In March 2025, I stepped away. Completely burnt out. Not from working too hard — from caring too much."
- Transition: Background darkens to Midnight Navy

#### Act 2: The World (Slides 6-9)

**Slide 6 — The First Step**
- Visual: Airport departure gate, single backpack, dawn light
- Text: "For the first time in my life, I just started traveling."
- Mood: Quiet hope, new beginning

**Slide 7 — The Conversations**
- Visual: Cafe scene, multiple people from different countries, speech bubbles with questions
- Text: "'Why do Koreans always ask about age?' 'Why does the verb come at the end?' 'Why do you write addresses backwards?'"
- Detail: Real questions from his profile

**Slide 8 — The Curiosity**
- Visual: World map with warm dots showing interest, people reaching toward Korea
- Text: "People weren't just curious about K-Pop or K-Drama. They wanted to understand HOW Koreans think."
- Emotion: Surprise, warmth, connection

**Slide 9 — The Spark**
- Visual: Jay's face lighting up, lightbulb moment, hands gesturing excitedly
- Text: "'This is what I'm meant to do.'"
- Transition: Moment of clarity

#### Act 3: The Ugly Truth (Slides 10-13)

**Slide 10 — The Videos**
- Visual: Phone screens showing cheap/clickbait content about Korea, red flags
- Text: "But then people showed me videos. Cheap, low-quality clips spreading wrong information about Korean culture."
- Emotion: Rising frustration

**Slide 11 — The Ignorance**
- Visual: People arguing in black and white, no gray area, crossed arms
- Text: "Made by people who never tried to understand. They judged from their narrow view and spoke out loud to the world."
- Emotion: Anger, but controlled

**Slide 12 — The Bigger Problem**
- Visual: Split world — people on opposite sides not listening to each other
- Text: "I saw it everywhere. Not just about Korea. People worldwide — just black and white. Not trying to understand each other."
- Emotion: This is the CORE motivation

**Slide 13 — The Mission**
- Visual: Jay standing up, determined look, warm glow behind him
- Text: "I decided: I will protect the real Korea. And help people understand each other better."
- Transition: Background shifts to warm amber

#### Act 4: The Frustration (Slides 14-16)

**Slide 14 — The Market**
- Visual: Laptop screen showing tutoring profiles, some in pajamas, low-effort vibes
- Text: "When I looked at the online tutoring market, I was frustrated. Some tutors treated this as an easy side gig."
- Detail: From his profile text — pajamas, weekly replies, unstructured chatting

**Slide 15 — The Damage**
- Visual: Sad student at desk, shame cloud over their head, broken confidence
- Text: "I met students who had been made to feel ashamed by their previous tutors."
- Emotion: This made it personal

**Slide 16 — The Promise**
- Visual: Jay rolling up sleeves, blueprint/plan in hand
- Text: "You deserve more than just a chat partner. You deserve someone who takes your goals as seriously as you do."
- Transition: Determination → Building

#### Act 5: The Build (Slides 17-20)

**Slide 17 — The System**
- Visual: Blueprint expanding into a beautiful structure, organized layers
- Text: "I didn't just start teaching. I built a SYSTEM."
- Detail: The best teacher makes themselves unnecessary

**Slide 18 — The Gap**
- Visual: Two dots with a clear path between them — "Where you are" to "Where you want to be"
- Text: "Step 1: Find the gap. Not a grammar test — a real conversation about your goals."

**Slide 19 — The Daily Routine**
- Visual: Calendar with daily micro-tasks, gentle nudges, voice recordings
- Text: "Step 2: Class time is for verification. Real growth happens between classes."
- Detail: Assignments, nudges, feedback within 12-24 hours

**Slide 20 — The Safe Space**
- Visual: Warm circle of light, mistakes floating in as "treasures" to collect
- Text: "Step 3: Mistakes are treasure. The more we find in class, the fewer you make in real life."
- Emotion: Safety, encouragement

#### Act 6: The Vision (Slides 21-24+)

**Slide 21 — Beyond 1:1**
- Visual: Single connection expanding into a web of connections between students
- Text: "But I dreamed of something bigger than 1:1 lessons."

**Slide 22 — The Group**
- Visual: Students in a circle, teaching each other, laughing, sharing
- Text: "Students helping students. Not just learning Korean — learning to explain, to listen, to understand each other."
- Detail: This was always the vision — from the 학원 days

**Slide 23 — The Community**
- Visual: Same-city clusters on a map, people meeting offline, travel buddies
- Text: "Same timezone. Same city. Study partners become travel buddies. Online connections become real friendships."

**Slide 24 — Uridle**
- Visual: Global map with warm threads connecting all dots, the word "우리들" glowing in the center
- Text: "우리들. All of us. Not just Korean. Every culture. Every language. Understanding each other better."
- CTA: "See What I've Built →"
- Transition: Smooth scroll to vertical sections

### Section B: The Pyramid ("You're in the Top 1%")

After storybook ends, vertical scroll begins with Planetono-style background transitions.

- **Hook**: "Millions of people say they want to learn Korean..."
- **Pyramid visualization** (animated, staggered reveal):
  - Base (millions): "Watching K-Drama with subtitles"
  - Level 2 (100K): "Downloaded Duolingo"
  - Level 3 (10K): "Bought a textbook"
  - Level 4 (1K): "Took a class"
  - Level 5 (100): "Studying regularly"
  - **Peak (1%)**: "Seeking a personal tutor" ← "You're here."
- **Emotional closure**: "You already made the hardest choice."

### Section C: Persona Comparison (Option D — 본질 Twist)

Instead of user-set priorities, present **6 persona cards** that visitors identify with. Each reveals what they THINK they need vs what they ACTUALLY need.

#### The 6 Personas

**1. The K-Drama Discoverer** (Free Content User)
- "You binge K-dramas and pick up phrases naturally"
- What you think: "I just need more content and I'll get fluent"
- 본질 twist: "You've built incredible listening intuition. What you actually need is someone to organize that raw material into a system you can speak with."
- Methods used: YouTube, TikTok, drama clips
- Comparison: Free/entertaining/huge variety BUT no feedback/no structure/passive only

**2. The App Streak Keeper** (App User — Duolingo etc.)
- "Your 200-day streak is your pride and joy"
- What you think: "If I just keep going, I'll become fluent"
- 본질 twist: "You've proven you can show up every day — that's the hardest part. What you actually need is to use that discipline on content that matches YOUR specific goals, not a generic algorithm."
- Methods used: Duolingo, Memrise, LingoDeer
- Comparison: Gamified/cheap/convenient BUT recognition-only/no speaking/generic

**3. The Conversation Seeker** (Language Exchange)
- "You've found Korean friends on HelloTalk and Tandem"
- What you think: "I just need more conversation practice"
- 본질 twist: "You've built real cultural connections. What you actually need isn't more conversation — it's someone who can tell you exactly WHY your sentences feel 'off' to native ears."
- Methods used: HelloTalk, Tandem, language cafes
- Comparison: Free/native speakers/cultural BUT no structure/uneven quality/time-consuming

**4. The Self-Study Warrior** (Online Platforms)
- "Your bookshelf has TTMIK, Korean Grammar in Use, and three notebooks"
- What you think: "I need a more advanced textbook"
- 본질 twist: "You have incredible self-discipline. What you actually need isn't more material — it's someone to show you which 20% of what you're studying will give you 80% of results."
- Methods used: TTMIK, Coursera, structured online courses
- Comparison: Structured/affordable/self-paced BUT no personalization/no live feedback/lonely

**5. The Classroom Learner** (Offline Academy)
- "You attend Korean classes at a local academy or university"
- What you think: "I need a better academy with better teachers"
- 본질 twist: "Like I told parents who asked about 학원s: 'If you want the best teaching, go to Megastudy. But if you want to enjoy studying WITH friends...' What you actually need isn't a better classroom — it's whether your goal is the certificate or the experience."
- Methods used: University courses, language schools, 학원
- Comparison: Social/structured/accountability BUT expensive/fixed schedule/one-size-fits-all

**6. The Serious Builder** (1:1 Tutoring — This Is You)
- "You've tried everything else and you're ready to invest in yourself"
- What you think: "I need a native speaker to practice with"
- 본질 twist: "You don't need a conversation partner. You need a system builder — someone who designs your roadmap, fixes your thinking patterns, and eventually makes themselves unnecessary."
- Methods used: Preply, iTalki, private tutors
- Comparison: Fully personalized/real-time feedback/accountability BUT higher investment/depends on tutor quality

#### Visualization
- **Card grid** (2x3 on desktop, 1-column on mobile)
- Each card: illustration of persona + title + "Is this you?" button
- Click/tap → card flips/expands to show the 본질 twist
- After exploring → subtle prompt: "Whatever path brought you here, you're in the right place."

#### 8 Comparison Dimensions (shown in expanded detail for each persona)
1. **Affordability** — Cost relative to value
2. **Personalization** — Generic vs custom to your goals
3. **Accountability** — Does someone check on you?
4. **Structure** — Random vs systematic progression
5. **Skill Coverage** — Reading only vs speaking/listening/reading/writing
6. **Feedback Speed** — Days/never vs real-time correction
7. **Cultural Depth** — Surface phrases vs deep understanding
8. **Consistency (일관성)** — Service quality variance

### Section D: Philosophy — Concentric Circles

Three interconnected pillars of Jay's teaching philosophy, visualized as concentric circles:

- **Outermost ring (Gold/Amber)**: CULTURE — "Language without culture is just noise"
  - Why Koreans ask about age (hierarchy = respect system)
  - Why addresses go large→small (collective before individual)
  - Nunchi (눈치) — reading the room before speaking

- **Middle ring (Teal/Sage)**: STRUCTURE — "Random studying = random results"
  - Korean word order: SOV (Subject-Object-Verb)
  - Sentence building blocks → systematic patterns
  - 35-day plans, monthly roadmaps, daily micro-tasks

- **Inner core (Coral/Terracotta)**: SOUNDS — "What you ultimately produce"
  - Pronunciation that natives actually understand
  - Intonation patterns that carry meaning
  - Self-correction techniques for independence

**Interaction**: Click/hover a ring → expands detail panel below. Culture opens by default on scroll.

### Section E: System Overview — Scroll Reveal

**5 phases auto-reveal on scroll** (IntersectionObserver):

1. **Trial Lesson**: "Tell me your story, not just your grammar level"
2. **The Roadmap**: "Where you are → Where you want to be → The path between"
3. **Between Classes**: "Assignments, voice recordings, gentle nudges, detailed feedback"
4. **In Class**: "Growth Verification Session — not a lecture"
5. **Independence**: "The goal is for you to not need me"

Sticky progress dots show current phase.

### Section F: Social Proof + CTA

- Student quotes (when available)
- Stats: "X students across Y countries"
- CTA: "Ready to start? →" links to Page 2

---

## 7. Page 2: The System (`src/packages.html`)

### Design: Continuous Thread (Optikka-style)
One SVG path connects all sections from top to bottom. Animated with stroke-dashoffset as user scrolls.

### Section A: Hero
- "Here's what I've built for you."
- Subtitle: "A complete system, not just a lesson."

### Section B: How It Works (5 Waypoints on the Thread)
1. **Book a Trial** → Brief conversation about goals
2. **Get Your Roadmap** → Custom plan based on the gap
3. **Choose Your Track** → Intensive / Steady / Light
4. **Build Your Routine** → Daily micro-tasks + weekly verification
5. **Fly Solo** → Independence milestone celebrations

### Section C: Package Cards
Adapted from flykorean pricing but simplified:

| Package | Lessons/Week | Includes | Target |
|---|---|---|---|
| **Starter** | 1x/week | Core lesson + light homework | Hobbyists |
| **Builder** | 2x/week | Lessons + daily assignments + voice feedback | Steady learners |
| **Accelerator** | 3x/week | Everything + priority feedback + exam prep | Deadline-driven |
| **Custom** | Flexible | Addon builder | Special needs |

### Section D: Addon Builder
Interactive selector (from flykorean but cleaner):
- Pronunciation Clinic
- Writing Workshop
- TOPIK Prep Module
- Cultural Deep Dive
- Personal Web App (sentence builder)
- Emergency Line (24/7 support)

Each addon: click → slide-in detail panel (title, description, student quote, before/after, pricing)

### Section E: Availability Heatmap
Timezone-aware scheduling grid (from flykorean):
- KST → auto-converts to visitor's timezone
- Color-coded availability (popular/moderate/available/off)
- Tuesday: "Reserved for in-person sessions"
- Lunch break separator
- Sunday: Group session blocks (aspirational)

### Section F: FAQ
Expandable accordion. Questions like:
- "What if I miss a class?"
- "How fast will I improve?"
- "Can I switch tracks?"
- "What makes you different from other tutors?"

### Section G: Booking Form + Preference Collector
- Name, email, timezone, current level, goal
- After submit → success animation → Step 2: select preferred time slots
- Webhook: data → Google Sheet

---

## 8. Technical Architecture

### Stack
- **Pure HTML/CSS/JS** — single-file per page (like flykorean)
- **Swiper.js** — CDN, horizontal storybook
- **GSAP + ScrollTrigger** — CDN, scroll animations
- **No build tools** — direct deployment to GitHub Pages

### Libraries (CDN)
```
Swiper.js    — https://cdn.jsdelivr.net/npm/swiper@11/
GSAP         — https://cdn.jsdelivr.net/npm/gsap@3/
ScrollTrigger — included with GSAP
```

### Hosting
- GitHub Pages: `g4jy.github.io/uridle/`
- Custom domain: TBD (uridle.com / uridle.kr)

### Performance
- GPU-only animations (transform + opacity)
- Lazy-load SVG illustrations per slide
- IntersectionObserver for scroll-reveal (native, no library)
- Preload critical fonts
- SVGs inline for animation control, optimize with SVGO

---

## 9. Marketplace Tools & Plugins

### Tier 1: Install Immediately

| Tool | Type | Why | Install |
|------|------|-----|---------|
| **Frontend Design Plugin** | Plugin (96K installs) | Prevents AI slop. Enforces bold aesthetic direction, scroll-triggered animations, motion orchestration | `/plugin` > `anthropics/claude-code` > `frontend-design` |
| **GSAP Master MCP** | MCP Server | 6 tools: animate, timeline, ScrollTrigger, SVG morph, debug, optimize. Natural language → 60fps GSAP code | `claude mcp add-json gsap-master '{"command":"npx","args":["bruzethegreat-gsap-master-mcp-server@latest"]}'` |

### Tier 2: Workflow Enhancement

| Tool | Type | Why | Install |
|------|------|-----|---------|
| **SVGMaker MCP** | MCP Server | AI text-to-SVG, SVG editing, raster-to-vector. For storybook illustrations | Needs API key from svgmaker.io |
| **Figma MCP** | MCP Server | Design-to-code bridge. Read Figma designs → generate code | Figma Desktop > Preferences > Dev Mode MCP |

### Already Available (SuperClaude setup)
- **Playwright MCP**: Browser testing, device emulation (143 profiles), screenshot
- **Magic UI (21st.dev) MCP**: React component generation from natural language
- **Context7 MCP**: Up-to-date library docs (GSAP, Swiper.js, etc.)
- **Morphllm MCP**: Bulk code transformations
- **Sequential MCP**: Complex analysis and debugging

### External SVG Tools (generate externally, import output)

| Tool | Styles | Best For |
|------|--------|----------|
| [VectorWitch](https://vectorwitch.com/) | Drawing, Doodle, Ink, Cartoon | 8 hand-drawn presets, SVG export |
| [Recraft](https://recraft.ai/) | Multiple illustration styles | First AI built for native SVG |
| [Ilus.ai](https://ilus.ai/) | Flat, Ink Drawing, Doodle, Custom | Consistent style across illustrations |
| [Kittl](https://kittl.com/tools/vector-generator) | Various artistic styles | Edit vectors in-app after generation |

**Note**: Claude can also generate SVG code directly — for simple hand-drawn-style illustrations (wobbly lines, sketchy fills, organic shapes), inline SVG generation without external tools is often sufficient.

### Skills to Create
- `/uridle-preview`: Launch local server + Playwright screenshot workflow
- `/uridle-deploy`: Build check + git commit + push to GitHub Pages
- `/uridle-illustration`: Generate SVG illustration prompt → save to assets/

---

## 10. Implementation Tasks

### Phase 0: Setup [DONE]
- [x] Create project directory (`G:\내 드라이브\uridle\`)
- [x] Write PROJECT_PLAN.md (this document)
- [x] Write CLAUDE.md (project instructions)
- [x] Initialize git repository
- [x] Install GSAP Master MCP server
- [x] Research marketplace tools (comprehensive report)
- [x] Analyze Instagram cultural design insight
- [x] Set up local preview workflow (Python HTTP server, Playwright verification)
- [ ] Install Frontend Design plugin (needs `/plugin` interactive command)

### Phase 1: Page 1 — Storybook [DONE]
- [x] Create `src/index.html` base structure + CSS design system
- [x] Implement Swiper.js horizontal storybook container
- [x] Write storybook slides Act 1 (Slides 1-5: The Care That Broke You)
- [x] Write storybook slides Act 2 (Slides 6-9: The World)
- [x] Write storybook slides Act 3 (Slides 10-13: The Ugly Truth)
- [x] Write storybook slides Act 4 (Slides 14-16: The Frustration)
- [x] Write storybook slides Act 5 (Slides 17-20: The Build)
- [x] Write storybook slides Act 6 (Slides 21-24: The Vision)
- [x] Emoji placeholders for illustrations (SVG generation in Phase 4)
- [ ] Add slide transition animations (background color shifts, parallax via GSAP)
- [x] Test storybook navigation (Playwright verified: all 24 slides render)

### Phase 2: Page 1 — Vertical Sections [DONE]
- [x] Build Pyramid section with staggered reveal animation (IntersectionObserver)
- [x] Build 6 Persona Comparison cards with expand interaction + 본질 twist
- [x] Build Philosophy concentric circles (CSS + click interaction)
- [x] Build System overview with scroll-reveal phases (5 phases)
- [x] Build CTA section
- [x] Cross-link to Page 2
- [ ] Implement Planetono-style background color transitions (GSAP ScrollTrigger — Phase 4)
- [ ] Sticky progress dots for system section (Phase 4)

### Phase 3: Page 2 — The System [DONE]
- [x] Create `src/packages.html` base structure
- [x] Build Hero + How It Works (5 waypoints with colored number circles)
- [x] Build Package cards (3 tiers: Starter/Builder/Accelerator)
- [x] Build Addon builder with slide-in detail panels (6 addons, backdrop blur)
- [x] Build Availability heatmap (7 timezones, color-coded cells, Tuesday blocked)
- [x] Build FAQ accordion (6 questions)
- [x] Build Booking form with success state
- [x] Cross-link back to Page 1
- [x] Playwright verification: all sections render, timezone switching works, addon panels open/close
- [ ] Implement continuous thread SVG (animated stroke-dashoffset — Phase 4)
- [ ] Webhook integration for form submission (Phase 5)

### Phase 4: Illustrations & Polish
- [ ] Generate AI SVG illustrations for all 24+ storybook slides
- [ ] Refine illustration style consistency
- [ ] Add hand-drawn filter effects (feTurbulence, paper texture)
- [ ] Add stroke-dasharray drawing animations for key illustrations
- [ ] Final animation timing polish
- [ ] Performance optimization (lazy load, SVGO, font preload)

### Phase 5: Testing & Deploy
- [ ] Mobile responsive testing (Playwright device emulation)
- [ ] Cross-browser testing (Chrome, Safari, Firefox)
- [ ] Accessibility audit (keyboard navigation, screen readers, contrast)
- [ ] Create GitHub repository
- [ ] Deploy to GitHub Pages
- [ ] Test live deployment
- [ ] Set up custom domain (if ready)

### Phase 6: Future Enhancements
- [ ] Add real student testimonials
- [ ] Add video embed (YouTube intro)
- [ ] Payment integration (Stripe/Toss)
- [ ] Group lesson waitlist
- [ ] Multi-language support (EN/KR/JP)
- [ ] Analytics (Plausible/Umami — privacy-first)

---

## 11. Key Design Decisions Log

| Decision | Chosen | Why | Date |
|---|---|---|---|
| Brand name | Uridle (우리들) | "All of us" — inclusive, matches ultimate vision | 2026-02-20 |
| Two pages | Story + Packages | Separate emotional storytelling from conversion | 2026-02-20 |
| Illustration style | Hand-drawn SVG | Warm, adorable, 동화책 feel — matches "Soft Mentor" persona | 2026-02-20 |
| Storybook format | Horizontal scroll (Swiper.js) | Deep context in bite-sized slides — solves long-page problem | 2026-02-20 |
| Comparison approach | Option D (Persona cards with 본질 twist) | More engaging than user-set priorities, reveals actual needs | 2026-02-20 |
| Color palette | Campfire (7 colors) | Warm, inviting, professional, works in dark/light | 2026-02-20 |
| Animation | GSAP + ScrollTrigger | Industry standard, CDN available, GPU-optimized | 2026-02-20 |
| Hosting | GitHub Pages | Free, fast, familiar, easy deploy | 2026-02-20 |
| Project location | `G:\내 드라이브\uridle\` (separate from Preply) | Own CLAUDE.md, skills, agents — cleaner separation | 2026-02-21 |
| Page length strategy | Short/focused per section, depth via storybook format | Western audience prefers shorter, but complex service needs persuasion | 2026-02-21 |

---

## 12. File Structure

```
G:\내 드라이브\uridle\
├── CLAUDE.md              # Project-specific AI instructions
├── docs/
│   └── PROJECT_PLAN.md    # This document (concept + workflow + tasks)
├── src/
│   ├── index.html         # Page 1: The Story
│   └── packages.html      # Page 2: The System
├── assets/
│   ├── illustrations/     # SVG illustrations for storybook
│   ├── fonts/             # Self-hosted fonts (if needed)
│   └── icons/             # UI icons
└── scripts/               # Build/deploy scripts (if needed)
```
