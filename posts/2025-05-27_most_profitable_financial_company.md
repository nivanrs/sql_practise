## 💻 SQL of the Day: Most Profitable Financial Company in the World (and by Continent)

Today's challenge comes from the Forbes Global 2010–2014 dataset. The goal is to find the most profitable financial company in the world.

📊 Global and Regional Profit Leaders in the Financial Sector

🔗 https://lnkd.in/ge_2KJBz

---

### 🧠 Solution (Global Leader Only):

```sql
select company, continent
from forbes_global_2010_2014
where sector = 'Financials'
  and rank = 1;
```

---

### 🌍 If you want to rank within each continent:

```sql
with ranked_financials as (
  select
    company,
    continent,
    row_number() over (
      partition by continent
      order by profits desc
    ) as continent_rank
  from forbes_global_2010_2014
  where sector = 'Financials'
)
select company, continent, continent_rank
from ranked_financials
where continent_rank = 1;
```

---

### 💡 Tips:

Always explore a few rows of the dataset before jumping into the query — it helps you understand the structure and spot things like existing rank columns or ordering assumptions.

---

### 🎯 Why this matters:

Profitability by continent is an interesting angle, because each region has different internal and external factors (financial infrastructure, regulation, etc.) that influence how profitable financial companies can be. Comparing top performers globally vs. regionally can become a base strategy to win the market.

#SQLoftheDay #SQL #StrataScratch #DataAnalysis #BusinessIntelligence #BusinessAnalytics #FinancialAnalytics #LearningByDoing #PracticeToProgress #DataAnalytics #FinancialSector #SQLTips
