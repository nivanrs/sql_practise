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
| Text | `#1A1A1A` near-black |
| Accent | `#B91646` crimson |
| Display font | Big Shoulders Bold |
| Body font | Instrument Sans Regular |
| Code font | JetBrains Mono |
| Script font | Nothing You Could Do (crimson only) |

Motifs (exact, never improvised): three filled dots top-right, right arrow bottom-right, pill badge for author name, horizontal rules top and bottom.

Full spec: `posts/media/brand-guidelines/warm-authority.md`

## Carousel PDF Generation

- Tool: Python + matplotlib (`PdfPages` backend)
- Canvas: `figsize=(10.8, 10.8)`, `xlim/ylim=(0,1)`, `axis('off')`, `subplots_adjust(left=0,right=1,top=1,bottom=0)`
- Save: `pdf.savefig(fig, dpi=150)` — no `bbox_inches`
- Syntax highlighting colors: keywords `#B91646`, functions `#1A5FA8`, strings `#2A7A30`, identifiers `#1A1A1A`
- Fonts directory: `/Users/nivanrs/.claude/skills/canvas-design/canvas-fonts/`
- Save reusable script to `/tmp/gen_{slug}.py`

## Index Rules

- Chronological order: oldest post = #1, newest = last row
- Posted date: decode from LinkedIn URN via `urn >> 22` to get Unix ms timestamp
- Leave posted date as `—` if the URN is unknown
- PDF link format: `[📄](media/pdfs/{filename}.pdf)` or `—`

## Installed Skills

| Skill | Scope | Purpose |
|-------|-------|---------|
| `humanizer` | project + global | Strip AI writing patterns from post text |
| `writing-clearly-and-concisely` | project + global | Tighten prose before finalising |
| `web-to-markdown` | project + global | Scrape StrataScratch/Codewars problem pages into markdown |
| `commit-work` | project + global | Stage, commit, and push with smart messages |
| `social-content` | project + global | LinkedIn-specific copy and hook writing |
| `copy-editing` | project + global | Polish takeaways and logic breakdown sections |
| `canvas-design` | project + global | Generate PDFs and PNGs from design systems |
| `pdf` | project + global | Programmatic PDF manipulation (merge, extract, inspect) |
| `playwright-cli` | project only | Browser automation for LinkedIn scraping |
