# Leetcode-SQL-Practice

**1350**: Subquery is more efficient than Join.

**613**: A good example to understand Cross Join

**1076**: order by function is not allowed in temp view.

**619**: 1 and 2 are basically the same. The difference is the output 
- the out put of 1 is always space when there is no rows returned while 2 is null. 
<br>1.select  top 1 num as num from my_numbers group by num having count(num) = 1 order by num desc </br>
<br>2.select max(a.num) as num from (select num from my_numbers group by num having count(num) = 1) a; </br>

**196**: Delete replicate records
- (do not work): DELETE FROM Person WHERE Person.Id NOT IN (SELECT MIN(Id) FROM Person GROUP BY Email) </br>
- (work): delete from Person where id not in (select A.id from (select min(id) as id from Person group by Email) as A); </br>
- (work): DELETE p1 FROM Person p1, Person p2 WHERE p1.Email = p2.Email AND p1.Id > p2.Id </br>


**197**: Rsining Temperature
- (do not work): select w1.id from Weather w1 join Weather w2 on w1.RecordDate = w2.dateadd(d, -1, RecordDate) where w1.Temperature < w2.Temperature (w2.id may work)
- (work): select B.Id from Weather a inner join Weather b on datediff(d,a.RecordDate, b.RecordDate) =1 where a.Temperature < b.Temperature


**270**: All People Report to the Given Manager
- Super Smart Solution: loop with function
WITH all_reports AS
(
    SELECT employee_id, manager_id, employee_name
    FROM Employees
    WHERE employee_id = 1
    
    UNION ALL
    
    SELECT E.employee_id, E.manager_id, E.employee_name
    FROM all_reports AS A
    JOIN Employees AS E
    ON E.manager_id = A.employee_id
    WHERE E.employee_id != 1
)
SELECT employee_id FROM all_reports
WHERE employee_name NOT LIKE 'Boss'
and  employee_id <> 1;

**612**: No on with Cross Join. Or inner join on t1.column <> t2.column;

**1341**: When use **Union** function, cannot union two complex query together directly but need to select columns you want from complex query first

Select distinct viewer_id as id from Views 
group by viewer_id, view_date
having count(distinct article_id) >1
order by viewer_id


with temp AS (Select distinct article_id, author_id, viewer_id, view_date from Views)

select distinct viewer_id as id from temp
group by viewer_id, view_date
having count(*) >1
order by viewer_id

**Hankerrank**: Select median without need for each group 
https://www.hackerrank.com/challenges/weather-observation-station-20/problem
Select round(S.LAT_N,4)  from station S where (select count(Lat_N) from station where Lat_N < S.LAT_N ) = (select count(Lat_N) from station where Lat_N > S.LAT_N)
