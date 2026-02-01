# Day 2: The Accountant (Aggregations & Grouping)

##  Objective
Transitioning from individual records to "The Big Picture." Day 2 focused on summarizing millions of rows into key performance indicators (KPIs) like Total Revenue, Average Order Value, and Profit Margins.

##  SQL Concepts Mastered
- **Aggregates**: `SUM()`, `AVG()`, `COUNT()`, `MIN/MAX()` for performance tracking.
- **GROUP BY**: Creating "buckets" of data to compare different business segments (e.g., Sales by Category).
- **HAVING**: Filtering calculated results—essential for identifying segments that meet specific performance thresholds.

## Business Scenario: Scooter Rental Profitability (EcoDrive)
**The Request:** "Profit margins are shrinking. Identify cities where maintenance costs are exceptionally high relative to the revenue generated."

### The Solution:
```sql
SELECT 
    city, 
    SUM(rental_revenue) AS total_revenue, 
    SUM(maintenance_cost) AS total_cost,
    (SUM(rental_revenue) - SUM(maintenance_cost)) AS net_profit
FROM Scooter_Logs
GROUP BY city
HAVING SUM(maintenance_cost) > 500
ORDER BY net_profit ASC;
