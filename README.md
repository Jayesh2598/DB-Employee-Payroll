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

## UC5- Retrieve salary data of particular employee and employees joined in a particular date range
### Retrieving salary of a particular employee
`SELECT salary FROM employee_payroll WHERE name = 'Terisa';`
### Retrieving employees joined after 2019-05-01 till now
`SELECT * FROM employee_payroll WHERE start BETWEEN CAST('2019-05-01' AS DATE) AND DATE(NOW());`

## UC6- Add a new column in employee payroll and set values to it
### Adding a new column gender after name column
`ALTER TABLE employee_payroll ADD gender CHAR(1) AFTER name;`
### Set gender for male employees as M
`UPDATE employee_payroll set gender = 'M' WHERE name = 'Bill' or name = 'Charlie' or name = 'Sam';`
### Set gender for female employees as F
`UPDATE employee_payroll set gender = 'F' WHERE name = 'Terisa';`
### See table entries
`select * from employee_payroll;`

## UC7- Use Sum, Avg, Min, Max, Count to get neeeded data
### Total Salary according to gender
`SELECT gender, SUM(salary) FROM employee_payroll GROUP BY gender;`
### Average Salary according to gender
`SELECT gender, AVG(salary) FROM employee_payroll GROUP BY gender;`
### Minimum Salary according to gender
`SELECT gender, MIN(salary) FROM employee_payroll GROUP BY gender;`
### Maximum Salary according to gender
`SELECT gender, MAX(salary) FROM employee_payroll GROUP BY gender;`
### Employee Count according to gender
`SELECT gender, COUNT(id) AS No_Of_Employees FROM employee_payroll GROUP BY gender;`
