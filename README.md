# AEC_DBMS_May_2024

* **Meeting Link:** https://tinyurl.com/2s3yxjnr
* **GitHub Link:** https://github.com/toarnabtrainer/AEC_DBMS_May_2024

<hr>

* **Oracle Live SQL Account Creation link:** https://livesql.oracle.com/
* **Oracle Notes and PPTs:** https://github.com/toarnabtrainer/vodafone_oracle_batch86
* **Korth Chapter-4 (SQL) Queries:** https://github.com/toarnabtrainer/Oracle_Notes/blob/main/Oracle-2%20Korth%20SQL%20Chapter-4.md  
* **Oracle Join Operations:** https://github.com/toarnabtrainer/Oracle_Notes/blob/main/Join_Operations.md
* **Korth Chap-4 Exercise Link:** https://github.com/toarnabtrainer/MySQL_Notes/blob/main/MD-4%20Korth%20Exercise%20(Questions).md
* **Transforming ERD to Database:** https://github.com/toarnabtrainer/Oracle_Notes/blob/main/ERD%20to%20Database.md
* **Test on DBMS (1):** https://bit.ly/3yHyVM3-
* **Test on DBMS (2):**	https://bit.ly/4bEZEaD

<hr>

**For Diagram Making:**<br>
https://app.diagrams.net/

**Tutorial Link for Draw.io:**<br>
https://www.youtube.com/watch?v=Em_8IeJBmsQ&list=PLX6xdk86h_0xpW82Q0YkdN6xpHa6hvHjO

**draw.io Desktop Version Download Link:**<br>
https://www.drawio.com/blog/diagrams-offline

<hr>
<b>

## Korth Exercise 4.2 Solve:

<pre>
-- *********************************************************************************************************

Query-A: Find employees who work for VSNL.
    
SELECT * FROM works;
select employee_name from works where company_name='vsnl';

-- *********************************************************************************************************

Query-B: Find names and cities of VSNL employees.
    
select employee_name, city
from employee e join works w using(employee_name)
where company_name = 'vsnl';

select employee_name, city
from employee natural JOIN works
where company_name = 'vsnl';

select employee_name, city
from employee inner join works using (employee_name)
where company_name = 'vsnl';

-- nested query
select employee_name, city
from employee
where employee_name in
	(select employee_name
	 from works
	 where company_name = 'vsnl');

-- *********************************************************************************************************

Query-C: Find AOL employees with salary > 20,000.
    
select employee_name,street,city
from employee natural JOIN works
where company_name = 'aol' AND salary > 20000;

select employee_name, street, city
from employee
where employee_name IN (
    select employee_name
    from works
    where company_name = 'aol' AND salary > 20000
);
    
-- *********************************************************************************************************

Query-D: Find employees living in same city as their companies in which they work respectively.

select distinct employee_name
from employee natural join works natural join company

select distinct employee_name
from employee e join works using(employee_name) join company c using (company_name)
where e.city = c.city;
    
-- *********************************************************************************************************

Query-E: Find employees living in same city and street as their respective managers.
    
select e.employee_name
from employee e, employee m
where e.city = m.city
  and e.street = m.street
  and (e.employee_name, m.employee_name) in
      (select * from manages);

-- *********************************************************************************************************
	
Query-F: Find employees not working for VSNL.

select employee_name
from works
minus
(select employee_name
from works
where company_name = 'vsnl');

SELECT distinct employee_name
FROM works
WHERE employee_name NOT IN (
    SELECT employee_name
    FROM works
    WHERE company_name = 'vsnl'
);

-- *********************************************************************************************************

Query-G:  Find employees earning more than every employee of Satyam.

select employee_name
from works
where salary > all (
    select salary
    from works
    where company_name = 'satyam'
);

-- *********************************************************************************************************

Query-H: Find companies located in every city where VSNL is located

-- division operation
select company_name
from company c
where company_name <> 'vsnl'
  and not exists (
	(select city
	from company
	where company_name = 'vsnl')
    minus
    (select city
    from company
    where company.city = c.city));

-- *********************************************************************************************************

Query-I: Find employees earning more than their company average payroll. Payroll means total salary given by that company.

select employee_name
from works w
where salary > (
	select avg(salary)
	from works
	where company_name = w.company_name
);

-- *********************************************************************************************************

Query-J: Find company with most number of employees.

select company_name
from works
group by company_name
having count(*) >= all (
	select count(*)
	from works
	group by company_name);

-- *********************************************************************************************************

Query-K: Find company with the smallest payroll. Payroll means total salary given by that company.

select company_name
from works
group by company_name
having sum(salary) <= all (
    select sum(salary)
	from works
	group by company_name);

-- *********************************************************************************************************
    
Query-L: Find companies whose average salary is more than Satyam average salary.

select company_name
from works
group by company_name
having avg(salary) > (
    select avg(salary)
    from works
    where company_name = 'satyam'
);

-- *********************************************************************************************************

Query-M: Find the employee_name with other details having second highest salary
    
select *
from employee
where employee_name in (
	select employee_name
	from works where salary in (
		select s from (
			select rownum rn, e, s
			from (
				select employee_name e, salary s
				from works
				order by salary desc)
    		)
		where rn = 2));
    
-- *********************************************************************************************************

drop table employee;
drop table manages;
drop table company;
drop table works;

-- *********************************************************************************************************

</pre>

## Claswork Queries: <br>

<pre>
-- From the Call Center Database write a query to find country wise call count.

select country_name_eng, count(*) cnt_call
from ((country cn join city ct on (cn.id = ct.country_id))
      join customer cm on (ct.id = cm.city_id))
      join call_table cl on (ct.id = cl.customer_id)
      group by country_name_eng;

-- Against each distinct outcome_text how many calls are registered.

select outcome_text, count(*) cnt_message
from call_table ct join call_outcome co on (ct.call_outcome_id = co.id)
group by outcome_text;

-- which employee has attended maximum number of calls

select * from employee
where id in
	(select emp.id
	 from call_table ct join employee emp on (ct.employee_id = emp.id)
     	 group by emp.id
     	 having count(*) >= all 
		(select count(*)
		 from call_table ct join employee emp on (ct.employee_id = emp.id)
     	 	 group by emp.id));

</pre>
</b>

<hr>

## Classwork-1

![image](https://github.com/toarnabtrainer/AEC_DBMS_May_2024/assets/111301975/a555d346-47ca-4ea2-997c-62622255f6af)

<hr>

## Schemas for Korth Chapter - 4 (SQL)
![image](https://github.com/toarnabtrainer/AEC_DBMS_May_2024/assets/111301975/b7b6af95-c2ff-48f1-b651-b0b677ddedca)

<hr>

