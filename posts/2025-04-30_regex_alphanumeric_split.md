---
layout: post
title: "Regex AlphaNumeric Split"
date: 2025-04-30
---

## 💻 SQL of the Day: Regex AlphaNumeric Split

Continuing the "SQL of the Day" series — today's challenge is all about splitting alphanumeric strings into pure letters and digits.

🔗 https://lnkd.in/gDJavWT3

> Given a `repositories` table with a mixed alphanumeric `address`, return three columns: `project`, `letters`, `numbers`.

---

### 🧠 Solution:

```sql
SELECT
  project,
  regexp_replace(address, '[^[:alpha:]]', '', 'g') AS letters,
  regexp_replace(address, '[^[:digit:]]', '', 'g') AS numbers
FROM repositories;
```

---

### ✅ How it works:

- `regexp_replace(address, '[^[:alpha:]]', '', 'g')` strips out anything that isn't A–Z (and a–z), leaving only letters.
- `regexp_replace(address, '[^[:digit:]]', '', 'g')` strips out everything that isn't 0–9, leaving only digits.

---

### 💡 Tips:

- Regex is your friend when you need precise string extraction — whether pulling letters, digits, or patterns.
- Always test your regex on edge cases (empty strings, special characters). A great tool for testing: https://regex101.com/

---

### 🎯 Why this matters:

Real-world data often comes in mixed formats (strings, symbols, codes, identifiers, etc). Being able to cleanly extract the pieces you need is key for downstream analysis, reporting, and ensuring data quality.

#SQLoftheDay #SQL #Codewars #Regex #DataCleaning #StringProcessing #PostgreSQL #BusinessIntelligence #LearningByDoing #AnalyticsTips
