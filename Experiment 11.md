# Experiment 11 - SQL Queries (MariaDB)

## Objective
To perform advanced SQL operations including DELETE, aggregation, subqueries, and grouping.

---

## Queries

### 1. Delete employees (before 31-Dec-82 & Mumbai/Delhi)
```sql
DELETE FROM employee
WHERE hiredate < '1982-12-31'
AND deptno IN (
    SELECT deptno FROM department
    WHERE location IN ('MUMBAI', 'DELHI')
);
```

### 2. Managers with dept and location
```sql
SELECT e.ename, e.job, d.dname, d.location
FROM employee e
JOIN department d ON e.deptno = d.deptno
WHERE e.job = 'MANAGER';
```

### 3. Salary = highest of grade
```sql
SELECT e.ename, e.sal
FROM employee e
JOIN salgrade s ON e.sal BETWEEN s.losal AND s.hisal
WHERE e.sal = (
    SELECT MAX(e2.sal)
    FROM employee e2
    JOIN salgrade s2 ON e2.sal BETWEEN s2.losal AND s2.hisal
    WHERE s2.grade = s.grade
);
```

### 4. Top 5 earners
```sql
SELECT ename, sal
FROM employee
ORDER BY sal DESC
LIMIT 5;
```

### 5. Highest salary employees
```sql
SELECT ename
FROM employee
WHERE sal = (SELECT MAX(sal) FROM employee);
```

### 6. Salary = average of max and min
```sql
SELECT *
FROM employee
WHERE sal = (
    (SELECT MAX(sal) FROM employee) +
    (SELECT MIN(sal) FROM employee)
) / 2;
```

### 7. Departments with at least 3 employees
```sql
SELECT d.dname
FROM department d
JOIN employee e ON d.deptno = e.deptno
GROUP BY d.dname
HAVING COUNT(*) >= 3;
```

### 8. Managers earning above average
```sql
SELECT ename
FROM employee
WHERE job = 'MANAGER'
AND sal > (SELECT AVG(sal) FROM employee);
```

### 9. Managers earning more than their employees avg
```sql
SELECT m.ename
FROM employee m
WHERE m.job = 'MANAGER'
AND m.sal > (
    SELECT AVG(e.sal)
    FROM employee e
    WHERE e.mgr = m.empno
);
```

### 10. Net pay >= any employee
```sql
SELECT ename, sal, comm, (sal + IFNULL(comm,0)) AS net_pay
FROM employee
WHERE (sal + IFNULL(comm,0)) >= ANY (
    SELECT (sal + IFNULL(comm,0)) FROM employee
);
```

---

## Notes
- Tables used: employee, department, salgrade
- Location values: MUMBAI, DELHI
- Net Pay = salary + commission

---

## Conclusion
This experiment demonstrates deletion, grouping, aggregation, and advanced subqueries in MariaDB.
