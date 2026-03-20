## 💻 SQL of the Day: Top Businesses with Most Reviews
🔗 https://platform.stratascratch.com/coding/10048-top-businesses-with-most-reviews?code_type=1

### Problem:
Find the **top 5 businesses** with the most reviews. Return the **business name** and **total review count**.

---

### 🧠 SQL Solution
```sql
WITH business_rank AS (
    SELECT
        business_id,
        name,
        SUM(review_count) AS review_count,
        RANK() OVER (ORDER BY SUM(review_count) DESC) AS rnk
    FROM yelp_business
    GROUP BY business_id, name
)

SELECT name, review_count
FROM business_rank
WHERE rnk <= 5;
```

---

### 🧩 Simple logic breakdown
- **Aggregate first**: `SUM(review_count)` grouped by business gives total reviews per business
- **Rank the totals**: `RANK()` assigns position based on descending review count. Two businesses with the same total both receive rank 3 — the next rank assigned is 5, not 4
- **Filter by position**: `WHERE rnk <= 5` keeps every business within the top 5 positions, including all tied entries at the boundary

---

### 📊 This pattern tells you:
- **Wrong function, invisible damage**: `ROW_NUMBER()` would run without error, return exactly 5 rows, and look correct. But if two businesses tie at position 4, one gets rank 4 and the other gets rank 5 — the tie is broken arbitrarily. A business that earned its spot on the Yelp leaderboard silently disappears.
- **`RANK()` vs `DENSE_RANK()` is a different failure**: `DENSE_RANK()` handles ties correctly but compresses rank numbers. With two businesses tied at rank 3, the next rank is 4, not 5. Applied to a top-5 filter, that admits an extra business at rank 5 that would fall outside the cutoff under `RANK()`. The result set expands beyond what the business expects.
- **Choose the function that matches the question**: "top 5 positions" calls for `RANK()`. "Top 5 distinct score levels" calls for `DENSE_RANK()`. "Assign a unique row number" calls for `ROW_NUMBER()`. The question determines the function, not habit.

---

### 🎯 Key takeaways
1. `ROW_NUMBER()` silently corrupts any top-N query where ties are possible. It produces clean output with no warning — just an incomplete leaderboard where tied entries are dropped by arbitrary ordering.
2. `RANK()` is the correct default for competitive rankings: tied businesses share the same position and the count skips ahead, so `<= 5` reliably returns all entries that belong in the top 5.
3. `DENSE_RANK()` is not a safe upgrade from `RANK()` for top-N filters. It can expand your result set beyond N rows when ties exist above the cutoff, because compressed numbering allows lower-ranked entries to squeeze into the filter range.

#SQLoftheDay #SQL #StrataScratch #DataAnalytics #DataAnalyst #WindowFunctions #Ranking #Yelp
