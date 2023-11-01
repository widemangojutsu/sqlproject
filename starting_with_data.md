Question 1: What is the average time a visitor is on the site before purchase?

SQL Queries:
take confirmed purchased fvid(fullvisitorid) and its associated columns 

all_sessions as als.(time, timeonsite, visitid, date, transactionid) 
analytics as an.(visitid, visitstarttime, date, fvid, timeonsite, visitnumber)
with cte to calculate (timeonsite - visitstarttime) to get difference
may need to cast timestamp to get accurate time


Answer: 



Question 2: 

SQL Queries:

Answer:



Question 3: 

SQL Queries:

Answer:



Question 4: 

SQL Queries:

Answer:



Question 5: 

SQL Queries:

Answer:
