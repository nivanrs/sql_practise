# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Repo Is

A personal archive of LinkedIn "SQL of the Day" posts. Each post is a SQL practice problem sourced from StrataScratch or Codewars. No build system, no tests — this is a content/documentation repo.

## Repository Structure

- `posts/*.md` — One markdown file per post, named `YYYY-MM-DD_{slug}.md` (e.g. `2026-02-02_premium_vs_freemium_downloads.md`)
- `posts/drafts/{slug}_raw.md` — Raw draft exactly as the user wrote it (any language, any format)
- `posts/drafts/{slug}_critique.md` — Coaching feedback saved alongside the raw draft
- `posts/linkedin/*.txt` — LinkedIn-copyable plain text version of each post (no markdown syntax)
- `posts/index.md` — Master index table: post number, title, source, exact posting date, links to file and PDF
- `posts/media/pdfs/` — LinkedIn carousel PDFs (7 files); all new carousels use Warm Authority; pre-2026-03-30 PDFs are legacy (dark/cyan Canva style, deprecated)
- `images/` — Legacy image assets for post #11 (Oscar problem)
- `readme.md` — Project overview

## Brand Guidelines

Design philosophy: **Warm Authority** — warmth of invitation pressed against the force of expertise.

Full spec: `posts/media/brand-guidelines/warm-authority.md` | PNG reference: `posts/media/brand-guidelines/brand-guidelines.png`

### Palette
| Role | Hex | Usage |
|------|-----|-------|
| Ground | `#FBF3E4` | Background — warm cream, never white |
| Authority | `#161616` | Headlines, body text, structural marks |
| Accent | `#B91646` | Section titles, script, emotional markers **only** |

### Typography
| Role | Font | Notes |
|------|------|-------|
| Display | Big Shoulders Bold | Ultra-condensed, all-caps, architectural scale |
| Subheading | Instrument Sans Bold | Labels and sub-level headings only; never used for prose |
| Body | Instrument Sans Regular | Humanist sans, never bold for prose |
| Script | Nothing You Could Do | Crimson only, single moments |
| Code | JetBrains Mono | Reduced weight, muted tone |

### Recurring Motifs (exact, never improvised)
- **Three filled dots** — top-right, carousel position indicator
- **Right-pointing arrow** — bottom-right navigation
- **Pill badge** — cream fill + black stroke, frames author name
- **Horizontal rules** — section dividers, page top/bottom borders
- **Crimson vertical bar** — left-aligned, precedes every section heading; consistent weight and height across all sections

### Principles
- Space first: generous vertical breathing room, constant horizontal margins
- Typography at two extremes only: monumental display OR quiet body — nothing in between
- Crimson is directional, not decorative — fires only at moments of genuine importance
- Technical content (code, logic) gets the same compositional care as emotional content

## Presentation sample

https://www.canva.com/design/DAG-HWtEYj4/rK2Ae5G6JGPUfbNHnNcR-A/edit


## Post Markdown Format

Each post file follows this structure (header emoji is `💻`):
```
## 💻 SQL of the Day: {Title}
🔗 {LinkedIn shortlink or StrataScratch URL} — StrataScratch links must include `?code_type=1` (e.g. `https://platform.stratascratch.com/coding/10141-apple-product-counts?code_type=1`)
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
{bullets}
{hashtags}
```

Hashtag format: `#SQLoftheDay #SQL #{Source} #DataAnalytics ...` (3–8 tags, topic-specific tags at the end).

## LinkedIn .txt Writing Skills (Mandatory)

When writing any `posts/linkedin/*.txt` file, you MUST invoke these skills in sequence before finalizing the content:

1. `writing-clearly-and-concisely` — apply Strunk's rules: cut filler, prefer active voice, favor short declarative sentences
2. `humanizer` — strip AI-generated patterns, make the prose sound like a person wrote it
3. `social-content` — optimize for LinkedIn reach: hook strength, readability, call-to-action placement

Do not skip these even when revising an existing `.txt` file. Apply all three every time.

## Writing Style Rules

- **No dashes or em dashes** in post prose. Never use `-` as a sentence separator and never use `—`. Use a colon, a period, or restructure the sentence instead.
- This applies to both `.md` and `.txt` files. Hyphens inside URLs, code, and compound adjectives used as modifiers before a noun are the only exceptions.
- **No external links in the `.txt` file.** LinkedIn's algorithm suppresses reach on posts that contain external links in the body. The `🔗` line stays in the `.md` file and the PDF (as a clickable annotation), but is omitted from the `.txt` entirely. Post the link manually as the **first comment** after publishing.

## Draft Coaching Workflow

When the user provides a rough draft (in any language, any format), do this before writing the polished post:

1. **Save the raw draft** to `posts/drafts/{slug}_raw.md` exactly as written — no edits
2. **Save the critique** to `posts/drafts/{slug}_critique.md` after running the coaching check
3. **Run the coaching check** and give feedback on these four areas before touching the final post:

### Coaching questions to answer per draft

**Hook: is there a failure or surprise angle?**
- What could go wrong if you used the wrong approach?
- Is the draft starting from the solution, or from the problem?
- If no hook is present, name the failure scenario the solution is protecting against.

**Logic: is the explanation precise?**
- Does the logic section explain WHY each step exists, or just what it does?
- Flag any SQL issues in the draft (e.g. ORDER BY inside CTE with no LIMIT, ambiguous column aliases, wrong function for the task).

**Insight: does it answer "so what"?**
- Is the insight describing the solution, or the consequence of getting it wrong?
- Can the insight be grounded in a real business scenario (platform, leaderboard, report)?

**Takeaway: is it a lesson or a topic heading?**
- "Must know X" is a topic. A takeaway names the specific rule or decision.
- Push toward: "When [condition], use [X] because [consequence of not doing so]."

### Format for coaching feedback
Return feedback in this order:
1. One-line summary of what's strong in the draft
2. Numbered list of coaching notes (one per weakness)
3. Confirm: "Ready to write the final post?" before proceeding

## Adding a New Post

1. Create `posts/YYYY-MM-DD_{slug}.md` using the format above
2. Create `posts/linkedin/YYYY-MM-DD_{slug}.txt` — LinkedIn-copyable plain text version (no markdown syntax; use `→` bullets, `•` for lists, numbered for takeaways, `─────` dividers, emojis and hashtags preserved). **Omit the `🔗` link line** — LinkedIn penalizes external links in the post body. Post the link as the first comment when publishing.
3. If a carousel PDF exists, generate with Python/matplotlib and save to `posts/media/pdfs/YYYY-MM-DD_{slug}.pdf`
4. Append a new row to `posts/index.md` and assign the next sequential number — index is **chronological** (oldest = #1, newest = last)
   - **Posted date**: decode from LinkedIn URN with `urn >> 22` to get Unix ms timestamp (`datetime.fromtimestamp((urn >> 22) / 1000, tz=timezone.utc)`)
   - PDF link: `[📄](media/pdfs/{filename}.pdf)` or `—`

## Carousel PDF Generation

All new carousels are generated with Python/matplotlib. Reusable scripts are saved to `/tmp/gen_{slug}.py`.

### Font setup (MUST come before any `plt` call)

Brand fonts live in the repo at `posts/media/brand-guidelines/fonts/`. Register them every session:

```python
import matplotlib.font_manager as fm, os

FONT_DIR = (r"C:\Users\nramadha\OneDrive - The Dairy Farm Company Ltd"
            r"\new_code\sql_practise\posts\media\brand-guidelines\fonts")
for _fn in ["BigShouldersDisplay-Bold.ttf", "InstrumentSans-Regular.ttf",
            "InstrumentSans-Bold.ttf", "NothingYouCouldDo-Regular.ttf",
            "JetBrainsMono-Regular.ttf"]:
    fp = os.path.join(FONT_DIR, _fn)
    if os.path.exists(fp):
        fm.fontManager.addfont(fp)

FD = "Big Shoulders Display"   # Display headlines
FB = "Instrument Sans"         # Body / subheading
FS = "Nothing You Could Do"    # Script accent
FC = "JetBrains Mono"          # Code blocks
```

### Canvas setup (critical — do NOT use `plt.subplots()`)

```python
W, H = 10.8, 10.8

def new_slide():
    fig = plt.figure(figsize=(W, H))
    fig.patch.set_facecolor(GND)
    ax = fig.add_axes([0, 0, 1, 1])   # fills 100% of figure — NO margins
    ax.set_facecolor(GND)
    ax.set_xlim(0, W); ax.set_ylim(0, H)
    ax.axis("off")
    return fig, ax

def save(pdf, fig):
    pdf.savefig(fig, facecolor=GND)   # NO bbox_inches — preserves exact canvas
    plt.close(fig)
```

Common mistakes that break layout:
- Using `plt.subplots()` or `plt.subplot()` — adds internal margins
- Using `bbox_inches="tight"` — crops canvas to content, destroys all proportions
- Running the script from git bash — causes fatal errors on this machine

### Running carousel scripts

Always run via PowerShell, never git bash:
```
powershell -Command "python 'C:\tmp\gen_{slug}.py'"
```

### Reference layout

Match `posts/media/pdfs/2026-05-04_top_cool_votes.pdf` for all design decisions:
- Section headers: Impact (Big Shoulders Display) fs=88, crimson, va="top" — **no** vertical bar on content slides
- Cover: title centered (ha="center", x=W/2), thin left crimson bar at x≈0.742
- Author pill: CENTERED at bottom (`px = (W - pw) / 2`)
- Script CTA "follow for daily SQL": CENTERED on slide 6
- Code block: FancyBboxPatch rounded corners, CODE_LH=0.50, calibrate char width with renderer probe. Reduce CODE_LH to ~0.41 and fs to 11 on dense code slides to keep the block above the bottom rule.
- Slide 5 header: two-line Impact stack in ACC and AUTH

### Clickable links in the PDF

The problem URL must appear as a **clickable annotation** in the PDF (on the cover and problem slides). Use `.set_url()` on the text object — matplotlib's PDF backend embeds a standard `/URI` action:

```python
t = ax.text(x, fy(y), "platform.stratascratch.com/coding/{id}",
            ha="center", va="top", fontsize=9, fontfamily=FC, color=MUTE)
t.set_url("https://platform.stratascratch.com/coding/{full-slug}?code_type=1")
```

This works even with `matplotlib.use("Agg")` because `PdfPages` writes via `backend_pdf` directly.

### Email CTA

Slide 6 and slide 7 of every carousel end with a two-line closing block (script font + mono font):

- Line 1 (script, crimson): `follow for more SQL problems`
- Line 2 (mono, muted): `questions? nivanrs@gmail.com`

The email text must also be clickable. Use `.set_url("mailto:nivanrs@gmail.com")` on the text object — PDF readers open the mail client on click:

```python
_email = ax.text(...)
_email.set_url("mailto:nivanrs@gmail.com")
```

Wording is fixed — do not vary it. "questions?" is intentional: it implies the reader had a reaction, and the email address lands last as the emphatic word (Strunk rule 18).

### Color constants
```python
GND  = "#FBF3E4"   # Ground — warm cream background
AUTH = "#161616"   # Authority — near-black
ACC  = "#B91646"   # Accent — crimson
CODE = "#F2E8D5"   # Code block background — slightly darker cream
```

## Key Facts

- 34 posts total (all indexed in `posts/index.md`)
- Post #11 (`person_with_most_oscars`) file is dated `2026-03-23` but index still shows `—` for posted date (URN unknown)
- `2026-03-30_facebook_accounts.md` — current file for post #1 (Facebook Accounts); carousel PDF at `posts/media/pdfs/2026-03-30_facebook_accounts.pdf`
- **Legacy PDFs** (pre-2026-03-30, dark/cyan Canva style) are deprecated — do not replicate that aesthetic
- `.playwright-mcp/` is gitignored — created when scraping LinkedIn via Playwright MCP
- **Standard email CTA**: slides 6 and 7 of every carousel close with `follow for more SQL problems` (script, crimson) + `questions? nivanrs@gmail.com` (mono, muted) — wording is fixed

## Package Manager & Runtime

- **Always use `bun`** instead of `npm`.
- **Always use `bunx`** instead of `npx`.
- This applies to all terminal commands, installation steps, and script executions in this repository.
