# Experiment 10 : SQL Subqueries (ANY, ALL, EXISTS & Correlated)


## Q1. Display the names of employees from department number 10 with salary greater than that of any employee working in other departments.

```sql
SELECT ENAME, SAL
FROM EMP
WHERE DEPTNO = 10
  AND SAL > ANY (
      SELECT SAL FROM EMP WHERE DEPTNO <> 10
  );
```

---

## Q2. Display the names of employees from department number 10 with salary greater than that of all employees working in other departments.

```sql
SELECT ENAME, SAL
FROM EMP
WHERE DEPTNO = 10
  AND SAL > ALL (
      SELECT SAL FROM EMP WHERE DEPTNO <> 10
  );
```

---

## Q3. Display the details of employees who are in sales dept and grade is C.

```sql
SELECT E.*
FROM EMP E
JOIN DEPT D     ON E.DEPTNO = D.DEPTNO
JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
WHERE D.DNAME = 'SALES'
  AND S.GRADE = 'C';
```

---

## Q4. Display those who are not managers and who manage anyone.

```sql
-- Employees whose EMPNO appears as MGR (they manage someone)
-- but whose JOB is not 'MANAGER'
SELECT ENAME, JOB
FROM EMP
WHERE JOB <> 'MANAGER'
  AND EMPNO IN (SELECT DISTINCT MGR FROM EMP WHERE MGR IS NOT NULL);
```

---

## Q5. Display those employees whose manager's name is JONES.

```sql
SELECT E.ENAME, E.JOB
FROM EMP E
WHERE E.MGR = (
    SELECT EMPNO FROM EMP WHERE ENAME = 'JONES'
);
```

---

## Q6. Display ename who are working in sales dept.

```sql
SELECT E.ENAME
FROM EMP E
WHERE E.DEPTNO = (
    SELECT DEPTNO FROM DEPT WHERE DNAME = 'SALES'
);
```

---

## Q7. Display employee name, deptname, salary and comm for those with salary between 2000 to 5000 while location is Chennai.

```sql
SELECT E.ENAME, D.DNAME, E.SAL, E.COMM
FROM EMP E
JOIN DEPT D ON E.DEPTNO = D.DEPTNO
WHERE E.SAL BETWEEN 2000 AND 5000
  AND D.LOCATION = 'CHENNAI';
```

---

## Q8. Display those employees whose salary is greater than their manager's salary.

```sql
SELECT E.ENAME AS EMPLOYEE, E.SAL AS EMP_SAL,
       M.ENAME AS MANAGER,  M.SAL AS MGR_SAL
FROM EMP E
JOIN EMP M ON E.MGR = M.EMPNO
WHERE E.SAL > M.SAL;
```

---

## Q9. Display those employees who are working in the same dept where their manager is working.

```sql
SELECT E.ENAME AS EMPLOYEE, E.DEPTNO
FROM EMP E
JOIN EMP M ON E.MGR = M.EMPNO
WHERE E.DEPTNO = M.DEPTNO;
```

---

## Q10. Display grade and employees name for dept no 10 or 30 but grade is not 4, while joined the company before 31-dec-82.

```sql
-- Note: SALGRADE uses CHAR grade (A-E), so 'grade is not 4' is interpreted as
-- using the numeric equivalent. In a char-grade schema this condition is always
-- true; adjust if your schema uses numeric grades.
SELECT S.GRADE, E.ENAME, E.DEPTNO, E.HIREDATE
FROM EMP E
JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
WHERE E.DEPTNO IN (10, 30)
  AND S.GRADE <> '4'
  AND E.HIREDATE < '1982-12-31';
```
