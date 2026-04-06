# Design System: SQL of the Day — Warm Authority

**Brand Source:** `posts/media/brand-guidelines/warm-authority.md`
**Visual Reference:** `posts/media/brand-guidelines/brand-guidelines.png`
**Carousel Reference:** `posts/media/pdfs/2026-06-01_highest_target_under_manager.pdf`

---

## 1. Visual Theme & Atmosphere

**Warm Authority.** The productive tension between invitation and expertise — two forces that should cancel each other out, but instead hold each other in check.

The canvas is a warm, slightly yellowed cream — neither clinical white nor heavy paper. It reads as a well-worn library surface: a place where serious things happen, but where you are welcome. Into this warmth, elements arrive with surgical economy. Nothing is placed without reason. Nothing decorates without directing.

The mood is: **Dense with air**. Information is present and precise, but vertical breathing room is treated as a structural element in its own right — not padding, not margin, but space that speaks. The aesthetic is simultaneously monumental and quiet: massive display type sharing a slide with delicate body text, a single crimson stroke doing the work of an entire color system.

This is the voice of someone who has spent years with this material and no longer needs to prove it.

---

## 2. Color Palette & Roles

| Name | Hex | Role |
|------|-----|------|
| **Warm Cream Ground** | `#FBF3E4` | The canvas itself. Every slide, every background. Never swapped for white — the warmth is structural, not decorative. |
| **Authority Near-Black** | `#161616` | All primary text, display headlines, structural marks, horizontal rules. Not pure black — the near-black reads as deliberate restraint. |
| **Crimson Accent** | `#B91646` | Section titles, crimson vertical bar motif, script accent lines, emotional punctuation. Never decorative — fires only at moments of genuine importance. |
| **Code Block Cream** | `#F2E8D5` | Rounded code block background — slightly darker than the ground to lift the block without harsh contrast. |
| **Muted Warm Gray** | `#6B5E4E` | Secondary text, URL annotations, email CTA line. Sits visibly on the cream ground without competing with Authority black. |

**Color principle:** The richness of this palette comes from restraint, not variety. Three primaries — Ground, Authority, Accent — do all structural work. Muted and Code are support roles only.

---

## 3. Typography Rules

### Type Hierarchy

| Role | Font | Weight | Case | Scale | When |
|------|------|--------|------|-------|------|
| **Display** | Big Shoulders Display | Bold | ALL-CAPS | 64–88pt (carousel) | Slide titles, problem headers, section labels |
| **Subheading** | Instrument Sans | Bold | Title Case | 14–18pt | Labels, sub-level headings only — never for prose |
| **Body** | Instrument Sans | Regular | Sentence case | 11–14pt | Explanations, bullet breakdowns, logic text |
| **Script Accent** | Nothing You Could Do | Regular | Lowercase | 28–36pt | Crimson CTA lines — one moment per slide maximum |
| **Code** | JetBrains Mono | Regular | as-is | 10–12pt | SQL code blocks, technical values, URLs |

### Typography Rules (non-negotiable)

- **Two extremes only** — monumental display OR quiet body. Nothing in between. A mid-weight, mid-size heading is a violation of the system.
- **Script is crimson only** — Nothing You Could Do never appears in black or muted tone. If the moment doesn't warrant crimson, the script doesn't appear.
- **Body prose is never bold** — Instrument Sans Bold is reserved for labels and subheadings. Running prose in bold reads as shouting.
- **Code gets the same compositional care as emotion** — a code block must breathe as freely as a script CTA.
- **Letter-spacing:** Display type runs tight (the condensed form handles density). Body and code run at default tracking. Script runs at default — no artificial stretching.

---

## 4. Component Stylings

### Carousel Slides

- **Canvas:** 10.8 × 10.8 inches, square. Warm Cream Ground fills 100% — no internal margins at the figure level. All layout is manual coordinate placement on the axes.
- **Top/bottom border rules:** Thin horizontal lines in Authority near-black, consistent weight across all slides.
- **Section heading block:** Crimson vertical bar (left-aligned, fixed weight and height) immediately preceding the section label in Display type at Crimson.
- **Cover slide exception:** Title centered (no vertical bar) — the display headline occupies the canvas like architecture.

### Code Blocks

- **Container:** `FancyBboxPatch` with gently rounded corners (not pill-shaped, not sharp). Code Block Cream fill (`#F2E8D5`).
- **Interior padding:** Generous — code never crowds the edge of the block.
- **Font:** JetBrains Mono Regular, muted tone.
- **Line height:** `CODE_LH = 0.50` for standard density; reduce to `~0.41` on dense slides to keep the block above the bottom rule.
- **Shadow:** None — flat elevation. The slight cream contrast does all the lifting.

### Author Pill (Badge)

- **Shape:** Pill-shaped — `border-radius: 50px` equivalent. Fully rounded ends.
- **Fill:** Warm Cream Ground (`#FBF3E4`).
- **Stroke:** Authority near-black (`#161616`), thin and clean — stamped-by-hand feel.
- **Content:** Full name — `Nivan Ramadhan Sugiantoro` — in Instrument Sans Regular, Authority color.
- **Position:** Centered horizontally at the bottom of the slide. Never left-aligned, never right-aligned.

### Navigation Motifs

| Motif | Description | Position | Size |
|-------|-------------|----------|------|
| Three filled dots | Carousel position indicator — three perfect circles, filled Authority near-black | Top-right | Small, equal size, consistent spacing |
| Right-pointing arrow | Navigation forward — thin, precise, geometric | Bottom-right | Single arrow, one weight only |
| Horizontal rules | Section dividers and page borders | Top and bottom of slide + between sections | Consistent stroke weight |
| Crimson vertical bar | Precedes every section heading on content slides | Left-aligned, flush against section label | Fixed height — never taller, never shorter |

### Email / CTA Block (Slides 6–7)

```
Line 1: follow for more SQL problems    [Script, Crimson, centered]
Line 2: questions? nivanrs@gmail.com    [JetBrains Mono, Muted, centered, mailto: linked]
```

Wording is fixed — do not vary. "questions?" is a deliberate lowercase opening; it implies the reader reacted. The email address lands last as the emphatic word (Strunk: end with the word that deserves emphasis).

---

## 5. Layout Principles

### Space as Structure

Vertical breathing room is not padding — it is a compositional element. Slides never feel crowded. When content is dense (e.g., a long SQL block), reduce font size and line-height before reducing whitespace.

### Horizontal Margins

Constant across all slides. Text and elements never drift edge-to-edge. The consistent horizontal inset creates the sense of a centered, formal document.

### Vertical Rhythm

```
Top border rule
↓  [breathing room]
Display headline (or cover title)
↓  [section gap]
Crimson bar + Section label
↓  [content gap]
Body text / code block / bullet list
↓  [breathing room]
Bottom border rule
↓  [author pill or navigation arrow]
```

### Visual Weight Hierarchy

1. **Display headline** — occupies space physically, like a column or a wall
2. **Crimson accent** — fires once per slide, directs the eye
3. **Body / code** — quiet, reads left-to-right, never competes with display
4. **Motifs** (dots, arrow, pill) — structural grammar, recede into the system

### Alignment Rules

| Element | Alignment |
|---------|-----------|
| Cover title | Centered (`ha="center"`, `x = W/2`) |
| Section headings (content slides) | Left-aligned with consistent left margin |
| Author pill | Centered (`px = (W - pill_width) / 2`) |
| Script CTA | Centered |
| Navigation arrow | Bottom-right, fixed position |
| Position dots | Top-right, fixed position |
| Code block | Left-aligned within consistent horizontal margins |

### Crimson Is Directional, Not Decorative

Every time crimson appears, it is answering one question: *where should the reader look next?* Section labels direct the reading order. The script CTA signals the emotional close. The vertical bar marks entry into a new idea. If crimson is firing on an element that does not direct the reader, it has been misapplied.
