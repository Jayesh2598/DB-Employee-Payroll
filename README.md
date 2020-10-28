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

## UC8- Extend employee_payroll to contain employee phone, address and department
### Adding phone
`ALTER TABLE employee_payroll ADD phone_number VARCHAR(15) AFTER name;`
### Adding address and setting default value to 'TBD'
`ALTER TABLE employee_payroll ADD address VARCHAR(250) DEFAULT 'TBD' AFTER phone_number;`
### Adding non-nullable column department
`ALTER TABLE employee_payroll ADD department VARCHAR(150) NOT NULL AFTER address;`

## UC9- Extend employee_payroll to contain basic_pay, deductions, taxable_pay, tax, net_pay
```
ALTER TABLE employee_payroll RENAME COLUMN salary TO basic_pay;
ALTER TABLE employee_payroll ADD deductions DOUBLE NOT NULL AFTER basic_pay;
ALTER TABLE employee_payroll ADD taxable_pay DOUBLE NOT NULL AFTER deductions;
ALTER TABLE employee_payroll ADD tax DOUBLE NOT NULL AFTER taxable_pay;
ALTER TABLE employee_payroll ADD net_pay DOUBLE NOT NULL AFTER tax;
```

## UC10.1- Make Terisa an employee belonging to Sales and Marketting departments
```
update employee_payroll set department='Sales' where name='Terisa';
insert into employee_payroll (name, department, gender, basic_pay, deductions, taxable_pay, tax, net_pay, start) VALUES
    -> ('Terisa', 'Marketing', 'F', 1000000.00, 50000.00, 150000.00, 50000.00, 100000.00, '2019-11-13');
```

## UC11- Implement the ER diagram by making tables
### Creating company table
```
INSERT INTO company(company_id, company_name) VALUES
    -> (1,'Capgemini'),
    -> (2,'Apple'),
    -> (3,'Tesla'),
    -> (4,'Niantic');
```
### Creating employee table
```
INSERT INTO employee(name,company_id,gender,address,phone_number) VALUES
    -> ('Bill', 1, 'M', 'NY', 7045279233),
    -> ('Charlie', 2, 'M', 'SF', 7045279234),
    -> ('Emilia', 1, 'F', 'London', 7045279235),
    -> ('Claire', 3, 'F', 'Washington', 7045279236);
```
### Creating department table
```
INSERT INTO department (department_id, department_name) VALUES
    -> (101, 'Marketing'),
    -> (102, 'Sales'),
    -> (103, 'R&D'),
    -> (104, 'HR');
```
### Creating payroll table
#### Setting default values to taxable_pay and net_pay as these are derived attributes
```
ALTER table payroll ALTER taxable_pay SET DEFAULT (basic_pay-deductions);
ALTER table payroll ALTER net_pay SET DEFAULT (taxable_pay*(1-(tax/100)));
```
#### Inserting values in payroll
```
INSERT INTO payroll (employee_id, basic_pay, deductions, tax) VALUES
    -> (1,10000.00,1000.00,20.00),
    -> (2,20000.00,2000.00,25.00),
    -> (3,30000.00,3000.00,30.00),
    -> (4,40000.00,4000.00,35.00);
```

### Creating employee_department table
```
INSERT INTO employee_department (employee_id, department_id) VALUES
    -> (1,101),
    -> (1,102),
    -> (2,103),
    -> (3,101),
    -> (3,104),
    -> (4,101),
    -> (4,102),
    -> (4,104);
```

### Checking if database is working correctly
```
select employee.name, department.department_name, payroll.net_pay from employee, department, employee_department, payroll
    -> where employee.employee_id = employee_department.employee_id and
    -> department.department_id = employee_department.department_id and
    -> employee.employee_id = payroll.employee_id;
```
