## 💻 SQL of the Day: People by Age (10+ Members)

Today's challenge: Identify age groups with at least 10 people.

🔗 https://lnkd.in/gwK5gxEU

> "Which ages occur at least 10 times in the people table?"

---

### 🧠 Solution:

```sql
SELECT
  age,
  COUNT(*) AS total_people
FROM people
GROUP BY age
HAVING COUNT(*) >= 10;
```

---

### ✅ What this does:

- Groups all records by age.
- Counts how many people share each age.
- Filters to only keep ages with 10 or more people.

---

### 💡 Tip — `HAVING` vs `WHERE`:

`WHERE` filters rows before any grouping (e.g., `WHERE age > 30`), whereas `HAVING` filters groups after aggregation.

In this problem, we can't know which ages hit the 10-person threshold until after we've grouped and counted, so we use `HAVING COUNT(*) >= 10`.

---

### 🎯 Why this matters:

Filtering on aggregated results is a powerful way to spotlight meaningful clusters in your data — whether it's age cohorts, sales brackets, or any category where you need a "minimum threshold" after grouping.

#SQLoftheDay #SQL #Codewars #DataAnalytics #BusinessIntelligence #Demographics #Grouping #HavingClause #LearningByDoing
