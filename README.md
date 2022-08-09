# Customer-Orders

SELECT * FROM BIT_DB.customers LIMIT 20;

SELECT * FROM BIT_DB.JanSales LIMIT 20

#1. How many orders were placed in January? 
SELECT count(orderID) FROM BIT_DB.JanSales 

#2. How many of those orders were for an iPhone? 
SELECT COUNT(orderID) FROM BIT_DB.JanSales WHERE Product="iPhone"

#3. Select the customer account numbers for all the orders that were placed in February. 
SELECT acctnum FROM BIT_DB.customers cust
INNER JOIN BIT_DB.FebSales Feb
ON cust.order_id=FEB.orderid

#4. Which product was the cheapest one sold in January, and what was the price? 
SELECT distinct Product,price FROM BIT_DB.JanSales WHERE price in (SELECT  min(price)FROM BIT_DB.JanSales)

#5. What is the total revenue for each product sold in January?
SELECT SUM(quantity)*price AS revenue, product FROM BIT_DB.JanSales GROUP BY product

#6. Which products were sold in February at 548 Lincoln St, Seattle, WA 98101, how many of each were sold, and what was the total revenue?
SELECT SUM(Quantity), product, SUM(quantity)*price AS revenue FROM BIT_DB.FebSales WHERE location='548 Lincoln St, Seattle, WA 98101' GROUP BY product

#7. How many customers ordered more than 2 products at a time, and what was the average amount spent for those customers? 
SELECT count(cust.acctnum), avg(quantity*price) FROM BIT_DB.FebSales  Feb LEFT JOIN BIT_DB.customers cust ON FEB.orderid=cust.order_id WHERE Feb.Quantity>2

SELECT orderdate
FROM BIT_DB.FebSales
WHERE orderdate between '02/13/19 00:00' AND '02/18/19 00:00'

SELECT location
FROM BIT_DB.FebSales
WHERE orderdate = '02/18/19 01:35'

SELECT SUM (quantity)
FROM BIT_DB.FebSales
WHERE orderdate LIKE '02/18/19%'

SELECT distinct Product
FROM BIT_DB.FebSales
WHERE Product LIKE '%Batteries%'

SELECT distinct Product, Price
FROM BIT_DB.FebSales
WHERE Price LIKE '%.99'

8.List all the products sold in Los Angeles in February, and include how many of each were sold.
SELECT Product, SUM(quantity)
FROM BIT_DB.FebSales
WHERE location like '%LosAngeles%'
GROUP BY Product

9.Which locations in New York received at least 3 orders in January, and how many orders did they each receive?
SELECT distinct location, COUNT (orderID)
FROM BIT_DB.JanSales
WHERE location like '%NY%'
GROUP BY location
HAVING count(orderID)>2

10.How many of each type of headphone were sold in February?
SELECT SUM(Quantity) AS quantity, Product
FROM BIT_DB.FebSales
WHERE Product LIKE '%headphones%'
GROUP BY Product

11. What was the average amount spent per account in February?
SELECT SUM(quantity*price)/COUNT(cust.acctnum)
FROM BIT_DB.FebSales Feb
LEFT JOIN BIT_DB.customers cust
ON FEB.orderid=cust.order_id

12. What was the average quantity of products purchased per account in February?
SELECT SUM(quantity)/COUNT(cust.acctnum)
FROM BIT_DB.FebSales Feb
LEFT JOIN BIT_DB.customers cust
ON FEB.orderid=cust.order_id

13. Which product brought in the most revenue in January and how much revenue did it bring in total?
SELECT product, SUM(quantity*price)
FROM BIT_DB.JanSales
GROUP BY product
ORDER BY SUM(quantity*price) desc LIMIT 1

