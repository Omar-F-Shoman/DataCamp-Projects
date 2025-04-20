# Motorcycle Parts Sales Analysis

## Project Description
A company specializing in motorcycle parts requested an analysis of their sales data.
The main goal was to calculate the **net revenue** for each product line, grouped by **month** and **warehouse**, focusing **only on Wholesale orders**.

The data was provided in a table named `sales`, containing columns such as order number, order date, warehouse name, client type, product line, quantity, unit price, payment method, and payment fee percentage.

## Objective
- Calculate the net revenue per product line for each month and warehouse.
- Filter the data to include only Wholesale orders.
- Present the results sorted by product line, month, and net revenue.

## Solution
The solution involved writing an SQL query that:
- Extracts the month from the order date and converts it into the month name (June, July, August).
- Calculates net revenue by subtracting the sum of payment fees from the sum of total sales.
- Filters the data to include only Wholesale client types.
- Groups the results by product line, month, and warehouse.
- Sorts the output by product line, month, and net revenue in descending order.

### Main Query:
```sql
SELECT 
    product_line,
    CASE 
        WHEN EXTRACT(MONTH FROM date) = 6 THEN 'June'
        WHEN EXTRACT(MONTH FROM date) = 7 THEN 'July'
        WHEN EXTRACT(MONTH FROM date) = 8 THEN 'August'
    END AS month,
    warehouse,
    SUM(total) - SUM(payment_fee) AS net_revenue
FROM sales
WHERE client_type = 'Wholesale'
GROUP BY product_line, month, warehouse
ORDER BY product_line, month, net_revenue DESC;
```

### Alternative Query:
```sql
SELECT 
    product_line,
    TRIM(TO_CHAR(date, 'Month')) AS month,
    warehouse,
    SUM(total) - SUM(payment_fee) AS net_revenue
FROM sales
WHERE client_type = 'Wholesale'
    AND EXTRACT(MONTH FROM date) IN (6, 7, 8)
GROUP BY product_line, TO_CHAR(date, 'Month'), warehouse
ORDER BY product_line, TO_CHAR(date, 'Month'), net_revenue DESC;
```

## SQL Techniques Used
`SELECT` | `CASE` | `EXTRACT` | `SUM` | `WHERE` | `GROUP BY` | `ORDER BY` | `TRIM` | `TO_CHAR`

## Tech Stack
- SQL
