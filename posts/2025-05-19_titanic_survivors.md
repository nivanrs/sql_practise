## 💻 SQL of the Day: Titanic Survivors and Non-Survivors

🔗 https://lnkd.in/g2tJVEkj

> "How many survivors and non-survivors were there in each passenger class (1st, 2nd, 3rd)?"

---

### 🧠 Solution:

```sql
select
  survived,
  sum(case when pclass = 1 then 1 else 0 end) as first_class,
  sum(case when pclass = 2 then 1 else 0 end) as second_class,
  sum(case when pclass = 3 then 1 else 0 end) as third_class
from titanic
group by survived;
```

---

### ✅ Why this works:

- `GROUP BY survived` groups the data into survivors (1) and non-survivors (0).
- Each `SUM(CASE...)` counts how many people in each class match that survival status.

---

### 💡 Tip:

This pattern where you define new columns using `CASE WHEN` inside aggregations is one of the most useful SQL techniques for building summary reports, dashboards, and business insights.

---

### 🎯 Why this matters:

Understanding how different segments behave (like class-based survival rates) is key in use cases like customer segmentation, retention reporting, and behavioral analytics.

#SQLoftheDay #SQL #StrataScratch #DataAnalytics #BusinessIntelligence #OperationsAnalytics #AnalyticsEngineer #SQLTips
