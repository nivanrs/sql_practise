# Boilerplate Setup Guide

A reusable scaffold for LinkedIn content series archives. Based on the "SQL of the Day" repo structure.

## What this is

This boilerplate gives you:
- Standardized post format (`.md` + `.txt`)
- Draft coaching workflow with 4-dimension feedback
- Brand guidelines template (Warm Authority style)
- Carousel PDF generation setup (Python + matplotlib)
- AI agent instructions (`CLAUDE.md` + `AGENTS.md`)
- Chronological post index

## Quick start

1. **Copy this folder** to a new directory and `git init`
2. **Find and replace all placeholders** (see table below) — search for `{{` to find every occurrence
3. **Install skills** (see "Installing Skills" below)
4. **Delete the `examples/` folder** once you understand the format
5. **Add your first post** following `post_template.md`
6. **Update `posts/index.md`** with your first entry

## How to use this repo

Once set up, every post follows the same five-step sequence. The AI agent (Claude Code with `CLAUDE.md` loaded) handles each step when you run it inside the repo directory.

### Step 0: Write a rough draft

Write your draft in any language, any format — notes, bullet points, pseudocode, mixed languages. Don't polish it. Just capture the problem, your solution, and a rough idea of the insight.

Drop it into Claude Code: *"Here's my draft for [topic]. Save it and give me coaching feedback."*

The agent will:
1. Save the raw draft verbatim to `posts/drafts/{slug}_raw.md`
2. Run the 4-dimension coaching check (Hook / Logic / Insight / Takeaway)
3. Return numbered feedback and ask for confirmation before writing the final post

### Step 1: Write the markdown post

After you confirm, the agent writes the full post to `posts/YYYY-MM-DD_{slug}.md` using the structure in `post_template.md`.

You can also do this yourself: copy `post_template.md`, fill in each section, and save it with today's date as the filename prefix.

### Step 2: Write the LinkedIn plain text

The agent creates `posts/linkedin/YYYY-MM-DD_{slug}.txt` — the same content stripped of markdown syntax, formatted for direct copy-paste into LinkedIn.

If doing it manually: no `#` headers, no `**bold**`, no backtick code fences. Use `→` for bullets, `─────` for dividers, and bold Unicode (`𝗦𝗼𝗹𝘂𝘁𝗶𝗼𝗻`) for section headers.

### Step 3: Generate the carousel PDF (optional)

Ask the agent: *"Generate the carousel PDF for [slug]."*

It writes a Python + matplotlib script to `/tmp/gen_{slug}.py`, runs it, and saves the output to `posts/media/pdfs/YYYY-MM-DD_{slug}.pdf`. The script uses your brand colors and fonts from `AGENTS.md`.

Skip this step if you don't need a carousel for a given post.

### Step 4: Update the index

The agent appends a new row to `posts/index.md`. You need to supply the LinkedIn URN once the post is live — paste it in and the agent decodes the posted timestamp automatically.

If you don't have the URN yet, leave the posted date as `—` and update it later.

---

### Typical prompt sequence

```
1. "Here's my draft: [paste draft]. Save it and coach me."
   → Agent saves raw draft, returns coaching feedback

2. "Looks good, write the final post."
   → Agent writes .md and .txt files

3. "Generate the carousel PDF."
   → Agent generates PDF

4. "Update the index. URN is [paste URN]."
   → Agent appends index row with decoded date
```

---

## Placeholder reference

| Placeholder | Example Value | Description |
|---|---|---|
| `{{SERIES_TITLE}}` | `Python Tip of the Day` | Full series name |
| `{{SERIES_HASHTAG}}` | `#PythonTipOfTheDay` | Primary hashtag |
| `{{HEADER_EMOJI}}` | `🐍` | Emoji used in post header |
| `{{TOPIC_DOMAIN}}` | `Python` | Subject area (one word or short phrase) |
| `{{CONTENT_SOURCES}}` | `LeetCode and HackerRank` | Where problems/topics come from |
| `{{LINKEDIN_PROFILE_URL}}` | `https://linkedin.com/in/you` | Your LinkedIn profile URL |
| `{{AUTHOR_NAME}}` | `Jane Doe` | Your full name |
| `{{CODE_LANGUAGE}}` | `python` | Language for fenced code blocks |
| `{{SECTION_1_EMOJI}}` | `🧠` | Emoji for solution section |
| `{{SECTION_1_TITLE}}` | `Solution` | Title for solution section |
| `{{SECTION_2_EMOJI}}` | `🧩` | Emoji for logic breakdown section |
| `{{SECTION_2_TITLE}}` | `Simple logic breakdown` | Title for logic breakdown section |
| `{{SECTION_3_EMOJI}}` | `📊` | Emoji for insight section |
| `{{SECTION_3_TITLE}}` | `This pattern tells you:` | Title for insight section |
| `{{SECTION_4_EMOJI}}` | `🎯` | Emoji for takeaways section |
| `{{SECTION_4_TITLE}}` | `Key takeaways` | Title for takeaways section |
| `{{BRAND_NAME}}` | `Warm Authority` | Your design system name |
| `{{COLOR_GROUND_HEX}}` | `#FBF3E4` | Background color hex |
| `{{COLOR_GROUND_NAME}}` | `warm cream` | Background color description |
| `{{COLOR_PRIMARY_HEX}}` | `#161616` | Primary text color hex |
| `{{COLOR_ACCENT_HEX}}` | `#B91646` | Accent color hex |
| `{{COLOR_ACCENT_NAME}}` | `crimson` | Accent color description |
| `{{FONT_DISPLAY}}` | `Big Shoulders Bold` | Display/headline font |
| `{{FONT_BODY}}` | `Instrument Sans Regular` | Body text font |
| `{{FONT_CODE}}` | `JetBrains Mono` | Code font |
| `{{FONT_SCRIPT}}` | `Nothing You Could Do` | Script/handwritten font |
| `{{WRITING_RULES}}` | `No dashes or em dashes in prose...` | Writing style rules |
| `{{PACKAGE_MANAGER}}` | `bun` | Package manager (bun/npm/yarn) |
| `{{PACKAGE_RUNNER}}` | `bunx` | Package runner (bunx/npx) |
| `{{CANVA_DESIGN_URL}}` | Canva edit link | Presentation sample link |
| `{{COACHING_Q1_TITLE}}` | `Hook: is there a failure angle?` | First coaching dimension title |
| `{{COACHING_Q1_BULLETS}}` | Sub-bullets for the hook check | First coaching dimension bullets |
| `{{COACHING_Q2_TITLE}}` | `Logic: is the explanation precise?` | Second coaching dimension title |
| `{{COACHING_Q2_BULLETS}}` | Sub-bullets for the logic check | Second coaching dimension bullets |
| `{{COACHING_Q3_TITLE}}` | `Insight: does it answer "so what"?` | Third coaching dimension title |
| `{{COACHING_Q3_BULLETS}}` | Sub-bullets for the insight check | Third coaching dimension bullets |
| `{{COACHING_Q4_TITLE}}` | `Takeaway: is it a lesson or a topic heading?` | Fourth coaching dimension title |
| `{{COACHING_Q4_BULLETS}}` | Sub-bullets for the takeaway check | Fourth coaching dimension bullets |

## Installing skills

Skills live in `.agents/skills/`. Install each with:

```bash
# Clone the skills repo (or copy individual skill files)
# Then add each skill to .agents/skills/{skill-name}/

# Core skills for any content series:
bun add humanizer                      # Strip AI writing patterns
bun add writing-clearly-and-concisely  # Tighten prose
bun add web-to-markdown                # Scrape source platforms
bun add commit-work                    # Smart git commits
bun add social-content                 # LinkedIn copy and hooks
bun add copy-editing                   # Polish sections (7-sweep framework)
bun add canvas-design                  # Generate carousel PDFs
bun add pdf                            # PDF manipulation
bun add playwright-cli                 # Browser automation
```

Invoke skills via the `Skill` tool (Claude Code) or reference them by name in other AI agents.

## Adapting the coaching workflow

The four coaching dimensions in `CLAUDE.md` are currently filled with SQL-specific questions. Replace `{{COACHING_Q*_TITLE}}` and `{{COACHING_Q*_BULLETS}}` with questions appropriate for your topic:

**Template for each dimension:**
```
**{{COACHING_Q1_TITLE}}**
- {{COACHING_Q1_BULLETS}}
```

Example for a Python tips series:
- Hook: "What breaks if you use the naive approach?"
- Logic: "Does the explanation show why this method is faster, not just that it is?"
- Insight: "Can this be grounded in a real codebase problem?"
- Takeaway: "When [condition], use [X] because [consequence of not doing so]."

## Adapting the brand

Edit `posts/media/brand-guidelines/brand-guidelines.md` and `design-philosophy.md` to match your visual identity:
1. Replace all `{{COLOR_*}}` placeholders with your hex codes
2. Replace all `{{FONT_*}}` placeholders with your chosen fonts
3. Update the "Recurring Motifs" section with your actual design elements
4. Rewrite the philosophy section to match your design voice

The carousel generation script in `AGENTS.md` uses the same hex values — update them there too.
