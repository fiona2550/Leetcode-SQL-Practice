# Leetcode-SQL-Practice

**1350**: Subquery is more efficient than Join.

**613**: A good example to understand Cross Join

**1076**: order by function is not allowed in temp view.

**619**: 1 and 2 are basically the same. The difference is the output 
- the out put of 1 is always space when there is no rows returned while 2 is null. 
<br>1.select  top 1 num as num from my_numbers group by num having count(num) = 1 order by num desc </br>
<br>2.select max(a.num) as num from (select num from my_numbers group by num having count(num) = 1) a; </br>








