<!-- EXAMPLE: Delete this file after you understand the format. -->

## 💻 SQL of the Day: Top Cool Votes
🔗 https://platform.stratascratch.com/coding/10060-top-cool-votes?code_type=1

### Problem:
Find the **review text** that received the highest number of cool votes. Return the **business name** and the **review text**.

---

### 🧠 SQL Solution
```sql
WITH rank_list AS (
    SELECT
        business_name,
        review_text,
        cool,
        DENSE_RANK() OVER (ORDER BY cool DESC) AS rnk
    FROM yelp_reviews
)

SELECT
    business_name,
    review_text
FROM rank_list
WHERE rnk = 1;
```

---

### 🧩 Simple logic breakdown
- **Rank every review** by `cool` votes from highest to lowest using `DENSE_RANK()`
- **Ties share the same rank**: two reviews each with 10 cool votes both receive rank 1, not rank 1 and rank 2
- **Filter `rnk = 1`**: returns every review at the top, not one arbitrarily chosen row

---

### 📊 This pattern tells you:
- **Silent data loss is the most dangerous kind of bug**: `ROW_NUMBER()` here would run without error, return one result, and look completely correct. No warning. The tied rows disappear with no trace.
- **Content platforms depend on accurate "top" queries**: surfacing top-reviewed businesses with `ROW_NUMBER()` would silently exclude any restaurant, hotel, or café that earned the same score. Every tied result is a valid recommendation the product should be showing.
- **Two distinct problems look identical at first**: "find the maximum score" returns a single number; "find all rows with the maximum score" returns a set. Ranking functions solve the second correctly only when you choose the right one.

---

### 🎯 Key takeaways
1. Choosing the wrong ranking function silently removes valid data. No error, no warning: just an incomplete result set that passes every visual check.
2. The three functions handle ties differently. `ROW_NUMBER()` assigns a unique number to every row regardless of equal values (1, 2, 3, 4). `RANK()` allows ties but skips the following rank (1, 1, 3, 4). `DENSE_RANK()` allows ties with no gaps (1, 1, 2, 3). When the goal is "return all rows tied for the top," only `DENSE_RANK()` is correct.
3. There is a simpler alternative for a flat maximum: `WHERE cool = (SELECT MAX(cool) FROM yelp_reviews)` retrieves all top rows without a CTE or ranking function. Use ranking when you need top-N across groups or partitions. Use a subquery when you need the single global maximum.

#SQLoftheDay #SQL #StrataScratch #DataAnalytics #DataAnalyst #WindowFunctions #Ranking #Yelp
