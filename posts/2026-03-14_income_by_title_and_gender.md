## 💻 SQL of the Day: Income By Title and Gender
🔗 https://platform.stratascratch.com/coding/10077-income-by-title-and-gender?code_type=1
### Problem:
Find the average total compensation based on employee titles and gender. Total compensation is calculated by adding both the salary and bonus of each employee. However, not every employee receives a bonus so disregard employees without bonuses in your calculation. Employees can receive more than one bonus.
Output the employee title, gender (i.e., sex), along with the average total compensation.
---
### 🧠 SQL Solution
```sql
WITH cte_total_bonus AS (
    SELECT
        worker_ref_id,
        SUM(bonus) AS total_bonus
    FROM sf_bonus
    GROUP BY worker_ref_id
)
SELECT
    e.employee_title,
    e.sex,
    AVG(e.salary + b.total_bonus) AS average_compensation
FROM sf_employee e
INNER JOIN cte_total_bonus b
    ON e.id = b.worker_ref_id
GROUP BY 1, 2;
```
---
### 🧩 Simple logic breakdown
- Calculate the total bonus for each employee before joining tables
- Inner join the aggregated bonus data to filter out employees without bonuses
- Calculate the average compensation grouping by title and gender
---
### 📊 This pattern tells you:
- High-level average compensation figures for each role and gender
- To make the data actionable, you need to check minimum, maximum, and headcount per role
- You can query the full distribution across quartiles to get a better read on equity:
```sql
WITH employee_comp AS (
    SELECT
        e.id,
        e.employee_title,
        e.sex,
        e.salary + SUM(b.bonus) AS total_comp
    FROM sf_employee e
    JOIN sf_bonus b
        ON e.id = b.worker_ref_id
    GROUP BY e.id, e.employee_title, e.sex, e.salary
)
SELECT
    employee_title,
    sex,
    percentile_cont(0.25) WITHIN GROUP (ORDER BY total_comp) AS p25,
    percentile_cont(0.50) WITHIN GROUP (ORDER BY total_comp) AS median,
    percentile_cont(0.75) WITHIN GROUP (ORDER BY total_comp) AS p75
FROM employee_comp
GROUP BY 1, 2;
```
---
### 🎯 Key takeaways
1. Averages compress context. Always measure the full distribution.
2. Using quartiles (`percentile_cont()`) gives you a clearer view of actual compensation tiers.
3. Pay close attention to business rules, like excluding employees without bonuses, to shape the initial SQL logic.

#SQLoftheDay #SQL #StrataScratch #DataAnalytics #DataEngineering #PostgreSQL
