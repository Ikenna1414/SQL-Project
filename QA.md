What are your risk areas? Identify and describe them.



QA Process:
Describe your QA process and include the SQL queries used to execute it.

I created the database one table at a time using the CREATE TABLE command, and assigned appropriate data types to the columns. A sample code is displayed below.

```SQL
DROP TABLE IF EXISTS all_sessions;
	
	CREATE TABLE IF NOT EXISTS all_sessions
(
    fullVisitorId numeric,
    channelGrouping character varying,
    time bigint,
    country character varying,
    city varchar,
    totalTransactionRevenue bigint,
    transactions character varying,
    timeOnSite bigint,
    pageviews bigint,
    sessionQualityDim bigint,
    date date,
    visitId bigint,
    type varchar,
	productRefundAmount varchar,
	productQuantity varchar,
	productPrice bigint,
	productRevenue bigint,
	productSKU varchar,
	v2ProductName varchar,
	v2ProductCategory varchar,
	productVariant varchar,
	currencyCode varchar,
	itemQuantity bigint,
    itemRevenue bigint,
	transactionRevenue bigint,
	transactionId varchar,
	pageTitle varchar,
	searchKeyword varchar,
	pagePathLevel1 varchar,
	eCommerceAction_type bigint,
	eCommerceAction_step bigint,
	eCommerceAction_option varchar

);
```
After this I loaded the data onto the database.

I created a new column in my database and divided the unit price by 1,000,000. I named it Updated_UnitPrice.
On the actual tables, to control the number of decimal places, I used the ROUND function

I tried to make sure that no country is NULL since I would be calculating total revenue per country

```SQL
SELECT *
FROM all_sessions
WHERE country is NULL
```

I did thesame thing for city

Another item that required cleaning is visitorId and fullvisitorid, but I did not require this in my queries.
