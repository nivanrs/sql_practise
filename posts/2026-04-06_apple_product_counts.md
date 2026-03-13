## 💻 SQL of the Day: Apple Product Counts
🔗 https://platform.stratascratch.com/coding/10141-apple-product-counts?code_type=1

### Problem:
Count the number of users who use Apple devices vs. total users per language. Assume Apple devices are: MacBook Pro, iPhone 5S, and iPad Air. Output the language, Apple device user count, and total user count, ordered by total users descending.

---

### SQL Solution
```sql
SELECT
    language,
    COUNT(DISTINCT CASE
        WHEN device IN ('macbook pro', 'iphone 5s', 'ipad air') THEN a.user_id
    END) AS apple_device_users,
    COUNT(DISTINCT a.user_id) AS total_users
FROM playbook_events a
JOIN playbook_users b ON a.user_id = b.user_id
GROUP BY language
ORDER BY 3 DESC;
```

---

### 🧩 Simple logic breakdown
- **JOIN** the two tables on `user_id`: `playbook_events` has the device, `playbook_users` has the language
- **CASE WHEN** inside `COUNT(DISTINCT ...)` acts as a filter. Apple device rows pass a `user_id`, other rows return `NULL`. `COUNT` ignores `NULL`.
- **COUNT(DISTINCT a.user_id)** counts every unique user regardless of device, giving the total per language
- **ORDER BY 3 DESC** sorts by total users so the most active language groups surface first

---

### 📊 This pattern tells you:
- **Device as a wealth proxy:** Apple device share is a rough signal of purchasing power per language community. Languages with high Apple penetration skew toward higher income markets.
- **Behavioral segmentation:** Users on laptops (MacBook Pro) vs. phones (iPhone) interact with products differently. This split can drive UX and feature prioritization.
- **Regional reach:** Language is a coarse proxy for geography. Stacking Apple share against total users reveals where localization effort would have the biggest ROI.

---

### 🎯 Key takeaways
1. `COUNT(DISTINCT CASE WHEN ... THEN col END)` is the pattern for conditional distinct counting. Other rows return `NULL`, which `COUNT` silently skips.
2. `COUNT(DISTINCT *)` does not exist. Always name the column: `COUNT(DISTINCT col)` deduplicates values, while `COUNT(*)` counts all rows.
3. `COUNT(CASE WHEN ... THEN col END)` and `SUM(CASE WHEN ... THEN 1 ELSE 0 END)` look similar but serve different purposes: the first counts distinct entities, the second counts occurrences.
4. `DISTINCT` inside an aggregate operates on the expression *before* grouping. `COUNT(DISTINCT a.user_id)` deduplicates `user_id` within each language bucket.

#SQLoftheDay #SQL #StrataScratch #DataAnalytics #DataAnalyst #ConditionalCounting #Apple #WindowFunctions
