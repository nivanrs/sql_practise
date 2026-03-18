# Design Spec: X and Threads Adaptation

**Date:** 2026-03-18
**Branch:** feature/x-and-threads
**Status:** Approved

---

## Overview

Adapt all existing SQL of the Day LinkedIn posts into native X (Twitter) and Threads thread formats, written in Indonesian. Add X and Threads generation to the standard workflow for all future posts.

---

## Goals

- Generate platform-native Indonesian threads for all 32 existing posts (backfill)
- Add X and Threads output as a required step in the "Adding a New Post" workflow
- No new scripts, dependencies, or API keys — Claude Code generates files inline

---

## File Structure

```
posts/
  x/
    YYYY-MM-DD_{slug}.txt       ← X thread (8-10 tweets, ≤280 chars each)
  threads/
    YYYY-MM-DD_{slug}.txt       ← Threads thread (8-10 posts, ≤500 chars each)
  linkedin/                     ← unchanged
  *.md                          ← unchanged
```

Both directories are added to `posts/index.md` as two new link columns — **X** and **Threads** — positioned after the existing PDF column, using the same `[🐦](x/{filename}.txt)` / `[🧵](threads/{filename}.txt)` link format. Cells are `—` until a file exists.

---

## Thread Structure

Each thread follows a fixed 8–10 post skeleton. Both X and Threads use the same skeleton; the difference is character limits and tone density.

| Post | Role | Description |
|------|------|-------------|
| 1 | **Hook** | The failure scenario — what breaks if you get this wrong. Punchy, 1–2 sentences in Indonesian. |
| 2 | **Problem** | Concise reframe of the SQL problem statement. |
| 3 | **SQL** | The query as a code block, with a one-line setup in Indonesian. |
| 4 | **Breakdown 1** | First step — explains *why* it exists, not just what it does. |
| 5 | **Breakdown 2** | Second step. |
| 6 | **Breakdown 3** | Third step. |
| 7 | **Breakdown 4** | Fourth step (merge with 6 if fewer than 4 logical steps). |
| 8 | **Insight** | "So what" — business consequence grounded in a real scenario. |
| 9 | **Takeaway** | The specific rule. Format: "Kalau [kondisi], pakai [X] karena [konsekuensi]." |
| 10 | **CTA** | Follow prompt + relevant hashtags in Indonesian. |

### Platform Differences

**X (posts/x/):**
- Hard limit: ≤280 characters per tweet
- Tweet 1 opens with `🧵` thread marker
- Breakdown posts 4–7 may be merged if needed to stay within character limits
- If the SQL query (Post 3) exceeds 280 characters, split it across two consecutive tweets (3a and 3b) and adjust the total count N accordingly
- Tighter, punchier sentences
- Numbered format: `[1/N]` on each tweet; N reflects the final post count after any merges or splits

**Threads (posts/threads/):**
- Soft limit: ≤500 characters per post
- No thread marker needed on post 1
- Each breakdown step gets its own full explanation
- More conversational, slightly more breathing room
- Numbered format: `[1/N]` on each post; N reflects the final post count after any merges

---

## Language & Tone

- **Language:** Indonesian throughout (Bahasa Indonesia)
- **Tone:** Native platform voice — informal, direct, conversational. Not a translation of the LinkedIn post; a fresh rewrite for the platform audience.
- **No dashes or em dashes** in prose (same rule as LinkedIn posts). Use a colon or restructure instead.
- Hyphens in code and compound adjectives are still allowed.

### Hashtags

Brand and technical tags stay in English regardless of post language. Topic-specific tags may be in Indonesian or English depending on common usage.

**Always include in English:** `#SQLoftheDay` `#SQL` `#DataAnalytics`

**Source tag:** match the source (e.g. `#StrataScratch`, `#Codewars`) — always English.

**Topic tags:** 1–3 additional topic-specific tags, in English (e.g. `#WindowFunctions`, `#ConditionalCounting`). Indonesian topic tags are allowed only when there is no English equivalent in common use.

**Count:** 4–7 total hashtags per thread. X and Threads may use slightly different tag sets where platform norms differ, but the brand tags above are always present.

---

## Generation Workflow

Claude Code generates both files inline by reading the source `posts/YYYY-MM-DD_{slug}.md` and writing:

1. `posts/x/YYYY-MM-DD_{slug}.txt`
2. `posts/threads/YYYY-MM-DD_{slug}.txt`

No external script. No API key. No dependencies.

---

## CLAUDE.md Changes

**1. "Adding a New Post" workflow** — gains two new steps after the LinkedIn `.txt` step:

```
3. Create `posts/x/YYYY-MM-DD_{slug}.txt` — X thread in Indonesian (8-10 tweets, ≤280 chars each)
4. Create `posts/threads/YYYY-MM-DD_{slug}.txt` — Threads thread in Indonesian (8-10 posts, ≤500 chars each)
```

Step numbering for PDF and index steps shifts accordingly.

**2. Key Facts** — update the post count line from:
> "26 posts total (24 indexed + 2 pending index entries: ...)"

to reflect the current total of 32 posts (all indexed).

---

## Backfill Plan

All 32 existing posts are processed in chronological order. For each post:

1. Read `posts/YYYY-MM-DD_{slug}.md`
2. Write `posts/x/YYYY-MM-DD_{slug}.txt`
3. Write `posts/threads/YYYY-MM-DD_{slug}.txt`

Posts without a full `.md` file (drafts only) are skipped until the `.md` exists.

---

## Out of Scope

- Carousel PDFs for X/Threads (not applicable to these platforms)
- Auto-scheduling or publishing to X/Threads
- Translating the `.md` source files themselves
- Any changes to the LinkedIn workflow or existing files
