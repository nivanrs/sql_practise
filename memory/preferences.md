# Preferences

## Writing style

- No dashes or em dashes in prose. Never `-` as a sentence separator, never `—`. Use a colon, a period, or restructure.
- Exceptions: hyphens in URLs, code, compound adjectives before a noun.
- Applies to both `.md` and `.txt` files.

## LinkedIn .txt files

### Hook-first structure (critical)

The `.txt` file always opens with a **hook sentence before the title**. LinkedIn truncates posts at roughly 2–3 lines before a "see more" button — everything above that fold determines whether readers click. The hook names the failure scenario in one compressed line.

Example:
```
My SQL query returned the correct result… but it was still wrong.

💻 SQL of the Day: Top Cool Votes
```

The hook comes before `💻 SQL of the Day:`, before the problem statement, before everything. It is not a section. It is the first thing the reader sees.

### General rules

- No external links in the body. LinkedIn suppresses reach on posts with outbound links.
- The `🔗` line goes in the `.md` and PDF only. User posts the link manually as the first comment after publishing.
- `.txt` formatting: `→` for bullets, `•` for lists, numbered for takeaways, `─────` dividers, emojis and hashtags preserved.
- Code blocks appear as **raw plain text** — no backticks, no markdown fencing. Just the SQL indented normally.
- Section headers use emoji + plain text (e.g. `🧠 SQL Solution`). Do **not** use bold Unicode characters (𝗦𝗤𝗟 𝗼𝗳 𝘁𝗵𝗲 𝗗𝗮𝘆) — earlier posts used this inconsistently; current standard is plain.

## LinkedIn .txt writing sequence (mandatory, every time)

Apply these three skills in order before finalising any `.txt` file:
1. `writing-clearly-and-concisely` — Strunk's rules, active voice, short sentences
2. `humanizer` — strip AI-generated patterns
3. `social-content` — hook strength, readability, CTA placement

## Post structure

`.md` files follow this canonical section order:

1. Problem
2. SQL Solution
3. Simple logic breakdown
4. This pattern tells you
5. Key takeaways
6. Hashtags

**Hashtag format:** `#SQLoftheDay #SQL #{Source} #DataAnalytics` followed by topic-specific tags. Total 3–8 tags. Source tag is `#StrataScratch` or `#Codewars`. Topic-specific tags go last (e.g. `#WindowFunctions #Ranking #Yelp`).

## Draft coaching workflow

When a raw draft is provided (any language, any format):
1. Save raw draft to `posts/drafts/{slug}_raw.md` unchanged
2. Run coaching check across four areas: Hook, Logic, Insight, Takeaway
3. Save critique to `posts/drafts/{slug}_critique.md`
4. Confirm "Ready to write the final post?" before proceeding

Drafts are commonly written in Indonesian — treat this as normal. **Deliver the coaching critique in the same language as the draft.** If the draft is in Indonesian, write the critique in Indonesian. This is a craft decision, not a concession — feedback lands better in the thinker's own language.

## Carousel structure

7 slides per carousel:
1. Cover (title, problem URL as clickable annotation, author pill)
2. The Problem
3. The Solution (code block)
4. How It Works (logic breakdown)
5. This Pattern Tells You
6. Key Takeaways + email CTA closing block
7. CTA slide (email CTA closing block repeated)

Slides 6 and 7 both end with the fixed two-line CTA: `follow for more SQL problems` (script, crimson) + `questions? nivanrs@gmail.com` (mono, muted, clickable mailto). The readme.md says "6 slides" — this is wrong. CLAUDE.md is the source of truth.

## Carousel generation

- Always run Python via PowerShell: `powershell -Command "python 'C:\tmp\gen_{slug}.py'"`
- Never run carousel scripts from git bash — causes fatal errors
- Font registration must happen BEFORE any `plt` call
- Use `fig.add_axes([0, 0, 1, 1])` — never `plt.subplots()` (adds margins)
- Never use `bbox_inches="tight"` — crops canvas, destroys layout
- Scripts saved to `/tmp/gen_{slug}.py` for reuse

## Index update

Chronological: **oldest post = #1, newest post = last row**. When adding a new post, append to the bottom and assign the next sequential number. Do not prepend. The readme.md says "reverse-chronological" — this is wrong. The actual index and CLAUDE.md are authoritative.

## Package manager

- Always `bun`, never `npm`
- Always `bunx`, never `npx`
