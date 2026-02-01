# Day 1: The Gatekeeper (Filtering & Sorting)

## Objective
The goal of Day 1 was to master data extraction and filtering. In a business context, this is about "Noise Reduction"—removing irrelevant data to focus on specific business segments.

## Key Concepts
- **SELECT/FROM**: Identifying relevant data sources and columns.
- **WHERE**: Filtering based on specific criteria (Geography, Value, Status).
- **LIKE & REGEXP**: Pattern matching for text data (e.g., finding specific email domains or naming conventions).
- **ORDER BY**: Sorting data to identify top/bottom performers.

## Practical Example: High-Value Confirmed Bookings
**Scenario:** A manager needs a list of all confirmed destination cities where the booking value exceeds $500, sorted alphabetically.

```sql
SELECT DISTINCT destination_city 
FROM Bookings 
WHERE payment_status = 'Confirmed' AND total_price > 500 
ORDER BY destination_city ASC;
