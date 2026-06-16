---
layout: post
title: "Unique Users per Client per Month"
date: 2025-04-27
---

## 💻 SQL of the Day: Unique Users per Client per Month

Today's exercise focuses on monitoring user engagement trends over time — an important aspect of product and client analytics.

🔗 https://lnkd.in/eTFNVaus

> "How many unique users did each client have, month by month?"

---

### 🧠 Solution:

```sql
SELECT
  client_id,
  EXTRACT(MONTH FROM time_id) AS event_month,
  COUNT(DISTINCT user_id) AS unique_user_count
FROM fact_events
GROUP BY EXTRACT(MONTH FROM time_id), client_id
ORDER BY event_month, unique_user_count DESC;
```

---

### ✅ Result:

A monthly breakdown of unique users for each client, ordered by month and descending user count.

---

### 🎯 Why this matters:

Monitoring the trend of unique users can give early signals about client health and engagement. If the number of unique users suddenly drops, it's often a sign that something might be wrong — whether on the product side, app side, market side, or user experience.

Also, analyzing different clients individually is important — because each client may show different behavior patterns, cycles, or user dynamics. Simple tracking like this helps teams move from reactive to proactive decision-making.

#SQLoftheDay #SQL #StrataScratch #MarketingAnalytics #UserEngagement #GrowthStrategy #DataAnalytics #BusinessIntelligence #PostgreSQL #SQLTips
