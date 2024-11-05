# LITA-CUSTOMER-SUBCRIPTION-ANALYSIS

## Project Title: LITA Wave Subscription Hub

## Project Overview
The LITA Wave Subscription Hub aims to analyze customer subscription data to uncover valuable insights that inform business strategies, enhance customer engagement, and drive revenue growth. By leveraging data analytics, the project seeks to identify patterns in customer behavior, monitor subscription performance, and develop strategies to reduce cancellations and improve renewals.

## Data Sources
The primary source for the LITA Wave Subscription Hub is the customer data, which includes a comprehensive dataset featuring fields such as Customer ID, Name, Region, Subscription Type, Subscription Started, Subscription Ended, Canceled, and Revenue, collectively enabling in-depth analysis of customer behavior and subscription trends.

## Tools Used
- Microsoft Excel: [Download Here](https://www.microsoft.com)
  1. for Data Cleaning
  2. for  Data Transformation 
  3. for Data Analysis
  4. for Data Visualisation

- Structured Query Language (SQL): for querying the customer subscription dataset, allowing for structured data retrieval and analysis.
- Microsoft Power BI: used to create interactive dashboards that visualize insights derived from the customer subscription data.
- Github: for portfolio building

  ### Data Cleaning and Preparations
 During the initial phase, we engage in an exploration and summarization of the customer subscription data to gain essential insights into customer behavior, subscription trends, and overall engagement patterns.
  1. Removed duplicates and checked for missing data value
  2. Created a new column "Subscription_Duration", which calculates the duration between "Subscription Started" and "Subscription Ended"
  3. Validate the accuracy of the data to ensure its reliability for analysis
  
## Exploratory Data Analysis
The Exploratory Data Analysis (EDA) phase is essential for understanding the customer subscription data and uncovering patterns that can inform strategic decisions. By utilizing pivot tables to aggregate data across various dimensions, we can calculate total revenue and average subscription duration by Subscription Type or Region, as well as count subscriptions and identify trends over time.

## Data Analysis
The Customer subscription data is properly loaded into the SQL Server by importing the data after saving as a CSV file. Created a Database called LITAPROJECT_DB
```SQL
Select * from [dbo].[LITACAPSULE_CustomerCare]
```
---Total Numbers of Customers in Each Region
```
Select Region, Count(CustomerId) as Total_Customers
from [dbo].[LITACAPSULE_CustomerCare]
Group by Region
Order by Count(CustomerId) desc
```
---Most Popular Subscription Type by Number of Customers
```
Select SubscriptionType, count(CustomerID) as Most_Popular
from [dbo].[LITACAPSULE_CustomerCare]
Group by SubscriptionType
Order by count(CustomerID) desc
```
---Customers who Canceled Subscription within 6 Months
```
Select CustomerID, CustomerName, Subscription_Duration, Canceled
from [dbo].[LITACAPSULE_CustomerCare]
Where DATEDIFF(Month, Subscription_Duration, Canceled) < 6
Group by CustomerID, CustomerName, Subscription_Duration , Canceled
```
---Average Subscription Duration for all Customers
```
Select CustomerID, CustomerName, AVG(Subscription_Duration) as AVG_Duration
From [dbo].[LITACAPSULE_CustomerCare]
Group by CustomerID, CustomerName
```
---Customers with Subscription Longer Than 12 Months
```
Select CustomerID, CustomerName, Subscription_Duration, SubscriptionStart, SubscriptionEnd, SubscriptionType, Canceled, Revenue, Region
From [dbo].[LITACAPSULE_CustomerCare]
Where MONTH (Subscription_Duration) > 12
Group by CustomerID, CustomerName, Subscription_Duration, SubscriptionStart, SubscriptionEnd, SubscriptionType, Canceled, Revenue, Region
```
---Total Revenue by Subscription Type
```
Select SubscriptionType, Sum(Revenue) as Total_Revenue
From [dbo].[LITACAPSULE_CustomerCare]
Group by SubscriptionType
Order by Sum(Revenue) Desc
```
---Select Top 3 Region by Subscription Cancellations
```
Select Top 3 Region, count(Canceled) as Top_3_Region
From [dbo].[LITACAPSULE_CustomerCare]
Group by Region
Order by Count(Canceled) Desc
```
---Total Number of Active and Canceled Subscription
```
Select Count(SubscriptionType) as Active_Subscription, count(canceled) as Canceled_Subscription
From [dbo].[LITACAPSULE_CustomerCare]
Group by SubscriptionType, Canceled
```

## Data Visualisation
![Screenshot_Pivot](https://github.com/user-attachments/assets/2c97286c-fa82-4607-807c-e702c5cec567)
