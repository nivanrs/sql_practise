## 🎬 SQL of the Day: Find the Genre of the Person with the Most Oscar Wins

🔗 [StrataScratch Problem #10171](https://platform.stratascratch.com/coding/10171-find-the-genre-of-the-person-with-the-most-number-of-oscar-winnings/solutions?code_type=1)

### ❓ Problem:

Find the genre(s) of the person who won the most Oscars.

---

### 🧠 SQL Solution

```sql
with winner as (
  select *
  from oscar_nominees a
  join nominee_information b
    on a.nominee = b.name
  where a.winner is true
),

actors as (
  select nominee, count(*)
  from winner
  group by nominee
  order by count(*) desc
)

select top_genre
from winner
where name = (select nominee from actors limit 1)
limit 1;
```

---

### 🔍 Step-by-step Explanation

#### Step 1: Identify where the winners are

We find that the winners are stored in the `oscar_nominees` table, using a `winner = true` condition.

#### Step 2: Join to get genre info

We need to join with `nominee_information` because `oscar_nominees` alone doesn’t include the genre. This join allows us to retrieve the `top_genre` field.

#### Step 3: Count nominee wins

In the `actors` CTE, we group by `nominee` and count how many times each nominee has won.

#### Step 4: Get the top nominee

Using a `LIMIT 1` on the sorted result, we select the nominee with the most wins.

#### Step 5: Final filter by nominee

We filter the joined dataset to only include the top winner and return their genre.

---

### ⚠️ What can go wrong:

- **Join key mismatch**: The key `a.nominee = b.name` assumes perfect name matching. Real data often has inconsistencies (e.g., "Johnny Deep" vs. "Johnny Depp").
- **Wrong join type**: Using an improper join (e.g., left join when inner join is needed) could result in null values or incorrect filtering.

---

### 🎯 Why this matters:

This kind of logic is useful for linking information across tables when datasets aren't normalized. It’s often seen in awards, competition results, or leaderboards, and it’s very relevant in Indonesian entertainment data — like identifying top film genres of the most awarded FFI actors or festival winners.

---

\#SQLoftheDay #DataCleaning #StrataScratch #SQLPractice #Joins #DataQuality #CTE #EntertainmentAnalytics #LearningByDoing #IndonesiaData #PracticeToProgress
