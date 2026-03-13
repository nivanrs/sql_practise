## 💻 SQL of the Day: Percentage of Shipable Orders
🔗 https://platform.stratascratch.com/coding/10090-find-the-percentage-of-shipable-orders?code_type=1

### Problem:
Find the percentage of shipable orders. Consider an order is shipable if the customer's address is known. Output the percentage of shipable orders.

---

### 🧠 SQL Solution
```sql
SELECT
    AVG((address IS NOT NULL)::INT) * 100 AS percent_shipable
FROM orders
INNER JOIN customers
    ON customers.id = orders.cust_id;
```

---

### 🧩 Simple logic breakdown
- **JOIN `orders` with `customers`**: this associates every order with the customer's stored address details
- **`address IS NOT NULL`**: evaluates to a boolean (`true` or `false`) based on whether the address is valid
- **`::INT`**: casts the boolean result to an integer (`1` or `0`)
- **`AVG(...) * 100`**: computes the ratio of valid addresses to the total number of orders, automatically returning the exact percentage

---

### 📊 This pattern tells you:
- **Validating delivery inputs:** establishing logic that checks for a complete and valid address before dispatching shipments is essential for efficient logistics.
- **Cost reduction:** verifying shippability upfront streamlines operations and prevents sunk costs associated with undeliverable packages.

---

### 🎯 Key takeaways
1. Pay close attention to exactly what must be calculated. Choosing between `COUNT()`, `SUM(CASE WHEN ...)` and `AVG()` depends entirely on your objective and each approach serves a distinct purpose.
2. The `AVG(boolean::INT)` trick is an elegant shorthand for calculating percentages without manually dividing two separate `COUNT` functions.
3. An alternative approach using `LEFT JOIN` alongside `COUNT(c.address) * 100.0 / COUNT(*)` achieves the same result by implicitly dropping nulls in the numerator.

#SQLoftheDay #SQL #StrataScratch #DataAnalytics #DataAnalyst #SupplyChainAnalytics #DataScience
