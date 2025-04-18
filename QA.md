What are your risk areas? Identify and describe them.



QA Process:
Describe your QA process and include the SQL queries used to execute it.

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
