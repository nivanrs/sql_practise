## 💻 SQL of the Day: Spam Posts
🔗 https://platform.stratascratch.com/coding/10134-spam-posts?code_type=1

### Problem:
Calculate the spam share for each day. The spam share is the percentage of posts flagged as spam (posts whose keywords contain the word 'spam') out of all posts viewed that day. Output the post date and the spam share, rounded to two decimal places.

---

### 🧠 SQL Solution
```sql
SELECT
    post_date,
    100 * COUNT(DISTINCT CASE WHEN a.post_keywords LIKE '%spam%' THEN a.post_id END)::FLOAT
        / COUNT(DISTINCT a.post_id) AS spam_share
FROM facebook_posts a
JOIN facebook_post_views b ON a.post_id = b.post_id
GROUP BY post_date;
```

---

### 🧩 Simple logic breakdown
- **JOIN** `facebook_posts` with `facebook_post_views` on `post_id`: this brings in the view data so we only count posts that were actually seen
- **GROUP BY post_date**: collapses every row into one bucket per day, so the result is one rate per date
- **CASE WHEN ... LIKE '%spam%'**: filters only spam-flagged posts; non-spam rows return `NULL`, which `COUNT` silently skips
- **COUNT(DISTINCT spam posts) / COUNT(DISTINCT all posts)**: the ratio of spam posts to total posts, multiplied by 100 to express as a percentage
- **::FLOAT**: casts the numerator to avoid integer division, which would truncate every result to 0

---

### 📊 This pattern tells you:
- **Platform health over time:** a rising spam share signals a degrading content ecosystem before user complaints surface. Teams can track this metric daily and trigger moderation alerts when it crosses a threshold.
- **Labeling at scale:** the `LIKE '%spam%'` keyword flag is a rule-based label. In practice, these labels feed machine learning classifiers that catch spam without explicit keywords. SQL gives you the denominator and ground-truth rate the model needs to evaluate precision and recall.
- **Where data analytics meets data science:** the analyst produces this rate; the data scientist trains a model on it. Neither can work without the other.

---

### 🎯 Key takeaways
1. `COUNT(DISTINCT CASE WHEN condition THEN col END)` is the go-to pattern for conditional distinct counting. It counts only the rows that pass the condition and deduplicates them in one step.
2. Know when to use `COUNT`, `SUM`, and `AVG`. `COUNT(DISTINCT ...)` counts unique entities. `SUM(CASE WHEN ... THEN 1 ELSE 0 END)` counts occurrences including duplicates. `AVG` computes a mean across rows, not a ratio you control. For a custom percentage, build the ratio explicitly with `COUNT / COUNT`.
3. Cast before you divide. Integer division in SQL truncates toward zero: `1 / 100 = 0`, not `0.01`. Casting one operand to `FLOAT` or `NUMERIC` before the division preserves the decimal.
4. `LIKE '%spam%'` is a contains-check, not an exact match. The leading `%` means the word can appear anywhere in the string, making this robust to multi-keyword fields.

#SQLoftheDay #SQL #StrataScratch #DataAnalytics #DataAnalyst #SpamDetection #ConditionalCounting #DataScience
