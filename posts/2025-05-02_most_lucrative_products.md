## 💻 SQL of the Day: Most Lucrative Products

Today's challenge: Find the top 5 most lucrative products in H1 2022.

🔗 https://lnkd.in/gm4F_yn3

> "Which products generated the highest total revenue between January 1, 2022 and June 30, 2022?"

---

### 🧠 Solution:

```sql
select
  product_id,
  sum(cost_in_dollars * units_sold) as total_revenue
from online_orders
where 1=1
  and date_sold >= date '2022-01-01'
  and date_sold <= date '2022-06-30'
group by product_id
order by total_revenue desc
limit 5;
```

---

### ✅ What it does:

- **Filters** (`WHERE 1=1 …`): narrows to orders sold in H1 2022.
- **Aggregates** (`SUM(cost_in_dollars * units_sold)`): computes total revenue per product.
- **Ranks** (`ORDER BY total_revenue DESC`): sorts from highest to lowest.
- **Limits** (`LIMIT 5`): shows only the top five products.

---

### 💡 Tip — `WHERE 1=1`:

Including `1=1` lets you append `AND` clauses dynamically (or just keep your static filters neat) without worrying about whether it's the first condition or not.

---

### 🎯 Why this matters:

Identifying your most profitable products over a key period helps drive inventory planning, marketing budgets, and strategic promotions. A simple aggregation like this can spotlight winners and inform where to focus next.

#SQLoftheDay #SQL #StrataScratch #RevenueAnalysis #BusinessIntelligence #EcommerceAnalytics #DataDriven #PracticeToProgress #LearningByDoing
