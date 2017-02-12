# BBI-Assess-Question-4
Question 4 of the BBI Assessment (SQL Calls)
1. Write a SQL Query to pull all customers

Select ID, NAME, ADDRESS, [PHONE NUMBER], EMAIL FROM Customers 

2. Write a SQL Query to pull all customers that have orders (no duplicates)

Select DISTINCT(cu.ID), cu.NAME, cu.ADDRESS, cu.[PHONE NUMBER], cu.EMAIL
from Customers cu inner join orders ord
on cu.id = ord.CUSTOMER_ID

3. Write a SQL Query to pull all customers that do not have orders

Select ID, NAME, ADDRESS, [PHONE NUMBER], EMAIL
FROM Customers WHERE ID NOT IN (Select CUSTOMER_ID FROM Orders)

4. If you had to create an index on these tables, which fields would you most likely index and why?

Primary indexes would be the ID fields.  I would probably put a secondary index on the CUSTOMER_ID field
of the Orders table.  If you had a business case where you needed to do something with another field you could
put an index on it (searching by email address or name for a customer as an example) but I would not do that unless a
business case or performance issue required it.

5. Write a query that lists each customer name, email, and the number of order they have

select cu.NAME, cu.EMAIL, COUNT(ord.ID)AS TotalOrders 
from customers cu inner join orders ord
on cu.id = ord.CUSTOMER_ID
group by cu.NAME, cu.EMAIL

6. Write a query that pulls all customers that have between 2 and 5 orders

select cu.NAME, cu.EMAIL, COUNT(ord.ID)AS TotalOrders 
from Customers cu inner join orders ord
on cu.id = ord.CUSTOMER_ID
group by cu.NAME, cu.EMAIL
having count(ord.ID) > 1 and Count(ord.ID) < 6
