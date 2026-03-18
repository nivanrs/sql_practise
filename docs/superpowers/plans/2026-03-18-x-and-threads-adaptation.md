# X and Threads Adaptation Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Generate Indonesian-language X (Twitter) and Threads thread versions for all 32 SQL of the Day posts and integrate them into the standard publishing workflow.

**Architecture:** Content-only repo with no build system or tests. Each task writes `.txt` thread files following the fixed skeleton from the spec, then updates `posts/index.md` link cells. CLAUDE.md is updated once in Task 1 to document the new directories and workflow. Backfill is done in 8 batches of 4 posts each, with a commit after every batch.

**Tech Stack:** Plain text files, Claude Code inline generation, Bash (mkdir for directory creation).

**Spec:** `docs/superpowers/specs/2026-03-18-x-and-threads-adaptation-design.md`

---

## Thread Skeleton Reference

Every `.txt` file follows this structure (adjust N to final post count):

```
[1/N]
🧵 (X only, post 1)
<Hook: failure scenario in Indonesian, punchy 1-2 sentences>

[2/N]
<Problem: concise reframe of the SQL question>

[3/N]
<One-line setup in Indonesian>

```sql
<query>
```

[4/N]
<Breakdown 1: WHY this step exists>

[5/N]
<Breakdown 2>

[6/N]
<Breakdown 3>

[7/N]
<Breakdown 4 — merge with 6 if fewer than 4 logical steps; minimum 2 breakdown posts>

[8/N]
<Insight: business consequence, grounded in a real scenario>

[9/N]
<Takeaway: "Kalau [kondisi], pakai [X] karena [konsekuensi].">

[10/N]
<CTA: follow prompt + 4-7 hashtags>
#SQLoftheDay #SQL #DataAnalytics #<Source> <1-3 topic tags>
```

**X rules:** ≤280 chars per post, `🧵` on post 1, split SQL across 3a/3b if query exceeds 280 chars, recalculate N after any splits/merges.
**Threads rules:** ≤500 chars per post, no `🧵` marker, each breakdown step gets its own full explanation, recalculate N after any merges. Merging breakdown posts on Threads is for logical reasons only (fewer than 4 distinct steps) — never for character-limit reasons.
**Language:** Indonesian throughout. No dashes or em dashes in prose.

---

## File Map

| Action | Path |
|--------|------|
| Create dir | `posts/x/` |
| Create dir | `posts/threads/` |
| Modify | `CLAUDE.md` (3 changes — see Task 1) |
| Modify | `posts/index.md` (add X and Threads columns) |
| Create ×32 | `posts/x/YYYY-MM-DD_{slug}.txt` |
| Create ×32 | `posts/threads/YYYY-MM-DD_{slug}.txt` |

---

## Task 1: Setup — Directories, CLAUDE.md, Index Header

**Files:**
- Modify: `CLAUDE.md`
- Modify: `posts/index.md`

- [ ] **Step 1: Create the output directories**

```bash
mkdir -p "posts/x" "posts/threads"
```

- [ ] **Step 2: Update CLAUDE.md — Repository Structure**

In the `## Repository Structure` section, add two bullets immediately after the `posts/linkedin/*.txt` line:

```
- `posts/x/*.txt` — X (Twitter) thread version of each post in Indonesian (8-10 tweets)
- `posts/threads/*.txt` — Threads thread version of each post in Indonesian (8-10 posts)
```

- [ ] **Step 3: Update CLAUDE.md — Adding a New Post workflow**

The current workflow steps 1-4 are:
1. Create `posts/YYYY-MM-DD_{slug}.md`
2. Create `posts/linkedin/YYYY-MM-DD_{slug}.txt`
3. If a carousel PDF exists, generate...
4. Append a new row to `posts/index.md`

Insert two new steps after step 2, shifting the old steps 3-4 to 5-6:

```
3. Create `posts/x/YYYY-MM-DD_{slug}.txt` — X thread in Indonesian (8-10 tweets, ≤280 chars each)
4. Create `posts/threads/YYYY-MM-DD_{slug}.txt` — Threads thread in Indonesian (8-10 posts, ≤500 chars each)
5. If a carousel PDF exists, generate with Python/matplotlib and save to `posts/media/pdfs/YYYY-MM-DD_{slug}.pdf`
6. Append a new row to `posts/index.md` ...
```

- [ ] **Step 4: Update CLAUDE.md — Key Facts post count**

Make two changes in the Key Facts section:

**Change A:** Replace:
```
- 26 posts total (24 indexed + 2 pending index entries: `finding_purchases.md`, `number_of_units_per_nationality.md`)
```
With:
```
- 32 posts total (all indexed); post #26 (`person_with_most_oscars`) still shows `—` for posted date (URN unknown)
```

**Change B:** Remove the now-superseded stale line (which contradicts the new count above):
```
- Post #11 (`person_with_most_oscars`) file is dated `2026-03-23` but index still shows `—` for posted date (URN unknown)
```
The Oscar post caveat is now captured in the new Key Facts count line above.

- [ ] **Step 5: Update posts/index.md — Add X and Threads column headers**

Replace the header row:
```
| # | Problem | Source | Posted | File | PDF |
|---|---------|--------|--------|------|-----|
```

With:
```
| # | Problem | Source | Posted | File | PDF | X | Threads |
|---|---------|--------|--------|------|-----|---|---------|
```

Also append ` — | — |` to every existing data row so the table stays valid markdown. All 32 rows get `— | —` in the new columns (they will be updated with real links as each batch is generated).

- [ ] **Step 6: Verify the index table renders correctly**

Open `posts/index.md` and confirm:
- Header has 8 columns
- All 32 data rows have 8 cells
- No row is missing the trailing `— | —`

- [ ] **Step 7: Commit**

```bash
git add CLAUDE.md posts/index.md
git commit -m "feat: add posts/x and posts/threads to repo structure and workflow"
```

---

## Task 2: Backfill Posts 1–4

Posts: `top_3_search_click_behavior`, `unique_users_per_client`, `shipments_per_month`, `people_by_age`

**Files to read:**
- `posts/2025-04-25_top_3_search_click_behavior.md`
- `posts/2025-04-27_unique_users_per_client.md`
- `posts/2025-04-28_shipments_per_month.md`
- `posts/2025-04-29_people_by_age.md`

**Files to create (8 total):**
- `posts/x/2025-04-25_top_3_search_click_behavior.txt`
- `posts/threads/2025-04-25_top_3_search_click_behavior.txt`
- `posts/x/2025-04-27_unique_users_per_client.txt`
- `posts/threads/2025-04-27_unique_users_per_client.txt`
- `posts/x/2025-04-28_shipments_per_month.txt`
- `posts/threads/2025-04-28_shipments_per_month.txt`
- `posts/x/2025-04-29_people_by_age.txt`
- `posts/threads/2025-04-29_people_by_age.txt`

- [ ] **Step 1: Read all 4 source `.md` files**

- [ ] **Step 2: Write X and Threads `.txt` files for each post**

For each post: follow the thread skeleton, write in Indonesian, apply X (≤280 chars) and Threads (≤500 chars) rules. Split SQL on X if needed. Minimum 2 breakdown posts.

- [ ] **Step 3: Update index.md rows 1–4**

Replace `— | —` in the X and Threads columns for rows 1–4 with:
- X: `[🐦](x/2025-04-25_top_3_search_click_behavior.txt)` (etc.)
- Threads: `[🧵](threads/2025-04-25_top_3_search_click_behavior.txt)` (etc.)

- [ ] **Step 4: Verify character limits and index links**

For each X file: confirm no individual `[N/N]` block (excluding the code block itself) exceeds 280 characters.
For each Threads file: confirm no block exceeds 500 characters.

Confirm index rows 1–4 now have real links (not placeholders):
```bash
grep -c "🐦" posts/index.md   # expect 4 after this batch
grep -c "🧵" posts/index.md   # expect 4 after this batch
```

- [ ] **Step 5: Commit**

```bash
git add posts/x/ posts/threads/ posts/index.md
git commit -m "feat: add X and Threads threads for posts 1-4 (Apr 2025)"
```

---

## Task 3: Backfill Posts 5–8

Posts: `regex_alphanumeric_split`, `candidates_complete_skill_sets`, `most_lucrative_products`, `highest_energy_consumption`

**Files to read:**
- `posts/2025-04-30_regex_alphanumeric_split.md`
- `posts/2025-05-01_candidates_complete_skill_sets.md`
- `posts/2025-05-02_most_lucrative_products.md`
- `posts/2025-05-03_highest_energy_consumption.md`

**Files to create (8 total):**
- `posts/x/2025-04-30_regex_alphanumeric_split.txt`
- `posts/threads/2025-04-30_regex_alphanumeric_split.txt`
- `posts/x/2025-05-01_candidates_complete_skill_sets.txt`
- `posts/threads/2025-05-01_candidates_complete_skill_sets.txt`
- `posts/x/2025-05-02_most_lucrative_products.txt`
- `posts/threads/2025-05-02_most_lucrative_products.txt`
- `posts/x/2025-05-03_highest_energy_consumption.txt`
- `posts/threads/2025-05-03_highest_energy_consumption.txt`

- [ ] **Step 1: Read all 4 source `.md` files**
- [ ] **Step 2: Write X and Threads `.txt` files for each post**
- [ ] **Step 3: Update index.md rows 5–8 with X and Threads links**
- [ ] **Step 4: Verify character limits and index links**

Apply the same character limit checks as Task 2. Then confirm cumulative link count:
```bash
grep -c "🐦" posts/index.md   # expect 8
grep -c "🧵" posts/index.md   # expect 8
```

- [ ] **Step 5: Commit**

```bash
git add posts/x/ posts/threads/ posts/index.md
git commit -m "feat: add X and Threads threads for posts 5-8 (Apr-May 2025)"
```

---

## Task 4: Backfill Posts 9–12

Posts: `bathrooms_bedrooms_distribution`, `titanic_survivors`, `top_10_songs_2010`, `most_profitable_financial_company`

**Files to read:**
- `posts/2025-05-05_bathrooms_bedrooms_distribution.md`
- `posts/2025-05-19_titanic_survivors.md`
- `posts/2025-05-23_top_10_songs_2010.md`
- `posts/2025-05-27_most_profitable_financial_company.md`

**Files to create (8 total):**
- `posts/x/2025-05-05_bathrooms_bedrooms_distribution.txt`
- `posts/threads/2025-05-05_bathrooms_bedrooms_distribution.txt`
- `posts/x/2025-05-19_titanic_survivors.txt`
- `posts/threads/2025-05-19_titanic_survivors.txt`
- `posts/x/2025-05-23_top_10_songs_2010.txt`
- `posts/threads/2025-05-23_top_10_songs_2010.txt`
- `posts/x/2025-05-27_most_profitable_financial_company.txt`
- `posts/threads/2025-05-27_most_profitable_financial_company.txt`

- [ ] **Step 1: Read all 4 source `.md` files**
- [ ] **Step 2: Write X and Threads `.txt` files for each post**
- [ ] **Step 3: Update index.md rows 9–12 with X and Threads links**
- [ ] **Step 4: Verify character limits and index links**

```bash
grep -c "🐦" posts/index.md   # expect 12
grep -c "🧵" posts/index.md   # expect 12
```

- [ ] **Step 5: Commit**

```bash
git add posts/x/ posts/threads/ posts/index.md
git commit -m "feat: add X and Threads threads for posts 9-12 (May 2025)"
```

---

## Task 5: Backfill Posts 13–16

Posts: `finding_updated_records`, `churro_activity_dates`, `roxanne_cafe_violation_history`, `how_easy_is_too_easy`

**Files to read:**
- `posts/2025-06-22_finding_updated_records.md`
- `posts/2025-08-26_churro_activity_dates.md`
- `posts/2025-08-29_roxanne_cafe_violation_history.md`
- `posts/2025-12-22_how_easy_is_too_easy.md`

**Files to create (8 total):**
- `posts/x/2025-06-22_finding_updated_records.txt`
- `posts/threads/2025-06-22_finding_updated_records.txt`
- `posts/x/2025-08-26_churro_activity_dates.txt`
- `posts/threads/2025-08-26_churro_activity_dates.txt`
- `posts/x/2025-08-29_roxanne_cafe_violation_history.txt`
- `posts/threads/2025-08-29_roxanne_cafe_violation_history.txt`
- `posts/x/2025-12-22_how_easy_is_too_easy.txt`
- `posts/threads/2025-12-22_how_easy_is_too_easy.txt`

- [ ] **Step 1: Read all 4 source `.md` files**
- [ ] **Step 2: Write X and Threads `.txt` files for each post**
- [ ] **Step 3: Update index.md rows 13–16 with X and Threads links**
- [ ] **Step 4: Verify character limits and index links**

```bash
grep -c "🐦" posts/index.md   # expect 16
grep -c "🧵" posts/index.md   # expect 16
```

- [ ] **Step 5: Commit**

```bash
git add posts/x/ posts/threads/ posts/index.md
git commit -m "feat: add X and Threads threads for posts 13-16 (Jun-Dec 2025)"
```

---

## Task 6: Backfill Posts 17–20

Posts: `new_products_yoy_comparison`, `users_by_average_session_time`, `highest_cost_orders`, `acceptance_rate_by_date`

**Files to read:**
- `posts/2025-12-29_new_products_yoy_comparison.md`
- `posts/2026-01-05_users_by_average_session_time.md`
- `posts/2026-01-12_highest_cost_orders.md`
- `posts/2026-01-19_acceptance_rate_by_date.md`

**Files to create (8 total):**
- `posts/x/2025-12-29_new_products_yoy_comparison.txt`
- `posts/threads/2025-12-29_new_products_yoy_comparison.txt`
- `posts/x/2026-01-05_users_by_average_session_time.txt`
- `posts/threads/2026-01-05_users_by_average_session_time.txt`
- `posts/x/2026-01-12_highest_cost_orders.txt`
- `posts/threads/2026-01-12_highest_cost_orders.txt`
- `posts/x/2026-01-19_acceptance_rate_by_date.txt`
- `posts/threads/2026-01-19_acceptance_rate_by_date.txt`

- [ ] **Step 1: Read all 4 source `.md` files**
- [ ] **Step 2: Write X and Threads `.txt` files for each post**
- [ ] **Step 3: Update index.md rows 17–20 with X and Threads links**
- [ ] **Step 4: Verify character limits and index links**

```bash
grep -c "🐦" posts/index.md   # expect 20
grep -c "🧵" posts/index.md   # expect 20
```

- [ ] **Step 5: Commit**

```bash
git add posts/x/ posts/threads/ posts/index.md
git commit -m "feat: add X and Threads threads for posts 17-20 (Dec 2025-Jan 2026)"
```

---

## Task 7: Backfill Posts 21–24

Posts: `finding_returning_users`, `premium_vs_freemium_downloads`, `finding_purchases`, `ranking_most_active_guests`

**Files to read:**
- `posts/2026-01-26_finding_returning_users.md`
- `posts/2026-02-02_premium_vs_freemium_downloads.md`
- `posts/2026-03-02_finding_purchases.md`
- `posts/2026-03-09_ranking_most_active_guests.md`

**Files to create (8 total):**
- `posts/x/2026-01-26_finding_returning_users.txt`
- `posts/threads/2026-01-26_finding_returning_users.txt`
- `posts/x/2026-02-02_premium_vs_freemium_downloads.txt`
- `posts/threads/2026-02-02_premium_vs_freemium_downloads.txt`
- `posts/x/2026-03-02_finding_purchases.txt`
- `posts/threads/2026-03-02_finding_purchases.txt`
- `posts/x/2026-03-09_ranking_most_active_guests.txt`
- `posts/threads/2026-03-09_ranking_most_active_guests.txt`

- [ ] **Step 1: Read all 4 source `.md` files**
- [ ] **Step 2: Write X and Threads `.txt` files for each post**
- [ ] **Step 3: Update index.md rows 21–24 with X and Threads links**
- [ ] **Step 4: Verify character limits and index links**

```bash
grep -c "🐦" posts/index.md   # expect 24
grep -c "🧵" posts/index.md   # expect 24
```

- [ ] **Step 5: Commit**

```bash
git add posts/x/ posts/threads/ posts/index.md
git commit -m "feat: add X and Threads threads for posts 21-24 (Jan-Mar 2026)"
```

---

## Task 8: Backfill Posts 25–28

Posts: `number_of_units_per_nationality`, `person_with_most_oscars`, `facebook_accounts`, `apple_product_counts`

**Files to read:**
- `posts/2026-03-16_number_of_units_per_nationality.md`
- `posts/2026-03-23_person_with_most_oscars.md`
- `posts/2026-03-30_facebook_accounts.md`
- `posts/2026-04-06_apple_product_counts.md`

**Files to create (8 total):**
- `posts/x/2026-03-16_number_of_units_per_nationality.txt`
- `posts/threads/2026-03-16_number_of_units_per_nationality.txt`
- `posts/x/2026-03-23_person_with_most_oscars.txt`
- `posts/threads/2026-03-23_person_with_most_oscars.txt`
- `posts/x/2026-03-30_facebook_accounts.txt`
- `posts/threads/2026-03-30_facebook_accounts.txt`
- `posts/x/2026-04-06_apple_product_counts.txt`
- `posts/threads/2026-04-06_apple_product_counts.txt`

- [ ] **Step 1: Read all 4 source `.md` files**
- [ ] **Step 2: Write X and Threads `.txt` files for each post**
- [ ] **Step 3: Update index.md rows 25–28 with X and Threads links**
- [ ] **Step 4: Verify character limits and index links**

```bash
grep -c "🐦" posts/index.md   # expect 28
grep -c "🧵" posts/index.md   # expect 28
```

- [ ] **Step 5: Commit**

```bash
git add posts/x/ posts/threads/ posts/index.md
git commit -m "feat: add X and Threads threads for posts 25-28 (Mar 2026)"
```

---

## Task 9: Backfill Posts 29–32

Posts: `spam_posts`, `percentage_of_shipable_orders`, `income_by_title_and_gender`, `top_cool_votes`

**Files to read:**
- `posts/2026-04-13_spam_posts.md`
- `posts/2026-04-20_percentage_of_shipable_orders.md`
- `posts/2026-04-26_income_by_title_and_gender.md`
- `posts/2026-05-04_top_cool_votes.md`

**Files to create (8 total):**
- `posts/x/2026-04-13_spam_posts.txt`
- `posts/threads/2026-04-13_spam_posts.txt`
- `posts/x/2026-04-20_percentage_of_shipable_orders.txt`
- `posts/threads/2026-04-20_percentage_of_shipable_orders.txt`
- `posts/x/2026-04-26_income_by_title_and_gender.txt`
- `posts/threads/2026-04-26_income_by_title_and_gender.txt`
- `posts/x/2026-05-04_top_cool_votes.txt`
- `posts/threads/2026-05-04_top_cool_votes.txt`

- [ ] **Step 1: Read all 4 source `.md` files**
- [ ] **Step 2: Write X and Threads `.txt` files for each post**
- [ ] **Step 3: Update index.md rows 29–32 with X and Threads links**
- [ ] **Step 4: Verify character limits and index links**

```bash
grep -c "🐦" posts/index.md   # expect 32
grep -c "🧵" posts/index.md   # expect 32
```

- [ ] **Step 5: Commit**

```bash
git add posts/x/ posts/threads/ posts/index.md
git commit -m "feat: add X and Threads threads for posts 29-32 (Apr-May 2026)"
```

---

## Task 10: Final Verification

- [ ] **Step 1: Count output files**

```bash
ls posts/x/ | wc -l
ls posts/threads/ | wc -l
```

Expected: 32 files in each directory.

- [ ] **Step 2: Confirm all 32 index rows have X and Threads links**

```bash
grep -c "🐦" posts/index.md
grep -c "🧵" posts/index.md
```

Expected: 32 for each. If either is less than 32, find the missing rows and regenerate their files.

- [ ] **Step 3: Spot-check one X file for character limits**

Open any `posts/x/*.txt`, count characters in the longest non-code block. Must be ≤280.

- [ ] **Step 4: Spot-check one Threads file for character limits**

Open any `posts/threads/*.txt`, count characters in the longest block. Must be ≤500.

- [ ] **Step 5: Confirm CLAUDE.md has both new workflow steps**

```bash
grep -n "posts/x/" CLAUDE.md
grep -n "posts/threads/" CLAUDE.md
```

Expected: at least 2 matches each (Repository Structure + workflow steps).

- [ ] **Step 6: Final commit if any fixes were needed**

```bash
git add -A
git commit -m "fix: final verification fixes for X and Threads backfill"
```
