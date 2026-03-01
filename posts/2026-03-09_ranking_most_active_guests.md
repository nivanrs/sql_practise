## 💻 SQL of the Day: Ranking Most Active Guests

🔗 https://platform.stratascratch.com/coding/10159-ranking-most-active-guests?code_type=1

### Problem:

Rank guests based on the total number of messages they've sent. Guests with the same total should receive the same rank. Output the rank, guest ID, and total number of messages.

---

### SQL Solution

```sql
SELECT

    DENSE_RANK() OVER (ORDER BY SUM(n_messages) DESC) AS ranking,
    id_guest,
    SUM(n_messages) AS sum_n_messages

FROM airbnb_contacts
GROUP BY id_guest
ORDER BY 3 DESC;
```

---

### 🧩 Simple logic breakdown

- **Aggregate first**: use `GROUP BY id_guest` and `SUM(n_messages)` to get the total messages per guest across all contacts.
- **Rank over the aggregate**: apply `DENSE_RANK()` on top of `SUM(n_messages) DESC` so guests are ranked from most to least active.
- **Same score = same rank, no gaps**: if two guests have the same total, they share one rank and the next rank follows immediately (e.g., 1, 1, 2, 3 and not 1, 1, 3, 4).

---

### 📊 This pattern tells you:

- **Who your power users are**: identify the most engaged guests on the platform by their messaging activity.
- **How to reward or target top users**: a consistent leaderboard without arbitrary gaps is fairer for programs like loyalty tiers or featured-host badges.
- **Where engagement is concentrated**: a steep drop-off in ranking quickly reveals if activity is dominated by a small group of guests.

---

### 🎯 Key takeaways

- Know the difference between the three ranking functions, choosing the wrong one changes your output:
  - `ROW_NUMBER()`: always unique, no ties (1, 2, 3, 4). Use when you need one winner per row regardless of equal values.
  - `RANK()`: ties get the same rank, but the next rank skips (1, 1, 3, 4). Use when gaps matter, e.g., "two guests tied for 1st, so no one is 2nd".
  - `DENSE_RANK()`: ties get the same rank, no gaps (1, 1, 2, 3). Use when you want a clean, continuous leaderboard.
- For leaderboards and active-user rankings, `DENSE_RANK()` is almost always the right choice because ties are expected and gaps feel wrong.
- Window functions like `DENSE_RANK()` can reference aggregated values (`SUM`) as long as the aggregation is resolved first in a `GROUP BY`.

#SQLoftheDay #SQL #StrataScratch #DataAnalytics #DataAnalyst #WindowFunctions #Ranking #Airbnb
