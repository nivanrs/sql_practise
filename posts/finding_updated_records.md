## 💻 SQL of the Day: Finding Updated Records

🔗 https://lnkd.in/gSmuPbFN

This SQL problem is a reminder that not all datasets are clean. In this case, we have multiple records for the same employee with different salary values.

### ❓ Problem:

Return each employee's latest salary, stated to be the highest salary for each employee.

---

### 🧠 Solution:

```sql
select
  id,
  first_name,
  last_name,
  department_id,
  max(salary) as latest_salary
from ms_employee_salary
group by id, first_name, last_name, department_id
order by id;
```

---

### 💡 Tip:

This kind of table is not ideal. Here, we're missing clear indicators of when records were added or updated (like a timestamp), which makes it hard to track changes properly.

If the table had a `created_at` or `updated_at` column, we could write a much more accurate query using `ROW_NUMBER()` or `RANK()` over that timestamp.

---

### 🎯 Why this matters:

Most of the time, we will work with imperfect data and missing data models. Learning how to extract the correct value using aggregates or window functions is crucial in every business domain (HR, finance, marketing, or operation analysis).

#SQLoftheDay #SQL #StrataScratch #MarketingAnalytics #DataAnalytics #DataCleaning #AnalyticsLearning #PracticeToProgress #BusinessIntelligence #LearningByDoing
