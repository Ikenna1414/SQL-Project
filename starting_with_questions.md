Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**
Answer:

The city with the most revenue is not available, but the next top 5 are Mountain View, San Francisco, Sunnyvale, Palo Alto and New York

The top 6 countries with most revenue are United States, United Kingdom, Canada, India, and Italy

SQL Queries:

Query for country from where the most revenue is generated:

WITH CTE_table AS ( 

	SELECT a.productsku,
		   p.sku,
		   productprice,
		   ROUND(updated_unitprice, 4),
		   orderedQuantity,
		   ROUND(updated_unitprice*orderedQuantity, 2) AS Revenue_per_product,
		   country,
		   city,
		   transactionrevenue,
		   totalTransactionRevenue
	
	FROM all_sessions AS a
	JOIN products AS p ON a.productsku = p.sku
)

SELECT SUM(revenue_per_product) AS Total_Revenue,
	   country
FROM CTE_table
GROUP BY country
ORDER BY total_revenue DESC

Query for city from where the most revenue is generated:

WITH CTE_table AS ( 

	SELECT a.productsku,
		   p.sku,
		   productprice,
		   ROUND(updated_unitprice, 4),
		   orderedQuantity,
		   ROUND(updated_unitprice*orderedQuantity, 2) AS Revenue_per_product,
		   country,
		   city,
		   transactionrevenue,
		   totalTransactionRevenue
	
	FROM all_sessions AS a
	JOIN products AS p ON a.productsku = p.sku
)

SELECT SUM(revenue_per_product) AS Total_Revenue,
	   city
FROM CTE_table
GROUP BY city
ORDER BY total_revenue DESC



**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries:



Answer:





**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:



Answer:





**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:



Answer:





**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:



Answer:







