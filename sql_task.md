## Создание таблиц и вставка данных

### Задание

Создайте таблицу **Employees** со следующими колонками:

- `employee_id` INT PRIMARY KEY
- `first_name` VARCHAR(50)
- `last_name` VARCHAR(50)
- `email` VARCHAR(100)
- `phone_number` VARCHAR(20)
- `hire_date` DATE
- `job_title` VARCHAR(50)
- `salary` DECIMAL(10, 2)
- `manager_id` INT
- `department_id` INT

```sql
CREATE TABLE Employees (
    employee_id INT PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    email VARCHAR(100),
    phone_number VARCHAR(20),
    hire_date DATE,
    job_title VARCHAR(50),
    salary DECIMAL(10, 2),
    manager_id INT,
    department_id INT
);
```

### Вставка данных

Вставьте в таблицу следующие данные:

```
(1, 'John', 'Smith', 'john.smith@example.com', '123-456-7890', '2018-01-15', 'Software Engineer', 6000.00, 3, 1)
(2, 'Jane', 'Doe', 'jane.doe@example.com', '987-654-3210', '2019-03-22', 'Project Manager', 7500.00, 3, 2)
(3, 'Emily', 'Jones', 'emily.jones@example.com', '555-555-5555', '2017-05-30', 'Director', 12000.00, NULL, 1)
(4, 'Michael', 'Brown', 'michael.brown@example.com', '111-222-3333', '2020-07-19', 'Business Analyst', 5500.00, 2, 3)
(5, 'Chris', 'Davis', 'chris.davis@example.com', '444-333-2222', '2016-11-10', 'Data Scientist', 7000.00, 2, 1)
(6, 'Patricia', 'Garcia', 'patricia.garcia@example.com', '333-444-5555', '2019-09-05', 'HR Specialist', 4800.00, 3, 2)
(7, 'Robert', 'Wilson', 'robert.wilson@example.com', '666-777-8888', '2021-04-25', 'Software Engineer', 6500.00, 1, 1)
(8, 'Linda', 'Martinez', 'linda.martinez@example.com', '999-000-1111', '2018-06-13', 'Software Engineer', 6200.00, 1, 3)
(9, 'Daniel', 'Taylor', 'daniel.taylor@example.com', '222-333-4444', '2015-08-30', 'Project Manager', 7800.00, 2, 3)
(10, 'Sophia', 'Anderson', 'sophia.anderson@example.com', '555-666-7777', '2020-02-18', 'Director', 12500.00, NULL, 2)
```

```sql
INSERT INTO Employees (
    employee_id, first_name, last_name, email, phone_number,
    hire_date, job_title, salary, manager_id, department_id
) VALUES
(1, 'John', 'Smith', 'john.smith@example.com', '123-456-7890', '2018-01-15', 'Software Engineer', 6000.00, 3, 1),
(2, 'Jane', 'Doe', 'jane.doe@example.com', '987-654-3210', '2019-03-22', 'Project Manager', 7500.00, 3, 2),
(3, 'Emily', 'Jones', 'emily.jones@example.com', '555-555-5555', '2017-05-30', 'Director', 12000.00, NULL, 1),
(4, 'Michael', 'Brown', 'michael.brown@example.com', '111-222-3333', '2020-07-19', 'Business Analyst', 5500.00, 2, 3),
(5, 'Chris', 'Davis', 'chris.davis@example.com', '444-333-2222', '2016-11-10', 'Data Scientist', 7000.00, 2, 1),
(6, 'Patricia', 'Garcia', 'patricia.garcia@example.com', '333-444-5555', '2019-09-05', 'HR Specialist', 4800.00, 3, 2),
(7, 'Robert', 'Wilson', 'robert.wilson@example.com', '666-777-8888', '2021-04-25', 'Software Engineer', 6500.00, 1, 1),
(8, 'Linda', 'Martinez', 'linda.martinez@example.com', '999-000-1111', '2018-06-13', 'Software Engineer', 6200.00, 1, 3),
(9, 'Daniel', 'Taylor', 'daniel.taylor@example.com', '222-333-4444', '2015-08-30', 'Project Manager', 7800.00, 2, 3),
(10, 'Sophia', 'Anderson', 'sophia.anderson@example.com', '555-666-7777', '2020-02-18', 'Director', 12500.00, NULL, 2);
```

---

## Задачи

1. Вывести все записи из таблицы **employees**.
```sql
SELECT
  *
FROM
  Employees;
```

2. Вывести только **имена** и **фамилии** сотрудников из таблицы **employees**.
```sql
SELECT
  first_name,
  last_name
FROM
  Employees;
```

3. Вывести всех сотрудников, работающих в отделе с идентификатором **5**.
```sql
SELECT
  *
FROM
  Employees
WHERE
  department_id = 5;
```

4. Вывести все уникальные значения **должностей** сотрудников из таблицы **employees**.
```sql
SELECT DISTINCT
  job_title
FROM
  Employees;
```

5. Вывести сотрудников, чья **зарплата превышает 5000**.
```sql
SELECT
  *
FROM
  Employees
WHERE
  salary > 5000;
```

6. Вывести сотрудников, чья фамилия **начинается с буквы 'S'**.
```sql
SELECT
  *
FROM
  Employees
WHERE
  last_name LIKE 'S%';
```

7. Вывести сотрудников, которые были **наняты после 1 января 2020 года**.
```sql
SELECT
  *
FROM
  Employees
WHERE
  hire_date > '2020-01-01';
```

8. Вывести **имена и фамилии** сотрудников, объединенные в одно поле через пробел, и их **зарплаты**.
```sql
SELECT
  CONCAT(first_name, ' ', last_name) AS full_name,
  salary
FROM
  Employees;
```

9. Вывести сотрудников, чьи **фамилии содержат подстроку 'son'**.
```sql
SELECT
  *
FROM
  Employees
WHERE
  last_name LIKE '%son%';
```

10. Вывести **количество сотрудников** в каждом отделе.
```sql
SELECT
  department_id,
  COUNT(*) AS employee_count
FROM
  Employees
GROUP BY
  department_id;
```

11. Вывести **среднюю зарплату** по каждому отделу.
```sql
SELECT
  department_id,
  AVG(salary) AS avg_salary
FROM
  Employees
GROUP BY
  department_id;
```

12. Вывести **минимальную и максимальную зарплаты** сотрудников.
```sql
SELECT
  MIN(salary) AS min_salary,
  MAX(salary) AS max_salary
FROM
  Employees;
```

13. Вывести сотрудников, чьи **зарплаты находятся в диапазоне от 4000 до 6000**.
```sql
SELECT
  *
FROM
  Employees
WHERE
  salary BETWEEN 4000 AND 6000;
```

14. Вывести **отделы** и **сумму зарплат** всех сотрудников в каждом отделе.
```sql
SELECT
  department_id,
  SUM(salary) AS total_salary
FROM
  Employees
GROUP BY
  department_id;
```

15. Вывести сотрудников, у которых **нет менеджера** (*manager_id IS NULL*).
```sql
SELECT
  *
FROM
  Employees
WHERE
  manager_id IS NULL;
```

16. Вывести **фамилии сотрудников в порядке возрастания**.
```sql
SELECT
  last_name
FROM
  Employees
ORDER BY
  last_name ASC;
```

17. Вывести **10 сотрудников с наибольшими зарплатами**.
```sql
SELECT
  *
FROM
  Employees
ORDER BY
  salary DESC
LIMIT
  10;
```

18. Вывести сотрудников, **нанятых в 2019 году**.
```sql
SELECT
  *
FROM
  Employees
WHERE
  hire_date BETWEEN '2019-01-01' AND '2019-12-31';
```

19. Вывести **количество сотрудников с каждой должностью**.
```sql
SELECT
  job_title,
  COUNT(*) AS count_per_title
FROM
  Employees
GROUP BY
  job_title;
```

20. Вывести всех **менеджеров** (*manager_id IS NOT NULL*) и их **подчиненных**.
```sql
SELECT
  manager_id,
  COUNT(*) AS subordinate_count
FROM
  employees
WHERE
  manager_id IS NOT NULL
GROUP BY
  manager_id;
```

21. Вывести **имена и фамилии сотрудников**, а также **идентификатор их отдела**, включая отдел с идентификатором **10**.
```sql
SELECT
  first_name,
  last_name,
  department_id
FROM
  Employees
WHERE
  department_id = 10
  OR department_id IS NOT NULL;
```

22. Вывести **названия должностей** и **количество сотрудников** на каждой должности, только если их количество **больше 5**.
```sql
SELECT
  job_title,
  COUNT(*) AS count_per_title
FROM
  Employees
GROUP BY
  job_title
HAVING
  COUNT(*) > 5;
```

23. Вывести **среднюю зарплату сотрудников**, работающих **под руководством менеджера с идентификатором 3**.
```sql
SELECT
  AVG(salary) AS avg_salary
FROM
  Employees
WHERE
  manager_id = 3;
```

24. Вывести **названия должностей** и **средние зарплаты сотрудников** на каждой должности.
```sql
SELECT
  job_title,
  AVG(salary) AS avg_salary
FROM
  Employees
GROUP BY
  job_title;
```

25. Вывести сотрудников, которые работают в **отделах с идентификаторами 1, 3 и 5**.
```sql
SELECT
  *
FROM
  Employees
WHERE
  department_id IN (1, 3, 5);
```

