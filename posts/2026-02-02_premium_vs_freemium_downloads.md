## 💻 SQL of the Day: Premium vs Freemium Downloads

🔗 https://lnkd.in/gp-CQzWH

### Problem:

Find the total number of downloads for paying and non-paying users by date.
Only include dates where non-paying users downloaded more than paying users.

---

### SQL Solution

```sql
with raw as (
  select
    df.date,
    df.downloads,
    ad.paying_customer
  from ms_download_facts df
  join ms_user_dimension ud on df.user_id = ud.user_id
  join ms_acc_dimension ad on ad.acc_id = ud.acc_id
)
select
  date,
  sum(case when paying_customer = 'no' then downloads end) as non_paying,
  sum(case when paying_customer = 'yes' then downloads end) as paying
from raw
group by date
having sum(case when paying_customer = 'no' then downloads end)
     > sum(case when paying_customer = 'yes' then downloads end)
order by date;
```

---

### 🧩 Simple logic breakdown

- **Combine all tables** — Join fact and dimension tables to get downloads and payment status in one dataset.
- **Separate paying vs non-paying users** — Use `case when` to identify each group.
- **Aggregate by date** — Use `sum()` because we are grouping daily downloads.
- **Filter with having** — Keep only dates where non-paying downloads exceed paying downloads. `HAVING` is used when filtering after aggregation, not before.

---

### 📊 This pattern tells you:

- Your free tier has strong engagement
- But you might be leaving conversion opportunities on the table
- Your pricing could be misaligned with user behavior
- Consider what's stopping free users from converting (price point? perceived value? timing?)

---

### 🎯 Key takeaways

- Understanding the table structure and relationships is critical before writing joins.
- This analysis helps monitor customer behavior, especially freemium usage patterns.
- Daily comparisons like this are useful for conversion analysis, product strategy, and pricing decisions.

#SQLoftheDay #SQL #StrataScratch #DataAnalytics #CustomerAnalytics #Freemium #ProductAnalytics #BusinessIntelligence
