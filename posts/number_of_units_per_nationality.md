## 💻 SQL of the Day: Number of Units per Nationality

🔗 https://platform.stratascratch.com/coding/10156-number-of-units-per-nationality?code_type=1

### Problem:

Find the number of apartments per nationality that are owned by people under 30 years old.
Output the nationality along with the number of apartments, sorted by apartment count in ascending order.

---

### SQL Solution

```sql
SELECT
    a.nationality,
    COUNT(DISTINCT b.unit_id) AS apartment_count
FROM airbnb_hosts a
INNER JOIN airbnb_units b
    ON a.host_id = b.host_id
WHERE a.age < 30
    AND b.unit_type = 'Apartment'
GROUP BY a.nationality
ORDER BY 2;
```

---

### 🧩 Simple logic breakdown

- **Join the tables** — Combine `airbnb_hosts` (demographics) and `airbnb_units` (listings) on `host_id`. An `INNER JOIN` is used here because we only care about hosts who actually have listings — unmatched rows on either side are irrelevant.
- **Apply filters** — Narrow down to hosts under 30 (`age < 30`) and only apartment-type units (`unit_type = 'Apartment'`).
- **Group and count** — Group by `nationality` and count distinct `unit_id`s to avoid double-counting units that might appear in multiple rows.
- **Sort** — Order by apartment count ascending to surface the smallest groups first.

---

### 📊 This pattern tells you:

- **Who your supply comes from** — Understanding which demographics (e.g. nationality, age group) are most active as hosts reveals where supply is concentrated.
- **Segmentation is powerful** — Categorizing hosts by attributes like nationality lets you tailor outreach, onboarding, or support to the right groups.
- **Joins are the backbone of reporting** — Almost every real business question involves combining data from more than one table.

---

### 🎯 Key takeaways

- Use `INNER JOIN` when you only want rows with a match on both sides. Use `LEFT JOIN` when you need to preserve all rows from the left table even without a match.
- `COUNT(DISTINCT ...)` guards against inflated counts when one-to-many relationships exist between tables.
- Knowing which type of join to reach for (`INNER`, `LEFT`, `RIGHT`, `FULL`, `CROSS`) is a fundamental SQL skill that shapes the shape of your result set.

#SQLoftheDay #SQL #StrataScratch #DataAnalytics #DataAnalyst #Airbnb #JoinTypes #BusinessIntelligence
