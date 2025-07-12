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
 
```sql
select *
FROM `sql file`
where category = 'footwear';
```
 
```sql
SELECT *
FROM `sql file`
WHERE category = 'Accessories';
```
 
```sql
select *
FROM `sql file`
where category = 'outerwear';
```
 
7.	**write a query that identifies distinct categories.**
```sql
SELECT DISTINCT(Category) FROM `sql file`;
```
 
8.	**Write a query to check distinct categories.**
```sql
select COUNT(DISTINCT category) from `sql file`;
```
 
9.	**write a query to find out how much each category brought in in terms of sales.**
```sql
select category,
sum(`Purchase Amount (USD)`) as Total_sales
from `sql file`
group by Category;
```
 
10.	**write a query to identify distinct items.**
``sql
SELECT DISTINCT(`Item Purchased`) from `sql file`; 
```
 
11.	Write a query to find out count of distinct items purchased.**
```sql
select COUNT(DISTINCT`Item Purchased`) from `sql file`;
```
 
12.	**write a query to find out the unique customers that  visited the store.**
```sql
SELECT COUNT(DISTINCT `Customer ID`) as Unique_customer 
FROM `sql file`;
```
 
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
 
15.	**write a query to for the total sales.**
```sql
select sum(`Purchase Amount (USD)`) as Total_Revenue
 from `sql file`;
 ```
 
16.	**write a query for  average sales.**
```sql
 select AVG(`Purchase Amount (USD)`) as Average_Sales
 from `sql file`;
 ```
 
17.	**write a query to fetch  top 2 categories by count.**
```sql
 select category,
 count(*)
 from `sql file`
 GROUP BY category
 order by count(*) desc
 LIMIT 2;
 ```
 
18.	**write a query to fetch top 2 categories by revenue.**
```sql
 select Category,
 sum(`Purchase Amount (USD)`) as total_revenue
 from `sql file`
 group by Category
 order by total_revenue desc
 limit 2;
 ```
 
19.	**write a query to fetch top 5 items by revenue.**
```sql
 select `Item Purchased`,
 sum(`Purchase Amount (USD)`) as total_revenue
 from `sql file`
 group by `Item Purchased`
 order by total_revenue desc
 limit 5;
 ```
 
20.	**write a query to fetch top 5 customers by spend.**
```sql
 select `Customer ID`, sum(`Purchase Amount (USD)`) as total_spent
 from `sql file`
 group by `Customer ID`
 order by total_spent desc
 limit 5;
 ```
 
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

