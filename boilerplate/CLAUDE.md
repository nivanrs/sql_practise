# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Repo Is

A personal archive of LinkedIn "{{SERIES_TITLE}}" posts. Each post is a {{TOPIC_DOMAIN}} practice problem sourced from {{CONTENT_SOURCES}}. No build system, no tests — this is a content/documentation repo.

## Repository Structure

- `posts/*.md` — One markdown file per post, named `YYYY-MM-DD_{slug}.md` (e.g. `2026-02-02_example_post.md`)
- `posts/drafts/{slug}_raw.md` — Raw draft exactly as the user wrote it (any language, any format)
- `posts/drafts/{slug}_critique.md` — Coaching feedback saved alongside the raw draft
- `posts/linkedin/*.txt` — LinkedIn-copyable plain text version of each post (no markdown syntax)
- `posts/index.md` — Master index table: post number, title, source, exact posting date, links to file and PDF
- `posts/media/pdfs/` — LinkedIn carousel PDFs; all new carousels use {{BRAND_NAME}}
- `images/` — Legacy image assets (if any)
- `readme.md` — Project overview

## Brand Guidelines

Design philosophy: **{{BRAND_NAME}}**

Full spec: `posts/media/brand-guidelines/brand-guidelines.md` | Design philosophy: `posts/media/brand-guidelines/design-philosophy.md`

### Palette
| Role | Hex | Usage |
|------|-----|-------|
| Ground | `{{COLOR_GROUND_HEX}}` | Background — {{COLOR_GROUND_NAME}}, never white |
| Authority | `{{COLOR_PRIMARY_HEX}}` | Headlines, body text, structural marks |
| Accent | `{{COLOR_ACCENT_HEX}}` | Section titles, script, emotional markers **only** |

### Typography
| Role | Font | Notes |
|------|------|-------|
| Display | {{FONT_DISPLAY}} | Ultra-condensed, all-caps, architectural scale |
| Subheading | Instrument Sans Bold | Labels and sub-level headings only; never used for prose |
| Body | {{FONT_BODY}} | Humanist sans, never bold for prose |
| Script | {{FONT_SCRIPT}} | {{COLOR_ACCENT_NAME}} only, single moments |
| Code | {{FONT_CODE}} | Reduced weight, muted tone |

### Recurring Motifs (exact, never improvised)
- **Three filled dots** — top-right, carousel position indicator
- **Right-pointing arrow** — bottom-right navigation
- **Pill badge** — cream fill + black stroke, frames author name
- **Horizontal rules** — section dividers, page top/bottom borders
- **{{COLOR_ACCENT_NAME}} vertical bar** — left-aligned, precedes every section heading; consistent weight and height across all sections

### Principles
- Space first: generous vertical breathing room, constant horizontal margins
- Typography at two extremes only: monumental display OR quiet body — nothing in between
- {{COLOR_ACCENT_NAME}} is directional, not decorative — fires only at moments of genuine importance
- Technical content (code, logic) gets the same compositional care as emotional content

## Presentation sample

{{CANVA_DESIGN_URL}}

## Post Markdown Format

Each post file follows this structure (header emoji is `{{HEADER_EMOJI}}`):
```
## {{HEADER_EMOJI}} {{SERIES_TITLE}}: {Title}
🔗 {source URL}
### Problem:
{problem statement}
---
### {{SECTION_1_EMOJI}} {{SECTION_1_TITLE}}
```{{CODE_LANGUAGE}}
{code}
```
---
### {{SECTION_2_EMOJI}} {{SECTION_2_TITLE}}
{bullet breakdown}
---
### {{SECTION_3_EMOJI}} {{SECTION_3_TITLE}}
{business context bullets}
---
### {{SECTION_4_EMOJI}} {{SECTION_4_TITLE}}
{bullets}
{hashtags}
```

Hashtag format: `{{SERIES_HASHTAG}} #{{TOPIC_DOMAIN}} #{Source} ...` (3–8 tags, topic-specific tags at the end).

## Writing Style Rules

{{WRITING_RULES}}

## Draft Coaching Workflow

When the user provides a rough draft (in any language, any format), do this before writing the polished post:

1. **Save the raw draft** to `posts/drafts/{slug}_raw.md` exactly as written — no edits
2. **Save the critique** to `posts/drafts/{slug}_critique.md` after running the coaching check
3. **Run the coaching check** and give feedback on these four areas before touching the final post:

### Coaching questions to answer per draft

**{{COACHING_Q1_TITLE}}**
{{COACHING_Q1_BULLETS}}

**{{COACHING_Q2_TITLE}}**
{{COACHING_Q2_BULLETS}}

**{{COACHING_Q3_TITLE}}**
{{COACHING_Q3_BULLETS}}

**{{COACHING_Q4_TITLE}}**
{{COACHING_Q4_BULLETS}}

### Format for coaching feedback
Return feedback in this order:
1. One-line summary of what's strong in the draft
2. Numbered list of coaching notes (one per weakness)
3. Confirm: "Ready to write the final post?" before proceeding

## Adding a New Post

1. Create `posts/YYYY-MM-DD_{slug}.md` using the format above
2. Create `posts/linkedin/YYYY-MM-DD_{slug}.txt` — LinkedIn-copyable plain text version (no markdown syntax; use `→` bullets, `•` for lists, numbered for takeaways, `─────` dividers, emojis and hashtags preserved)
3. If a carousel PDF exists, generate with Python/matplotlib and save to `posts/media/pdfs/YYYY-MM-DD_{slug}.pdf`
4. Append a new row to `posts/index.md` and assign the next sequential number — index is **chronological** (oldest = #1, newest = last)
   - **Posted date**: decode from LinkedIn URN with `urn >> 22` to get Unix ms timestamp (`datetime.fromtimestamp((urn >> 22) / 1000, tz=timezone.utc)`)
   - PDF link: `[📄](media/pdfs/{filename}.pdf)` or `—`

## Key Facts

- 0 posts total
- **Carousel generation**: all new PDFs use Python/matplotlib (`PdfPages`, `figsize=(10.8, 10.8)`, Warm Authority fonts); reusable scripts saved to `/tmp/gen_{slug}.py`
- `.playwright-mcp/` is gitignored — created when scraping LinkedIn via Playwright MCP

## Package Manager & Runtime

- **Always use `{{PACKAGE_MANAGER}}`** instead of `npm`.
- **Always use `{{PACKAGE_RUNNER}}`** instead of `npx`.
- This applies to all terminal commands, installation steps, and script executions in this repository.
