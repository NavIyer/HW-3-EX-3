
# JOINS on HR Database

### 1)

Write a query in SQL to display the first name, last name, department number, and department name for each employee.

```sql
SELECT employees.first_name,
       employees.last_name,
       departments.department_id,
       departments.department_name
  FROM employees
  INNER JOIN departments
    ON employees.department_id = departments.department_id;
```

### 2)

Write a query in SQL to display the first and last name, department, city, and state province for each employee.

```sql
SELECT 
    employees.first_name, employees.last_name, departments.department_name, locations.city, locations.state_province
  FROM employees
  INNER JOIN departments
    ON employees.department_id = departments.department_id
  INNER JOIN locations
    ON departments.location_id = locations.location_id;
```

### 3)

Write a query in SQL to display all departments including those where does not have any employee.

```sql
SELECT DEPARTMENT_NAME FROM departments;
```

# JOINS on Sales Database

### 1)

```sql
SELECT s.name,
       c.cust_name,
       c.city
  FROM salesman s
  INNER JOIN customer c
    ON s.city = c.city;
```

This query will return the name of the salesman, the name of the customer, and the city of the customer, where the city of the salesman is equal to the city of the customer.

### 2)

```sql
SELECT c.cust_name AS "Customer Name",
       c.city,
       s.name AS "Salesman",
       s.commission
  FROM customer c
  INNER JOIN salesman s
    ON c.salesman_id = s.salesman_id
  WHERE s.commission > 0.12;
```

This query will return the name of the customer, the city of the customer, the name of the salesman, and the commission of the salesman, where the commission of the salesman is greater than 0.12 and the salesman_id of the customer is equal to the salesman_id of the salesman.

# SUBQUERIES on HR Database

### 1)

Write a query to display the name (first name and last name) for those employees who gets more salary than the employee whose ID is 163.

```sql
SELECT first_name,
       last_name
  FROM employees
  WHERE salary > (SELECT salary
                    FROM employees
                    WHERE employee_id = 163);
```

### 2)

Write a query to display the employee id, employee name (first name and last name) for all employees who earn more than the average salary.

```sql
SELECT employee_id,
       first_name,
       last_name
  FROM employees
  WHERE salary > (SELECT AVG(salary)
                    FROM employees);
```

### 3)

Write a query to display all the information of an employee whose salary and reporting person id is 3000 and 121, respectively.

```sql
SELECT *
  FROM employees
  WHERE salary = 3000
    AND manager_id = 121;
```

# SUBQUERIES on Sales Database

### 1)

```sql
SELECT *
  FROM orders
  WHERE salesman_id = (SELECT salesman_id
                         FROM salesman
                         WHERE name = 'Paul Adam');
```

This query returns all the information about the orders made by a salesman with the name 'Paul Adam'.

### 2)

```sql
SELECT *
  FROM orders
  WHERE salesman_id = (SELECT salesman_id
                         FROM salesman
                         WHERE city = 'London');
```

This query returns all the information about the orders made by any salesman who is located in London.

### 3) (bonus)

```sql
SELECT ord_date,
       SUM(purch_amt)
  FROM orders a
  GROUP BY ord_date
  HAVING SUM(purch_amt) > (SELECT MAX(purch_amt) + 1000
                             FROM orders b
                             WHERE a.ord_date = b.ord_date);
```

This query returns the order date and the total purchase amount for each order date, where the total purchase amount is greater than the maximum purchase amount plus 1000 for that order date.




