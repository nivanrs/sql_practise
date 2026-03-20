# AGENTS.md

Guidance for all AI agents working in this repository.

## What This Repo Is

A personal archive of weekly LinkedIn "SQL of the Day" posts. Each post is a SQL practice problem sourced from StrataScratch or Codewars. No build system, no tests. This is a content and documentation repo.

## Repository Structure

```
posts/
├── index.md                       # Post index, chronological (oldest = #1)
├── YYYY-MM-DD_{slug}.md           # One markdown file per post
├── linkedin/
│   └── YYYY-MM-DD_{slug}.txt      # LinkedIn plain text version
└── media/
    ├── pdfs/                      # Carousel PDFs (Warm Authority style)
    └── brand-guidelines/          # Design system spec and PNG reference
```

## Workflow: Adding a New Post

1. **Markdown post** — `posts/YYYY-MM-DD_{slug}.md`
2. **LinkedIn plain text** — `posts/linkedin/YYYY-MM-DD_{slug}.txt`
3. **Carousel PDF** — `posts/media/pdfs/YYYY-MM-DD_{slug}.pdf` (Python + matplotlib)
4. **Index** — append a new row to `posts/index.md` with the next sequential number

## Post Markdown Format

```
## 💻 SQL of the Day: {Title}
🔗 {StrataScratch URL}?code_type=1
### Problem:
{problem statement}
---
### 🧠 SQL Solution
```sql
{query}
```
---
### 🧩 Simple logic breakdown
{bullet breakdown}
---
### 📊 This pattern tells you:
{business context bullets}
---
### 🎯 Key takeaways
{numbered list}
{hashtags}
```

Hashtags: `#SQLoftheDay #SQL #{Source} #DataAnalytics ...` (3–8 tags).

## LinkedIn Plain Text Format (.txt)

No markdown syntax. Rules:
- `→` for logic breakdown bullets
- `•` for pattern/insight bullets
- Numbered list for takeaways
- `─────────────────────────────` as section dividers
- Bold Unicode (`𝗦𝗤𝗟 𝗦𝗼𝗹𝘂𝘁𝗶𝗼𝗻`) for section headers

## Writing Style Rules

- No dashes or em dashes in prose. Use a colon, a period, or restructure the sentence.
- Exception: hyphens inside URLs, code identifiers, and true compound adjectives before a noun.
- Run the **humanizer** skill on any post text before finalising to strip AI writing patterns.

## Brand: Warm Authority

All carousel PDFs use this design system.

| Role | Value |
|------|-------|
| Background | `#FBF3E4` warm cream |
| Text | `#161616` near-black |
| Accent | `#B91646` crimson |
| Display font | Big Shoulders Bold (all-caps, carousel scale 64–80pt) |
| Subheading font | Instrument Sans Bold (labels/headings only, never prose) |
| Body font | Instrument Sans Regular (carousel scale 11–14pt) |
| Script font | Nothing You Could Do (crimson only, carousel scale 28–36pt) |
| Code font | JetBrains Mono (carousel scale 10–12pt) |

Motifs (exact, never improvised): three filled dots top-right, right arrow bottom-right, pill badge for author name, horizontal rules top and bottom, crimson vertical bar left-aligned before every section heading.

Full spec: `posts/media/brand-guidelines/warm-authority.md`

### Presentation sample

https://www.canva.com/design/DAG-HWtEYj4/rK2Ae5G6JGPUfbNHnNcR-A/edit

## Carousel PDF Generation

- Tool: Python + matplotlib (`PdfPages` backend)
- Canvas: `figsize=(10.8, 10.8)`, `xlim/ylim=(0,1)`, `axis('off')`, `subplots_adjust(left=0,right=1,top=1,bottom=0)`
- Save: `pdf.savefig(fig, dpi=150)` — no `bbox_inches`
- Syntax highlighting colors: keywords `#B91646`, functions `#1A5FA8`, strings `#2A7A30`, identifiers `#161616`
- Fonts directory: `/Users/nivanrs/.agents/skills/canvas-design/canvas-fonts/`
- Save reusable script to `/tmp/gen_{slug}.py`

## Index Rules

- Chronological order: oldest post = #1, newest = last row
- Posted date: decode from LinkedIn URN via `urn >> 22` to get Unix ms timestamp
- Leave posted date as `—` if the URN is unknown
- PDF link format: `[📄](media/pdfs/{filename}.pdf)` or `—`

## Key Facts

- **Legacy PDFs** (pre-2026-03-30, dark/cyan Canva style) are deprecated — do not replicate that aesthetic
- `.playwright-mcp/` is gitignored — created when scraping LinkedIn via Playwright MCP

## Package Manager & Runtime

- **Always use `bun`** instead of `npm`.
- **Always use `bunx`** instead of `npx`.
- This applies to all terminal commands, installation steps, and script executions in this repository.

## Installed Skills

Skills in `.agents/skills/` are the primary set for this project. Invoke via the `Skill` tool.

### Project skills (`.agents/skills/`)

| Skill | Purpose |
|-------|---------|
| `humanizer` | Strip AI writing patterns from post text |
| `writing-clearly-and-concisely` | Tighten prose before finalising |
| `web-to-markdown` | Scrape StrataScratch/Codewars problem pages into markdown |
| `commit-work` | Stage, commit, and push with smart Conventional Commit messages |
| `social-content` | LinkedIn-specific copy and hook writing |
| `copy-editing` | Polish takeaways and logic breakdown sections (7-sweep framework) |
| `canvas-design` | Generate carousel PDFs and PNGs using Warm Authority brand |
| `pdf` | Programmatic PDF manipulation (merge, extract, inspect) |
| `playwright-cli` | Browser automation for LinkedIn scraping and URN extraction |

### Global skills — relevant for this project

| Skill | When to use |
|-------|-------------|
| `superpowers:brainstorming` | Before drafting a new post or designing a carousel |
| `superpowers:writing-plans` | Before multi-step work (e.g. new platform adaptation, post series) |
| `superpowers:verification-before-completion` | Before committing post + index + PDF together |

### Global skills — marginal (situational only)

| Skill | Condition |
|-------|-----------|
| `brand-color-psychology` | Only if Warm Authority palette is revisited from scratch |
| `data-visualization` | Only if carousels become chart-forward rather than code-forward |
| `storytelling-with-data` | Concept applies to "📊 This pattern tells you:" sections, but `copy-editing` (So What sweep) already covers this; only add if carousels gain actual charts |
| `simplify` | Only for one-off Python carousel generation scripts |

### Global skills — not relevant for this project

`pptx`, `ppt-visual`, `scientific-slides`, `senior-data-scientist`, `senior-data-engineer`, `data-quality-frameworks`, `data-storytelling`, `brand-guidelines` (Anthropic brand only), `web-typography`, `minimalist-ui`, `frontend-design`, `ui-ux-pro-max`, `web-design-guidelines`, `web-design-reviewer`, `xlsx`, `claude-api`, `notebooklm`, `loop`, `superpowers:tdd`, `code-review:code-review`, `update-config`, `keybindings-help`, and registry skills (`pptx-presentation-builder`, `refero-design`, `visual-identity-direction`, `brand-typography-systems`, `revealjs-slides`, `slidev-styling`).
