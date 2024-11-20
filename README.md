# 19CS404- SUBQUERIES-AND-VIEWS
# Registration number: 212223240126

# AIM: 
To Study & Implementation of Sub queries Views 
 
# THEORY: 
SUBQUERIES: 
The query within another is known as a subquery. A statement containing a subquery is called a 
parent statement. The rows returned by subquery are used by the parent statement or in other 
words A subquery is a SELECT statement that is embedded in a clause of another SELECT 
statement 
 
You can place the subquery in a number of SQL clauses: 
1)WHERE clause 
2)HAVING clause 
3)FROM clause 
4)OPERATORS( IN.ANY,ALL,<,>,>=,<= etc..) 
 
# Types: 
1.Sub queries that return several values 
Sub queries can also return more than one value. Such results should be made use along with the 
operators in and any. 
 
2.Multiple queries 
Here more than one subquery is used. These multiple sub queries are combined by means of 
‘and’ & ‘or’ keywords. 
 
3.Correlated subquery 
A subquery is evaluated once for the entire parent statement whereas a correlated Sub query is 
evaluated once per row processed by the parent statement. 
 
 
 
# VIEW: 

In SQL, a view is a virtual table based on the result-set of an SQL statement. A view contains 
rows and columns, just like a real table. The fields in a view are fields from one or more real 
tables in the database. You can add SQL functions, WHERE, and JOIN statements to a view and 
present the data as if the data were coming from one single table. A view is a virtual table, which 
consists of a set of columns from one or more tables. It is similar to a table but it does not store 
in the database. View is a query stored as an object 
  
Syntax: 
CREATE VIEW AS 
SELECT FROM relation_name WHERE (Condition) 
 
DROPPING A VIEW: 
A view can be deleted with the DROP VIEW command. 
 
Syntax: DROP VIEW ; 
 
# Question 1: 
From the following tables write a SQL query to find all orders generated by New York-based 
salespeople. Return ord_no, purch_amt, ord_date, customer_id, salesman_id. 
 
Answer: 

SELECT Orders.ord_no, Orders.purch_amt, Orders.ord_date, Orders.customer_id, 
Orders.salesman_id 
FROM Orders 
JOIN Salesman ON Orders.salesman_id = Salesman.salesman_id 
WHERE Salesman.city = 'New York'; 

Output: 

 ![image](https://github.com/user-attachments/assets/2714a9eb-f64d-4a9c-acbb-b973e0dca3e2)

 
Question 2: 
Write a SQL query to Find employees who have an age less than the average age of employees 
with incomes over 1 million 
Employee Table 

![image](https://github.com/user-attachments/assets/f4c44c07-1f1a-4c48-ba21-210a1ba269d6)

 
Answer: 

SELECT id,name, age, city, income 
FROM Employee 
WHERE age < (SELECT AVG(age)
             FROM Employee  
             WHERE income > 1000000); 
 
Output: 
 
![image](https://github.com/user-attachments/assets/1f84c318-3c56-426f-b310-9c06fbcf7fe3)

Question 3: 
From the following tables write a SQL query to find the order values greater than the average 
order value of 10th October 2012. Return ord_no, purch_amt, ord_date, customer_id, 
salesman_id. 
Note: date should be yyyy-mm-dd format 
ORDERS TABLE 

![image](https://github.com/user-attachments/assets/71f65535-d446-4156-b338-59c4897063d0)

Answer: 

SELECT ord_no, purch_amt, ord_date, customer_id, salesman_id 
FROM Orders 
WHERE purch_amt > (SELECT AVG(purch_amt) 
                   FROM Orders 
                   WHERE ord_date = '2012-10-10'); 


Output: 

![image](https://github.com/user-attachments/assets/f435d383-111b-48c8-b125-7a74b1e3b433)
 
 
Question 4: 
Write a SQL query to Find employees who have an age less than the average age of employees 
with incomes over 2.5 Lakh 
Employee Table 

![image](https://github.com/user-attachments/assets/be9dd5aa-d94f-49b6-801c-3e5f1cb91542)

Answer: 

SELECT id,name, age, city, income 
FROM Employee 
WHERE age < (SELECT AVG(age)  
             FROM Employee  
             WHERE income > 250000); 
 
Output: 
 
![image](https://github.com/user-attachments/assets/03d8c9a9-3cfc-4a44-b29e-653de3668517)
 
Question 5: 
Write a SQL query to Identify customers whose city is different from the city of the customer 
with the highest ID 
SAMPLE TABLE: customer 

![image](https://github.com/user-attachments/assets/446b2491-d40d-480d-945f-b2a6a15d5798)

Answer: 

SELECT id, name, city, email, phone 
FROM customer 
WHERE city != (SELECT city  
               FROM customer  
               ORDER BY id DESC  
               LIMIT 1);
               
Output: 

![image](https://github.com/user-attachments/assets/65477e26-463a-40ce-b610-7f190b886a90)
 
 
Question 6: 
From the following tables write a SQL query to count the number of customers with grades 
above the average in New York City. Return grade and count. 
customer table 

![image](https://github.com/user-attachments/assets/b818730c-847d-4b6a-8981-75cb0f70fee9)

Answer: 

SELECT grade, COUNT(*) 
FROM customer 
WHERE  grade > (SELECT AVG(grade) FROM customer WHERE city = 'New York') 
GROUP BY grade; 


Output: 

 ![image](https://github.com/user-attachments/assets/c0da5304-f3ef-45d3-a8a7-68989829e460)

 
Question 7: 
Write a query to display all the customers whose ID is the difference between the salesperson ID 
of Mc Lyon and 2001. 

salesman table 
![image](https://github.com/user-attachments/assets/7edacfc0-7b6e-4d8f-8c5a-d9326c2535bb)

customer table 
![image](https://github.com/user-attachments/assets/b44d4c12-e227-43a1-9af2-30e380be7ed7)

Answer: 

SELECT customer_id, cust_name, city, grade, salesman_id 
FROM customer 
WHERE customer_id = ( 
    SELECT salesman_id - 2001 
    FROM salesman 
    WHERE name = 'Mc Lyon' 
); 

Output 
 
![image](https://github.com/user-attachments/assets/6a1bb04b-4eb0-43bd-9551-b211c7272cf8)
 
Question 8: 
From the following tables, write a SQL query to find all the orders issued by the salesman 'Paul 
Adam'. Return ord_no, purch_amt, ord_date, customer_id and salesman_id. 
 
Answer: 

SELECT ord_no, purch_amt, ord_date, customer_id, salesman_id 
FROM Orders 
WHERE salesman_id = ( 
    SELECT salesman_id  
    FROM Salesman  
    WHERE name = 'Paul Adam' 
); 
 
Output: 

![image](https://github.com/user-attachments/assets/9a40849c-55c5-4b3a-88b4-36db2875b4c5)


Question 9: 
Write a SQL query that retrieve all the columns from the table "Grades", where the grade is 
equal to the maximum grade achieved in each subject. 
Sample table: GRADES 
 
Answer: 
WITH MaxGrades AS ( 
    SELECT subject, MAX(grade) AS max_grade 
    FROM Grades 
    GROUP BY subject 
) 
 
SELECT g.* 
FROM Grades g 
JOIN MaxGrades mg ON g.subject = mg.subject AND g.grade = mg.max_grade; 
 
Output: 

![image](https://github.com/user-attachments/assets/74388b8a-f966-45ac-a8f6-4590c7b08d87)
 
 
Question 10: 
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose 
salary is greater than $4500. 
Sample table: CUSTOMERS 

![image](https://github.com/user-attachments/assets/7c82dc8f-f3be-451b-ae3d-d99b56797c0a)

 
Answer: 
SELECT * 
FROM CUSTOMERS 
WHERE SALARY > 4500; 
 
Output: 

![image](https://github.com/user-attachments/assets/d0f105ac-d4f5-42f4-a459-2594e641eaa8)
 
 
Result: 
Thus , the SQL queries to implement Sub queries Views have been executed successfully.
