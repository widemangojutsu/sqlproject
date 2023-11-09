Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries:
###
with highestrev as
(select distinct country, sum(totaltransactionrevenue) as ttr, city from all_sessions
 where totaltransactionrevenue is not null
 group by country, city
)
select max(ttr), country, city
from highestrev
where city not like 'not av%'

group by highestrev.country, highestrev.city


Answer:
United States, San francisco 

###

**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries:

used the view to join on needed data

select (select distinct trim(' ' from city)) as city, (select distinct trim(' ' from country)) as country, avg(csr.total_ordered)
from salessku sks
join cleansr csr
on sks.productsku = csr.productsku
join skcc skc
on sks.productsku = skc.productsku
group by city, country


Answer:
SELECT 
  city,
  country,
  (SUM(csr.total_ordered) / COUNT(DISTINCT city)) AS average_units_sold_per_city_country
FROM salessku
JOIN cleansr csr ON salessku.productsku = csr.productsku
JOIN skcc skc ON salessku.productsku = skc.productsku
GROUP BY city, country
create view as sks, csrs




**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:
with cte as (
select distinct country, city, count(*)
from skcc skc
group by country, city
)
select v2productcategory, country, city, count(v2productcategory) as cit
	from fvidcategory fcat
	join skcc on fcat.fvid = skcc.fvid
	where v2productcategory not like '(not%)'
	group by v2productcategory, country, city
order by cit desc


Answer:
more coastal cities have higher outerwear or wear category placed




**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:

with cte as (
select distinct country, city, count(*)
from skcc skc
group by country, city
)
select v2productcategory, country, city, count(city) as cit, skcc.productsku, csr.name
	from fvidcategory fcat
	join skcc on fcat.fvid = skcc.fvid
	join cleansr csr
	on fcat.productsku = csr.productsku
	where v2productcategory not like '(not%)'
	group by v2productcategory, country, city, skcc.productsku, csr.name
order by cit desc

Answer:
camera indoor security for mountain view




**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:
create view unirev as (
select unit_price, (revenue/1000000) as updatedrevenue, (select left(cast(fullvisitorid as varchar), 6) as fvid)
	from analytics
	where revenue is not null

select city, country, sum((unit_price * total_ordered)) as totrev
	from skcc skc
	join unirev uv
	on uv.fvid = skc.fvid 
	join cleansr csr
	on skc.productsku = csr.productsku
	group by skc.city, skc.country

Answer:
Poland Warsaw and Ireland were leading total_revenue outside of United States country.





