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
