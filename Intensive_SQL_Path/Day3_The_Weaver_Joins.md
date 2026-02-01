# Day 3: The Weaver (Advanced JOINs & Gap Analysis)

##  Objective
In modern data architecture, information is distributed across multiple "normalized" tables to maintain efficiency. Day 3 was focused on mastering **JOINs**—the ability to weave these disparate data sources into a single, cohesive business story.

##  SQL Concepts Mastered
- **INNER JOIN**: Isolating overlapping data points where records exist in both tables.
- **LEFT JOIN (The Industry Standard)**: Retaining the integrity of the primary dataset while enriching it with secondary data. 
- **Non-Equi Joins**: Connecting tables using ranges (`BETWEEN`) instead of simple ID matches.
- **Aliases & Readability**: Implementing table nicknames (e.g., `FROM Table AS t`) to write professional, scalable code.
- **Null Logic**: Mastering the `IS NULL` operator to identify gaps in data (Gap Analysis).

---

## Featured Project: "The Report" (Non-Equi Join)
**Business Challenge:** The HR department needs a student performance report. However, names are sensitive data; they should only be visible for students with a Grade 8 or higher. Furthermore, the "Grades" are not linked by a specific ID but by a range of marks.
Table 1: Students (Name, Marks)
Table 2: Grades (Grade, Min_Mark, Max_Mark)

### The Solution:
```sql
SELECT 
    CASE WHEN g.Grade >= 8 THEN s.Name ELSE 'NULL' END AS Name, 
    g.Grade, 
    s.Marks
FROM Students AS s
JOIN Grades AS g ON s.Marks BETWEEN g.Min_Mark AND g.Max_Mark
ORDER BY 
    g.Grade DESC, 
    Name ASC, 
    s.Marks ASC;
```
Business Scenario: Netflix "Gap Analysis"

Scenario: The Marketing team wants to identify "Churned" users—people who exist in our system but currently do not have an active subscription.

Analytical Approach: Use a LEFT JOIN to keep all users, and a filter to find those where the subscription record is empty.
```SQL

SELECT u.user_name
FROM Users AS u
LEFT JOIN Subscriptions AS s ON u.user_id = s.user_id
WHERE s.subscription_id IS NULL;  -- Targeting the 'Gap'
```

