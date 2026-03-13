## 💻 SQL of the Day: Facebook Accounts

🔗 https://platform.stratascratch.com/coding/10296-facebook-accounts?code_type=1

### Problem:

Calculate the ratio of closed Facebook accounts to all accounts on January 10, 2020.

---

### SQL Solution

```sql
SELECT
    COUNT(CASE WHEN status = 'closed' THEN 1 END)::float
    /
    COUNT(*) AS closed_ratio
FROM fb_account_status
WHERE status_date = '2020-01-10';
```

---

### 🧩 Simple logic breakdown

- **Filter the date** `WHERE status_date = '2020-01-10'` narrows the data to the snapshot we care about.
- **Count closed accounts** `COUNT(CASE WHEN status = 'closed' THEN 1 END)` counts only the rows where `status` is `'closed'`. Rows that don't match return `NULL`, and `COUNT` ignores `NULL`s.
- **Count all accounts** `COUNT(*)` counts every row on that date, regardless of status.
- **Divide for the ratio** dividing the closed count by the total count gives the proportion. The `::float` cast prevents integer division from rounding to `0`.

---

### 📊 This pattern tells you:

- **Account health at a glance** a single ratio instantly reveals what share of your user base has churned on a given day.
- **Trend tracking** run this query across multiple dates to spot whether closures are accelerating or slowing.
- **Benchmarking** comparing closed ratios across time periods or segments helps set retention targets.

---

### 🎯 Key takeaways

- `CASE WHEN ... THEN 1 END` inside `COUNT()` is the classic conditional-counting pattern. It counts only rows that match a condition without needing a subquery or separate filter.
- Always cast to `::float` (or `* 1.0`) when dividing two integers in PostgreSQL. Without it, `3 / 10` returns `0`, not `0.3`.
- `COUNT(*)` counts all rows; `COUNT(expression)` counts only non-`NULL` values of that expression. This difference is what makes the `CASE WHEN` trick work.
- This same pattern scales to any "ratio of subset to total" problem: swap the condition inside `CASE WHEN` to count any category you need.

#SQLoftheDay #SQL #StrataScratch #DataAnalytics #DataAnalyst #ConditionalCounting #Facebook #BusinessIntelligence
