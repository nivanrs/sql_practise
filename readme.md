# SQL of the Day

A personal archive of weekly SQL practice problems posted on [LinkedIn](https://www.linkedin.com/in/nivanrs/). Problems are sourced from StrataScratch and Codewars.

## Structure

```
posts/
├── index.md                  # Full post index (chronological, oldest first)
├── YYYY-MM-DD_{slug}.md      # One file per post (26 total)
├── linkedin/
│   └── YYYY-MM-DD_{slug}.txt # LinkedIn-copyable plain text version
└── media/
    ├── pdfs/                 # LinkedIn carousel PDFs
    └── brand-guidelines/     # Warm Authority design system
```

## Posts

26 posts archived, spanning **April 2025 – April 2026**.

→ [View full post index](posts/index.md)

| Range | Topics |
|-------|--------|
| Apr – May 2025 | Aggregations, JOINs, regex, window functions |
| Jun – Aug 2025 | Filtering, CTEs, inspection data, subqueries |
| Dec 2025 – Feb 2026 | YoY comparisons, session analysis, freemium metrics |
| Mar – Apr 2026 | Conditional counting, ranking, ratio analysis |

## Workflow

Each post follows this sequence:

**1. Write the markdown post** (`posts/YYYY-MM-DD_{slug}.md`)

Standard sections: Problem, SQL Solution, Simple logic breakdown, This pattern tells you, Key takeaways. Header emoji is 💻. StrataScratch links include `?code_type=1`.

**2. Write the LinkedIn plain text** (`posts/linkedin/YYYY-MM-DD_{slug}.txt`)

No markdown syntax. Uses `→` for bullets, `•` for lists, `─────` dividers, bold Unicode for section headers. No dashes or em dashes in prose.

**3. Generate the carousel PDF** (`posts/media/pdfs/YYYY-MM-DD_{slug}.pdf`)

6 slides: Cover, The Problem, The Solution, How It Works, This Pattern Tells You, Key Takeaways. Generated with Python + matplotlib using the Warm Authority design system (cream `#FBF3E4`, crimson `#B91646`, near-black `#1A1A1A`). Generator scripts saved to `/tmp/gen_{slug}.py`.

**4. Update the index** (`posts/index.md`)

Prepend a new row as `#1` and renumber all existing rows. Index is reverse-chronological. Posted date is decoded from the LinkedIn URN (`urn >> 22` gives Unix ms timestamp). Leave as `—` if the URN is unknown.

## Design System

All carousels use the **Warm Authority** brand: warm cream background, crimson accent, Big Shoulders Bold display type, Instrument Sans body, JetBrains Mono for code. Full spec in `posts/media/brand-guidelines/warm-authority.md`.
