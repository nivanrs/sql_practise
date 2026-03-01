## 💻 SQL of the Day: Churro Activity Dates (Inspection Failures)

🔗 StrataScratch Problem #9688

> "Find the dates when STREET CHURROS received a health inspection score of 95 or below, along with the inspection reason."

Link: https://lnkd.in/gJQ64rEY

---

### SQL Solution

```sql
select
  activity_date,
  pe_description
from los_angeles_restaurant_health_inspections
where facility_name = 'STREET CHURROS'
  and score <= 95;
```

---

### Why this still matters:

Even the easiest SQL queries matter in real-world applications:

- Imagine if your business receives a bad inspection result — it could damage brand reputation and decrease business performance.
- Filtering by thresholds (like scores ≤ 95) is a common pattern across industries.

---

### 💡 Tips:

- Always include a `WHERE 1=1` pattern when you have multiple filters, to make adding or removing filters easier.
- Only select the columns you need — avoid using `SELECT *` for better readability and performance.

#SQLoftheDay #SQL #StrataScratch #DataAnalytics
