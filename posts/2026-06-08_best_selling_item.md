## 💻 SQL of the Day: Best Selling Item
🔗 https://platform.stratascratch.com/coding/10172-best-selling-item?code_type=1 — StrataScratch #10172

### Problem:
Find the best-selling item for each month (no need to separate months by year) where the biggest total invoice amount was paid. Output the month, item description, and total paid.

---

### 🧠 SQL Solution
```sql
with raw as (
    select
        extract(month from invoicedate) as month,
        description,
        unitprice * quantity as total_paid
    from online_retail
    where quantity > 0
),

agg as (
    select
        month,
        description,
        sum(total_paid) as total_paid
    from raw
    group by month, description
),

ranked as (
    select
        month,
        description,
        total_paid,
        rank() over (partition by month order by total_paid desc) as rnk
    from agg
)

select month, description, total_paid
from ranked
where rnk = 1;
```

---

### 🧩 Simple logic breakdown
- `WHERE quantity > 0` removes returns. The dataset stores refunds as negative quantities. Without this filter, a heavily-returned item can rank first by revenue magnitude.
- `unitprice * quantity` computes revenue per transaction row.
- `SUM(total_paid)` aggregates to total revenue per item per month.
- `RANK()` assigns position 1 to the highest-revenue item each month and preserves ties — two items with identical revenue both get rank 1.
- `WHERE rnk = 1` returns the monthly winner, or winners if tied.

---

### 📊 This pattern tells you:
- Which items peak in specific months, useful for inventory planning and pre-ordering stock before demand arrives.
- Where discounts waste margin: if an item is already the month's top seller, a promotion reduces margin without adding demand.
- A baseline for seasonal product strategy: items that consistently top the chart vs. those that spike once and disappear.

---

### 🎯 Key takeaways
1. Define "best-selling" before writing the query. Revenue and units sold can return completely different winners. Both queries are technically correct. The business question determines which metric you need.
2. `WHERE quantity > 0` is not a convenience filter. It removes returns. In transactional datasets, negative quantities are refunds. Without it, a heavily-returned item can rank first by revenue magnitude.
3. `RANK()` preserves ties. `ORDER BY ... LIMIT 1` picks one row arbitrarily when two items tie. The report looks complete. It is not.

#SQLoftheDay #SQL #StrataScratch #DataAnalytics #WindowFunctions #Ranking #RetailAnalytics
