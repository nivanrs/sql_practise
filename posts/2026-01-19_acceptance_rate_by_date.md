## 💻 SQL of the Day: Acceptance Rate by Date

🔗 https://lnkd.in/g-nAiJfF

### Problem:

Calculate the friend acceptance rate for each date when friend requests were sent.
Only include dates where at least one request was accepted.

---

### SQL Solution

**Approach 1: Explicit sent vs accepted logic**

```sql
with sent as (
  select date, user_id_sender, user_id_receiver
  from fb_friend_requests
  where action = 'sent'
),
accepted as (
  select user_id_sender, user_id_receiver
  from fb_friend_requests
  where action = 'accepted'
)
select
  s.date,
  count(a.user_id_sender)::float / count(*) as acceptance_rate
from sent s
left join accepted a
  on s.user_id_sender = a.user_id_sender
  and s.user_id_receiver = a.user_id_receiver
group by s.date
having count(a.user_id_sender) > 0
order by s.date;
```

**Approach 2: Using window function (lead)**

```sql
with lst as (
  select
    date,
    action,
    lead(action) over (
      partition by user_id_sender, user_id_receiver
      order by date
    ) as done
  from fb_friend_requests
)
select
  date,
  count(done) * 1.0 / count(action) as acceptance_rate
from lst
where action = 'sent'
group by date
having count(done) > 0
order by date;
```

---

### 🧩 Logic breakdown

**Approach 1**
- Split data into two logical sets: `sent` → all friend requests, `accepted` → requests that were accepted
- Join both sets by sender and receiver
- Acceptance rate = accepted requests / total sent requests per date
- Use `having` to keep only dates with at least one acceptance

**Approach 2**
- Keep all events in one table
- Use `lead()` to check whether a `sent` action is followed by an `accepted` action
- Group by send date and calculate acceptance rate
- This works because acceptance always comes after a request

---

### 🎯 Key takeaways

- The same metric can be computed in multiple ways. As long as the output is the same, it's still correct.
- Explicit joins are easier to understand and debug.
- Window functions are powerful when event order matters.
- Details in business logic matter — acceptance may happen days after the request.
- This kind of logic appears frequently in funnel analysis, conversion tracking, and product analytics.

#SQLoftheDay #SQL #StrataScratch #ProductAnalytics #FunnelAnalysis #MarketingAnalytics #DataAnalyst #DataAnalytics
