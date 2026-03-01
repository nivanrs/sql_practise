## 💻 SQL of the Day: Highest Energy Consumption

Today's challenge: Find the date with the highest total energy consumption across Meta's three regional data centers.

🔗 https://lnkd.in/gPXWX2sC

> "Which date had the highest sum of energy consumption when you combine EU, Asia, and NA data?"

---

### 🧠 Solution:

```sql
WITH all_region AS (
  SELECT date, consumption FROM fb_eu_energy
  UNION ALL
  SELECT date, consumption FROM fb_asia_energy
  UNION ALL
  SELECT date, consumption FROM fb_na_energy
)
SELECT date, SUM(consumption) AS total_consumption
FROM all_region
GROUP BY date
ORDER BY total_consumption DESC
LIMIT 2;
```

---

### ✅ What it does:

- Combines all three regional tables into one CTE (`all_region`) using `UNION ALL`.
- Groups by date and sums the consumption values.
- Orders by `total_consumption` descending and limits to the top row — the date with the highest combined consumption.

---

### 💡 Tip:

- Use `UNION ALL` (instead of `UNION`) to keep duplicates and improve performance when you know the source tables don't overlap on the same row.
- A CTE makes your main query much cleaner and easier to read when you need to union or pre-process multiple sources.

---

### 🎯 Why this matters:

Real-world analytics often requires merging multiple data sources before you can answer high-level questions. Mastering `UNION ALL` and CTEs helps you build more maintainable, performant pipelines for cross-region or cross-department reporting.

#SQLoftheDay #SQL #StrataScratch #DataUnion #CTE #UnionAll #EnergyAnalytics #BusinessIntelligence #LearningByDoing #PracticeToProgress
