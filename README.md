## LITA-CAPSTONE-PROJECT-ON-SQL
### ENEFU PATIENCE UBA PROJECT WORK WITH LITA
### PROJECT 1 AND 2

CREATE DATABASE PATIENCE_U_ENEFU_DB


select * from [dbo].[LITA Capstone project1]

Select * from [dbo].[LITA Capstone Dataset project NEW]

------retrieve the total sales for each product category-------

select Product, sum (TotalSales) as product_total_Sales 
from [dbo].[LITA Capstone project1]
Group by Product

select product, sum (Quantity) as Quantity_Revenue
from [dbo].[LITA Capstone project1]
Group by product

------find the number of sales transactions in each region-------

select Region, count (customer_id) as sales_by_Region from
[dbo].[LITA Capstone project1]
Group by region

------- the highest selling product of total sales value(revenue)----


select top 1 product, sum(Quantity*UnitPrice) as Total_Revenue
FROM [dbo].[LITA Capstone project1]
group by Product

----calculate total revenue per product------

select Product, sum (TotalSales) as product_total_Sales 
FROM [dbo].[LITA Capstone project1]
Group by product


----calculate monthly sales  totals for the current year----

select orderdate, sum(TotalSales) as Total_Sales 
FROM [dbo].[LITA Capstone project1]
where orderdate>='2024-01-01'
Group by orderdate

----find the top 5 customers by total purchase amount---

select customerId sum (TotalSales) as TotalSales, 
FROM [dbo].[LITA Capstone project1]
Group by customerId
order by TotalSales decs

------ calculate the percentage of total sales contributed by each region----

SELECT Region, SUM(TotalSales) AS RegionTotalSales,
FORMAT(ROUND((SUM(TotalSales) / CAST((SELECT SUM(TotalSales)
FROM [dbo].[LITA Capstone project1]) AS DECIMAL(10,2)) * 100), 1), '0.#') 
AS PercentageOfTotalSales
FROM [dbo].[LITA Capstone project1]
GROUP BY Region
ORDER BY PercentageOfTotalSales DESC

------identify products with no sales in the last quarter-----

SELECT Product FROM [dbo].[LITA Capstone project1]
GROUP BY Product
HAVING SUM(CASE 
WHEN OrderDate BETWEEN '2024-06-01' AND '2024-08-31' 
THEN 1 ELSE 0 END) = 0


Sql 2 project(Capstone Customer Data)

Select * from [dbo].[LITA Capstone Dataset project NEW]

------retrieve the total number of customers from each region-----

Select  Region, count(distinct CustomerID) as total_customers 
from [dbo].[LITA Capstone Dataset project NEW]
Group by Region;

---- the most popular subscription type by the number of customers----

Select top 1 SubscriptionType, count(distinct customerID) as total_customers
from [dbo].[LITA Capstone Dataset project NEW]
Group by SubscriptionType 
Order by total_customers desc;

-----find the customers who canceled their subscription whithin 6 months--

Select CustomerID from [dbo].[LITA Capstone Dataset project NEW]
Where datediff (month, SubscriptionStart, SubscriptionEnd) <= 6;

-----calculate the average subscription duration for all customers----

Select avg(datediff (day, SubscriptionStart, SubscriptionEnd)) as avg_Subscription_Duration
from [dbo].[LITA Capstone Dataset project NEW]

---find customers with subscriptions longer than 12 months-----

Select customerID
from [dbo].[LITA Capstone Dataset project NEW]
Where datediff(month, SubscriptionStart,SubscriptionEnd) > 12;

-----calculate total revenue by subscription type-----

Select SubscriptionType,
Sum(Revenue) as total_revenue 
from [dbo].[LITA Capstone Dataset project NEW]
Group by SubscriptionType;

-----find the top 3 regions by subscription cancellations-----

Select top 3 region,
Count(*) as SubscriptionEnd_count
from [dbo].[LITA Capstone Dataset project NEW]
Where SubscriptionEnd is null
Group by region
Order by SubscriptionEnd_count desc;


