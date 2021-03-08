## #4 SQL -> Creating your first complex Database

> 
Before we start, I would like you to go through the below article.
-  [How to C.R.U.D](https://carboncoffee.hashnode.dev/3-sql-greater-how-to-crud) 

# Let's First create a database for a company X

- The Below Tables show how and what information we need in tables.

Employee

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1615197710715/Ttz8gPTn1.png)
Branch
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1615195663580/YfeJIsDc4.png)
Branch supplier 
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1615195684817/1U1kBFiWA.png)
Client
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1615195714505/p5x6wLxjD.png)
Works with
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1615196709313/b8frkYvE9F.png)
- Let's start with creating the employee table.

```
CREATE TABLE employee (
    emp_id INT PRIMARY KEY,
    first_name VARCHAR(25),
    last_name VARCHAR(25),
    birth_date DATE,
    sex VARCHAR(1),
    salary INT,
    super_id INT,
    branch_id INT

);
``` 
- Now we need to create the branch table. 

```
CREATE TABLE branch(
    branch_id INT PRIMARY KEY,
    branch_name VARCHAR(40),
    mgr_id INT,
    mgr_start_date DATE,
    FOREIGN KEY(mgr_id) REFERENCES employee(emp_id) ON DELETE SET NULL
);
``` 
- Since there was no existence of a branch table earlier we were not able to define the FOREIGN keys, but now we can ALTER the TABLE.

```
ALTER TABLE employee
ADD FOREIGN KEY(branch_id)
REFERENCES branch(branch_id)
ON DELETE SET NULL;
``` 

- We can now create the client TABLE.

```
CREATE TABLE client(
    client_id INT PRIMARY KEY,
    client_name VARCHAR(25),
    branch_id INT,
    FOREIGN KEY(branch_id) REFERENCES branch(branch_id) ON DELETE SET NULL
``` 
- Now we should create the works_with TABLE.

```
CREATE TABLE works_with (
    emp_id INT,
    client_id INT,
    total_sales INT,
    PRIMARY KEY(emp_id,client_id),
    FOREIGN KEY(emp_id) REFERENCES employee(emp_id) ON DELETE CASCADE,
    FOREIGN KEY(client_id) REFERENCES client(client_id) ON DELETE CASCADE
);
``` 

-  Finally, we have to create the branch_supplier TABLE.

```
CREATE TABLE branch_supplier(
    branch_id INT,
    supplier_name VARCHAR(25),
    supply_type VARCHAR(25),
    PRIMARY KEY(branch_id,supplier_name),
    FOREIGN KEY(branch_id) REFERENCES branch(branch_id) ON DELETE CASCADE
);
``` 

- Now we can go ahead and start INSERTing the information INTO the TABLES. While Inserting into the employee table we need to keep in might that first, we need to insert the branch managers who are employees in this way we can later update the branches of the other employees.


```
INSERT INTO employee VALUES(1000,'Jaylee','Pascall','1995-11-15','M',25000,NULL,NULL);
INSERT INTO branch VALUES(1,'Accounts',1000,'2008-10-19');
UPDATE employee
SET branch_id = 1
WHERE emp_id = 1000;

INSERT INTO employee VALUES(1001,'Buck ','Brooks','1996-01-15','M',30000,NULL,NULL);
INSERT INTO branch VALUES(2,'Corporate',1001,'2008-10-19');
UPDATE employee
SET branch_id = 2
WHERE emp_id = 1001;

INSERT INTO employee VALUES(1002,'Luke','Geis','1992-01-15','M',40000,NULL,NULL);
UPDATE employee
SET branch_id = 1
WHERE emp_id = 1002;

INSERT INTO employee VALUES(1003,'Akaa','God','2001-01-15','M',60000,NULL,NULL);
UPDATE employee
SET branch_id = 2
WHERE emp_id = 1003;

INSERT INTO employee VALUES(1004,'Audrey','Audr','1999-01-15','M',60000,NULL,NULL);
UPDATE employee
SET branch_id = 2
WHERE emp_id = 1004;

-- once all the branch managers are completed we can directly insert the branch id instead of using the UPDATE on but here I just wanted to show you how to use the UPDATE command 

-- We now need to add the super_id, which is the Supervisor of each employee here we are keeping a single person as the supervisor.

UPDATE employee
SET super_id = 1000
WHERE emp_id = 1001;

UPDATE employee
SET super_id = 1000
WHERE emp_id = 1002;

UPDATE employee
SET super_id = 1000
WHERE emp_id = 1003;

UPDATE employee
SET super_id = 1000
WHERE emp_id = 1004;
``` 

- Now we have to take care of the other tables. Let us insert it into the branch supplier table.


```
INSERT INTO branch_supplier VALUES(1,'Classmate','Paper');
INSERT INTO branch_supplier VALUES(1,'Luxor','Pen');
INSERT INTO branch_supplier VALUES(2,'Classmate','Copies');
INSERT INTO branch_supplier VALUES(2,'Luxor','Pen');
``` 
- Now we can insert it into the client table.

```
INSERT INTO client VALUES(10,'Bank of India',1);
INSERT INTO client VALUES(20,'Bris',2);
INSERT INTO client VALUES(30,'Inco New',1);
INSERT INTO client VALUES(40,'Did',2);
``` 
- Finally, we need to tally and put the information into the works with the table to set the employee who works for a particular client.

```
INSERT INTO works_with VALUES(1000,10,55000);
INSERT INTO works_with VALUES(1001,20,90000);
INSERT INTO works_with VALUES(1002,30,55000);
INSERT INTO works_with VALUES(1003,40,55000);
INSERT INTO works_with VALUES(1004,20,90000);
``` 
- In order to see all the information we can use the below query.

```
SELECT * FROM employee;
SELECT * FROM branch;
SELECT * FROM branch_supplier;
SELECT * FROM client;
SELECT * FROM works_with;
``` 

- We have successfully populated the tables and in the next article we will work on some complex queries to get the required information out from this table.


## Thank-you! 

I am glad you made it to the end of this article. I hope you got to learn something, if so please leave a **Like** which will encourage me for my upcoming write-ups. 


> 
- [My GitHub Repos](https://github.com/akxat)  
- Connect with me on  [Linkedin](https://www.linkedin.com/in/sharma-akshat/) 
- Start  [your own blogs ](https://hashnode.com/@AkshatSharma/joinme) 

%%[wid-1]