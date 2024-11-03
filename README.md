# LITA-CAPSTONE-PROJECT-2

## PROJECT TITLE: ANALYSIS ON CUSTOMER SEGMENTATION FOR A SUBSCRIPTION SERVICE
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

Q4 Calculate the average subscription duration for all customers

```SQL
SELECT Count(CustomerID) As All_Customers,AVG(DATEDIFF(DAY,SubscriptionStart,SubscriptionEnd)) AS Average_Subscription_Duration
FROM [dbo].[LITA_CUSTOMER.DATA]
WHERE SubscriptionEnd IS NOT NULL
```

Q5  Find customers with subscriptions longer than 12 months.DATEDIFF

```SQL
SELECT CustomerName,SubscriptionType,SubscriptionStart,SubscriptionEnd
FROM [dbo].[LITA_CUSTOMER.DATA]
WHERE DATEDIFF(MONTH,SubscriptionStart,SubscriptionEnd) >=12
```

Q6  calculate total revenue by subscription type

```SQL
SELECT SubscriptionType,SUM(Revenue) AS Total_Revenue
FROM [dbo].[LITA_CUSTOMER.DATA]
GROUP BY SubscriptionType
```

Q7 Find the top 3 regions by subscription cancellations.

```SQL
SELECT TOP 3 Region,Canceled
FROM [dbo].[LITA_CUSTOMER.DATA]
```

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






