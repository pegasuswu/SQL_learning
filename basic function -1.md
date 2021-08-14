### 1. order by
1) Function: sort query results
2) Syntax format: order by field name sorting method;
3) Sorting method: ASC (default): ascending ; Desc: descending
```sql
SELECT * FROM salaries group by emp_no order by salary desc
```
output:  
![image](https://user-images.githubusercontent.com/81301502/129457417-68abd342-be18-480d-b23b-f284de657df5.png)

### 2. group by
1) Function: group query results, usually used together with aggregate functions
2) Syntax format: group by field name
```sql
SELECT * FROM employees_test.salaries group by emp_no
```
output:  
![image](https://user-images.githubusercontent.com/81301502/129457396-46988586-cfd1-4e15-a25e-7f7606f7226d.png)

### 3. aggregate functions
1) avg(field name) : get average value of the field    
```sql
SELECT emp_no,avg(salary) as max_salary FROM salaries group by emp_no
```
output:

![image](https://user-images.githubusercontent.com/81301502/129460141-41844b1b-583a-4f98-8ce1-08f1737667d0.png)

2) sum(field name) : get total value of the field    
```sql
SELECT emp_no, sum(salary) as totalsalary FROM salaries group by emp_no order by totalsalary desc
```
output:  
![image](https://user-images.githubusercontent.com/81301502/129457543-0973a044-d31a-4ac1-a19d-b281a8eef743.png)

3) max(field name) : get max value of the fieled  

```sql
SELECT emp_no, max(salary) FROM salaries group by emp_no
```
output:  
![image](https://user-images.githubusercontent.com/81301502/129460206-cc2ad7c4-23e5-4b8c-b4ad-0807aab364ea.png)

4) min(field name) : get min value of the field  
```sql
select emp_no, min(salary) as new_salary from salaries  group by emp_no
```
output:  
![image](https://user-images.githubusercontent.com/81301502/129460666-fbc4c9d3-20d1-4175-afc0-f8ae13ba76bb.png)

5) count(field name): get the record count of the field  
```sql
SELECT emp_no, count(salary)as counts,avg(salary) as avg_salary FROM salaries group by emp_no
```
output:  
![image](https://user-images.githubusercontent.com/81301502/129460235-fb8e5c62-3356-4c01-b1f5-b366e2e79cc3.png)

### Attention: aggregate functions can not be used with the single field together as the output of the SQL statement.
For example ,the following sql statement is meaningless and confused.
```sql
SELECT emp_no, count(salary)as counts,avg(salary) as avg_salary FROM salaries
```
the output is:    
![image](https://user-images.githubusercontent.com/81301502/129460335-167207a8-c138-405b-91ba-8e7422182425.png)
  
Actually it is not right.Because the aggregate functions deal the data group not a single record!
### 4 having
1) Function: further filter query results, usually used in combination with group by.  
2) Syntax format: group by field name having condition. 
```sql
SELECT emp_no, avg(salary) FROM employees_test.salaries group by emp_no having avg(salary)>60000
```
output:    

![image](https://user-images.githubusercontent.com/81301502/129457388-90860ea8-603e-4b9f-9173-c29394b8e501.png)


### 5 distinct
1) function：Do not display the repeated value of the field
2) Syntax format：select distinct field lists from table; 
```sql
select distinct emp_no from salaries;
```
output:  
![image](https://user-images.githubusercontent.com/81301502/129460487-53dd35f4-cde4-4efd-952f-9d4ef9903c47.png)

However, if the sql statement is:
```sql
select distinct emp_no,salary from salaries;
```
output:  
![image](https://user-images.githubusercontent.com/81301502/129460535-c2cac8c9-dac7-47ca-a83a-49e4b85e01dd.png)

You can see repeated the records of same emp_no,This is because:
###distinct is dealing with all the fields between distinct and from ,so all the fields should be same then it can de repeated.###  

### 6 arithmetic operations when querying records.
```sql
select emp_no, salary*10 as new_salary from salaries 
select emp_no, salary+1000 as new_salary from salaries 
```

