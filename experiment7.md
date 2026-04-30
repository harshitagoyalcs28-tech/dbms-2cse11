
------------------------------------------------------------------------

## Aim

To perform advanced aggregate operations, date calculations and grouped
queries using MariaDB.

------------------------------------------------------------------------

## Software Used

-   Command prompt / MySQL
-   Visual Studio Code

------------------------------------------------------------------------

## Queries

### 1. Compute the number of days remaining in this year

``` sql
SELECT DATEDIFF(
    STR_TO_DATE(CONCAT(YEAR(CURDATE()),'-12-31'),'%Y-%m-%d'),
    CURDATE()
) AS DAYS_REMAINING;
```

------------------------------------------------------------------------

### 2. Find the highest and lowest salaries and the difference between them

``` sql
SELECT 
MAX(SAL) AS HIGHEST_SALARY,
MIN(SAL) AS LOWEST_SALARY,
MAX(SAL) - MIN(SAL) AS DIFFERENCE
FROM EMPLOYEE;
```

------------------------------------------------------------------------

### 3. List employees whose commission is greater than 25% of their salary

``` sql
SELECT ENAME, SAL, COMM
FROM EMPLOYEE
WHERE COMM > (SAL * 0.25);
```

------------------------------------------------------------------------

### 4. Display salary in dollar format

``` sql
SELECT ENAME, CONCAT('$', FORMAT(SAL,2)) AS SALARY_DOLLAR
FROM EMPLOYEE;
```

------------------------------------------------------------------------

### 5. Display job and total salary for each job based on department number (matrix query)

``` sql
SELECT DEPTNO, JOB, SUM(SAL) AS TOTAL_SALARY
FROM EMPLOYEE
GROUP BY DEPTNO, JOB;
```

------------------------------------------------------------------------

### 6. Display total employees and number hired in 1980, 1981, 1982 and 1983

``` sql
SELECT
COUNT(*) AS TOTAL_EMPLOYEES,
SUM(YEAR(HIREDATE)=1980) AS Y1980,
SUM(YEAR(HIREDATE)=1981) AS Y1981,
SUM(YEAR(HIREDATE)=1982) AS Y1982,
SUM(YEAR(HIREDATE)=1983) AS Y1983
FROM EMPLOYEE;
```

------------------------------------------------------------------------

### 7. Query to get the last Sunday of any month (current month)

``` sql
SELECT DATE_SUB(
    LAST_DAY(CURDATE()),
    INTERVAL (DAYOFWEEK(LAST_DAY(CURDATE())) - 1) DAY
) AS LAST_SUNDAY;
```

------------------------------------------------------------------------

### 8. Display department numbers and total number of employees working in each department

``` sql
SELECT DEPTNO, COUNT(*) AS TOTAL_EMPLOYEES
FROM EMPLOYEE
GROUP BY DEPTNO;
```

------------------------------------------------------------------------

### 9. Display various jobs and total number of employees within each job group

``` sql
SELECT JOB, COUNT(*) AS TOTAL_EMPLOYEES
FROM EMPLOYEE
GROUP BY JOB;
```

------------------------------------------------------------------------

### 10. Display department numbers and total salary for each department

``` sql
SELECT DEPTNO, SUM(SAL) AS TOTAL_SALARY
FROM EMPLOYEE
GROUP BY DEPTNO;
```

------------------------------------------------------------------------

## Result

Advanced aggregate and grouped SQL queries were successfully executed
using MariaDB.
