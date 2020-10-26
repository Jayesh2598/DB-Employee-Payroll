# DB-Employee-Payroll
## UC1- Create a database payroll_service
`create database payroll_service;`
### See the database
`show databases;`
`show databases like 'payroll_service';`
### Go to database
`use payroll_service;`
## UC2- Create a employee_payroll table in payroll_service
```
create table employee_payroll
    -> (
    -> id INT unsigned NOT NULL AUTO_INCREMENT,
    -> name VARCHAR(150) NOT NULL,
    -> salary Double NOT NULL,
    -> start DATE NOT NULL,
    -> PRIMARY KEY (id)
    -> );
```
## UC3- Insert employee payroll data into database
```
INSERT INTO employee_payroll(name , salary , start) VALUES
    -> ('Bill', 1000000.00, '2018-01-03'),
    -> ('Terisa', 2000000.00, '2019-11-13'),
    -> ('Charlie', 3000000.00, '2020-05-21'),
    -> ('Sam', 4000000.00, '2021-05-13');
```
## UC4- Retrieve employee payroll data from database
`select * from employee_payroll;`
