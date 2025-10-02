# Mastering-SQL-Joins

## INNER JOIN
### what it does: Returns only the rows where both tables have a match
#### Example: Show all customers with product names
SELECT
customer_name,
product_name
FROM customers_sales AS c 
INNER JOIN 
products_info AS p
ON c.product_id = p.product_id;

## LEFT JOIN
### Returns all rows from the first table(left), plus matches from the second. If no match you get null values.
#### Example: show all customers and the products they attempted to purchase
SELECT 
customer_name,
product_name
FROM customers_sales
LEFT JOIN 
products_info USING (product_id);

## RIGHT JOIN
### What it does: Returns all rows from the second  table(right), plus matches from the first.
#### Example: show all products, even if nobody bought them.
SELECT 
customer_name,
product_name
FROM products_info 
RIGHT JOIN 
customers_sales USING (product_id);

# FULL OUTER JOIN/ FULL JOIN
### What it does: combines LEFT and RIGHT. You get everything from both tables with NULLs where matches dont exist. 
#### Example: Show all customers and products purchased, whether matched or not
SELECT 
customer_name,
product_name
FROM customers_sales
FULL JOIN 
products_info USING (product_id)
ORDER BY product_name;

# CROSS JOIN
### What it does: Creates every possible combination of rows between the two tables.
#### Example: Every customer matched with every product they purchased. Can be dangerous if tables are large.
SELECT 
    c.customer_name,
    p.product_name
FROM customers_sales c
CROSS JOIN products_info p;

# NATURAL JOIN
#### What it does: Joins automatically based on columns with same name.
### Example: If two tables have product_id, it will join on that without you writing the condition
SELECT *
FROM customers_sales
NATURAL JOIN products_info;

# STRAIGHT JOIN (MySQL specific) 
#### What it does: Like INNER JOIN but forces the optimizer to read the tables in the order given. Useful in rare cases for performance tuning
SELECT
    c.customer_name,
    p.product_name
FROM customers_sales c
STRAIGHT_JOIN products_info AS  p
ON c.product_id = p.product_id;

# SELF JOIN
#### What it does: a table joins with itself.
### Find customers who bought the same product on different dates.

# UNION
#### What it does:It combines results of two queries and removes duplicates.
### Example: Combine sales IDSs from customer sales and product info table.
SELECT sale_id,
customer_name
FROM customers_sales
UNION
SELECT product_id,
product_name
FROM products_info;

# UNION ALL
#### What it does: Same as UNION, but keeps duplicates. Faster because it doesnt check uniqueness.
SELECT sale_id,
customer_name
FROM customers_sales
UNION ALL
SELECT product_id,
product_name
FROM products_info;








