What issues will you address by cleaning the data?

I see that there are alot of columns which I do not really need so I stripped them out and created a view which I could focus on for cleaning my data.

The value for unit price is alot and could be in a different currency. Normalized it all by dividing by 1 million.

I can see that product price and product unit price (once normalized) are same. So I eliminated one of those columns.

Neither fullvisitorid nor visitorid are unique in the all_sessions table. This was in an attempt to find a primary key for the table.

sku is unique on the products table so I used this as the primary key. This can be verified by ensuring that the number of rows when you ``` SEELECT sku FROM products``` is equal to the number of rows when you ```SELECT DISTINCT sku FROM products```

For the sales_report tabl, name is not unique because  when you ``` SEELECT name FROM sales_report``` and when you ```SELECT DISTINCT name FROM sales_report``` the number of rows are not equal.
Queries:
Below, provide the SQL queries you used to clean your data.

```SQL
ALTER TABLE all_sessions
ADD COLUMN updated_unitprice NUMERIC;

UPDATE all_sessions
SET updated_unitprice = productprice /1000000.00;
```
```SQL
 CREATE OR REPLACE VIEW V_all_sessions AS
SELECT fullvisitorid,
		country,
		city,
		visitid,
		productprice,
		productsku,
		v2productname,
		v2productcategory,
		pagetitle,
		updated_unitprice
FROM all_sessions;
```
```SQL
SELECT productprice, updated_unitprice 
FROM tt_all_sessions
```
```SQL
CREATE OR REPLACE VIEW v_analytics AS
SELECT fullvisitorid,
		visitid,
		ROUND(unit_price/1000000.0,4)
```
