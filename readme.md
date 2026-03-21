# SQL of the Day

A personal archive of weekly SQL practice problems posted on [LinkedIn](https://www.linkedin.com/in/nivanrs/). Problems are sourced from StrataScratch and Codewars.

## Structure

```
posts/
├── index.md                  # Full post index (chronological, oldest first)
├── YYYY-MM-DD_{slug}.md      # One file per post
├── drafts/
│   ├── {slug}_raw.md         # Raw draft exactly as written (any language)
│   └── {slug}_critique.md    # Coaching feedback on the raw draft
├── linkedin/
│   └── YYYY-MM-DD_{slug}.txt # LinkedIn-copyable plain text version
└── media/
    ├── pdfs/                 # LinkedIn carousel PDFs
    └── brand-guidelines/     # Warm Authority design system
```

## Posts

36 posts archived, spanning **April 2025 – June 2026**.

→ [View full post index](posts/index.md)

| Range | Topics |
|-------|--------|
| Apr – May 2025 | Aggregations, JOINs, regex, window functions |
| Jun – Aug 2025 | Filtering, CTEs, inspection data, subqueries |
| Dec 2025 – Feb 2026 | YoY comparisons, session analysis, freemium metrics |
| Mar – May 2026 | Conditional counting, ranking, ratio analysis, string expansion |
| Jun 2026 | Subquery patterns, performance management |

## Workflow

Each post follows this sequence:

**0. Write and save a rough draft** (`posts/drafts/{slug}_raw.md`)

Write in any language, any format. The draft gets saved as-is, then reviewed for: hook angle, SQL correctness, logic precision, insight framing, and takeaway quality. Coaching feedback is saved to `posts/drafts/{slug}_critique.md` before the final post is written.

**1. Write the markdown post** (`posts/YYYY-MM-DD_{slug}.md`)

Standard sections: Problem, SQL Solution, Simple logic breakdown, This pattern tells you, Key takeaways. Header emoji is 💻. StrataScratch links include `?code_type=1`.

**2. Write the LinkedIn plain text** (`posts/linkedin/YYYY-MM-DD_{slug}.txt`)

Opens with a hook sentence (the failure scenario) before the post title. No markdown syntax. Uses `→` for bullets, `•` for lists, `─────` dividers, emoji + plain text for section headers. No dashes or em dashes in prose. No external links in the body — post the problem URL as the first comment after publishing.

**3. Generate the carousel PDF** (`posts/media/pdfs/YYYY-MM-DD_{slug}.pdf`)

7 slides: Cover, The Problem, The Solution, How It Works, This Pattern Tells You, Key Takeaways, CTA. Generated with Python + matplotlib using the Warm Authority design system (cream `#FBF3E4`, crimson `#B91646`, near-black `#161616`). Generator scripts saved to `/tmp/gen_{slug}.py`.

**4. Update the index** (`posts/index.md`)

Append a new row at the bottom and assign the next sequential number. Index is chronological — oldest post is #1, newest is last. Posted date is decoded from the LinkedIn URN (`urn >> 22` gives Unix ms timestamp). Leave as `—` if the URN is unknown.

## Design System

All carousels use the **Warm Authority** brand: warm cream background, crimson accent, Big Shoulders Bold display type, Instrument Sans body, JetBrains Mono for code. Full spec in `posts/media/brand-guidelines/warm-authority.md`.
