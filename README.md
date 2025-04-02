# mysql
Learning the mysql

SHOW DATABASES;
USE orgi;

CREATE TABLE Worker(
	WORKER_ID INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    FIRST_NAME CHAR(25), 
    LAST_NAME CHAR(25), 
    SALARY INT(15), 
    JOINING_DATE DATETIME,
    DEPARTMENT CHAR(25)
);

INSERT INTO Worker 
	(WORKER_ID, FIRST_NAME, LAST_NAME, SALARY, JOINING_DATE, DEPARTMENT) VALUES
    (001, 'Monika', 'Arora', 100000, '14-02-20 09.00.00', 'HR'), 
    (002, 'Niharika', 'Verma', 80000, '14-06-11 09.00.00', 'HR'),
    (003, 'Vishal', 'Singhal', 300000, '14-02-20 09.00.00', 'HR'),
    (004, 'Amitabh', 'Singh', 500000, '14-02-20 09.00.00', 'Admin'),
    (005, 'Vivek', 'Bhati', 500000, '14-06-11 09.00.00', 'Admin'),
    (006, 'Vipul', 'Diwan', 200000, '14-06-11 09.00.00', 'Account'),
    (007, 'Satish', 'Kumar', 75000, '14-01-20 09.00.00', 'Account'),
    (008, 'Geetika', 'Chauhan', 90000, '14-04-11 09.00.00', 'Admin');

SELECT * FROM Worker;

CREATE TABLE Bonus(
	WORKER_REF_ID INT,
    BONUS_AMOUNT INT(15), 
    BONUS_DATE DATETIME, 
    FOREIGN KEY (WORKER_REF_ID)
    REFERENCES Worker(WORKER_ID) 
    ON DELETE CASCADE
);

INSERT INTO Bonus 
 (WORKER_REF_ID, BONUS_AMOUNT, BONUS_DATE) VALUES
 (001, 5000, '16-02-20'),
 (002, 3000, '16-06-11'), 
 (003, 4000, '16-02-20'), 
 (004, 4500, '16-02-20'), 
 (005, 3500, '16-06-11');
 
 SELECT * FROM Bonus;
 
 CREATE TABLE Title(
 WORKER_REF_ID INT, 
 WORKER_TITLE CHAR(25), 
 AFFECTED_FROM DATETIME, 
 FOREIGN KEY (WORKER_REF_ID)
 REFERENCES Worker(WORKER_ID) 
 ON DELETE CASCADE
 );
 
INSERT INTO Title 
(WORKER_REF_ID, WORKER_TITLE, AFFECTED_FROM) VALUES
(001, 'Manager', '2016-02-20 00:00:00'),
(002, 'Executive', '2016-06-11 00:00:00'),
(008, 'Executive', '2016-06-11 00:00:00'),
(005, 'Manager', '2016-06-11 00:00:00'),
(004, 'Asst. Manager', '2016-06-11 00:00:00'),
(007, 'Executive', '2016-06-11 00:00:00'),
(006, 'Lead', '2016-06-11 00:00:00'),
(003, 'Lead', '2016-06-11 00:00:00');


SELECT * FROM Title;


-- Questions 
-- 1) Write a sql query to fetch the first_name from worker table using the alias name as <Worker_name>
select FIRST_NAME as WORKER_NAME FROM Worker;

-- 2) Write a sql query to fetch the first_name from worker table in upper case
select UPPER(first_name) from Worker;

-- 3) Write a sql query to fetch the unique values of department from the worker table
select distinct department from worker;
-- same can be achieved throught group by 


-- 4) write a sql query to fetch first three character of the first_name from the worker table
select substring(first_name, 1, 3) from worker;studentsstudents
    
 
 -- 5) Write a sql query to find the position of the alphabet b in the first name column Amitabh
 select INSTR(first_name, 'b') from worker where first_name = 'Amitabh';
    
-- 6) Write a sql query to print the first_name from the worker table after removing the white spaces from the right side 
select rtrim(first_name)  from worker;
select rtrim("Hello     ") as trimmedString;

-- 7) -- 6) Write a sql query to print the first_name from the worker table after removing the white spaces from the left side 
select ltrim(first_name) from worker;
select ltrim("     SQL") as trimmedString;
select ltrim(rtrim("    Hi     ")) as trimmedString;


-- 8) Write an sql query to fetch the unique department values from the worker table and print its length
select distinct department, length(department) from worker;

-- 9) Write an sql query to print the first_name from worker table after replacing 'a' with 'A'
select replace(first_name, 'a', 'A') from worker;	


-- 10) Write an sql query to print the first_name and last_name together into a single column named complete_name
select concat(first_name, ' ', last_name) as Combined_name from worker;    

-- 11) Write an sql query to print the worker details from the worker table order by ascending order 
select * from worker order by first_name asc;

-- 12) Write a sql query to print the worker details from the worker table order by first name as ascneding and department descending 
select * from worker order by first_name asc,  department desc;	


-- 13) write a sql query to print the worker details from the worker table where first name is either vipul or satish
select * from worker where first_name = 'Vipul' OR first_name = 'Satish';
select * from worker where first_name IN ('Vipul' , 'Satish');

-- 14) Write an sql query to print the details of the worker except from satish and vipul
select * from worker where first_name NOT IN ('Satish', 'Vipul');

-- 15) write a sql query to print the details of the worker with department as admin* means first 5 character need to be adming strictly
select * from worker where department like 'Admin%';

-- 16) write the sql query in which the first_name of the employee contains the alphabet a 
select * from worker where first_name like '%a%';

-- 17) write a sql query to find the employees where first_name ends with a 
select * from worker where first_name like '%a';

-- 18) write a sql query to find the employees where first_name start with a 
select * from worker where first_name like 'a%';

-- 19) write a sql query to find the employee where first_name ends with h and contains 6 alphabets
select * from worker where length(first_name) = 6 AND first_name like '%h';
select * from worker where first_name like '_____h';

-- 20) write a sql query to find the employee whose salary lies between 100000 , 500000
select * from worker where salary >= 100000 AND salary <= 500000;
select * from worker where salary between 100000 and 500000;

-- 21) write a sql query to find the employee who have joined in feb 2014
select * from worker where joining_date >= '2014-02-01' and joining_date <= '2014-02-28';
    
-- 22) write an sql query to print the count of the employees who are working in the admin department
select count(*) as employee_count from worker where department = 'Admin';
  
-- 23) write an sql query to fetch worker full names whose salary greater than 50000 and 100000
select concat(first_name, ' ', last_name) as full_name from worker where salary between 50000 and 100000;

-- 24) write an sql query to fetch the no of workers for each department in descending order
select department, count(*) as no_of_worker from worker group by department order by count(worker_id) desc;	

-- 25) join the worker table with title table using inner join where employee title is manager
select w.* from worker as w inner join title as t on w.worker_id = t.worker_ref_id where t.worker_title = 'manager';    

-- 26) write an sql query to fetch number (more than 1) of same titles in org of different types
select worker_title, count(*) from title group by worker_title;

-- 27) write a sql query to show only odd rows of a table
select * from worker where mod (worker_id, 2) != 0;

-- 28) write a sql query to show only even rows of a table
select * from worker where mod(worker_id, 2) = 0;

-- 29) write a sql query to clone a new table from another table
create table worker_clone like worker;  -- first we copied the schema from worker table in worker_clone using like command
insert into worker_clone select * from worker;  -- then we inserted the data from worker to worker_clone
select * from worker_clone;  -- at last we just check our worker_table. 

-- 30) write a sql to fetch the intersecting record of two tables
select w.* from worker as w inner join worker_clone as wc on w.worker_id = wc.worker_id;

-- 31) write an sql query to show the records from one table that another table does not have
select * from worker left join worker_clone using(worker_id) where worker_clone.worker_id = null;

-- 32) write an sql query to find the current date and time
select curdate();
select now();

-- 33) write an sql query to show the top 5 records of a table order by descending order
select * from worker order by salary desc limit 5;

-- 34) write a sql query to derive the 5th highest salary from worker table
select * from worker order by salary desc limit 4,1;

-- 35) write a sql query to fetch the 3rd highes salary from the worker table
select * from worker order by salary desc limit 2,1;

-- 36) write a sql query to get the 5th highest salary without using limit keyword

-- 37) write a sql query to get the 2nd highest salary in the worker table
select * from worker order by salary desc limit 1,1;

-- 38) write a sql query to show one row twice in results from a table
select * from worker 
Union all
select * from worker order by worker_id;

-- 39) write a sql query to list the worker who does not get a bonus
select worker_id from worker where worker_id not in (select worker_ref_id from bonus);

-- 40) write a sql query to list all the worker name who does not get a bonus
select concat(first_name, ' ', last_name) as full_name from worker where worker_id not in (select worker_ref_id from bonus);	

-- 41) write an sql query to fetch the 50% 	records from a table
select salary from worker order by salary desc limit 2,2;
select * from worker;

-- find the sum of the salary
select sum(salary) as sum_of_salary from worker;

-- find the average of the salary
select avg(salary) as avg_of_salary from worker;

-- 42) write a sql query to list worker_id who does not get a bonus
select worker_id from worker where worker_id not in (select worker_ref_id from bonus);

-- 43) write a sql query to find the workers who does not get bonus ensure full name of workers
select concat(first_name, ' ', last_name) as full_name from worker where worker_id not in (select worker_ref_id from bonus);


-- 44) write a sql query to fetch the first 50% record from a table
select * from worker where worker_id <= (select count(worker_id)/2 from worker);

-- 41) write a sql query in which a department  has less than 4 people in it. 
 select department, count(department) as depcount from worker group by department having depcount < 3;
 
 -- 42) write a sql query in which it shows all the department and people working there
 select department, count(department) as depcount from worker group by department;
 
 -- 43) write a sql query to show the last record from a table
 select * from worker where worker_id = (select max(worker_id) from worker);
 
 -- 44) write a sql query to show the very first record from a table
 select * from worker limit 1;
 
 -- write a query to find the worker with minimum salary
 select * from worker where worker_id = (select min(worker_id) from worker);
 
 -- 45) write a sql query to find the last 5 records from a table
 (select * from worker order by worker_id desc limit 5) order by worker_id;
 
 -- 46) write a sql query to fetch the highest salary of workers in each department
 select max(salary) as maxsal, department from worker group by department;
 
 -- 47) write a sql query to fetch the three max salaries from the table 
select distinct salary from worker order by salary desc limit 3;
 
 -- 48) write a sql query to fetch the three min salary from the table
 select distinct salary from worker order by salary  limit 3;
 
 -- 49) write an sql query to fetch the departments along with the total salaries paid to each of them
 select department, sum(salary) as depsal from worker group by department order by depsal desc;
 
 
 -- 50) write a query to fetch the names of the worker who is having the highest salary 
 select first_name, salary from worker where salary = (select max(salary) from worker);
 









    
    
