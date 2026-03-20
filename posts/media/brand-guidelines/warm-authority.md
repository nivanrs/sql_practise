# Warm Authority

A design philosophy built on productive tension — the warmth of invitation pressed against the force of expertise. Cream holds everything. Crimson commands. Black declares. Neither apologises.

## Philosophy

Space is the first statement. Before any mark is made, the ground speaks: a warm, slightly yellowed cream that neither shouts nor whispers but simply *exists* with confidence. It is the light of a well-worn library, a page that has been touched before. Into this warmth, elements are placed with the deliberate economy of a surgeon — only what is essential, placed only where it must be.

Typography operates at two extremes, never in the middle. At the top of the hierarchy: condensed display type so bold and compressed it occupies the canvas like architecture — columns of compressed authority, all-caps, carrying weight through sheer physical presence. At the opposite end: quiet, regular-weight humanist sans-serif for prose. Between these poles, a single script accent in crimson introduces the human hand — a signature, an invitation, a reminder that a person lives behind the system. These three voices never interrupt each other; they take measured turns.

Colour is a three-note chord. The warm cream ground never competes. Near-black (#161616) speaks with absolute clarity for structural text, headlines, and system marks. Crimson (#B91646) is reserved — it appears only at moments of genuine importance: section titles, the script accent, the emotional punctuation of the page. When crimson fires, it is never decorative; it is directional. The palette achieves its richness not through variety but through restraint meticulously executed.

Recurring motifs are the grammar of the system. Three filled circles, top-right, identify position in a sequence — small, perfect, unhurried. A horizontal arrow, thin and precise, points navigation forward. A pill-shaped badge, cream-filled with a clean black stroke, frames the author's name as if stamped by hand. Horizontal rules divide sections with the authority of chapter breaks. Each motif appears in exactly one weight, one size, one place — never improvised, always placed with the care of someone who has spent countless hours arriving at this single arrangement.

The philosophy demands that technical information wear the same aesthetic as emotion. A block of code deserves the same compositional attention as a script-lettered phrase. A bullet-point breakdown of logic should breathe as freely as a closing call-to-action. This insistence on visual parity between the analytical and the human is where the philosophy achieves its deepest expression — and where only painstaking, master-level craft can hold both in balance without one overwhelming the other.

## Visual Properties

- **Ground**: Warm cream `#FBF3E4` — breathing room, never dead white
- **Authority**: Near-black `#161616` — condensed display, all-caps, monumental scale
- **Accent**: Crimson `#B91646` — section titles, script, emotional markers only
- **Display**: Ultra-condensed bold sans (Big Shoulders Bold) — all-caps; carousel scale 64–80pt
- **Subheading**: Humanist sans (Instrument Sans Bold) — labels and sub-level headings only; never used for prose
- **Body**: Humanist sans (Instrument Sans Regular) — reading weight, never bold for prose; carousel scale 11–14pt
- **Script**: Handwritten script (Nothing You Could Do) — crimson only, single moments; carousel scale 28–36pt
- **Code**: Monospace (JetBrains Mono) — reduced weight, muted tone; carousel scale 10–12pt
- **Motifs** — five exact marks, never improvised, never resized:
  - **Three filled dots** — top-right, carousel position indicator
  - **Right-pointing arrow** — bottom-right navigation
  - **Pill badge** — cream fill + black stroke, frames author name
  - **Horizontal rules** — section dividers, page top/bottom borders
  - **Crimson vertical bar** — left-aligned, precedes every section heading; consistent weight and height across all sections
- **Rhythm**: Generous vertical breathing room; horizontal margins held constant; text never crowds

## Font Files

All brand fonts are stored in the repo at `posts/media/brand-guidelines/fonts/`.

| Role | matplotlib name | File |
|------|----------------|------|
| Display (headlines) | `Big Shoulders Display` | `BigShouldersDisplay-Bold.ttf` |
| Body | `Instrument Sans` | `InstrumentSans-Regular.ttf`, `InstrumentSans-Bold.ttf` |
| Script | `Nothing You Could Do` | `NothingYouCouldDo-Regular.ttf` |
| Code | `JetBrains Mono` | `JetBrainsMono-Regular.ttf` |

These fonts must be registered with `fm.fontManager.addfont()` at the start of every carousel script before any `plt` call. See `CLAUDE.md` → "Carousel PDF Generation" for the full setup block.
