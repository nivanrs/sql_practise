# {{SERIES_TITLE}} — Brand Guidelines

> Based on the carousel slide design used across LinkedIn posts.
> Design philosophy: [`design-philosophy.md`](design-philosophy.md)

<!-- Replace all {{PLACEHOLDER}} values with your actual design values. -->

---

## 1. Color Palette

| Role | Name | Hex | Usage |
|---|---|---|---|
| Background | {{COLOR_GROUND_NAME}} | `{{COLOR_GROUND_HEX}}` | All slide backgrounds |
| Primary Text | Near Black | `{{COLOR_PRIMARY_HEX}}` | Body copy, sub-labels |
| Accent / Highlight | {{COLOR_ACCENT_NAME}} | `{{COLOR_ACCENT_HEX}}` | Section headings, script CTA |
| Surface Dark | Code Panel | `#1E1E1E` | Code block background |
| Code Text | Soft White | `#E8E8E8` | Code body text |
| Decorative | Black Dots | `#000000` | Three-dot ornament (title slide) |

**Color Rules:**
- Never use the {{COLOR_ACCENT_NAME}} for body text — it is a headline-only accent
- The {{COLOR_GROUND_NAME}} background is the only background color; do not use pure white (`#FFFFFF`)
- The dark code panel may be used as a visual break when showing code snippets

---

## 2. Typography

### Type Hierarchy

| Level | Role | Style | Case | Color |
|---|---|---|---|---|
| T1 — Hero | Main title ("{{SERIES_TITLE}}") | Ultra-bold, condensed sans-serif | UPPERCASE | Black |
| T2 — Section Header | Slide topic titles | Bold, condensed sans-serif | UPPERCASE | {{COLOR_ACCENT_NAME}} |
| T3 — Body | Problem statement, bullet points | Regular weight sans-serif | Sentence case | Black |
| T4 — Script CTA | "let's Connect" closing | Flowing script / cursive | Mixed case | {{COLOR_ACCENT_NAME}} |
| T5 — Label / Badge | Author name, date, link | Light weight, small caps | UPPERCASE | Black |
| T6 — Code | Code snippets | Monospace | As-written | Soft white on dark panel |

### Recommended Font Stack

| Role | Font |
|---|---|
| T1 / T2 Hero & Section Headings | **{{FONT_DISPLAY}}** |
| T3 Sub-labels / Subheadings | **Instrument Sans Bold** |
| T3 Body | **{{FONT_BODY}}** |
| T4 Script CTA | **{{FONT_SCRIPT}}** |
| T6 Code | **{{FONT_CODE}}** |

### Type Rules
- Hero headline (T1) should be the dominant visual element — use it large
- Section headers (T2) use the same condensed font as T1 but in {{COLOR_ACCENT_NAME}}
- Body text should never compete with headers — keep weight at Regular or Light
- The script font (T4) is used **only** on the closing "connect" slide
- All slide titles are UPPERCASE; body text is Sentence case

---

## 3. Layout System

### Canvas Size
- **1920 × 1080 px** (16:9 widescreen) — LinkedIn carousel standard

### Grid & Margins
- Generous outer margins (~80–100 px on all sides)
- Content is left-aligned on content slides; centred only on title and CTA slides
- Negative space is intentional — do not crowd slides

### Slide Structure (5-slide template)

| # | Slide Type | Purpose | Key Elements |
|---|---|---|---|
| 1 | **Title / Cover** | Hook + author branding | Hero headline, problem title + date, author badge, three-dot ornament |
| 2 | **Problem** | State the challenge | "PROBLEM" section header ({{COLOR_ACCENT_NAME}}), source link, problem text |
| 3 | **{{SECTION_1_TITLE}}** | Present the solution | "{{SECTION_1_TITLE}}" header ({{COLOR_ACCENT_NAME}}), logic bullets (left), code panel (right) |
| 4 | **{{SECTION_3_TITLE}}** | Business context + key lessons | Two sections: "{{SECTION_3_TITLE}}" + "{{SECTION_4_TITLE}}" |
| 5 | **CTA / Closing** | Drive connection | Script "let's Connect", horizontal rule lines |

### Recurring Layout Details
- **Bottom-right navigation line** — a short horizontal rule indicates slide progress; appears consistently on slides 1–4
- **Three-dot ornament** (`• • •`) — top-right corner of title slide only; serves as a visual anchor/brand mark
- **Code panels** — dark-background inset boxes, right-aligned on solution slides

---

## 4. Visual Elements

### Decorative Marks
| Element | Location | Notes |
|---|---|---|
| `• • •` three dots | Title slide, top-right | Black; size proportional to slide |
| Horizontal rule lines | CTA slide, top and bottom | Thin single lines, full-width |
| Bottom-right rule | Slides 1–4, bottom-right corner | Short line, acts as page marker |
| Author badge / outline box | Title slide | Thin black border, {{COLOR_GROUND_NAME}} fill, UPPERCASE label inside |
| {{COLOR_ACCENT_NAME}} vertical bar | Left of every section heading | Consistent weight and height; never improvised |

### Code Block Styling
- Dark panel (~60% of slide width on Solution slides)
- Slight inner padding
- Syntax highlighting: keywords in distinct color, rest in soft white
- Rounded corners optional but keep shadow-free (flat style)

### Emoji Usage
- One emoji per slide maximum — used to introduce the problem title
- Placed inline before the title/subtitle text, not as decorative background elements

---

## 5. Voice & Tone

| Dimension | Guideline |
|---|---|
| **Educational** | Always explain the "why" behind the logic, not just the syntax |
| **Concise** | Bullet points over paragraphs; one idea per bullet |
| **Practical** | Frame insights in business/product context |
| **Personal** | Close with a warm, handwritten-feel CTA — not a corporate call to action |
| **Consistent branding** | Always include author name + date + problem source on the cover |

### Section Labels (standard)
Use these exact labels across all posts:
- `Problem:` — intro to the challenge
- `{{SECTION_2_EMOJI}} {{SECTION_2_TITLE}}` — solution walkthrough bullets
- `{{SECTION_3_TITLE}}` — business interpretation bullets
- `{{SECTION_4_TITLE}}` — lessons

---

## 6. Post Metadata Standards

Every carousel should include on the cover slide:
- Series name: **{{SERIES_TITLE}}**
- Problem title
- Post date: `D MMM YYYY` format (e.g., `2 Feb 2026`)
- Author: {{AUTHOR_NAME}}

---

## 7. What to Avoid

- **No bright/saturated backgrounds** — only {{COLOR_GROUND_NAME}}
- **No more than two typeface families per slide** (exclude the code mono)
- **No {{COLOR_ACCENT_NAME}} body text** — {{COLOR_ACCENT_NAME}} is reserved for display headings and the script CTA
- **No heavy drop shadows or gradients** — the style is flat and editorial
- **No full-bleed images behind text** — the {{COLOR_GROUND_NAME}} background must always be the base
- **No centered body text** — left-align all copy except CTA slide
