What issues will you address by cleaning the data?


--divide unitprice by 1,000,000
-- divide unitprice /1000000
update analytics
set unit_price = unit_price/1000000


starting with analytics table
- i see missing city values
- joining analytics on all_sessions on visitid
- on visitid i see duplicate visitid's

select distinct als.visitid, als.country, als.city
from all_sessions als
-- join visitid from analytics
join analytics an
on an.visitid = als.visitid

3661 distinct visitid's

-add als.fullvisitorid to query, ran it, got exponential number e+18
-converted to numeric type, got a number with alot of 0's
- add an.fullvisitorid to query, have it as double precision type, will change to numeric type
- noticed same first 6 digits, als.fullvisitorid has matching first 6 has an.fullvisitorid has more digits after
- will try to test this and see if they all match up


select distinct als.visitid, als.country, als.city, als.fullvisitorid, an.fullvisitorid
from all_sessions als
-- join visitid from analytics
join analytics an
on an.visitid = als.visitid

-this query return 3746 results
-removing distinct als.visitid returned 107159


select distinct als.fullvisitorid, als.country, als.city, an.fullvisitorid
from all_sessions als
-- join visitid from analytics
join analytics an
on an.visitid = als.visitid

-returned 3719 results

(select substring(cast(fullvisitorid as varchar), 1, 6) as anfvid
from analytics)

-get this to string, get first 6th, will compare with all_sessions.fullvisitorid
-- this gets the first 6 digits, removing the 13 zeros 
select left(cast(fullvisitorid as varchar), 6) as fvid
from analytics

--no values in userid
select userid, visitid
from analytics
where userid is null
--returns 4301122 nulls

--this can be used as PK
select an.visitid, als.visitid
from analytics an
join all_sessions als
on als.visitid = an.visitid
-returns 107159


select userid
from analytics

-returned 4301122 nulls
select userid
from analytics
where userid = null
-returned 0 of 0


--discrepency between sales_by_sku and sales_report
select *
from cleansr
where total_ordered != 0
group by productsku, id, total_ordered, name
--returns 304
--created as view called cleansr

sales_by_sku returns 306
select productsku, id, total_ordered from sales_by_sku
where total_ordered != 0
group by productsku, id, total_ordered
-created as view called salesku

--left join to find differences
select *
from cleansr csr
left join salessku slks
on csr.productsku = slks.productsku
where csr.total_ordered != 0
--returned 304
i think its usable now, distinct productsku's filtered with group by prior to





Queries:
Below, provide the SQL queries you used to clean your data.
