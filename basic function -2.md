# Summary of various usage of SQL join query
The following is the various join types in SQL.

![image](https://user-images.githubusercontent.com/81301502/129463661-aaef2f3a-42d0-423b-b2af-cdab93c1e329.png)


 ## No.1 【INNER JOIN】
This is the most commonly used method to obtain records in which the specified fields in two tables meet the matching relationship.

![](https://pic2.zhimg.com/80/v2-eaa5d9a2aa94c71d0a0633339481afd9_1440w.jpg)

```SQL
select A.emp_no,A.first_name,A.last_name,A.gender,B.salary from employees A
inner join salaries B on A.emp_no = B.emp_no
```
The  total record number of the inner join statment above is 1000.
The record of Table A is 524 ,The record of Table B is 1000. In the two tables above, if we calculate more seriously, We can get other fingers.
```sql
SELECT distinct emp_no FROM employees_test.salaries;
```
The number of the the query result above is 101( it means that in table salaries, one emp_no may have more than one records).  So we can get that the inner Join of table A and B should be included all the emp_no both in A and B, so the record number is 1000.
                                                              
## No.2 【LEFT JOIN】
Left join get all records in the left table, even if there is no corresponding matching record in the right table.

![](https://pic4.zhimg.com/80/v2-45fcd21c1199f2ff71ecf1231a18c86b_1440w.jpg)

```sql
select A.emp_no,A.first_name,A.last_name,A.gender,B.salary from employees A
left join salaries B on B.emp_no = A.emp_no
```
The record number of the querey result of sql above  is 1423. Why is this number? Now we write another sql:
```sql
select count(*) from employees where emp_no not in 
(select emp_no from salaries)
```
The number of the sql above is 423. It means that in table  employees, there are 423 emp_no records which are in employees however disappear in table salaries. Left join get all records in the left table employees. So the total record number is 1000(from table salaries) plus 423(from employees)=1423.
So, Guess the following sql querey result:
```sql
select A.emp_no,A.first_name,A.last_name,A.gender,B.salary from salaries B
left join employees A on B.emp_no = A.emp_no
```
Yes, the record number is 1000.

## No.3 【RIGHT JOIN】
Right join get all records in the right table, even if there is no corresponding matching record in the left table. 

![](https://pic1.zhimg.com/80/v2-742cc2400cf90e34e4b19d0587047dec_1440w.jpg)  

From above, we can get to know:
A left join B = B right join A
B left join A = A right join B  
So  We do not discuss it any more.

## No.4 【FULL JOIN】
Full Join retuns all the records in A and B.

![](https://pic3.zhimg.com/80/v2-4da74dd801c81a61eb10e3699d87e4c6_1440w.jpg)

MySql does not support the full join.

## No.5 【CROSS JOIN】
The result is the Cartesian product, which is the number of rows in the first table multiplied by the number of rows in the second table.
```sql
select A.emp_no,A.first_name,A.last_name,A.gender,B.salary 
from salaries B CROSS JOIN employees A
```
The record number is 524000.Because A is 524, B is 1000, So the cross join is 524000.
