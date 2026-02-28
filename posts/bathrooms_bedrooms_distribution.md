## 💻 SQL of the Day: Bathrooms & Bedrooms Distribution

A quick dive into comparing average vs. median listing sizes by city and property type.

🔗 https://lnkd.in/g2-mafh5

> "For each city and property type, what are the average numbers of bathrooms and bedrooms?"

---

### 🧠 Solution:

```sql
select
  city,
  property_type,
  avg(bathrooms) as avg_bathrooms,
  avg(bedrooms) as avg_bedrooms
from airbnb_search_details
group by city, property_type;
```

---

### ✅ What it does:

Calculates the mean (`avg`) for bathrooms and bedrooms per city and property type.

---

### 💡 Tip:

- Averages are easy to compute but can be skewed by outliers (e.g., a few luxury villas).
- Whenever you need a robust central value, pair `avg()` with a median approach using `percentile_cont(0.5)`.
- You can also add other percentiles like P25 and P75 to better grasp the distribution.

---

### 🎯 Why this matters:

Average metrics give quick benchmarks for listing sizes and are often useful for high-level reporting and trend spotting. Just be aware of skew and consider more resilient measures when precision matters or the consumers of the data need more precision.

#SQLoftheDay #SQL #OperationAnalyst #BusinessIntelligence #DataAnalysis #PracticeToProgress #LearningByDoing #AnalyticsTips
