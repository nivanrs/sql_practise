## 💻 SQL of the Day: Roxanne Cafe Violation History by Year

🔗 StrataScratch Problem #9728

**Goal:** Track how many health violations Roxanne Cafe had per year.

---

### SQL Solution

```sql
select
  extract(year from inspection_date) as inspection_year,
  count(*) as number_of_violations
from sf_restaurant_health_violations
where business_name = 'Roxanne Cafe'
group by inspection_year
order by inspection_year;
```

---

### Why This Matters:

- Annual tracking helps identify trends: Is the restaurant improving or getting worse over time?
- This kind of logic is reusable in any domain with timestamped events — for example: frauds per year, sales per quarter, etc.

---

### 💡 Tips:

- `EXTRACT(YEAR FROM date)` or any form of extraction is super useful when grouping time-based events.
- Make sure the date is in date format.
- Always sort your grouped results so the output tells a chronological story.

#SQLoftheDay #SQL #StrataScratch #MarketingAnalytics #DataAnalytics #DataCleaning #AnalyticsLearning #BusinessIntelligence
