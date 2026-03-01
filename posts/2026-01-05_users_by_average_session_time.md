## 💻 SQL of the Day: Users by Average Session Time

🔗 https://lnkd.in/gqRqDh5k

### Problem:

Calculate each user's average session time. A session is defined as the time between `page_load` and `page_exit` on the same day.

**Rules:**
- Each user has only one session per day
- If there are multiple events, use: latest `page_load` and earliest `page_exit`
- Only count sessions where `page_load` happens before `page_exit`

---

### SQL Solution

```sql
with sessions as (
  select
    user_id,
    date(timestamp) as session_date,
    max(case when action = 'page_load' then timestamp end) as page_load,
    min(case when action = 'page_exit' then timestamp end) as page_exit
  from facebook_web_log
  group by user_id, date(timestamp)
),
daily_session as (
  select
    user_id,
    session_date,
    case
      when page_exit > page_load
      then extract(epoch from (page_exit - page_load))
      else 0
    end as session_duration_seconds
  from sessions
)
select
  user_id,
  avg(session_duration_seconds) as average_session
from daily_session
group by user_id
having avg(session_duration_seconds) > 0;
```

---

### 🎯 Key takeaways

- Custom business logic and definitions are often used in real-world analytics. In this case, clearly understanding what a "session" means is critical before writing any query.
- Time-based analysis like this is common in product, marketing, and growth analytics.
- Session analysis helps us understand user engagement. Short sessions can signal user confusion, low relevance, or poor web UX. Monitoring this metric over time can also act as an early indicator that something might be wrong.

This is a good example of how SQL is not just about syntax, but about translating business rules into data logic.

#SQLoftheDay #SQL #StrataScratch #ProductAnalytics #DataAnalytics #MarketingAnalytics #CustomerAnalytics
