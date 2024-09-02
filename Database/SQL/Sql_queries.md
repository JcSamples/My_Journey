
# SQL Queries Documentation

This document contains a series of SQL queries translated to English and with fictitious names for security purposes. Each block of SQL is labeled with a comment explaining its purpose.


```sql
-- 1. Count the total number of customers
SELECT COUNT(*) AS total_customers
FROM customers;

-- 2. Count the number of customers with the job title 'Purchasing Manager'
SELECT COUNT(*)
FROM customers
WHERE job_title LIKE 'Purchasing Manager';

-- 3. List distinct payment types from orders where the payment type is not null
SELECT DISTINCT payment_method AS [Payment Types]
FROM orders
WHERE payment_method IS NOT NULL;

-- 4. Retrieve all orders where the shipping date is null
SELECT *
FROM orders
WHERE shipping_date IS NULL;

-- 5. Calculate the average final price of products
SELECT AVG(final_price) AS average_price
FROM products;

-- 6. Count the number of orders by location
SELECT location, COUNT(*) AS order_count
FROM orders
GROUP BY location;

-- 7. Count the number of customers grouped by job title and location
SELECT job_title, location, COUNT(*) AS customer_count
FROM customers
GROUP BY job_title, location;

-- 8. Count payment methods that were used more than 5 times
SELECT payment_method, COUNT(*) AS payment_count
FROM orders
GROUP BY payment_method
HAVING COUNT(payment_method) > 5;

-- 9. Find the number of orders sent in May 2006
-- Note: Dates should be in the format 'year-month-day'
SELECT COUNT(*) AS may_orders
FROM orders
WHERE shipping_date BETWEEN '2006-05-01' AND '2006-05-31';

-- 10. Show all orders (Order Code) made by the customer John Doe
SELECT orders.OrderCode, customers.first_name, customers.last_name
FROM orders
JOIN customers ON customers.id = orders.CustomerID
WHERE customers.first_name = 'John' AND customers.last_name = 'Doe';

-- 11. Show the order code, quantity, and price for purchases made by customer John Doe
SELECT orders.OrderCode, purchases.Quantity, purchases.Price
FROM orders
JOIN purchases ON orders.OrderCode = purchases.OrderCode
JOIN customers ON customers.id = orders.CustomerID
WHERE customers.first_name = 'John' AND customers.last_name = 'Doe';

-- 12. Show the order code, shipping date, and employee name for orders handled by employee Sarah Lee
SELECT orders.OrderCode, orders.ShippingDate, employees.first_name
FROM orders
JOIN employees ON orders.EmployeeID = employees.id
WHERE employees.first_name = 'Sarah' AND employees.last_name = 'Lee'
AND shipping_date IS NOT NULL;

-- 13. Count the number of orders handled by employee Sarah Lee with a non-null shipping date
SELECT COUNT(*) AS handled_orders
FROM orders
JOIN employees ON orders.EmployeeID = employees.id
WHERE employees.first_name = 'Sarah' AND employees.last_name = 'Lee'
AND shipping_date IS NOT NULL;

-- 14. List product names from purchases
SELECT products.Name
FROM purchases
JOIN products ON products.ID = purchases.ProductID;

-- 15. Find the most purchased product with at least 5 purchases
SELECT TOP 1 products.Name, COUNT(*) AS purchase_count
FROM products
JOIN purchases ON purchases.ProductID = products.Id
GROUP BY products.Name
HAVING COUNT(*) >= 5
ORDER BY purchase_count DESC;

-- 16. Find the most purchased product with at least 3 purchases
SELECT TOP 1 products.Name, COUNT(*) AS purchase_count
FROM products
JOIN purchases ON purchases.ProductID = products.Id
GROUP BY products.Name
HAVING COUNT(*) >= 3
ORDER BY purchase_count DESC;

-- 17. List customers who have not placed any orders
SELECT Id, first_name, last_name 
FROM customers
WHERE Id NOT IN (SELECT customers.Id FROM customers
JOIN orders ON customers.Id = orders.CustomerID);
```

