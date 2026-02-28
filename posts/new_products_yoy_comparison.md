## 💻 SQL of the Day: New Products (Year-over-Year Comparison)

🔗 https://lnkd.in/gTZSM9E6

### Problem:

Calculate the net change in the number of products launched in 2020 compared to 2019 for each company.

*(Net difference = launches in 2020 − launches in 2019)*

---

### SQL Solution

**Approach 1: Simple aggregation**

```sql
select
  company_name,
  count(case when year = 2020 then product_name end)
  - count(case when year = 2019 then product_name end) as net_difference
from car_launches
where year in (2019, 2020)
group by company_name;
```

**Approach 2: Window function**

First, count products per company per year. Then compare year-over-year using `lag()`.

```sql
with yearly_counts as (
  select
    company_name,
    year,
    count(product_name) as launches
  from car_launches
  where year in (2019, 2020)
  group by company_name, year
)
select
  company_name,
  launches - lag(launches) over (
    partition by company_name
    order by year
  ) as net_difference
from yearly_counts;
```

---

### 🎯 Key takeaways

- **One problem can have multiple valid solutions.** The right approach depends on the data and your SQL skills.
- **Period comparison is a common business case.** It shows up in product, growth, and performance analysis.
- **Window functions are powerful.** They are reusable and scale well for future analysis.

#SQLoftheDay #SQL #StrataScratch #DataAnalytics #WindowFunctions #BusinessAnalytics
