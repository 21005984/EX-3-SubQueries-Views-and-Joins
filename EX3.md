# EX 3 SubQueries, Views and Joins 
# AIM:
To create a manager database and execute DML queries using SQL.
# DML:
The SQL commands that deal with the manipulation of data present in the database belong to DML or Data Manipulation Language and this includes most of the SQL statements. It is the component of the SQL statement that controls access to data and to the database. Basically, DCL statements are grouped with DML statements.
## Create employee Table
```sql
CREATE TABLE EMP (EMPNO NUMBER(4) PRIMARY KEY,ENAME VARCHAR2(10),JOB VARCHAR2(9),MGR NUMBER(4),HIREDATE DATE,SAL NUMBER(7,2),COMM NUMBER(7,2),DEPTNO NUMBER(2));
```
## Insert the values
```sql
INSERT INTO EMP (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7369, 'SMITH', 'CLERK', 7902, '17-DEC-80', 800, NULL, 20);

INSERT INTO EMP (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7499, 'ALLEN', 'SALESMAN', 7698, '20-FEB-81', 1600, 300, 30);

INSERT INTO EMP (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7521, 'WARD', 'SALESMAN', 7698, '22-FEB-81', 1250, 500, 30);

INSERT INTO EMP (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7566, 'JONES', 'MANAGER', 7839, '02-APR-81', 2975, NULL, 20);

INSERT INTO EMP (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7654, 'MARTIN', 'SALESMAN', 7698, '28-SEP-81', 1250, 1400, 30);

INSERT INTO EMP (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7698, 'BLAKE', 'MANAGER', 7839, '01-MAY-81', 2850, NULL, 30);

INSERT INTO EMP (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7782, 'CLARK', 'MANAGER', 7839, '09-JUN-81', 2450, NULL, 10);

INSERT INTO EMP (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7788, 'SCOTT', 'ANALYST', 7566, '19-APR-87', 3000, NULL, 20);

INSERT INTO EMP (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7839, 'KING', 'PRESIDENT', NULL, '17-NOV-81', 5000, NULL, 10);

INSERT INTO EMP (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7844, 'TURNER', 'SALESMAN', 7698, '08-SEP-81', 1500, 0, 30);

INSERT INTO EMP (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7876, 'ADAMS', 'CLERK', 7788, '23-MAY-87', 1100, NULL, 20);

INSERT INTO EMP (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7900, 'JAMES', 'CLERK', 7698, '03-DEC-81', 950, NULL, 30);

INSERT INTO EMP (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7902, 'FORD', 'ANALYST', 7566, TO_DATE('03-DEC-81', 'DD-MON-RR'), 3000, 20, 20);

INSERT INTO EMP (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7934, 'MILLER', 'CLERK', 7782, TO_DATE('23-JAN-82', 'DD-MON-RR'), 1300, 10, 10);
```
# OUTPUT

![WhatsApp Image 2023-10-05 at 22 16 42_96135a87](https://github.com/21005984/EX-3-SubQueries-Views-and-Joins/assets/94748389/2201d11a-9adb-44cb-b2b1-e18f3aa2b360)

## Create department table
```sql
CREATE TABLE DEPT (DEPTNO NUMBER(2) PRIMARY KEY,DNAME VARCHAR2(14),LOC VARCHAR2(13));
```
## Insert the values in the department table
```sql
INSERT INTO DEPT (DEPTNO, DNAME, LOC) VALUES (10, 'ACCOUNTING', 'NEW YORK');

INSERT INTO DEPT (DEPTNO, DNAME, LOC) VALUES (20, 'RESEARCH', 'DALLAS');

INSERT INTO DEPT (DEPTNO, DNAME, LOC) VALUES (30, 'SALES', 'CHICAGO');

INSERT INTO DEPT (DEPTNO, DNAME, LOC) VALUES (40, 'OPERATIONS', 'BOSTON');
```

### Q1) List the name of the employees whose salary is greater than that of employee with empno 7566.
### QUERY:
~~~
select ename from emp where sal>(select sal from emp where empno=7566);
~~~
### OUTPUT:

![WhatsApp Image 2023-10-05 at 22 17 58_248fa1d2](https://github.com/21005984/EX-3-SubQueries-Views-and-Joins/assets/94748389/572a4d5f-cb14-44c2-83b5-bed4ae921311)

### Q2) List the ename,job,sal of the employee who get minimum salary in the company.
### QUERY:
~~~
select ename,job,sal from emp where sal=(select min(sal) from emp);
~~~
### OUTPUT:

![WhatsApp Image 2023-10-05 at 22 18 19_0d6a3106](https://github.com/21005984/EX-3-SubQueries-Views-and-Joins/assets/94748389/4d06d846-be9d-41d2-adbc-04a95740cb49)

### Q3) List ename, job of the employees who work in deptno 10 and his/her job is any one of the job in the department ‘SALES’.
### QUERY:
~~~
select ENAME,JOB from emp where deptno = 10 AND job in(select job from
emp where job='salesman');
~~~
### OUTPUT:

![WhatsApp Image 2023-10-05 at 22 18 43_10d11829](https://github.com/21005984/EX-3-SubQueries-Views-and-Joins/assets/94748389/07de97a5-21e5-45aa-b8be-50fc2dd20927)

### Q4) Create a view empv5 (for the table emp) that contains empno, ename, job of the employees who work in dept 10.
### QUERY:
~~~
create view emv5 as select empno,ename,job from emp where deptno=10;
select ename,empno,job from emv5;
~~~
### OUTPUT:

![WhatsApp Image 2023-10-05 at 22 19 40_2c853eeb](https://github.com/21005984/EX-3-SubQueries-Views-and-Joins/assets/94748389/c2f4b8f3-fe1a-4b8c-8074-bbf4374245e9)


### Q5) Create a view with column aliases empv30 that contains empno, ename, sal of the employees who work in dept 30. Also display the contents of the view.
### QUERY:
~~~
create view empv30 as select empno,ename,sal from emp where deptno=30;
select ename,empno,sal from empv30;
~~~
### OUTPUT:

![WhatsApp Image 2023-10-05 at 22 21 40_fa451495](https://github.com/21005984/EX-3-SubQueries-Views-and-Joins/assets/94748389/3920e76e-c119-42f0-ba45-5b0a7786d937)

### Q6) Update the view empv5 by increasing 10% salary of the employees who work as ‘CLERK’. Also confirm the modifications in emp table
### QUERY:
~~~
update empv5 set sal = sal+(sal*0.1) where job='clerk':
~~~
### OUTPUT:

![image](https://github.com/21005984/EX-3-SubQueries-Views-and-Joins/assets/94748389/1f874bca-56a4-4a9b-8ad7-9b244d49e06e)


## Create a Customer1 Table
```sql
CREATE TABLE Customer1 (customer_id INT,cust_name VARCHAR(20),city VARCHAR(20),grade INT,salesman_id INT);
```
## Inserting Values to the Table
```sql
INSERT INTO Customer1 (customer_id, cust_name, city, grade, salesman_id) VALUES(3002, 'Nick Rimando', 'New York', 100, 5001);
INSERT INTO Customer1 (customer_id, cust_name, city, grade, salesman_id) VALUES(3007, 'Brad Davis', 'New York', 200, 5001);
INSERT INTO Customer1 (customer_id, cust_name, city, grade, salesman_id) VALUES(3005, 'Graham Zusi', 'California', 200, 5002);
INSERT INTO Customer1 (customer_id, cust_name, city, grade, salesman_id) VALUES(3008, 'Julian Green', 'London', 300, 5002);
INSERT INTO Customer1 (customer_id, cust_name, city, grade, salesman_id) VALUES(3004, 'Fabian Johnson', 'Paris', 300, 5006);
INSERT INTO Customer1 (customer_id, cust_name, city, grade, salesman_id) VALUES(3009, 'Geoff Cameron', 'Berlin', 100, 5003);
INSERT INTO Customer1 (customer_id, cust_name, city, grade, salesman_id) VALUES(3003, 'Jozy Altidor', 'Moscow', 200, 5007);
INSERT INTO Customer1 (customer_id, cust_name, city, grade, salesman_id) VALUES(3001, 'Brad Guzan', 'London', NULL, 5005);
```
## Create a Salesperson1 table
```sql
CREATE TABLE Salesman1 (salesman_id INT,name VARCHAR(20),city VARCHAR(20),commission DECIMAL(4,2));
```
## Inserting Values to the Table
```sql
INSERT INTO Salesman1 (salesman_id, name, city, commission) VALUES(5001, 'James Hoog', 'New York', 0.15);
INSERT INTO Salesman1 (salesman_id, name, city, commission) VALUES(5002, 'Nail Knite', 'Paris', 0.13);
INSERT INTO Salesman1 (salesman_id, name, city, commission) VALUES(5005, 'Pit Alex', 'London', 0.11);
INSERT INTO Salesman1 (salesman_id, name, city, commission) VALUES(5006, 'Mc Lyon', 'Paris', 0.14);
INSERT INTO Salesman1 (salesman_id, name, city, commission) VALUES(5007, 'Paul Adam', 'Rome', 0.13);
INSERT INTO Salesman1 (salesman_id, name, city, commission) VALUES(5003, 'Lauson Hen', 'San Jose', 0.12);
```
# OUTPUT:

![WhatsApp Image 2023-10-05 at 22 23 10_064a0bf5](https://github.com/21005984/EX-3-SubQueries-Views-and-Joins/assets/94748389/8f5a89a6-24f2-4010-98bd-e91d2d955c4f)

### Q7) Write a SQL query to find the salesperson and customer who reside in the same city. Return Salesman, cust_name and city.
### QUERY:
~~~
select salesman1.name AS "salesman",customer1.cust_name AS "customername",customer1.city
from salesman1,customer1 where salesman1.city=customer1.city;
~~~
### OUTPUT:

![WhatsApp Image 2023-10-05 at 22 23 54_1a3b9b24](https://github.com/21005984/EX-3-SubQueries-Views-and-Joins/assets/94748389/b384b12e-7f28-4d0e-8864-963b25678f7f)


### Q8) Write a SQL query to find salespeople who received commissions of more than 13 percent from the company. Return Customer Name, customer city, Salesman, commission.
### QUERY:
~~~
select customer1.cust_name as "CUSTOMER NAME",customer1.city as "CUSTOMER CITY", salesman1.name as "SALESMAN NAME",salesman1.commission as "COMMISSION" from salesman1 INNER JOIN customer1 on salesman1.salesman_id = customer1.salesman_id where salesman1.commission > 0.13;
~~~
### OUTPUT:

![WhatsApp Image 2023-10-05 at 22 26 08_7229eccc](https://github.com/21005984/EX-3-SubQueries-Views-and-Joins/assets/94748389/057db4d9-a0c0-4cb7-bc4b-8a767f92f0f9)

### Q9) Perform Natural join on both tables
### QUERY:
~~~
select * from customer1 NATURAL JOIN salesman1;
~~~
### OUTPUT:

![WhatsApp Image 2023-10-05 at 22 27 05_1296c670](https://github.com/21005984/EX-3-SubQueries-Views-and-Joins/assets/94748389/55c3ddfd-f15e-4963-a672-e10afe0655bc)

### Q10) Perform Left and right join on both tables
### QUERY:
~~~
select * from salesman1 LEFT JOIN customer1 on salesman1.salesman_id=customer1.salesman_id;
select * from salesman1 RIGHT JOIN customer1 on salesman1.salesman_id = customer1.salesman_id;
~~~
### OUTPUT:

![WhatsApp Image 2023-10-05 at 22 27 59_595b2737](https://github.com/21005984/EX-3-SubQueries-Views-and-Joins/assets/94748389/1d835a1c-9615-447e-ac75-937336f5a19e)

![WhatsApp Image 2023-10-05 at 22 28 21_cc46fb34](https://github.com/21005984/EX-3-SubQueries-Views-and-Joins/assets/94748389/c5b66483-5af5-4449-95fe-ac5170ce4066)

# RESULT:
The program has been executed successfully for the above queries.

