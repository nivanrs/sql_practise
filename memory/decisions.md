# Decisions

## 2026-03-30: Switched from Canva to Python/matplotlib for carousels

**Decision:** All new carousel PDFs are generated with Python/matplotlib using the Warm Authority brand. Canva (dark/cyan style) is deprecated and must not be replicated.

**Why:** Canva carousels lacked design consistency and couldn't be version-controlled or scripted. Python gives full control over layout, fonts, and brand compliance. Warm Authority was introduced as a coherent brand identity.

**How to apply:** Post #27 (2026-03-30_facebook_accounts) is the first Warm Authority PDF. All new posts use this system. Reference layout is `posts/media/pdfs/2026-05-04_top_cool_votes.pdf`.

---

## 2026-03-30: Warm Authority as the single brand identity

**Decision:** One design system for all carousels: Warm Authority. Palette is GND `#FBF3E4`, AUTH `#161616`, ACC `#B91646`. Fonts are Big Shoulders Display (display), Instrument Sans (body/subheading), Nothing You Could Do (script), JetBrains Mono (code).

**Why:** Consistency across posts builds visual recognition on LinkedIn. A single system also makes scripting faster — no per-post design decisions.

**How to apply:** Never deviate from the palette or motif set (three dots, right arrow, pill badge, horizontal rules, crimson vertical bar). Crimson is directional, not decorative.

---

## ongoing: No external links in LinkedIn post body

**Decision:** Omit the `🔗` problem URL from `.txt` files. Post it manually as the first comment after publishing.

**Why:** LinkedIn's algorithm suppresses reach on posts containing external links in the body. The link lives in the `.md` file and as a clickable annotation in the PDF carousel.

**How to apply:** Every `.txt` file starts directly with the hook. Remind user to post the link as first comment.

---

## ongoing: StrataScratch URLs must use `?code_type=1`

**Decision:** Always append `?code_type=1` to StrataScratch problem links.

**Why:** Without it, the link opens the Python editor. `code_type=1` forces the SQL view, which is what the post is about.

---

## ongoing: Posted date decoded from LinkedIn URN

**Decision:** When the exact post date is needed, decode it from the LinkedIn URN: `datetime.fromtimestamp((urn >> 22) / 1000, tz=timezone.utc)`.

**Why:** LinkedIn's UI doesn't expose exact timestamps. The URN encodes milliseconds since epoch in the upper bits.

---

## ongoing: Email CTA wording is fixed

**Decision:** Slides 6 and 7 of every carousel end with exactly: `follow for more SQL problems` (script, crimson) and `questions? nivanrs@gmail.com` (mono, muted, clickable mailto link).

**Why:** "questions?" implies the reader had a reaction. The email address lands last as the emphatic word (Strunk rule 18). Wording is not varied between posts to build recognition.

---

## ~2026-04: Hook sentence precedes the post title in `.txt` files

**Decision:** Every `.txt` file opens with a one-line hook sentence *before* the `💻 SQL of the Day:` title. Example: "My SQL query returned the correct result… but it was still wrong."

**Why:** LinkedIn truncates posts to roughly 2–3 lines before a "see more" button. The hook is the only content the reader sees without clicking. If it doesn't grab them, they scroll. Adopted around April 2026 (income_by_title_and_gender is the first observed instance). Earlier posts (facebook_accounts, March 2026) did not have this — they started with the title directly. The hook is now standing practice.

**How to apply:** Write the hook first when generating a `.txt` file. It is a single compressed sentence that names the failure scenario or the surprise. It is the hardest sentence in the post to write. Treat it as such.

---

## ongoing: Coaching critique is written in the draft's language

**Decision:** When a draft is in Indonesian, write the coaching critique in Indonesian.

**Why:** Feedback delivered in the thinker's own language reduces the translation step between "I understand the feedback" and "I can apply the feedback." The improvement happens in the writer's native register. This is a craft decision, not a concession to informality. Observed: `reviews_of_categories_critique.md` was written in Indonesian because the draft was in Indonesian.

**How to apply:** If the draft is in Indonesian, write coaching notes in Indonesian. The final `.md` and `.txt` are always in English regardless.

---

## ongoing: `::float` is the preferred cast syntax for ratio queries

**Decision:** Use PostgreSQL-idiomatic `::float` (not `CAST(x AS FLOAT)`) when casting integer numerators for division.

**Why:** Briefer. Idiomatic to PostgreSQL. Consistent across all ratio posts in this series. Without it, integer division in PostgreSQL silently rounds: `3 / 10 = 0`, not `0.3`. This is a silent error — same class as LIMIT 1 dropping ties.

---

## standing: readme.md is outdated — do not cite it

**Decision:** Do not use `readme.md` as a source of truth for project state or structure.

**Why:** It contains at least three factual errors: says "reverse-chronological" (index is chronological), says "26 posts" (36 as of this session), says "6 slides" per carousel (7). CLAUDE.md is the authoritative reference for all workflow and structural decisions.
