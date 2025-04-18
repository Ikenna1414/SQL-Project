What issues will you address by cleaning the data?

The value for unit price is alot and could be in a different currency. Normalized it all by dividing by 1 million.




Queries:
Below, provide the SQL queries you used to clean your data.

```SQL
ALTER TABLE all_sessions
ADD COLUMN updated_unitprice NUMERIC;

UPDATE all_sessions
SET updated_unitprice = productprice /1000000.00;
```
