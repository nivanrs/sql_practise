---
layout: post
title: "Candidates with Complete Skill Sets"
date: 2025-05-01
---

## 💻 SQL of the Day: Candidates with Complete Skill Sets

Today's challenge: Identify candidates who possess all three required skills — Python, Tableau, and PostgreSQL.

🔗 https://lnkd.in/gvPbaMfZ

> "Which candidates have entries for Python, Tableau, AND PostgreSQL in the candidates table?"

---

### 🧠 Solution:

```sql
SELECT candidate_id
FROM candidates
WHERE skill IN ('Python', 'Tableau', 'PostgreSQL')
GROUP BY candidate_id
HAVING COUNT(DISTINCT skill) = 3;
```

---

### ✅ How it works:

- **Filter** (`WHERE skill IN (...)`): keep only rows for the three target skills.
- **Group** (`GROUP BY candidate_id`): bundle those rows by candidate.
- **Aggregate** (`COUNT(DISTINCT skill)`): count each candidate's unique skills.
- **Filter groups** (`HAVING ... = 3`): retain only candidates whose count equals all three skills.

---

### 💡 Tip — `HAVING` vs `WHERE`:

- Use `WHERE` to filter rows **before** grouping.
- Use `HAVING` to filter groups **after** you've aggregated.

Here, we can't check "has all three skills" until after grouping and counting.

---

### 🎯 Why this matters:

This pattern — filtering, grouping, then using `HAVING` to enforce a minimum distinct-count threshold — is essential to ensure that each entity in your dataset meets all of a set of criteria (skills, tags, categories, etc.).

#SQLoftheDay #SQL #DataFiltering #GroupBy #HavingClause #SkillMatching #DataAnalytics #PracticeToProgress #LearningByDoing
