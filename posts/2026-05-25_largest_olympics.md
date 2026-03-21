## 💻 SQL of the Day: Largest Olympics
🔗 https://platform.stratascratch.com/coding/9942-largest-olympics?code_type=1

### Problem:
Find the Olympics with the most distinct athletes. Return the name of the edition and the number of distinct athletes.

---

### 🧠 SQL Solution
```sql
WITH Olymp AS (
  SELECT games, COUNT(DISTINCT id) AS athletes
  FROM olympics_athletes_events
  GROUP BY games
)
SELECT *
FROM Olymp
WHERE athletes = (
  SELECT MAX(athletes)
  FROM Olymp
);
```

---

### 🧩 Simple logic breakdown
- **Count distinct athletes per edition**: `COUNT(DISTINCT id)` groups by `games` and counts unique athlete IDs. One athlete competing in three events within the same Olympics is still one person.
- **Find the maximum**: The subquery `SELECT MAX(athletes) FROM Olymp` returns the single highest count across all editions.
- **Filter by equality**: `WHERE athletes = (SELECT MAX(...))` keeps every edition matching that peak count, including any ties.

---

### 📊 This pattern tells you:
- **`LIMIT 1` silently discards ties**: If two Olympics editions share the same athlete count, `ORDER BY athletes DESC LIMIT 1` returns one arbitrarily. The other is dropped with no error, no warning. A report built on that result is acting on a coin flip.
- **Olympic participation fluctuates — ties are plausible**: Attendance depends on host politics, boycotts, and global participation growth. Assuming a unique winner is an assumption, not a fact. If your "most attended Olympics" report shows one edition when two tied, the report is wrong.
- **Conditional equality scales to any aggregation**: This pattern works for revenue peaks, user records, or any scenario where you need the top value and cannot afford to miss tied entries. `= (SELECT MAX(...))` is the safer default.

---

### 🎯 Key takeaways
1. Use `COUNT(DISTINCT id)` when athletes can appear in multiple rows: counting rows overcounts people. Counting distinct IDs counts people.
2. When grouping and counting distinct entities, prefer conditional equality (`= (SELECT MAX(...))`) over `ORDER BY + LIMIT 1`. The latter silently discards ties and produces results that look correct until an edge case surfaces.
3. `LIMIT 1` is not a bug detector. It returns clean output even when it drops valid data. The only way to catch it is to know ties are possible before you write the query.

#SQLoftheDay #SQL #StrataScratch #DataAnalytics #DataAnalyst #Olympics
