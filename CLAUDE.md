# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Repo Is

A personal archive of LinkedIn "SQL of the Day" posts. Each post is a SQL practice problem sourced from StrataScratch or Codewars. No build system, no tests — this is a content/documentation repo.

## Repository Structure

- `posts/*.md` — One markdown file per post, named by slug (e.g. `premium_vs_freemium_downloads.md`)
- `posts/index.md` — Master index table: post number, title, source, exact posting date, links to file and PDF
- `posts/media/pdfs/` — LinkedIn carousel PDFs (5 files, covering posts #1–5, Jan–Feb 2026)
- `images/` — Legacy image assets for post #10 (Oscar problem)
- `readme.md` — Project overview

## Post Markdown Format

Each post file follows this structure:
```
## {emoji} SQL of the Day: {Title}
🔗 {LinkedIn or StrataScratch URL}
### Problem:
{problem statement}
---
### SQL Solution
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
{bullets}
{hashtags}
```

## Adding a New Post

1. Create `posts/{slug}.md` using the format above
2. If a carousel PDF exists, save to `posts/media/pdfs/`
3. Add a row to `posts/index.md` — columns: `# | Problem | Source | Posted | File | PDF`
   - **Posted date**: decode from LinkedIn URN with `urn >> 22` to get Unix ms timestamp (`datetime.fromtimestamp((urn >> 22) / 1000, tz=timezone.utc)`)
   - PDF link: `[📄](media/pdfs/{filename}.pdf)` or `—`

## Key Facts

- 23 posts indexed, spanning April 2025 – February 2026
- Post #10 (`person_with_most_oscars`) has no LinkedIn URN (posted date unknown)
- `.playwright-mcp/` is gitignored — created when scraping LinkedIn via Playwright MCP
