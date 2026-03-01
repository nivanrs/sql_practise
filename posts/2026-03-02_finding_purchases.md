## 💻 SQL of the Day: Finding Purchases

🔗 https://platform.stratascratch.com/coding/10553-finding-purchases?code_type=1

### Problem:

Identify users who made a repeat purchase within 1 to 7 days of any previous purchase.
Ignore same-day purchases.

---

### SQL Solution

```sql
WITH transactions AS (
    SELECT
        user_id,
        created_at,
        LAG(created_at) OVER (
            PARTITION BY user_id
            ORDER BY created_at
        ) AS prev_date
    FROM amazon_transactions
)
SELECT DISTINCT user_id
FROM transactions
WHERE prev_date IS NOT NULL
  AND created_at - prev_date BETWEEN 1 AND 7;
```

---

### 🧩 Simple logic breakdown

- **Use Window Function** — Select `user_id` and `created_at`, then use the `LAG()` window function to fetch the previous purchase date (`prev_date`) for each user based on chronological order.
- **Filter Date Range** — Keep rows where `prev_date` is not null and the gap between `created_at` and `prev_date` is exactly 1 to 7 days.
- **Ignore Same-day Purchases** — A gap of 0 days is explicitly excluded by the `BETWEEN 1 AND 7` condition.

---

### 📊 This pattern tells you:

- **Who are repeat purchasers** — Spot users who show strong short-term loyalty.
- **Customer behavior trends** — Understand the natural buying frequency and returning behavior of the customer base.
- **When to launch a campaign** — If this consistent returning behavior suddenly drops, it might be the perfect trigger to launch a re-engagement campaign.

---

### 🎯 Key takeaways

- `LAG()` is highly effective for row-to-row comparisons (like finding time gaps) and is computationally cleaner than a self-join.
- Using `DISTINCT` ensures users aren't counted multiple times if they had several 1-7 day re-purchase events.
- Window functions paired with date arithmetic are the backbone of time-series event analysis.

#SQLoftheDay #SQL #StrataScratch #DataAnalytics #DataAnalyst #CustomerBehavior #Retention #BusinessIntelligence
