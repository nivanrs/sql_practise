<!-- EXAMPLE: Delete this file after you understand the format. -->

# Critique: Top Cool Votes

**What's strong:** You identified the right tool (DENSE_RANK) and the right structure (CTE + filter). The instinct was correct.

---

**Coaching notes:**

1. **SQL bug.** `ORDER BY 4` inside the CTE has no guaranteed effect in PostgreSQL. An `ORDER BY` inside a CTE without a `LIMIT` is essentially ignored — the database is free to return rows in any order. Move it to the outer query, or drop it entirely (the `WHERE rnk = 1` filter makes ordering irrelevant for the result anyway).

2. **No hook.** Your draft starts at the solution. The most compelling part of this post — "I used the wrong function and the query looked correct but wasn't" — isn't in your draft at all. Before writing the logic, ask yourself: what goes wrong if I use `ROW_NUMBER()` here? That failure is your opening.

3. **Logic describes what, not why.** "urutkan rank yang sesuai terus filter column" tells me the steps but not the reason. The logic section should answer: why `DENSE_RANK` specifically? What makes rank 1 mean "all tied rows" rather than "just one row"?

4. **Insight starts from the solution, not the problem.** "DENSE_RANK is fair" is describing the tool positively. The insight lands harder when you name what fails without it: `ROW_NUMBER()` runs without error, returns one row, looks correct, and silently drops everything else.

5. **Takeaway is a topic heading, not a lesson.** "harus tau kapan pake dense_rank, rank, dan row" = a syllabus item. A takeaway finishes the sentence: "Use DENSE_RANK when you need all rows tied for a position, because ROW_NUMBER() will silently discard them with no warning."
