## 💻 SQL of the Day: Highest Target Under Manager

🔗 <https://platform.stratascratch.com/coding/9905-highest-target-under-manager?code_type=1>

### Problem

Find the first name and target of the Salesforce employee with the highest target among those reporting to manager_id = 13.

---

### 🧠 SQL Solution

```sql
SELECT first_name, target
FROM salesforce_employees
WHERE target = (
    SELECT MAX(target)
    FROM salesforce_employees
    WHERE manager_id = 13
)
AND manager_id = 13;
```

---

### 🧩 Simple logic breakdown

- **Subquery finds the maximum target** `SELECT MAX(target) WHERE manager_id = 13` returns the single highest target value among all employees under this manager.
- **Outer query filters to that target** The `WHERE target = (...)` clause finds all employees whose target matches that maximum value.
- **Manager filter applied twice** Both the subquery and outer query filter by `manager_id = 13` to ensure we only look at the right team.
- **Returns all ties** If multiple employees share the highest target, this query returns all of them. A `LIMIT 1` approach would silently drop ties.

---

### 📊 This pattern tells you

- **Performance outliers** identifying top performers helps managers understand who is carrying the heaviest work and may need support.
- **Compensation equity** when multiple people tie for the highest target, HR can verify if compensation and recognition align with workload.
- **Team capacity planning** knowing the ceiling target helps set realistic expectations when onboarding new team members.

---

### 🎯 Key takeaways

- Use `MAX()` in a subquery to find the boundary value, then filter the main table to match that value. This preserves ties that `ORDER BY ... LIMIT 1` would discard.
- When filtering to a specific group (like a manager's team), apply the filter in both the subquery and outer query to avoid cross-contamination.
- `MAX()` is deterministic and clear. `LIMIT 1` without `ORDER BY` returns arbitrary rows. `ORDER BY` with `LIMIT 1` drops ties. The subquery pattern is the only way to capture all top performers.

# SQLoftheDay #SQL #StrataScratch #DataAnalytics #DataAnalyst #Subqueries #Salesforce #PerformanceManagement
