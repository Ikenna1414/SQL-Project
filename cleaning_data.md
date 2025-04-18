What issues will you address by cleaning the data?

I see that there are alot of columns which I do not really need so I stripped them out and created a view which I could focus on for cleaning my data.

The value for unit price is alot and could be in a different currency. Normalized it all by dividing by 1 million.

I can see that product price and product unit price are same


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
