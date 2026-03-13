
# Facebook Accounts — Carousel Design Philosophy

**Warm Authority · SQL of the Day · 30 Mar 2026**

---

## Intent

This carousel reduces a ratio problem to its essential geometry: one number divided by another, with the cast that makes the division honest. The design mirrors that clarity — nothing extraneous, every element earning its space.

## Slide-by-Slide Rationale

**Slide 1 — Cover**
The title stack (`SQL / OF THE / DAY`) in Big Shoulders Bold establishes architectural scale before content begins. Script treatment of "facebook accounts" in crimson signals the subject without competing with the structural type. The author pill sits quiet at the bottom — authority without announcement.

**Slide 2 — The Problem**
The problem statement is short enough to breathe. A hint table (`fb_account_status` columns: `status_date`, `status`) grounds the reader in the schema before they see the solution. The script "think about it..." invites a pause — this is pedagogy, not a quiz.

**Slide 3 — The Solution**
The SQL block uses the brand's code treatment: JetBrains Mono on a tinted cream field (`#F2E8D5`), keywords in crimson, all other tokens in near-black. The cast `::float` is the punchline of the pattern; crimson draws attention to it without a separate callout.

**Slide 4 — How It Works**
Four entries, each with a crimson Big Shoulders label and an Instrument Sans explanation. Vertical rhythm is strict: equal spacing between items. No decorative bullets — the label color does the separation work.

**Slide 5 — This Pattern Tells You**
Two-line header splits the declaration across crimson and black. The three business insights are tight prose, not fragmented bullets. The reader should finish this slide knowing *why the query matters*, not just what it does.

**Slide 6 — Key Takeaways**
Crimson numbering (1–4) acts as both list marker and visual anchor. The hashtag line sits in reduced Instrument Sans — present but not competing. The script "follow for daily SQL" is the only moment of direct address in the carousel; it earns that register by appearing only once.

## Color Discipline

Crimson fires in exactly six roles across all six slides:
1. Section headers (`THE PROBLEM`, `THE SOLUTION`, etc.)
2. SQL keywords (`SELECT`, `FROM`, `WHERE`, `COUNT`, `CASE`, `WHEN`, `THEN`, `END`, `AS`)
3. The `::float` cast token (solution slide)
4. Script treatments (cover subtitle, problem hint, closing CTA)
5. How-It-Works item labels
6. Key-takeaway numbers

Nowhere else. Every use is directional, not decorative.

## Typography Hierarchy

Three levels, no intermediate states:
- **Monumental** — Big Shoulders Bold, 130pt on cover, 68–72pt for section headers
- **Quiet body** — Instrument Sans Regular, 12–14pt for all explanatory text
- **Code** — JetBrains Mono, 12–13pt, muted weight on tinted field

## Spacing System

Content occupies `y = 0.14` to `y = 0.82` (normalized units on 1080×1080px canvas). Horizontal margins hold at `x = 0.08` to `x = 0.92`. Top and bottom horizontal rules sit at `y = 0.920` and `y = 0.082` respectively — same on every slide, the only constant that unifies the sequence.
