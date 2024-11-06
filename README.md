# LITA-CAPSTONE-PROJECT-2

## PROJECT TITLE: ANALYSIS ON CUSTOMER SEGMENTATION FOR A SUBSCRIPTION SERVICE

[Project Overview](#project-overview)

[Data Sources](#data-sources)

[Tools Used](#tools-used-in-this-project)

[Data Collected](#data-collected)

[Data Cleaning and Preparations](#data-cleaning-and-preparations)

[Exploratory Data Analysis](#exploratory-data-analysis)

[Data Analysis](#data-analysis)

[Inference](#inference)

PROJECT OVERVIEW: In this project, I am tasked with performing an analysis on Customer Segmentation for a Subscription Service. I will be exploring a customer data to uncover and understand patterns and trends such as average subscription duration and identifying the most popular subscription type. The focus of this project is to produce an interactive and interesting Power BI dashboard that highlights these findings.

### DATA SOURCE
- Excel
- SQL

### TOOLS USED IN THIS PROJECT
- Microsoft Excel [Download Here].(https://www.microsoft.com)
1. for Data Cleaning
2. Analysis
3. Visualization
- SQL - Structured Query Language
1. Quering of Data
- Power BI - Power Business Intelligent
1. Data visualisation
2. Report

### DATA COLLECTED
The dataset includes the following key columns:

- CustomerID: This is the number attached to each customer whon bought one product or the other
- Customer Name: This is the name of the customers that bought one item or the other
- Region: This is the different locations where the product are sold and bought
- Subscription Type: The three types of subscription includes: Basic, Standard and Premium
- Subscription Start/End: This is the date the customers started their subscription and when they canceled it
- Cancelled: This shows the customers that cancelled their subscription
- Revenue: The total monetary value generated from the sale

### DATA CLEANING AND PREPARATION
In this initial phase of the Data cleaning and preparations, I performed the following actions:

- Data loading and Inspection
- Removing duplicates
- Cleaning and changing the data types
- Performing analysis to get the difference in duration

### EXPLORATORY DATA ANALYSIS
This involves the exploring of the data to answer some questions about the data. Such as:

- Subscription Count by Region
- Popular Subscription Types
- Subscription Duration Analysis
- Monthly Subscription Trends
- Revenue by Subscription Type
- Cancellation Rate by Region

### DATA ANALYSIS
This is where I include some line of codes, queries or some of the DAX expressions to answer the questions above. The following analysis were done in Excel:

Q1.    ![image](https://github.com/user-attachments/assets/c63cd7be-4337-4741-99de-9116a9ceb048)

![image](https://github.com/user-attachments/assets/b138a602-07ba-4247-87af-231dc6cd4788)

Q2.    ![image](https://github.com/user-attachments/assets/82bc5720-5c86-40ce-8459-3a1227c2dc70)

![image](https://github.com/user-attachments/assets/4893b93d-b25c-428d-a967-3ef07da0f4bb)

Q3.    ![image](https://github.com/user-attachments/assets/70d329be-0954-4dae-9707-809dd7aaa943)

![image](https://github.com/user-attachments/assets/f4e2f421-d66e-4a43-8c6d-5fa1f31386ce)

Q4.    ![image](https://github.com/user-attachments/assets/6ac3ffc8-d66d-4453-b21a-9746c5ae605f)

![image](https://github.com/user-attachments/assets/9444837c-bf11-40d9-bcef-f334e5a8eea6)

Q5.    ![image](https://github.com/user-attachments/assets/cf40867a-428b-4179-8043-2df20a9707e6)

![image](https://github.com/user-attachments/assets/f345d8f8-52ba-4f1b-8ed8-bbd165f4d8b7)


### The following are the analysis conducted on SQL

Q1 Retrieve the total number of customers from each region.

```SQL
SELECT Region, COUNT(CustomerID) AS Total_No_of_Customers
FROM [dbo].[LITA_CUSTOMER.DATA]
GROUP BY Region
```

![image](https://github.com/user-attachments/assets/000dbd35-6871-436d-b980-8e6b7fc18ef6)


Q2 Find the most popular subscription type by the number of customers.

```SQL
SELECT SubscriptionType,COUNT(CustomerID)AS NO_Of_Customers
FROM [dbo].[LITA_CUSTOMER.DATA]
GROUP BY SubscriptionType
```

![image](https://github.com/user-attachments/assets/eb1796e5-d785-4adb-a8b5-879646a64c2f)


Q3  Find customers who canceled their subscription within 6 months

```SQL
SELECT CustomerName,Canceled,SubscriptionStart
FROM [dbo].[LITA_CUSTOMER.DATA]
WHERE Canceled =0 AND MONTH(SubscriptionStart) <= 6
```
OR
```SQL
SELECT CustomerName,Canceled,SubscriptionStart
FROM [dbo].[LITA_CUSTOMER.DATA]
WHERE Canceled =0 AND MONTH(SubscriptionStart) BETWEEN 1 AND 6
```

![image](https://github.com/user-attachments/assets/49bd54ce-62ce-461a-bb68-b8cbcb8901f2)            ![image](https://github.com/user-attachments/assets/5f625958-c567-475f-b676-28f56d2ba4ff)          ![image](https://github.com/user-attachments/assets/4ee8dd9a-49a0-466c-a233-652c17cc5ec0)


Q4 Calculate the average subscription duration for all customers

```SQL
SELECT Count(CustomerID) As All_Customers,AVG(DATEDIFF(DAY,SubscriptionStart,SubscriptionEnd)) AS Average_Subscription_Duration
FROM [dbo].[LITA_CUSTOMER.DATA]
WHERE SubscriptionEnd IS NOT NULL
```

![image](https://github.com/user-attachments/assets/f71a1801-c852-4240-857f-31e60d512eb2)


Q5  Find customers with subscriptions longer than 12 months.DATEDIFF

```SQL
SELECT CustomerName,SubscriptionType,SubscriptionStart,SubscriptionEnd
FROM [dbo].[LITA_CUSTOMER.DATA]
WHERE DATEDIFF(MONTH,SubscriptionStart,SubscriptionEnd) >=12
```

![image](https://github.com/user-attachments/assets/a770e723-49f0-4520-86cd-c5d82fc0e27e)       ![image](https://github.com/user-attachments/assets/331961e8-b78b-41c1-8cdb-ca8c5ceaa58c)


Q6  calculate total revenue by subscription type

```SQL
SELECT SubscriptionType,SUM(Revenue) AS Total_Revenue
FROM [dbo].[LITA_CUSTOMER.DATA]
GROUP BY SubscriptionType
```

![image](https://github.com/user-attachments/assets/04ddfb53-452b-445b-9f5b-8768ddb6b300)


Q7 Find the top 3 regions by subscription cancellations.

```SQL
SELECT TOP 3 Region,Canceled
FROM [dbo].[LITA_CUSTOMER.DATA]
```

![image](https://github.com/user-attachments/assets/b54e8bde-177d-4748-a306-011f34a31b7b)


Q8  Find the total number of active and canceled subscriptions.

```SQL
SELECT canceled, SUM(Active_subscription) AS Number_of_Active_Sub
FROM [dbo].[LITA_CUSTOMER.DATA]
GROUP BY canceled
```

```SQL
SELECT canceled, SUM(Non_Active_subscription) AS Number_of_nonActive_Sub
FROM [dbo].[LITA_CUSTOMER.DATA]
GROUP BY canceled
```

![image](https://github.com/user-attachments/assets/6c7dd387-1e8d-4bde-993b-d6f1eea89a47)


### These are the visualization done on Power BI

![image](https://github.com/user-attachments/assets/be134751-d23a-4bd1-aaae-a949c989c932)


### Inference

#### Analysis on Revenue by Subscription Type
1. Basic Subscription: This subscription type generates the highest revenue, contributing nearly 50% of the total revenue. With a total of $33.77 million, it is the dominant subscription type and appears to have a large user base or higher pricing, or both.
2. Premium and Standard Subscriptions: Both Premium and Standard subscriptions generate similar revenue, contributing around 25% each. The Premium subscription generates $16.9 million, while Standard brings in $16.86 million. This suggests that the two might be priced similarly or have comparable user adoption rates.

#### Insights and Recommendations
- Dominance of Basic Subscription: The Basic subscription type significantly outperforms the other two types in terms of revenue. If this is a result of a larger user base or higher pricing, it may be worthwhile to analyze how customers are segmented between Basic, Premium, and Standard subscriptions. Additionally, if there’s an opportunity to upsell Basic users to Premium, this could further increase revenue from this segment.

- Premium vs. Standard Subscriptions: The Premium and Standard subscriptions are generating almost identical revenue, despite having different names and potentially different features. A deeper look into the feature set and pricing structure for these two tiers might reveal whether they overlap too much, or whether a price adjustment or better differentiation could boost performance.

- Potential for Growth in Premium/Standard Tiers: Given that the Basic tier is generating nearly double the revenue of Premium and Standard combined, there could be room for targeted marketing or promotions aimed at increasing the adoption of the Premium and Standard subscriptions. Consider offering trial periods, enhanced features, or discounts for users on the Basic plan to encourage them to upgrade.

#### Conclusion
Basic Subscription is the top performer, contributing about half of the total revenue. Premium and Standard subscriptions contribute equally but significantly less in comparison to the Basic tier.
Further analysis of the pricing structure, user demographics, and feature set for each subscription type would be beneficial for understanding why the Basic plan is dominant and how to boost the other tiers.
By focusing on understanding customer preferences and ensuring clear differentiation between the subscription types, there is a potential to increase revenue across all tiers.

#### Analysis on Subscription Type by Revenue and Region
- Basic Subscription: This is the only subscription type recorded in both the East and North regions, with the number of subscribers being; East: 16,958,763 and North: 16,817,972. The Basic subscription does not appear in the South or West regions.
- Premium Subscription: The South region has a recorded subscription for the Premium plan; South: 16,899,064.
The Premium plan is not present in the East, North, or West regions.
- Standard Subscription: The West region has a recorded subscription for the Standard plan; West: 16,864,376. The Standard plan is not recorded in the East, North, or South regions.
- There is a notable lack of variety in subscription types across different regions: The East and North regions only have the Basic subscription, while the South and West regions have their own unique subscription types (Premium in the South and Standard in the West).
- Subscription Type Concentration: The Basic subscription is more prevalent in the East and North regions, while Premium and Standard are each concentrated in only one region.
- Regional Total Comparisons: The subscription numbers across the regions are relatively close to one another:

East: 16,958,763 (Basic), 
North: 16,817,972 (Basic), 
South: 16,899,064 (Premium), 
West: 16,864,376 (Standard)

- Conclusion:
This data presents a snapshot of regional subscription distribution, showing how Basic, Premium, and Standard subscription types are distributed across the East, North, South, and West regions. There seems to be a significant regional concentration of each subscription type, with Basic being the most widespread, and Premium and Standard being more regionalized. Further analysis could help uncover the reasons behind these trends and how subscription services can adapt or expand in these regions.









