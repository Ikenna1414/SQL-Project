Question 1: 
Find the restocking lead time for the most ordered product.

SQL Queries:
```SQL
SELECT name,
		total_ordered,
		restockingleadtime
FROM sales_report
ORDER BY  total_ordered DESC
```
Answer: 
The most ordered product is Ballpoint LED Light Pen which was ordered a total of 456 times. Its lead time is 11


Question 2: 
What is the average number of products ordered by each country
SQL Queries:
```SQL
SELECT country,
        AVG(orderedquantity)

FROM products JOIN all_sessions ON sku = productsku
GROUP BY country
ORDER BY AVG(orderedquantity) DESC
```
Answer:
Montenegro has the highest average


Question 3: 
From the top 5 most ordered products, identify the product with the least stock level
SQL Queries:
```SQL
SELECT name,
		stocklevel,
		orderedquantity

FROM (SELECT * 
FROM products 
ORDER BY orderedquantity DESC 
LIMIT 5)
ORDER BY stocklevel
```
Answer:
The product with the least stock level among the top 5 most ordered products is Kick Ball with a stock level of 723


Question 4: 

SQL Queries:

Answer:



Question 5: 
What is the average number of products ordered by each city
SQL Queries:
```SQL
SELECT city,

	   AVG(orderedquantity)

FROM products JOIN all_sessions ON sku = productsku
GROUP BY city
ORDER BY AVG(orderedquantity) DESC
```
Answer:
Council Bluffs has the highest average order volume.
