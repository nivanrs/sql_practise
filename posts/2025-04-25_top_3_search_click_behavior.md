---
layout: post
title: "Top 3 Search Click Behavior"
date: 2025-04-25
---

## 💻 SQL of the Day: Top 3 Search Click Behavior

Today's exercise dives into user behavior within search results. It's a great case for measuring both engagement and missed opportunities.

🔗 https://lnkd.in/etHnxfJp

> "Of all search records, what percentage were clicked in the top 3 results — and what percentage weren't?"

---

### 🧠 Solution:

```sql
select
  (100.0 * count(case when clicked = 1 and search_results_position <= 3 then 1 end) / count(*)) as top_3_clicked,
  (100.0 * count(case when clicked = 0 and search_results_position <= 3 then 1 end) / count(*)) as top_3_notclicked
from fb_search_events;
```

---

### ✅ Result:

Two percentages in one row — giving you a snapshot of how users interact with top-ranked results.

---

### 🎯 Why this matters:

Click-through rate is one of the clearest signals of user engagement in search. This kind of metric helps us understand:

- Are top results delivering value?
- Are users skipping the first few results?
- How can we improve the ranking or relevance?

This can provide useful feedback for search algorithms, product teams, and UX designers.

#SQLoftheDay #SQL #StrataScratch #SearchAnalytics #MarketingAnalytics #UserBehavior #DataAnalytics #UXInsights #ProductMetrics #LearningByDoing #BusinessIntelligence #SQLTips
