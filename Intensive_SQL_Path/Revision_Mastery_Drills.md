# Revision & Mastery: Strengthening the Foundation

## Objective
Before moving into Advanced Query Architecture (Day 4), I dedicated a session to mastering the logical nuances of SQL. The focus was on eliminating common syntax "traps," refining multi-table joins, and ensuring 100% accuracy in data types and aggregation logic.

---

## Mastery Drill 1: Warehouse Audit (Filtering Logic)
**Scenario:** Identify high-volume stock locations while excluding damaged goods.
**Key Mastery:** Correctly distinguishing between row-level filters (`WHERE`) and aggregate filters (`HAVING`).

```sql
SELECT 
    warehouse_location, 
    SUM(quantity_in_stock) AS total_quantity
FROM Inventory
WHERE warehouse_location != 'Damaged'  
GROUP BY warehouse_location
HAVING SUM(quantity_in_stock) > 500;   
```

##  Mastery Drill 2: YouTube Analytics (Multi-Condition Patterns)

Scenario: Analyzing average performance across specific video categories.
Key Mastery: Using NOT IN for clean exclusions.
``` SQL

SELECT 
    category, 
    AVG(views) AS avg_views
FROM Videos
WHERE category NOT IN ('Spam', 'Private')
GROUP BY category 
HAVING AVG(views) > 10000;
```

The "Basics Graduation" Challenge: Spotify Case Study

Scenario: A complex request requiring a JOIN, multiple filters, and specific sorting to find top-performing artists.
```SQL

SELECT 
    a.artist_name, 
    COUNT(al.album_id) AS total_albums
FROM Artists AS a
JOIN Albums AS al ON a.artist_id = al.artist_id
WHERE a.artist_name != 'Unknown' 
  AND al.release_year > 2010
GROUP BY a.artist_name
HAVING COUNT(al.album_id) > 5
ORDER BY total_albums DESC;
```

Analyst’s Log: The "Why" Behind the Math
Topic: COUNT vs. SUM for Primary Keys

During this mastery session, I refined my understanding of Quantitative vs. Qualitative data.

The Insight:
When analyzing IDs (like album_id), we must use COUNT instead of SUM.

    The Reason: IDs are labels (Primary Keys), not measures of value. SUM(101 + 102) would result in 203, which is mathematically meaningless. COUNT(101, 102) results in 2, which accurately represents the volume of records.

Business Application:
I use SUM for revenue, cost, or time-played. I use COUNT for volume, frequency, and transaction totals. This ensures that the reports I provide to stakeholders are logically sound and provide a "Single Source of Truth."
