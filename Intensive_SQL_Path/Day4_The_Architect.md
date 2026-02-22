# Day 4: The Architect (CTEs & Subqueries)

##  Objective
As data requests become more complex, writing "Spaghetti Code" is no longer an option. Day 4 focused on **Query Architecture**—breaking complex business problems into logical, readable steps using Common Table Expressions (CTEs) and Subqueries.

## SQL Concepts Mastered
- **Subqueries**: Writing "internal" queries to calculate global benchmarks (like company averages) to use as filters.
- **CTEs (WITH Statements)**: Creating temporary result sets to organize code into a step-by-step narrative.
- **Data Pipelines**: Learning to aggregate data in one step and filter/join it in the next.

---

##  Featured Project: HackerRank "Top Earners"
**Business Challenge:** Identify the maximum possible earnings in the company and calculate how many employees have reached that "ceiling."

### The Solution:
```sql
SELECT (salary * months) AS earnings, COUNT(*)
FROM Employee
WHERE (salary * months) = (SELECT MAX(salary * months) FROM Employee)
GROUP BY earnings;
```

---

### Business Scenario: Spotify Churn (Legacy User Analysis)

Scenario: Identify "Legacy" users who have 0 minutes of streaming time but an account age higher than the company average.

Analytical Approach:

    Use a LEFT JOIN to find the gap (users with no streaming history).

    Use a Subquery to calculate the average account age across the entire database.

    Use a CTE to keep the code clean and maintainable for remote teams.

---

### Analyst’s Logic: Readability is Reliability

In a remote international team, my code is my primary form of communication.

The Insight:
While a complex problem can often be solved with a single, nested subquery, I prioritize CTEs. CTEs allow my teammates in different time zones to debug my logic step-by-step. If they can't read my code, they can't trust my data.

    
