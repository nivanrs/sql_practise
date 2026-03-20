# AGENTS.md

Guidance for all AI agents working in this repository.

## What This Repo Is

A personal archive of weekly LinkedIn "{{SERIES_TITLE}}" posts. Each post is a {{TOPIC_DOMAIN}} practice problem sourced from {{CONTENT_SOURCES}}. No build system, no tests. This is a content and documentation repo.

## Repository Structure

```
posts/
├── index.md                       # Post index, chronological (oldest = #1)
├── YYYY-MM-DD_{slug}.md           # One markdown file per post
├── drafts/
│   ├── {slug}_raw.md              # Raw draft exactly as written (any language)
│   └── {slug}_critique.md        # Coaching feedback on the raw draft
├── linkedin/
│   └── YYYY-MM-DD_{slug}.txt      # LinkedIn plain text version
└── media/
    ├── pdfs/                      # Carousel PDFs ({{BRAND_NAME}} style)
    └── brand-guidelines/          # Design system spec
```

## Workflow: Adding a New Post

1. **Markdown post** — `posts/YYYY-MM-DD_{slug}.md`
2. **LinkedIn plain text** — `posts/linkedin/YYYY-MM-DD_{slug}.txt`
3. **Carousel PDF** — `posts/media/pdfs/YYYY-MM-DD_{slug}.pdf` (Python + matplotlib)
4. **Index** — append a new row to `posts/index.md` with the next sequential number

## Post Markdown Format

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
{numbered list}
{hashtags}
```

Hashtags: `{{SERIES_HASHTAG}} #{{TOPIC_DOMAIN}} #{Source} ...` (3–8 tags).

## LinkedIn Plain Text Format (.txt)

No markdown syntax. Rules:
- `→` for logic breakdown bullets
- `•` for pattern/insight bullets
- Numbered list for takeaways
- `─────────────────────────────` as section dividers
- Bold Unicode for section headers

## Writing Style Rules

{{WRITING_RULES}}

## Brand: {{BRAND_NAME}}

All carousel PDFs use this design system.

| Role | Value |
|------|-------|
| Background | `{{COLOR_GROUND_HEX}}` {{COLOR_GROUND_NAME}} |
| Text | `{{COLOR_PRIMARY_HEX}}` near-black |
| Accent | `{{COLOR_ACCENT_HEX}}` {{COLOR_ACCENT_NAME}} |
| Display font | {{FONT_DISPLAY}} (all-caps, carousel scale 64–80pt) |
| Subheading font | Instrument Sans Bold (labels/headings only, never prose) |
| Body font | {{FONT_BODY}} (carousel scale 11–14pt) |
| Script font | {{FONT_SCRIPT}} ({{COLOR_ACCENT_NAME}} only, carousel scale 28–36pt) |
| Code font | {{FONT_CODE}} (carousel scale 10–12pt) |

Motifs (exact, never improvised): three filled dots top-right, right arrow bottom-right, pill badge for author name, horizontal rules top and bottom, {{COLOR_ACCENT_NAME}} vertical bar left-aligned before every section heading.

Full spec: `posts/media/brand-guidelines/brand-guidelines.md`

### Presentation sample

{{CANVA_DESIGN_URL}}

## Carousel PDF Generation

- Tool: Python + matplotlib (`PdfPages` backend)
- Canvas: `figsize=(10.8, 10.8)`, `xlim/ylim=(0,1)`, `axis('off')`, `subplots_adjust(left=0,right=1,top=1,bottom=0)`
- Save: `pdf.savefig(fig, dpi=150)` — no `bbox_inches`
- Syntax highlighting colors: keywords `{{COLOR_ACCENT_HEX}}`, functions `#1A5FA8`, strings `#2A7A30`, identifiers `{{COLOR_PRIMARY_HEX}}`
- Fonts directory: `/Users/{{AUTHOR_NAME}}/.agents/skills/canvas-design/canvas-fonts/`
- Save reusable script to `/tmp/gen_{slug}.py`

## Index Rules

- Chronological order: oldest post = #1, newest = last row
- Posted date: decode from LinkedIn URN via `urn >> 22` to get Unix ms timestamp
- Leave posted date as `—` if the URN is unknown
- PDF link format: `[📄](media/pdfs/{filename}.pdf)` or `—`

## Key Facts

- 0 posts total
- `.playwright-mcp/` is gitignored — created when scraping LinkedIn via Playwright MCP

## Package Manager & Runtime

- **Always use `{{PACKAGE_MANAGER}}`** instead of `npm`.
- **Always use `{{PACKAGE_RUNNER}}`** instead of `npx`.
- This applies to all terminal commands, installation steps, and script executions in this repository.

## Installed Skills

Skills in `.agents/skills/` are the primary set for this project. Invoke via the `Skill` tool.

### Project skills (`.agents/skills/`)

| Skill | Purpose |
|-------|---------|
| `humanizer` | Strip AI writing patterns from post text |
| `writing-clearly-and-concisely` | Tighten prose before finalising |
| `web-to-markdown` | Scrape source platform problem pages into markdown |
| `commit-work` | Stage, commit, and push with smart Conventional Commit messages |
| `social-content` | LinkedIn-specific copy and hook writing |
| `copy-editing` | Polish takeaways and logic breakdown sections (7-sweep framework) |
| `canvas-design` | Generate carousel PDFs and PNGs using {{BRAND_NAME}} brand |
| `pdf` | Programmatic PDF manipulation (merge, extract, inspect) |
| `playwright-cli` | Browser automation for LinkedIn scraping and URN extraction |
