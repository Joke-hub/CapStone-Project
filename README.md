# CapStone-Project
This Project us to help show the break down of data for a sales company and includes the metrics and tools used.

### Data Cleaning & Preparation
In the initial stage certain actions were performed
1. Data Loading and Inspection
2. Handling Missing Varibles
3. Formatting of cells
4. Data Visualization was also done.

### Exploratory Data Analysis
In this Phase we were able to calulate the
- Average of data
- Total Revenue
- Maximum Subscriptions
- Top performing region
- % of total sale

  ### Data Visualization
This helps shows what we ave on our dashboard and helps with a beautiful presentation of our Data.


### Data Analysis
This includes Basic Lines of Code or Queries used during analysis
~~~SQL
Select * from [dbo].[Sales Performance Data]
Select Product, SUM(Total_revenuE) as Total_Sales FROM [dbo].[Sales Performance Data] GROUP BY Product


Select Region, COUNT(Total_revenuE) as Number_Sales FROM [dbo].[Sales Performance Data] GROUP BY Region

Select MAX(Product), Count(*) as Highest_Selling_Product FROM [dbo].[Sales Performance Data]

Select Datename(Month, OrderDate) AS Month,
Sum (Total_revenuE) AS MonthlySalesTotal
From [dbo].[Sales Performance Data]
GROUP BY datename (Month, OrderDate)


Select TOP 5 Customer_id, sum(Total_revenuE) as Total_Purchase from [dbo].[Sales Performance Data]
Group by Customer_id Order by Total_Purchase Desc

WITH Total_revenue AS (
    SELECT SUM(Total_revenuE) AS TotalSalesAmount
    FROM [dbo].[Sales Performance Data]
)
SELECT
    Region,
    SUM(Total_revenuE) AS RegionSales,
    (SUM(Total_revenuE) * 100.0 / (SELECT TotalSalesAmount FROM Total_revenuE)) AS PercentageContribution
FROM [dbo].[Sales Performance Data]
GROUP BY Region;

Select Product From [dbo].[Sales Performance Data]
GROUP BY Product
Having Max(OrderDate) < DATEADD(Quarter, -1, GetDate())



Subscription Table

Select * from [dbo].[Subscription Data]

Select Region, Count(CustomerName) as Total_Customer FROM [dbo].[Subscription Data] GROUP BY Region

Select TOP 1 SubscriptionType, Count (CustomerName) As total_Customer From [dbo].[Subscription Data]
Group By SubscriptionType
Order by Total_Customer DESC
SELECT CustomerName
FROM [dbo].[CustomerData]
WHERE Canceled = 1
AND DATEDIFF(MONTH, SubscriptionStart, SubscriptionEnd) <= 6;

----Average subscription duration for all customers----
SELECT AVG(DATEDIFF(DAY, SubscriptionStart, SubscriptionEnd)) AS AverageSubscriptionDuration
FROM [dbo].[CustomerData]

----Customers with subscription longer than 12 months---
SELECT CustomerName
FROM [dbo].[CustomerData]
WHERE DATEDIFF(MONTH, SubscriptionStart, SubscriptionEnd) > 12;

---Total Revenue by subscription type---
SELECT SubscriptionType, SUM(Revenue) AS TotalRevenue
FROM [dbo].[CustomerData]
GROUP BY SubscriptionType;

----Top 3 regions by subscription cancellation---
SELECT TOP 3 Region, COUNT(CustomerID) AS Cancellations
FROM [dbo].[CustomerData]
WHERE Canceled = 1
GROUP BY Region
ORDER BY Cancellations DESC;

---total number of active and cancelled subscription---
SELECT
    SUM(CASE WHEN Canceled = 0 THEN 1 ELSE 0 END) AS ActiveSubscriptions,
    SUM(CASE WHEN Canceled = 1 THEN 1 ELSE 0 END) AS CanceledSubscriptions
FROM [dbo].[CustomerData]
```


