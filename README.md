# Capstone-Project-Customer-Data

### Project Outline:

- [Project Title](Project-Title)

- [Project Overview](Project-Overview)

- [Dataset](Dataset)

- [Tools Used](Tools-Used)

- [Analysis Steps](Analysis-Steps)

- [Key Findings](Key-Findings)

- [Recommendations](Recommendations)

- [Conclusion](Conclusion)

  ---------------

### Project Title : Customer Segmentation for a Subscription Service

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

#### *Pivot Table Visualzations:*

![cdpt6](https://github.com/user-attachments/assets/65318678-b327-4e3b-bfaa-f79e3823168b)
![cdpt4](https://github.com/user-attachments/assets/3e359752-ea9c-47b7-a869-b61814c62975)
![cdpt1](https://github.com/user-attachments/assets/98091786-f77f-4d44-991b-8f8ce0958380)
![cdpt2](https://github.com/user-attachments/assets/00e8e72a-92c7-4ab7-bfea-d7211ea28547)

![cdpt3](https://github.com/user-attachments/assets/e5deda9b-0f8b-444a-8db7-7c47852b52ba)
![cdpt5](https://github.com/user-attachments/assets/5b52a189-5f07-451f-b705-d99db592515b)



#### 3. Data Analysis

Here, I used Basic Excel functions to to calculate the average subscription duration and identify the most popular 
subscription type using the AVERAGE and COUNTIF Functions. Using the minus formula, I was able to calculate the subscription duration
for each customer by subtracting the end subscription date from the start subscription date.
For example; ```=F2-E2```

Below is a sample of the arguments/ Formula used to run the analysis.

``` Excel
=AVERAGE(I2:I75001)
```
Using the above formula, the Average subscription duration is **365.35.**

``` Excel
=COUNTIF($D$2:$D$75001,N10)
```

![cdvisuals 1](https://github.com/user-attachments/assets/35864c75-d9ec-4276-97ef-d9885841d28a)

From the above analysis, the most popular subscription type is the Basic subscription with a count of 37,500 subscriptions.

With the use of SQL, I was also able to perform some calculations such as the average subscription duration for all customers, total revenue by subscription type. I was also able to gain more insight into customer behaviour by finding the top 3 regions by subscription cancellations, the total number of active and canceled subscriptions, the most popular subscription type by the number of customers, customers with subscriptions longer than 12 months.

Below are some of the queries used;

**To calculate total revenue by subscription type**

``` SQL
select sum([Revenue]) as totalrevenue, [SubscriptionType] from [dbo].[LITA Capstone customer data]
Group by [SubscriptionType]
```

![cdsql4](https://github.com/user-attachments/assets/419a8b4b-596c-4ff2-b549-73eddb7e4d52)

**To retrieve the total number of customers from each region**

```SQL
select count([CustomerID]) as numberofcustomers, [Region] from [dbo].[LITA Capstone customer data]
Group by Region
```
![cdsql1](https://github.com/user-attachments/assets/3edd28c6-2e4f-4170-b2ee-6a667cdcc26a)

**To calculate the average subscription duration for all customers**

```SQL
select AVG([Subscriptionduration]) as averagesubscriptionduration from [dbo].[LITA Capstone customer data]
```

The average subscription duration is **12months**

**To find the most popular subscription type by the number of customers**

```SQL
select count([CustomerID]) as numberofsubscriptions, [SubscriptionType] from [dbo].[LITA Capstone customer data]
Group by [SubscriptionType]
```
![cdsql2](https://github.com/user-attachments/assets/2153af2f-31b8-409a-a375-a42579426e34)

The most popular subscription type is the Basic subscription.

**To find customers who canceled their subscription within 6 months**

```SQL
alter table [dbo].[LITA Capstone customer data]
add Subscriptionduration int

update [dbo].[LITA Capstone customer data]
set [Subscriptionduration] = DATEDIFF(month,[SubscriptionStart],[SubscriptionEnd])

select * from [dbo].[LITA Capstone customer data]
where [Subscriptionduration] between 0 and 6 and [Canceled]='TRUE'
```

There were no customers who canceled their subscriptions within 6 months.

**To find the top 3 regions by subscription cancellations**

```SQL
select top (3) COUNT([Canceled]) as Canceledsubscription, [Region] from [dbo].[LITA Capstone customer data]
where [Canceled]='TRUE'
Group by [Region]
Order by 1 desc
```
![cdsql3](https://github.com/user-attachments/assets/7ea84799-8ca4-4a2f-8dc1-792285411d44)

The top 3 regions by Subscription cancellations were the North, South and West.


**To find customers with subscriptions longer than 12 months**

```SQL
select * from [dbo].[LITA Capstone customer data]
where[Subscriptionduration] >12
```

There were no customers who canceled their subscriptions within 12 months.

**To find the total number of active subscriptions**

```SQL
select COUNT([Canceled]) as Canceledsubscriptions from [dbo].[LITA Capstone customer data]
where [Canceled]='TRUE'
```

The total number of active subscriptions is 33750

**To find the total number of canceled subscriptions**

```SQL
select COUNT([Canceled]) as activesubscriptions from [dbo].[LITA Capstone customer data]
where [Canceled]='FALSE'
```

The total number of active subscriptions is 41250

#### 4. Visualization

  - Created interactive dashboards to visualize:

  - Key Customer Segments
 
  - Subscription cancelations
 
  - Subscription trends 

Some of the visualizations can be seen below;

![customer data visuals 1](https://github.com/user-attachments/assets/ba1ca203-be1a-4c71-bff9-9c17af155ea5)

![customer data visuals 2](https://github.com/user-attachments/assets/e93d0ed3-387e-4a71-8a27-f326762a7d5e)

![customer data visuals 3](https://github.com/user-attachments/assets/1cc0f163-f9a5-4daf-95b5-64ce5899e91a)

![customer data visuals 4](https://github.com/user-attachments/assets/e1e27566-2e32-40e9-9a3c-b43eec23f7eb)


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
There was an overall decline in the subscription pattern in 2023. The total subscription for 2022 was 45000 which dropped to 30000 in 2024. The active subscribers in the East region dropped from 11250 in 2022 to 7500,the North and West did not have any active subscriptions in 2023 and the South which did not have any active subscription in 2022 had 7500 active subscribers in 2023. The decline in the other regions should be looked into for possible causes so they can be avoided and possible reasons for the increase in the South can be applied to other regions




