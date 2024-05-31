# AEC_DBMS_May_2024

* **Meeting Link:** https://tinyurl.com/2s3yxjnr
* **GitHub Link:** https://github.com/toarnabtrainer/AEC_DBMS_May_2024

<hr>

* **Oracle Live SQL Account Creation link:** https://livesql.oracle.com/
* **Oracle Notes and PPTs:** https://github.com/toarnabtrainer/vodafone_oracle_batch86
* **Korth Chapter-4 (SQL) Queries:** https://github.com/toarnabtrainer/Oracle_Notes/blob/main/Oracle-2%20Korth%20SQL%20Chapter-4.md  
* **Oracle Join Operations:** https://github.com/toarnabtrainer/Oracle_Notes/blob/main/Join_Operations.md
* **Korth Chap-4 Exercise Link-1:** https://github.com/toarnabtrainer/Oracle_Notes/blob/main/Korth%20Chap-4%20Exercise.md
* **Korth Chap-4 Exercise Link-2:** https://github.com/toarnabtrainer/MySQL_Notes/blob/main/MD-4%20Korth%20Exercise%20(Questions).md
* **Transforming ERD to Database:** https://github.com/toarnabtrainer/Oracle_Notes/blob/main/ERD%20to%20Database.md
<hr>

**For Diagram Making:**<br>
https://app.diagrams.net/

**Tutorial Link for Draw.io:**<br>
https://www.youtube.com/watch?v=Em_8IeJBmsQ&list=PLX6xdk86h_0xpW82Q0YkdN6xpHa6hvHjO

**draw.io Desktop Version Download Link:**<br>
https://www.drawio.com/blog/diagrams-offline

<hr>
<b>
  
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

