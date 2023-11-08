What issues will you address by cleaning the data?


null values
will be removed with


select distinct als.fullvisitorid, als.country, als.city, an.fullvisitorid
from all_sessions als
-- join visitid from analytics
join analytics an
on an.visitid = als.visitid

(select substring(cast(fullvisitorid as varchar), 1, 6) as anfvid
from analytics)

-get this to string, get first 6th, will compare with all_sessions.fullvisitorid
-- this gets the first 6 digits, removing the 13 zeros 
select left(cast(fullvisitorid as varchar), 6) as fvid
from analytics


--this can be used as PK
select an.visitid, als.visitid
from analytics an
join all_sessions als
on als.visitid = an.visitid

select userid
from analytics

-returned 4301122 nulls
select userid
from analytics
where userid = null
-returned 0 of 0

--left join to find differences
select *
from cleansr csr
left join salessku slks
on csr.productsku = slks.productsku
where csr.total_ordered != 0




Queries:
Below, provide the SQL queries you used to clean your data.


SELECT *
FROM all_sessions
WHERE city not LIKE '(not%' 
and city not like 'not av%'


select distinct als.visitid, als.country, als.city, als.fullvisitorid, an.fullvisitorid
from all_sessions als
-- join visitid from analytics
join analytics an
on an.visitid = als.visitid




created a view
with
create view csr

--left join to find differences
select *
from cleansr csr
left join salessku slks
on csr.productsku = slks.productsku
where csr.total_ordered != 0
