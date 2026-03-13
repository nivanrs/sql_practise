# SQL of the Day — Repository Overview

A personal archive of weekly LinkedIn **"SQL of the Day"** posts by [@nivanrs](https://www.linkedin.com/in/nivanrs/). Each post is a SQL practice problem sourced from **StrataScratch** or **Codewars**, published with a markdown write-up, a LinkedIn plain-text copy, and (for newer posts) a branded carousel PDF.

---

## Repository Structure

```
sql_of_the_day/
├── readme.md                          # Project overview
├── AGENTS.md                          # AI agent instructions (Antigravity / generic)
├── CLAUDE.md                          # Claude Code-specific agent instructions
├── post_template.md                   # Blank template for new posts
├── .gitignore                         # Ignores .DS_Store only
│
├── posts/
│   ├── index.md                       # Master index: 26 rows, chronological (#1 = oldest)
│   ├── 2025-04-25_*.md … 2026-04-06_*.md   # 28 post markdown files
│   ├── linkedin/                      # LinkedIn plain-text copies (2 files so far)
│   │   ├── 2026-03-30_facebook_accounts.txt
│   │   └── 2026-04-06_apple_product_counts.txt
│   ├── media/
│   │   ├── pdfs/                      # 9 carousel PDFs (see PDF section below)
│   │   └── brand-guidelines/          # Warm Authority design system (3 files)
│   └── slide/                         # PPTX slide decks (2) + 2 PDFs from them
│
├── .agents/skills/humanizer/          # Humanizer skill (strips AI writing)
├── .agent/skills/humanizer            # Symlink / duplicate reference
└── .claude/skills/playwright-cli/     # Playwright skill (LinkedIn scraping)
```

---

## Content Inventory

### Posts: 28 markdown files

| Period | Count | Topics |
|--------|-------|--------|
| Apr–May 2025 | 12 | Aggregations, JOINs, regex, window functions, top-N, energy data |
| Jun–Aug 2025 | 3 | Filtering, CTEs, inspection/violation data |
| Dec 2025 | 2 | YoY comparisons, compilation-style post |
| Jan–Feb 2026 | 5 | Session analysis, cost orders, acceptance rates, freemium metrics |
| Mar–Apr 2026 | 6 | Purchases, rankings, nationality units, Oscars, Facebook accounts, Apple product counts |

Sources: **24 from StrataScratch**, **2 from Codewars** (posts #4 and #5).

### Index: [posts/index.md](file:///Users/nivanrs/Library/Mobile%20Documents/com~apple~CloudDocs/sql_of_the_day/posts/index.md)

26 rows tracked. Two posts are noted as pending index entries in [CLAUDE.md](file:///Users/nivanrs/Library/Mobile%20Documents/com~apple~CloudDocs/sql_of_the_day/CLAUDE.md): [finding_purchases.md](file:///Users/nivanrs/Library/Mobile%20Documents/com~apple~CloudDocs/sql_of_the_day/posts/2026-03-02_finding_purchases.md) and [number_of_units_per_nationality.md](file:///Users/nivanrs/Library/Mobile%20Documents/com~apple~CloudDocs/sql_of_the_day/posts/2026-03-16_number_of_units_per_nationality.md). Three posts have `—` for posted date (URN unknown).

### Carousel PDFs: 9 total

| Type | Files | Notes |
|------|-------|-------|
| **Legacy** (dark/cyan Canva) | 5 PDFs in `media/pdfs/` (`SQL of the Day (…).pdf`) + 2 in `slide/` | Pre-2026-03-30, deprecated style |
| **Warm Authority** (matplotlib) | 2 PDFs ([2026-03-30_facebook_accounts.pdf](file:///Users/nivanrs/Library/Mobile%20Documents/com~apple~CloudDocs/sql_of_the_day/posts/media/pdfs/2026-03-30_facebook_accounts.pdf), [2026-04-06_apple_product_counts.pdf](file:///Users/nivanrs/Library/Mobile%20Documents/com~apple~CloudDocs/sql_of_the_day/posts/media/pdfs/2026-04-06_apple_product_counts.pdf)) | Current standard |

### LinkedIn Plain Text: 2 files

Only the two most recent posts have [.txt](file:///Users/nivanrs/Library/Mobile%20Documents/com~apple~CloudDocs/sql_of_the_day/posts/linkedin/2026-03-30_facebook_accounts.txt) versions in `posts/linkedin/`.

---

## Post Format Evolution

The post template matured over time. Comparing earliest vs. latest:

| Element | Post #1 (Apr 2025) | Post #26 (Apr 2026) |
|---------|---------------------|----------------------|
| Header | `🧠 Solution` | `### SQL Solution` with ` ```sql ` block |
| Sections | Solution, Result, Why this matters | Problem, SQL Solution, Logic breakdown, Pattern tells you, Key takeaways |
| Hashtags | 12 tags | 8 tags |
| Source link | LinkedIn shortlink | Direct StrataScratch URL with `?code_type=1` |
| Depth | ~2 paragraphs | 4 detailed takeaway bullets + 3 business context bullets |

The current canonical format is defined in [post_template.md](file:///Users/nivanrs/Library/Mobile%20Documents/com~apple~CloudDocs/sql_of_the_day/post_template.md).

---

## Design System: Warm Authority

Defined in [warm-authority.md](file:///Users/nivanrs/Library/Mobile%20Documents/com~apple~CloudDocs/sql_of_the_day/posts/media/brand-guidelines/warm-authority.md). Core philosophy: *"warmth of invitation pressed against the force of expertise."*

| Role | Value |
|------|-------|
| Background | `#FBF3E4` warm cream |
| Text | `#1A1A1A` near-black |
| Accent | `#B91646` crimson |
| Display font | Big Shoulders Bold (ultra-condensed, all-caps) |
| Body font | Instrument Sans Regular |
| Code font | JetBrains Mono |
| Script font | Nothing You Could Do (crimson only) |

**Motifs** (exact, never improvised): three filled dots (top-right), right arrow (bottom-right), pill badge (author name), horizontal rules (top/bottom borders).

**PDF generation**: Python + matplotlib, `PdfPages` backend, `figsize=(10.8, 10.8)`, 150 dpi. Scripts saved to `/tmp/gen_{slug}.py`. Fonts loaded from `/Users/nivanrs/.claude/skills/canvas-design/canvas-fonts/`.

---

## Workflow: Adding a New Post

```mermaid
flowchart LR
    A["1. Write MD post"] --> B["2. Write LinkedIn .txt"]
    B --> C["3. Generate carousel PDF"]
    C --> D["4. Update index.md"]
```

1. **Markdown post** → `posts/YYYY-MM-DD_{slug}.md` (5 sections: Problem, SQL Solution, Logic breakdown, Pattern tells you, Key takeaways)
2. **LinkedIn plain text** → `posts/linkedin/YYYY-MM-DD_{slug}.txt` (no markdown; uses `→`, `•`, `─────` dividers, bold Unicode headers)
3. **Carousel PDF** → `posts/media/pdfs/YYYY-MM-DD_{slug}.pdf` (6 slides: Cover, Problem, Solution, How It Works, Pattern, Takeaways)
4. **Index update** → append next sequential number to `posts/index.md`; decode posted date from LinkedIn URN (`urn >> 22` → Unix ms)

---

## Writing Rules

- **No dashes or em dashes** in prose. Use colons, periods, or restructure instead.
- Hyphens are allowed inside URLs, code identifiers, and compound adjectives before a noun.
- Run the **humanizer** skill on all post text before finalizing.

---

## Agent Configuration

Two agent instruction files exist with overlapping content:

| File | Audience | Unique content |
|------|----------|----------------|
| [AGENTS.md](file:///Users/nivanrs/Library/Mobile%20Documents/com~apple~CloudDocs/sql_of_the_day/AGENTS.md) | All AI agents | Carousel syntax-highlighting colors, fonts directory path |
| [CLAUDE.md](file:///Users/nivanrs/Library/Mobile%20Documents/com~apple~CloudDocs/sql_of_the_day/CLAUDE.md) | Claude Code only | Key facts (pending index entries), Canva design link, legacy PDF deprecation note |

**Installed skills:**

| Skill | Location | Purpose |
|-------|----------|---------|
| humanizer | `.agents/skills/humanizer/` | Strip AI writing patterns from text |
| playwright-cli | `.claude/skills/playwright-cli/` | Browser automation for LinkedIn scraping |

---

## Gaps and Observations

> [!NOTE]
> These are not problems, just observations about the current state of the repo.

- **LinkedIn .txt coverage**: Only 2 of 28 posts have `.txt` files. The older 26 posts lack LinkedIn plain-text copies.
- **PDF coverage**: Only 8 of 28 posts have carousel PDFs. Posts #1–#17 have no PDF at all.
- **Index gaps**: Two posts (`finding_purchases.md`, `number_of_units_per_nationality.md`) are noted as pending but actually appear in the current index. Three posts show `—` for posted date.
- **Early post format**: The first ~12 posts use a simpler structure (different section headers, no "Simple logic breakdown" section). They could be backfilled to match the current template.
- **`posts/slide/` directory**: Contains 2 PPTX files and 2 PDFs for posts #24–#25, seemingly an intermediate format between Canva and matplotlib generation.
