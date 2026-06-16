---
layout: post
title: "Number of Shipments per Month"
date: 2025-04-28
---

## 💻 SQL of the Day: Number of Shipments per Month

Today's challenge: Calculate the number of unique shipments per month-year from Amazon.

🔗 https://lnkd.in/gc4F4dAA

> "How many shipments were completed each month?"

---

### 🧠 Solution:

```sql
with data as (
  select
    concat(shipment_id, sub_id) as composite_id,
    to_char(shipment_date, 'yyyy-mm') as year_month
  from amazon_shipment
)
select
  year_month,
  count(distinct composite_id)
from data
group by year_month;
```

---

### ✅ Result:

Two columns that count how many unique shipments occurred in each year-month period.

---

### 🎯 Why this matters:

Tracking the number of shipments per month helps businesses identify:

- Seasonal demand patterns
- Operational bottlenecks
- Anomalies in operations
- Shipping cycle performance

Recognizing these patterns is crucial for improving inventory planning, staffing decisions, and customer experience.

#SQLoftheDay #SQL #StrataScratch #LogisticsAnalytics #SupplyChain #OperationsAnalytics #BusinessIntelligence #LearningByDoing #SQLPractice
