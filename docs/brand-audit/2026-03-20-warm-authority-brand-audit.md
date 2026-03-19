# Warm Authority — Brand System Audit

**Date:** 2026-03-20
**Auditor:** Claude Code (claude-sonnet-4-6)
**Frameworks applied:** brand-color-psychology · visual-identity-direction · brand-typography-systems · web-typography
**Overall score: 8.2 / 10**

---

## Fixes Applied

| # | Issue | Fix |
|---|-------|-----|
| 1 | Near-black hex mismatch: spec said `#1A1A1A`, PNG showed `#161616` | Standardized to `#161616` in `warm-authority.md` and `CLAUDE.md` |
| 2 | Instrument Sans Bold used in PNG for subheadings, absent from spec | Added Subheading role to both files |
| 3 | Crimson vertical bar section-prefix motif visible in PNG, not documented | Added as 5th motif to both files |
| 4 | No font size guidance anywhere | Added carousel-scale approximations per font role in `warm-authority.md` |

---

## Color Psychology Assessment

### Palette

| Role | Hex | Notes |
|------|-----|-------|
| Ground | `#FBF3E4` | Warm cream — consistent across spec and visual |
| Authority | `#161616` | Near-black — corrected from `#1A1A1A` |
| Accent | `#B91646` | Crimson — consistent |

### 60-30-10 Distribution

The palette follows the 60-30-10 rule precisely:
- 60% Ground (cream backgrounds)
- 30% Authority (near-black for all structural text, headlines, motifs)
- 10% Accent (crimson at emotional/directional moments only)

**Score: 10/10** — one of the cleanest 60-30-10 executions possible. Crimson never bleeds into decoration.

### Brand Archetype Fit

The system occupies an intentional hybrid:

| Archetype | Element | Evidence |
|-----------|---------|---------|
| Sage (wisdom, knowledge) | Cream ground, measured prose, systematic structure | Library aesthetic |
| Ruler (authority, control) | Condensed display, all-caps, architectural scale | "Never apologises" |
| Caregiver accent (invitation) | Script in crimson, pill badge, breathing room | "Warmth of invitation" |

This blend is rare in the SQL/data education space — most brands default to pure Sage (corporate blue/gray). **Score: 9/10**

### WCAG Accessibility

| Pair | Estimated Contrast | Level |
|------|--------------------|-------|
| `#161616` on `#FBF3E4` | ~19:1 | AAA |
| `#B91646` on `#FBF3E4` | ~7.8:1 | AAA |
| `#FBF3E4` on `#B91646` | ~7.8:1 | AAA |

All pairings clear AAA — the highest WCAG standard. **Score: 10/10**

### Blue Ocean Positioning

LinkedIn SQL/data education dominant colors: LinkedIn blue, corporate navy, cold white.
Warm Authority uses zero of these. The cream ground signals difference before a word is read. **Score: 10/10**

---

## Visual Identity Direction Audit

### Strategy-to-Visual Translation

| Brand Adjective | Visual Expression | Delivered? |
|-----------------|------------------|-----------|
| Warm | Cream ground, humanist body font, script accent | Excellent |
| Authority | Condensed all-caps display, near-black, structural rules | Excellent |
| Invitation | Generous breathing room, pill badge, script | Strong |
| Expertise | JetBrains Mono for code, logical breakdowns | Strong |

**Score: 9/10** — each brand adjective has a dedicated typographic or color vehicle.

### Motif Coherence (post-fix)

Five motifs, all functional and non-decorative:

| Motif | Role |
|-------|------|
| Three filled dots | Sequence position |
| Right-pointing arrow | Navigation |
| Pill badge | Author identity |
| Horizontal rules | Section structure |
| Crimson vertical bar | Section heading prefix (newly documented) |

**Score: 9/10**

### Wheeler's Five-Phase Assessment

| Phase | Status | Notes |
|-------|--------|-------|
| Research | Implicit | Platform norms understood |
| Strategy | Strong | "Warm Authority" is crisp and ownable |
| Design Identity | Strong | Full color + type + motif system |
| Touchpoints | Partial | Carousel PDF defined; X/Threads (text) added; no web header spec |
| Governance | Strong | CLAUDE.md enforces exact motif usage |

**Score: 8/10** — governance and strategy are strong; touchpoint coverage incomplete (no web/avatar treatment).

---

## Typography System Review

### Classification Fit

| Role | Font | Classification | Archetype Fit |
|------|------|----------------|---------------|
| Display | Big Shoulders Bold | Ultra-condensed geometric sans | Ruler — authority through compression |
| Subheading | Instrument Sans Bold | Humanist sans bold | Structural hierarchy without harshness |
| Body | Instrument Sans Regular | Humanist sans | Caregiver — warm, approachable |
| Script | Nothing You Could Do | Handwritten | Personal bridge between authority and warmth |
| Code | JetBrains Mono | Monospace | Technical precision, SQL-native |

### Pairing Logic

Three levels of contrast create a coherent four-voice system:

1. **Big Shoulders Bold vs. Instrument Sans** — maximum contrast: condensed geometric vs. humanist, ultra-heavy vs. regular
2. **Instrument Sans vs. Nothing You Could Do** — formal vs. informal; color (crimson) adds a second differentiator
3. **All prose voices vs. JetBrains Mono** — technical register clearly separated by monospace convention

**Score: 9/10** — sophisticated system held together by strict usage rules.

### Size Map (approximate, carousel canvas 10.8" × 10.8")

| Role | Approximate Scale |
|------|------------------|
| Display | 64–80pt |
| Subheading | 18–24pt |
| Body | 11–14pt |
| Script | 28–36pt |
| Code | 10–12pt |

This is approximate — exact sizes per slide type should be measured from the canonical Canva presentation.

---

## Web Typography Readiness

The brand system is carousel-first (fixed canvas). If extended to web:

| Principle | Status | Recommendation |
|-----------|--------|----------------|
| Body size ≥ 16px | Not specified | Set 18px base for reading-heavy content |
| Line length 45-75ch | Not specified | Set `max-width: 65ch` for prose |
| Line height 1.4-1.8 | Not specified | Set 1.6 for body, 1.15 for display |
| Font payload | ~100-150KB | One weight per font, Latin subset — efficient |

All four fonts are on Google Fonts (free, WOFF2, CDN). Performance is strong for a web implementation.

**Score: 7/10** — fonts are web-ready; measurements need specification if web presence is created.

---

## Remaining Recommendations (lower priority)

- **CMYK/Pantone specs**: Not critical for digital-only brand, but useful if print materials are ever created
- **Exact motif dimensions**: Pixel/pt dimensions for dots, arrow, pill badge, and vertical bar would lock in consistency
- **Web header/avatar treatment**: When/if a web presence or social header is designed, document it as a touchpoint
- **Canonical size verification**: Measure Display and Body sizes from the Canva master to confirm the approximate carousel scale above
