##Question 1: How could you update unit_price to show the correct revenue?



##Answer: select unit_price, (revenue/1000000) as updatedrevenue, (select left(cast(fullvisitorid as varchar), 6) as fvid)
	from analytics
	where revenue is not null



##Question 2: top 3 time spent on site by visitorid

SQL Queries:

select visitid, timeonsite
from all_sessions
where timeonsite is not null
group by visitid, timeonsite
order by timeonsite desc

##Answer:
1479144257	"01:17:41"
1493327095	"01:05:37"
1482431484	"01:03:42"


##Question 3: Using views created how many distinct city and country total revenue of city and country


SQL Queries:
select city, country, sum((unit_price * total_ordered)) as totrev
	from skcc skc
	join unirev uv
	on uv.fvid = skc.fvid 
	join cleansr csr
	on skc.productsku = csr.productsku
	group by skc.city, skc.country


##Answer:23


##Question 4: show distinct category order counts

SQL Querie

select distinct v2productcategory, country, city, cit from (
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
)
order by cit desc


##Answer: 1816

