# Customer-Orders

SELECT * FROM BIT_DB.customers LIMIT 20;

SELECT * FROM BIT_DB.JanSales LIMIT 20

SELECT count(orderID) FROM BIT_DB.JanSales 

SELECT COUNT(orderID) FROM BIT_DB.JanSales WHERE Product="iPhone"

SELECT * FROM BIT_DB.customers

SELECT acctnum FROM BIT_DB.customers cust
INNER JOIN BIT_DB.FebSales Feb
ON cust.order_id=FEB.orderid

SELECT distinct Product,price FROM BIT_DB.JanSales WHERE price in (SELECT  min(price)FROM BIT_DB.JanSales)

SELECT SUM(quantity)*price AS revenue, product FROM BIT_DB.JanSales GROUP BY product

SELECT SUM(Quantity), product, SUM(quantity)*price AS revenue FROM BIT_DB.FebSales WHERE location='548 Lincoln St, Seattle, WA 98101' GROUP BY product

SELECT count(cust.acctnum), avg(quantity*price) FROM BIT_DB.FebSales  Feb LEFT JOIN BIT_DB.customers cust ON FEB.orderid=cust.order_id WHERE Feb.Quantity>2
