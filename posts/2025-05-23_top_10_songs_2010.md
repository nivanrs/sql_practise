## 💻 SQL of the Day: Top 10 Songs of 2010

In this post, I explore a fun dataset (Billboard Top 100) from Spotify while practicing essential SQL skills like filtering, limiting, and understanding data structure.

🔗 https://lnkd.in/gx8QsGv2

> "Return the top 10 ranked songs for the year 2010 based on Billboard's year-end chart."

---

### 🧠 Solution:

```sql
select distinct year_rank, group_name, song_name
from billboard_top_100_year_end
where year = 2010
limit 10;
```

---

### ✅ Why this works:

- `DISTINCT` ensures we avoid duplicate rows.
- `LIMIT 10` gives the top 10 rows because the data is already sorted by `year_rank`.
- `WHERE year = 2010` filters the dataset to just one year.

---

### 🎯 Why this matters:

Ranking, filtering, and limiting can be found in almost every part of the business, not just in the music industry. Whether you're checking top products, most loyal users, or performance metrics, this pattern always shows up. To use it better, we need to look into the data first — so we can adjust our query based on the structure and the actual business needs.

#SQLoftheDay #SQL #StrataScratch #MusicAnalytics #DataAnalytics #MarketingAnalytics #BusinessIntelligence #LearningByDoing #PracticeToProgress #PostgreSQL #SQLTips
