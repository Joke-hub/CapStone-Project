# CapStone-Project
This Project help us to show the break down of data for a sales company and includes the metrics and tools used.

### Project Overview
This project involves the use of some tools such as Power BI, excel and SQL to help a company determine what needs to be done or how best to improve on their products and servicess. It also helps to show the progress made within a year and also know the loyalty of their customers / returning customers.

### Data Cleaning & Preparation
In the initial stage certain actions were performed
1. Data Loading and Inspection
2. Handling Missing Varibles
3. Formatting of cells
4. Data Visualization was also done.

### Data Source
The primary source of Data used was gotten from CapStone LITA Project

### Tool Used
- Microsoft Excel [Download here](https://www.microsoft.com/en-us/microsoft-365/excel?ocid=ORSEARCH_Bing&msockid=04bff806b0a966640250ed20b10567a6)
- SQL[Download here](https://www.bing.com/search?q=microsoft+sql+server+download&filters=dtbk:%22MCFjZ192NV9kb3dubG9hZCFjZ192NV9kb3dubG9hZCFkODhhZWI3ZC00ZTViLTNjOWItMTkwMC0zOTNlNmQ1ZmNmNGU%3d%22+sid:%22d88aeb7d-4e5b-3c9b-1900-393e6d5fcf4e%22&FORM=DEPNAV)
- Power BI [Download here](https://www.microsoft.com/en-us/power-platform/products/power-bi/downloads?msockid=04bff806b0a966640250ed20b10567a6)

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


