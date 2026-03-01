## 💻 SQL of the Day: Finding Returning Users

🔗 https://lnkd.in/gJBXjHi3

### Problem:

Identify users who made a second purchase within 1 to 7 days after their first purchase.
Ignore same-day purchases.

---

### SQL Solution

```sql
with ranked_purchases as (
  select
    user_id,
    created_at,
    row_number() over (
      partition by user_id
      order by created_at
    ) as rn
  from amazon_transactions
),
first_second_order as (
  select
    user_id,
    max(case when rn = 1 then created_at end) as first_purchase,
    max(case when rn = 2 then created_at end) as second_purchase
  from ranked_purchases
  group by user_id
)
select user_id
from first_second_order
where second_purchase is not null
  and second_purchase - first_purchase between 1 and 7;
```

---

### 🧩 Simple logic breakdown

- **Rank purchases per user** — Use `row_number()` to order purchases chronologically for each user.
- **Extract first and second purchase** — Use `case when` to mark the first and second purchase. `max()` is used to safely return the non-null timestamp per user.
- **Filter returning users** — Keep users where:
  a. a second purchase exists
  b. the second purchase happens 1–7 days after the first

---

### 🎯 Key takeaways

- First vs second purchase timing tells a lot about product price and buying behavior (short gaps usually indicate lower-cost or repeat-friendly products).
- This logic is very useful for:
  - Customer loyalty analysis
  - Measuring campaign success
  - Evaluating new user activation

#SQLoftheDay #SQL #StrataScratch #CustomerAnalytics #MarketingAnalytics #DataAnalyst #DataAnalytics
