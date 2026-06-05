# SQL-coding-questions

# 📊 Top SQL Interview Questions for Data Analysts

A collection of frequently asked SQL interview questions with optimized solutions.

---

## 🗂️ Sample Employee Table

| emp_id | name | salary | department_id | manager_id |
|--------|-------|---------|---------------|------------|
| 1 | Alice | 80000 | 1 | NULL |
| 2 | Bob | 60000 | 2 | 1 |
| 3 | Charlie | 75000 | 1 | 1 |
| 4 | David | 60000 | 3 | 2 |

---

# 1️⃣ Find the Second Highest Salary

### Solution (Using DISTINCT)

```sql
SELECT MAX(salary) AS second_highest_salary
FROM employees
WHERE salary < (
    SELECT MAX(salary)
    FROM employees
);
```

### Alternative (Using LIMIT)

```sql
SELECT DISTINCT salary
FROM employees
ORDER BY salary DESC
LIMIT 1 OFFSET 1;
```

---

# 2️⃣ Detect Duplicate Records

Find duplicate employee names.

```sql
SELECT
    name,
    COUNT(*) AS duplicate_count
FROM employees
GROUP BY name
HAVING COUNT(*) > 1;
```

---

# 3️⃣ Count Employees in Each Department

```sql
SELECT
    department_id,
    COUNT(*) AS total_employees
FROM employees
GROUP BY department_id;
```

---

# 4️⃣ Pull Employees Earning Above Average Salary

```sql
SELECT
    name,
    salary
FROM employees
WHERE salary >
(
    SELECT AVG(salary)
    FROM employees
);
```

---

# 5️⃣ Get the Nth Highest Salary

### Example: 3rd Highest Salary

```sql
SELECT DISTINCT salary
FROM employees
ORDER BY salary DESC
LIMIT 1 OFFSET 2;
```

### Generic Formula

```sql
LIMIT 1 OFFSET N-1
```

### Alternative Using DENSE_RANK()

```sql
SELECT salary
FROM
(
    SELECT
        salary,
        DENSE_RANK() OVER(
            ORDER BY salary DESC
        ) AS ranking
    FROM employees
) t
WHERE ranking = N;
```

---

# 6️⃣ List Employees With No Manager

```sql
SELECT
    emp_id,
    name
FROM employees
WHERE manager_id IS NULL;
```

---

# 7️⃣ Show Departments With More Than 5 Employees

```sql
SELECT
    department_id,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department_id
HAVING COUNT(*) > 5;
```

---

# 8️⃣ Find Names That Start With 'A'

```sql
SELECT
    name
FROM employees
WHERE name LIKE 'A%';
```

### Case-insensitive (PostgreSQL)

```sql
SELECT
    name
FROM employees
WHERE name ILIKE 'A%';
```

---

# 9️⃣ Find the Highest Salary by Department

```sql
SELECT
    department_id,
    MAX(salary) AS highest_salary
FROM employees
GROUP BY department_id;
```

### Along with Employee Name

```sql
SELECT
    e.name,
    e.department_id,
    e.salary
FROM employees e
JOIN
(
    SELECT
        department_id,
        MAX(salary) AS max_salary
    FROM employees
    GROUP BY department_id
) d
ON e.department_id = d.department_id
AND e.salary = d.max_salary;
```

---

# 🔟 Join Employees and Departments

## Department Table

| department_id | department_name |
|--------------|-----------------|
| 1 | HR |
| 2 | IT |
| 3 | Finance |

### Query

```sql
SELECT
    e.name,
    d.department_name
FROM employees e
INNER JOIN departments d
ON e.department_id = d.department_id;
```

### Output

| name | department_name |
|-------|----------------|
| Alice | HR |
| Bob | IT |
| Charlie | HR |
| David | Finance |

---

# 🚀 Quick Revision

| Question | SQL Concept |
|-----------|------------|
| Second Highest Salary | MAX(), Subquery |
| Duplicate Records | GROUP BY, HAVING |
| Employee Count | COUNT(), GROUP BY |
| Above Average Salary | AVG(), Subquery |
| Nth Highest Salary | LIMIT, DENSE_RANK() |
| Employees Without Manager | IS NULL |
| Departments > 5 Employees | GROUP BY, HAVING |
| Names Starting With A | LIKE |
| Highest Salary by Department | MAX(), GROUP BY |
| Employee & Department Details | JOIN |

---

## ⭐ Commonly Asked In

- Data Analyst Interviews
- SQL Developer Interviews
- Business Analyst Interviews
- Data Engineer Interviews
- Product Analyst Interviews

---
