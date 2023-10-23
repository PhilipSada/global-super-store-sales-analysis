# Global Super Store: Sales Analysis
## Introduction
This is a SQL and Tableau project on the sales analysis of a global superstore. This project aims to provide insights to answer important questions and help the superstore make data driven decisions.
The dataset used in this project can be found in Kaggle.
## Exploratory Data Analysis
The following explorary data analysis was conducted in Microsoft SQL Server to understand the dataset.
Executed the query below to find out the number of items in the data
```sql
select count(*) from [dbo].[Orders$]
```
Executed the query below to check if the Order ID can be a primary key. The result showed that order id can't be a primary key alone since multiple rows have the same order id
```sql
select [Order ID], count(*) from [dbo].[Orders$] group by [Order ID] having count(*) > 1
```
Executed the query below to check if Order Date is less than Ship Date. The result showed that all the order dates were less than the ship dates.
```sql
select * from [dbo].[Orders$] where [Ship Date] < [Order Date]
```
Executed the query below to find the distinct ship modes in the data. The result showed that there are 4 distinct ship modes (First Class, Same Day, Standard Class and Second Class)
```sql
select distinct [Ship Mode] from [dbo].[Orders$]
```
Executed the query below to find the time range( min and max days) for the ship modes(i.e Ship Mode = 'Second Class')
```sql
select min(a.NumOfDays) MinDays, max(a.NumOfDays) MaxDays from (
select DATEDIFF(DAY, [Order Date], [Ship Date]) as NumOfDays, * from [dbo].[Orders$] where [Ship Mode] = 'Second Class'
) a
```
Executed the query below to check if the customer can order multiple items. The result showed that a customer can order multiple times
```sql
select min(a.NumOfDays) MinDays, max(a.NumOfDays) MaxDays from (
select DATEDIFF(DAY, [Order Date], [Ship Date]) as NumOfDays, * from [dbo].[Orders$] where [Ship Mode] = 'Second Class'
) a
