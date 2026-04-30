------------------------------------------------------------------------

## Aim

To perform different types of joins and self-join operations using
MariaDB.

------------------------------------------------------------------------

## Software Used

-   MariaDB / MySQL
-   Visual Studio Code

------------------------------------------------------------------------

## Queries

### 1. Display all employees with their department name

``` sql
SELECT E.ENAME, D.DNAME
FROM EMPLOYEE E
JOIN DEPARTMENT D
ON E.DEPTNO = D.DEPTNO;
```

------------------------------------------------------------------------

### 2. Display employees whose manager name is JONES along with their manager name

``` sql
SELECT E.ENAME AS EMPLOYEE, M.ENAME AS MANAGER
FROM EMPLOYEE E
JOIN EMPLOYEE M
ON E.MGR = M.EMPNO
WHERE M.ENAME = 'JONES';
```

------------------------------------------------------------------------

### 3. Display employee name, job, department name and manager name

``` sql
SELECT 
E.ENAME,
E.JOB,
D.DNAME,
M.ENAME AS MANAGER
FROM EMPLOYEE E
LEFT JOIN EMPLOYEE M ON E.MGR = M.EMPNO
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO;
```

------------------------------------------------------------------------

### 4. List all employees name, job and department name except clerks, sorted by highest salary

``` sql
SELECT E.ENAME, E.JOB, E.SAL, D.DNAME
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
WHERE E.JOB <> 'CLERK'
ORDER BY E.SAL DESC;
```

------------------------------------------------------------------------

### 5. Display employee name, job and manager including employees without manager

``` sql
SELECT E.ENAME, E.JOB, M.ENAME AS MANAGER
FROM EMPLOYEE E
LEFT JOIN EMPLOYEE M
ON E.MGR = M.EMPNO;
```

------------------------------------------------------------------------

### 6. List employee name, job, annual salary, department number and department name for employees earning 36000 annually or not clerks

``` sql
SELECT 
E.ENAME,
E.JOB,
(E.SAL*12) AS ANNUAL_SAL,
E.DEPTNO,
D.DNAME
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
WHERE (E.SAL*12) >= 36000 OR E.JOB <> 'CLERK';
```

------------------------------------------------------------------------

### 7. List employee name, job, annual salary, department number and department name for employees earning 30000 annually and not clerks

``` sql
SELECT 
E.ENAME,
E.JOB,
(E.SAL*12) AS ANNUAL_SAL,
E.DEPTNO,
D.DNAME
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
WHERE (E.SAL*12) >= 30000 AND E.JOB <> 'CLERK';
```

------------------------------------------------------------------------

### 8. List employees along with their manager's name and number, showing 'No Manager' where applicable

``` sql
SELECT 
E.EMPNO,
E.ENAME,
IFNULL(M.EMPNO,'No Manager') AS MANAGER_NO,
IFNULL(M.ENAME,'No Manager') AS MANAGER_NAME
FROM EMPLOYEE E
LEFT JOIN EMPLOYEE M
ON E.MGR = M.EMPNO;
```

------------------------------------------------------------------------

### 9. Display department name, department number and sum of salary

``` sql
SELECT D.DNAME, D.DEPTNO, SUM(E.SAL) AS TOTAL_SALARY
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
GROUP BY D.DNAME, D.DEPTNO;
```

------------------------------------------------------------------------

### 10. Display employee number, name and department name of the department in which they work

``` sql
SELECT E.EMPNO, E.ENAME, D.DNAME
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO;
```

------------------------------------------------------------------------

### 11. Display employee name and department name for each employee

``` sql
SELECT E.ENAME, D.DNAME
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO;
```

------------------------------------------------------------------------

## Result

Join and self-join operations were successfully executed using MariaDB.
