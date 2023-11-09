What are your risk areas? Identify and describe them.

I think its important to have the data clean.
There are many instances where values are (not set) ie city, and totaltransactionrevenue were null's

SELECT
            country, city, productsku, COUNT(*) AS totalcount
        FROM all_sessions
        GROUP BY country, city, productsku
        ORDER BY country, city, COUNT(*) DESC

returns city and country with (not set)

a


QA Process:
Describe your QA process and include the SQL queries used to execute it.

i used alot of where clause is not to remove (not set) from city, and is not null for the nulls

also paid alot of attention to the total results, using that to match up with other results or rows

