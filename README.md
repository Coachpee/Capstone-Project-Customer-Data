# Capstone-Project-Customer-Data

### Project Title : : Customer Segmentation for a Subscription Service

### 📊 Project Overview

This project involves analyzing customer data for a subscription service to identify 
segments and trends. The goal is to understand customer behavior, track subscription types, 
and identify key trends in cancellations and renewals.

---------

### 📂 Dataset

The dataset used in this project contains sales transactions in 2023 and 2024. It includes the following fields:
- #### Customer ID
- #### Customer Name
- #### Region
- #### Subscription type
- #### Subscription Start
- #### Subscription End
- #### Canceled
- #### Revenue

  -------------

  ### 🧰 Tools Used

- Microsoft Excel: For initial data exploration and pivot table analysis

- Structured Query Language (SQL): For Data Querying and Analysis
  
- Power BI: For building interactive dashboards and visualizations

  ---------

  ### 🔍 Analysis Steps

#### 1. Data Cleaning

- Ensured there were no duplicate records and missing values

- Ensured that product names and customer regions were standardized.

#### 2. Exploratory Data Analysis (EDA)

- Analyzed subscription patterns 

- Investigated trends to identify high performing regions

- Identified most common subscription type

#### 3. Data Analysis

Here, I used Basic Excel functions to to calculate the average subscription duration and identify the most popular 
subscription types using the AVERAGEIF and COUNTIF Functions. Using the minus formula, I was able to calculate the subscription duration
for each customer by subtracting the end subscription date from the start subscription date.
For example; ```=F2-E2```

Below is a sample of the arguments used to run the analysis.

``` Excel
=AVERAGEIF(G2:G75001,"TRUE",I2:I75001)
```

``` Excel
=COUNTIF($D$2:$D$75001,N10)
```

With the use of SQL, I was also able to perform some calculations such as the average subscription duration for all customers, total revenue by subscription type. I was also able to gain more insight into customer behaviour by finding the top 3 regions by subscription cancellations, the total number of active and canceled subscriptions, the most popular subscription type by the number of customers, customers with subscriptions longer than 12 months.

Below are some of the queries used;

**To calculate total revenue by subscription type**

``` SQL
select sum([Revenue]) as totalrevenue, [SubscriptionType] from [dbo].[LITA Capstone customer data]
Group by [SubscriptionType]
```

**To calculate the average subscription duration for all customers**

```SQL
select AVG([Subscriptionduration]) as averagesubscriptionduration from [dbo].[LITA Capstone customer data]
```

**To find the most popular subscription type by the number of customers**

```SQL
select count([CustomerID]) as numberofsubscriptions, [SubscriptionType] from [dbo].[LITA Capstone customer data]
Group by [SubscriptionType]
```

**To find the top 3 regions by subscription cancellations**

```SQL
select top (3) COUNT([Canceled]) as Canceledsubscription, [Region] from [dbo].[LITA Capstone customer data]
where [Canceled]='TRUE'
Group by [Region]
Order by 1 desc
```

**To find the total number of active subscriptions**

```SQL
select COUNT([Canceled]) as Canceledsubscriptions from [dbo].[LITA Capstone customer data]
where [Canceled]='TRUE'
```

**To find the total number of canceled subscriptions**

```SQL
select COUNT([Canceled]) as activesubscriptions from [dbo].[LITA Capstone customer data]
where [Canceled]='FALSE'
```

------------------------

### 💡 Key Findings

- #### Most Popular Subscription Type:
The most popular subscription type is the Basic subscription having a 50% subscription out of the 75,000 customers.

- #### Geographical Trends:
The South, West regions had only Premium and Standard respectively whereas the East and North regions had only Basic subcribers. 
All the regions had equal number subscribers with each having a total of 18,750 subscribers.
The East did not have any records of subscription cancellations.The West,South and North regions had equal numbers of subscription cancellations (11,250).

- #### Subscription Pattern:
The average subscription duration was 365.3333 days.The Basic subscription type had the most active subscribers(26,250) as against other subscription types which had 7500 active subscribers.
There was an overall decline in the subscription pattern in 2023. The total subscription for 2022 was 45000 which dropped to 30000 in 2024. The active subscribers in the East region dropped from 11250 in 2022 to 7500,the North and West did not have any active subscriptions in 2023 and the South which did not have any active subscription in 2022 had 7500 active subscribers in 2023. The decline in the other regions should be looked into for possible causes .



