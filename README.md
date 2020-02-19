# Leetcode-SQL-Practice

**1350**: Subquery is more efficient than Join.

**613**: A good example to understand Cross Join

**1076**: order by function is not allowed in temp view.

**619**: 1 and 2 are basically the same. The difference is the output 
- the out put of 1 is always space when there is no rows returned while 2 is null. 
<br>1.select  top 1 num as num from my_numbers group by num having count(num) = 1 order by num desc </br>
<br>2.select max(a.num) as num from (select num from my_numbers group by num having count(num) = 1) a; </br>

**196**: Delete replcate records
- (do not work): DELETE FROM Person WHERE Person.Id NOT IN (SELECT MIN(Id) FROM Person GROUP BY Email) </br>
- (work): delete from Person where id not in (select A.id from (select min(id) as id from Person group by Email) as A); </br>


**197**: Rsining Temperature
- (do not work): select w1.id from Weather w1 join Weather w2 on w1.RecordDate = w2.dateadd(d, -1, RecordDate) where w1.Temperature < w2.Temperature
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




