# SQL Queries for Customer, Product, and Orders Database

This repository contains SQL queries (DQL) to retrieve data from a relational database consisting of three tables: **Customer**, **Product**, and **Orders**.

## Table Structures

- **Customer** (`Customer_id` PK, customer_Name, customer_Tel)
- **Product** (`Product_id` PK, product_name, category, Price)
- **Orders** (`Customer_id`, `Product_id`, OrderDate, quantity, total_amount)  
  *Composite PK: (Customer_id, Product_id), FKs to Customer and Product*

## Queries

1. **Display all customers**  
   `SELECT * FROM Customer;`

2. **Products with price between 5000 and 10000**  
   `SELECT product_name, category FROM Product WHERE Price BETWEEN 5000 AND 10000;`

3. **All products sorted by price descending**  
   `SELECT * FROM Product ORDER BY Price DESC;`

4. **Order statistics (total orders, average, max, min total_amount)**  
   `SELECT COUNT(*), AVG(total_amount), MAX(total_amount), MIN(total_amount) FROM Orders;`

5. **Number of orders per product**  
   `SELECT Product_id, COUNT(*) FROM Orders GROUP BY Product_id;`

6. **Customers with more than 2 orders**  
   `SELECT Customer_id, COUNT(*) FROM Orders GROUP BY Customer_id HAVING COUNT(*) > 2;`

7. **Number of orders per month in 2020**  
   `SELECT EXTRACT(MONTH FROM OrderDate) AS month, COUNT(*) FROM Orders WHERE EXTRACT(YEAR FROM OrderDate) = 2020 GROUP BY EXTRACT(MONTH FROM OrderDate);`

8. **Order details with product name and customer name**  
   `SELECT o.OrderDate, p.product_name, c.customer_Name FROM Orders o JOIN Product p ON o.Product_id = p.Product_id JOIN Customer c ON o.Customer_id = c.Customer_id;`

9. **Orders made three months ago**  
   `SELECT * FROM Orders WHERE OrderDate >= ADD_MONTHS(SYSDATE, -3) AND OrderDate < SYSDATE;`

10. **Customers who never ordered**  
    `SELECT Customer_id FROM Customer WHERE Customer_id NOT IN (SELECT DISTINCT Customer_id FROM Orders);`

## Notes

- Date functions (`EXTRACT`, `ADD_MONTHS`, `SYSDATE`) follow Oracle SQL syntax.
- Adjust `BETWEEN` price range if needed.
- The `ADD_MONTHS(SYSDATE, -3)` clause assumes today’s date as reference; modify as required.
