# SALES-ANALYSIS-USING-SQL
This project focuses on Sales Data Analysis to uncover key insights that help businesses make informed decisions. Using real or simulated transaction data, we perform exploratory data analysis (EDA) to identify sales trends and product performance. The analysis supports decision-making and revenue optimization.
##  Table of Contents

- [ Project Overview](#project-overview)
- [ Dataset Description](#dataset-description)
- [ Project Objectives](#project-objectives)
- [ Data Source](#data-source)
- [ Data Analysis](#data-analysis)
- [ Project Files](#project-files)
- [ Tools Used](#tools-used)
### PROJECT OVERVIEW
The primary goal of this project is to perform a comprehensive analysis of sales data using SQL to uncover trends, identify high performing product category, low performing product categories  and provide actionable insights to support strategic decision making.

### DATASET DESCRIPTION
The dataset contains structured data for sales transactions. It will be used to support reporting, analytics and decision making processes.

### The key components of the dataset include:
 •	Tables: organized collections of data.  

 •	Relationships: Defined using primary and foreign keys to maintain data integrity across tables.
 
 •	Data types: Each column has a defined data type. E.g INT, CHAR, VARCHAR  to ensure consistency.

### PROJECT OBJECTIVES
#### 1.	Perform Exploratory Data Analysis
•	Perform basic Exploratory Data Analysis to understand the dataset:
Check for NULLS and missing data

 Check for duplicates
 
 Determine the total Revenue

 Determine the total customers

 Determine the total product categories
 
#### 2.	Evaluate product performance

 Determine the best selling product categories based on revenue generated.

 Determine underperforming product categories.
 
#### 3.	Business Analysis

 Use SQL to answer specific business questions and derive insights from the sales data.
 
#### 4.	Support strategic decision-making 

Provide insights that help the business with marketing efforts and pricing strategies.

### DATA SOURCE
The data used in this analysis was sourced from kaggle.
### DATA ANALYSIS
The following SQL queries were developed to answer specific business Questions:
1.	** write a query  to check if there is data in the table.**
**This Query outputs the data of the various items in the sales table.
```sql
SELECT* FROM`sql file` ;
```
<img width="509" height="691" alt="image" src="https://github.com/user-attachments/assets/d3939d0f-c74a-4a01-ba0a-e39cee6c9966" />
 
2.	**write a query to find out the number of transactions that were made.**
```sql
select COUNT(*) AS Total_Transactions
FROM `sql file`;
```
<img width="208" height="61" alt="image" src="https://github.com/user-attachments/assets/7bd04951-73eb-4bcb-aa83-61fe32c120b2" />
 

3.	**write a query to check for  missing values in the table.**
```sql
select
sum(case when `Customer ID` is null then 1 else 0 end) as missing_customer_id,
sum(case when `Item Purchased` is null then 1 else 0 end) as missing_item_purchased,
sum(case when Category is null then 1 else 0 end) as missing_category,
sum(case when `Purchase Amount (USD)` is null then 1 else 0 end) as missing_purchase_amount
from `sql file`;
```
<img width="806" height="77" alt="image" src="https://github.com/user-attachments/assets/bd17d147-ee32-4ce3-8e9a-8fb5c8a8e420" />
 
4.	**write a query to check for duplicates in the sales data.**
```sql
select
`Customer ID`,
`Item Purchased`,
Category,
`Purchase Amount (USD)`, 
case
when count(*) over (partition by`Customer ID`,
`Item Purchased`,Category,`Purchase Amount (USD)`)>1
then 'Duplicate'
else 'Unique'
end as Record_Status
from `sql file`;
```
<img width="717" height="691" alt="image" src="https://github.com/user-attachments/assets/fa880aa4-3790-45ba-9cab-f18e4a120975" />
 
5.	**write a query to check if purchase amount is in numeric format.**
```sql
update `sql file`
set `Purchase Amount (USD)` = cast(`Purchase Amount (USD)` as decimal(10,0));
```

6.	**write  queries  to identify items in each category that was sold.**

```sql
select *
FROM `sql file`
where category = 'clothing';
```
<img width="363" height="661" alt="image" src="https://github.com/user-attachments/assets/26895810-e869-41cd-82df-8f3181951a7a" />
 
```sql
select *
FROM `sql file`
where category = 'footwear';
```
<img width="352" height="666" alt="image" src="https://github.com/user-attachments/assets/9f1ddc13-7337-45f6-b397-4d0911667f17" />
 
```sql
SELECT *
FROM `sql file`
WHERE category = 'Accessories';
```
 <img width="380" height="636" alt="image" src="https://github.com/user-attachments/assets/f8953aab-2883-492b-8790-5c66079d74b1" />

```sql
select *
FROM `sql file`
where category = 'outerwear';
```
<img width="363" height="666" alt="image" src="https://github.com/user-attachments/assets/07ae544e-2864-4d03-9e76-084818f57a25" />
 
7.	**write a query that identifies distinct categories.**
```sql
SELECT DISTINCT(Category) FROM `sql file`;
```
<img width="158" height="150" alt="image" src="https://github.com/user-attachments/assets/fecca4ce-14f4-42c7-8fd5-2462b8ad52d1" />
 
8.	**Write a query to check distinct categories.**
```sql
select COUNT(DISTINCT category) from `sql file`;
```
<img width="278" height="95" alt="image" src="https://github.com/user-attachments/assets/53c89c12-93de-4b61-ba34-7a6afc5e21ea" />
 
9.	**write a query to find out how much each category brought in in terms of sales.**
```sql
select category,
sum(`Purchase Amount (USD)`) as Total_sales
from `sql file`
group by Category;
```
<img width="233" height="142" alt="image" src="https://github.com/user-attachments/assets/5b042a4b-856f-4249-b58f-c4b912d47d5b" />
 
10.	**write a query to identify distinct items.**
``sql
SELECT DISTINCT(`Item Purchased`) from `sql file`; 
```
<img width="145" height="688" alt="image" src="https://github.com/user-attachments/assets/fa76a486-c5af-428f-b6c4-7e33e7ab4b11" />
 
11.	Write a query to find out count of distinct items purchased.**
```sql
select COUNT(DISTINCT`Item Purchased`) from `sql file`;
```
<img width="238" height="109" alt="image" src="https://github.com/user-attachments/assets/890991e6-1439-462e-aa03-100fe84f205a" />
 
12.	**write a query to find out the unique customers that  visited the store.**
```sql
SELECT COUNT(DISTINCT `Customer ID`) as Unique_customer 
FROM `sql file`;
```
 <img width="159" height="66" alt="image" src="https://github.com/user-attachments/assets/c84b94f2-2f5c-4171-9a05-ad70d0c7a58d" />

13.	**write a query to find duplicates on customer Id, item purchased, category and purchase amount.**
```sql
SELECT `Customer ID`
`Item Purchased`,
Category,
`Purchase Amount (USD)`, 
count(*) as duplicate_count
FROM `sql file`
GROUP BY `Customer ID`,`Item Purchased`,Category,`Purchase Amount (USD)`
having count(*)>1;
```

14.	** write a query to find out sales per item purchased.**
```sql
select `Item Purchased`,
sum(`Purchase Amount (USD)`) as itemsales
from `sql file`
group by `Item Purchased`
order by itemsales desc;
```
<img width="241" height="688" alt="image" src="https://github.com/user-attachments/assets/a426938e-d90d-4db9-8325-9480971e0cc6" />
 
15.	**write a query to for the total sales.**
```sql
select sum(`Purchase Amount (USD)`) as Total_Revenue
 from `sql file`;
 ```
 <img width="127" height="63" alt="image" src="https://github.com/user-attachments/assets/67834e35-e944-4bb4-b8f4-fddfd82fd2fb" />

16.	**write a query for  average sales.**
```sql
 select AVG(`Purchase Amount (USD)`) as Average_Sales
 from `sql file`;
 ```
<img width="141" height="80" alt="image" src="https://github.com/user-attachments/assets/b4d2837a-3d79-4461-99f4-1269a1598da9" />
 
17.	**write a query to fetch  top 2 categories by count.**
```sql
 select category,
 count(*)
 from `sql file`
 GROUP BY category
 order by count(*) desc
 LIMIT 2;
 ```
<img width="203" height="92" alt="image" src="https://github.com/user-attachments/assets/903a7aa3-a7e4-47c7-bcac-53e3cd27e8e2" />
 
18.	**write a query to fetch top 2 categories by revenue.**
```sql
 select Category,
 sum(`Purchase Amount (USD)`) as total_revenue
 from `sql file`
 group by Category
 order by total_revenue desc
 limit 2;
 ```
 <img width="253" height="100" alt="image" src="https://github.com/user-attachments/assets/b37cc0e7-f7c4-4707-ae92-5e6cd89858cb" />

19.	**write a query to fetch top 5 items by revenue.**
```sql
 select `Item Purchased`,
 sum(`Purchase Amount (USD)`) as total_revenue
 from `sql file`
 group by `Item Purchased`
 order by total_revenue desc
 limit 5;
 ```
<img width="267" height="191" alt="image" src="https://github.com/user-attachments/assets/00c69e3f-a65a-46c0-b8fa-0ce5cb93105f" />
 
20.	**write a query to fetch top 5 customers by spend.**
```sql
 select `Customer ID`, sum(`Purchase Amount (USD)`) as total_spent
 from `sql file`
 group by `Customer ID`
 order by total_spent desc
 limit 5;
 ```
<img width="222" height="184" alt="image" src="https://github.com/user-attachments/assets/afbdfb4f-7a60-47dc-9964-0fc3cb4543f2" />
 
21.	**Write a query to fetch revenue and total sales by product category.**
```sql
 select Category, count(*) as total_sales,
 sum(`Purchase Amount (USD)`) as total_revenue
 from `sql file`
 group by Category
 order by total_revenue desc;
```
<img width="359" height="145" alt="image" src="https://github.com/user-attachments/assets/22c3b528-be91-4f19-b53e-bd1236cb2fb4" />
 

### KEY INSIGHTS
•	Clothing is the best-selling category in both revenue and volume.

•	Top 5 items generated over $10000 each in sales revenue.


•	Customer spending is evenly distributed with a few customers spending $100 each.

•	Accessories and footwear offer strong opportunities for growth.


•	Outerwear had the lowest sales and may need strategic review.

### RECOMMENDATIONS

•	Promote high performing items using targeted campaigns.

•	Introduce bundles or discounts to increase average order value ($59.76).

•	Target top customers with exclusive offers.

•	Build customer loyalty through reward systems for repeat buyers.

•	Reassess product strategy for low-performing categories.


### Project Files
•	Sales_data_analysis.sql- All SQL queries used

•	Sales_data.xlsx- Raw data

•	README.md-project summary and insights

### Tools Used
•	MySQL

•	Excel (for raw data)

