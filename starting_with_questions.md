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

Query for cities with higest average number of products ordered:
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

SELECT ROUND(AVG(orderedquantity),4) AS AVG_orderdquantity,
		SUM(revenue_per_product) AS revenue_sum,
		count(orderedquantity) AS revenue_count,
		SUM(revenue_per_product)/count(orderedquantity) AS AVG_revenue,
	   city
FROM CTE_table
GROUP BY city
ORDER BY AVG_orderdquantity DESC

Query for countries with higest average number of products ordered:

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

SELECT ROUND(AVG(orderedquantity),4) AS AVG_orderdquantity,
		SUM(revenue_per_product) AS revenue_sum,
		count(orderedquantity) AS revenue_count,
		SUM(revenue_per_product)/count(orderedquantity) AS AVG_revenue,
	   country
FROM CTE_table
GROUP BY country
ORDER BY AVG_orderdquantity DESC

Answer:

The cities with the highest average number of ordered products are Council Bluffs, Bellflower, Cork, Santiago, and Bellingham

The countties with the highest average number of ordered products are Montenegro, Mali, Papua New Guinea, Reunion, and Georgia.

**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:

For Country:
WITH CTE_table AS ( 

	SELECT a.productsku,
		   p.sku,
		   v2ProductCategory,
		   v2ProductName
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
-- WINDOW FUNCTION
SELECT 
	 count(v2ProductCategory) AS count_productCategory,
	 v2ProductCategory,
	 country
FROM CTE_table
GROUP BY v2ProductCategory, country
ORDER BY count_productCategory DESC

For Cities:

WITH CTE_table AS ( 

	SELECT a.productsku,
		   p.sku,
		   v2ProductCategory,
		   v2ProductName
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
-- WINDOW FUNCTION
SELECT 
	 count(v2ProductCategory) AS count_productCategory,
	 v2ProductCategory,
	 city
FROM CTE_table
GROUP BY v2ProductCategory, city
ORDER BY count_productCategory DESC



Answer:
For category by countries, the united states is leading consumer in most product categories. This could be due to lots of factors including population, booming economy, and consumer culture.
United Kingdom, and  India are second and third highest consumers for Shop by Brand/YouTube.

For categories by cities, for the data available, the most consumer-focused cities are Mountain View (Mens shirt, Nest, Electronics, Men's apparel, Shop by brand/Google and office), New York (Men's T-Shirts), London (Shop by Brand/YouTube), and San Francisco (Men's T-Shirt)




**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:

QUERY FOR COUNTRY:

WITH CTE_table AS ( 

	SELECT a.productsku,
		   p.sku as key1,
		   v2ProductCategory,
		   v2ProductName,
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
),

CTE_summary AS (
SELECT 
	 count(v2ProductName) AS count_v2ProductName,
	 v2ProductName,
	 country,
	 key1
FROM CTE_table
GROUP BY v2ProductName, country, key1
ORDER BY count_v2ProductName DESC
--ORDER BY country
)
,

CTE_Final AS (
SELECT DISTINCT ON (country)*
FROM CTE_summary 
ORDER BY country, count_v2ProductName DESC  
)

SELECT *
FROM CTE_Final
ORDER BY count_v2ProductName DESC

QUERY FOR CITY:

WITH CTE_table AS ( 

	SELECT a.productsku,
		   p.sku as key1,
		   v2ProductCategory,
		   v2ProductName,
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
),

CTE_summary AS (
SELECT 
	 count(v2ProductName) AS count_v2ProductName,
	 v2ProductName,
	 city,
	 key1
FROM CTE_table
GROUP BY v2ProductName, city, key1
ORDER BY count_v2ProductName DESC
--ORDER BY country
)
,

CTE_Final AS (
SELECT DISTINCT ON (city)*
FROM CTE_summary 
ORDER BY city, count_v2ProductName DESC  
)

SELECT *
FROM CTE_Final
ORDER BY count_v2ProductName DESC

Answer:
FOR COUNTRY:
We can see that the USA gives the rest of the countries a huge margin with 163 shirts bought, second is the united Kingdom with 22 units of the bottle infuser bought, next is india, Germany and Canada

FOR CITY:
The cities that bought the most of the items are Mountain View, New York, San Francisco, and London




**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:
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

FOR COUNTRY:
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


Answer:







