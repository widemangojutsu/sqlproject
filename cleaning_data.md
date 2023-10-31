What issues will you address by cleaning the data?

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
-





select userid
from analytics

-returned 4301122 nulls
select userid
from analytics
where userid = null
-returned 0 of 0




Queries:
Below, provide the SQL queries you used to clean your data.
