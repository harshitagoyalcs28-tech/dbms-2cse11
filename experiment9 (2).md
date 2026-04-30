------------------------------------------------------------------------

## Aim

To perform data retrieval using subqueries and nested SQL queries in
MariaDB.

------------------------------------------------------------------------

## Software Used

-   MariaDB / MySQL
-   Visual Studio Code

------------------------------------------------------------------------

## Queries

### 1. Display the name of employee who earns the highest salary

``` sql
SELECT ENAME
FROM EMPLOYEE
WHERE SAL = (SELECT MAX(SAL) FROM EMPLOYEE);
```

------------------------------------------------------------------------

### 2. Display employee number and name of clerk earning highest salary among clerks

``` sql
SELECT EMPNO, ENAME
FROM EMPLOYEE
WHERE JOB = 'CLERK'
AND SAL = (
    SELECT MAX(SAL)
    FROM EMPLOYEE
    WHERE JOB = 'CLERK'
);
```

------------------------------------------------------------------------

### 3. Display names of salesman earning more than the highest salary of any clerk

``` sql
SELECT ENAME
FROM EMPLOYEE
WHERE JOB = 'SALESMAN'
AND SAL > (
    SELECT MAX(SAL)
    FROM EMPLOYEE
    WHERE JOB = 'CLERK'
);
```

------------------------------------------------------------------------

### 4. Display names of clerks earning more than JAMES but less than SCOTT

``` sql
SELECT ENAME
FROM EMPLOYEE
WHERE JOB = 'CLERK'
AND SAL > (SELECT SAL FROM EMPLOYEE WHERE ENAME = 'JAMES')
AND SAL < (SELECT SAL FROM EMPLOYEE WHERE ENAME = 'SCOTT');
```

------------------------------------------------------------------------

### 5. Display names of employees earning more than JAMES or more than SCOTT

``` sql
SELECT ENAME
FROM EMPLOYEE
WHERE SAL > (SELECT SAL FROM EMPLOYEE WHERE ENAME = 'JAMES')
OR SAL > (SELECT SAL FROM EMPLOYEE WHERE ENAME = 'SCOTT');
```

------------------------------------------------------------------------

### 6. Display employees earning highest salary in their respective departments

``` sql
SELECT ENAME, DEPTNO, SAL
FROM EMPLOYEE E
WHERE SAL = (
    SELECT MAX(SAL)
    FROM EMPLOYEE
    WHERE DEPTNO = E.DEPTNO
);
```

------------------------------------------------------------------------

### 7. Display employees earning highest salary in their respective job groups

``` sql
SELECT ENAME, JOB, SAL
FROM EMPLOYEE E
WHERE SAL = (
    SELECT MAX(SAL)
    FROM EMPLOYEE
    WHERE JOB = E.JOB
);
```

------------------------------------------------------------------------

### 8. Display employee names working in ACCOUNTING department

``` sql
SELECT ENAME
FROM EMPLOYEE
WHERE DEPTNO = (
    SELECT DEPTNO FROM DEPARTMENT
    WHERE DNAME = 'ACCOUNTING'
);
```

------------------------------------------------------------------------

### 9. Display employee names working in CHICAGO location

*(Assuming department location table exists as DEPT_LOC)*

``` sql
SELECT ENAME
FROM EMPLOYEE
WHERE DEPTNO IN (
    SELECT DEPTNO
    FROM DEPT_LOC
    WHERE LOCATION = 'CHICAGO'
);
```

------------------------------------------------------------------------

### 10. Display job groups having total salary greater than maximum salary of managers

``` sql
SELECT JOB, SUM(SAL) AS TOTAL_SALARY
FROM EMPLOYEE
GROUP BY JOB
HAVING SUM(SAL) > (
    SELECT MAX(SAL)
    FROM EMPLOYEE
    WHERE JOB = 'MANAGER'
);
```

------------------------------------------------------------------------

## Result

Subqueries and nested SQL queries were successfully executed using
MariaDB.
