# KML-SQL-CASE-STUDY
## PROJECT TITLE: KML CASE STUDY

## Project Overview 
As a Data Analyst i was tasked with analyzing the data of a company that provides e-commerce analytics solutions to sellers on platforms like Amazon. This task includes analyzing products and customer review data to generate insights that can guides product improvement, marketing strategies, and customer engagement, as well as profer solutions where necessary.

## Data Source
The primary data source used for this project is the KMS case study which contains information like;
- Order Information: Quantity, Sales, Discount, Ship Mode, Product Name etc.
- Customer engagement: Shipping Date, Product Name, Customer's Name etc.
- Each row represents a unique product, with aggregated reviewer data stored as comma-separated values and exported to SQL server

## Tool Used 💾:
SQL Server Script was used in completing this project. I was able to do the following;

- Data collection

- Data cleaning

- Data analysis

## Analysis Tasks
I utized a few SQL commands, extracted results, and gave insights where necessary to answer the following questions:

### 1. Which product category had the highest sales 📈?
~~~
select top 1
	Product_Category, Sales
from [dbo].[KMS Sql Case Study]
order by Sales desc
~~~
![1](https://github.com/user-attachments/assets/448a96cc-9216-4199-aecf-8307650dbe6a)

### 2. What are the Top 3 and Bottom 3 regions in terms of sales 📊?
~~~
select top 3 Region, sum(Sales) as [Total Sales]
from [dbo].[KMS Sql Case Study]
group by Region
order by [Total Sales] desc

select top 3 Region, sum(Sales) as [Total Sales]
from [dbo].[KMS Sql Case Study]
group by Region
order by [Total Sales] asc
~~~
![2](https://github.com/user-attachments/assets/d29c905d-e329-4dce-8eed-50bfbb5eae98)

### 3. What were the total sales of appliances in Ontario 🧰?
~~~
select Region, sum(Sales) as [Total Sales of Appliance] from [dbo].[KMS Sql Case Study]
where Province = 'Ontario'
And Product_Sub_Category = 'Appliances'
group by Region
~~~
![3](https://github.com/user-attachments/assets/7c830c6e-818b-4e75-be90-02bfc20bb549)

### 4. Advise the management of KMS on what to do to increase the revenue from the bottom 10 customers 💡
~~~
select top 10 Customer_Name,
sum(Sales) as [Total Sales]
from [dbo].[KMS Sql Case Study]
group by Customer_Name
order by [Total Sales] asc
~~~
##### To increase the revenue of the bottom 10 customers, the Management should offer discounts, bundles or special offers for this category of customers. This could include limited-time offers.
##### Run surveys to collect feedback and adjust strategy accordingly.

### 5. KMS incurred the most shipping cost using which shipping method 🛳️?
~~~
select top 3 Ship_Mode, sum(Shipping_Cost) as [Total Shipping_Cost]
from [dbo].[KMS Sql Case Study]
group by Ship_Mode
order by [Total Shipping_Cost] desc
~~~
![5](https://github.com/user-attachments/assets/e38c30f0-e6bc-49d4-8163-9046a640abd9)

### 6. Who are the most valuable customers, and what products or services do they typically purchase 🧑‍🤝‍🧑?
~~~
select top 3 Customer_Name, Product_Category, sum(Sales) as [Total Sales]
from [dbo].[KMS Sql Case Study]
group by Customer_Name, Product_Category
order by [Total Sales] desc
~~~
![6](https://github.com/user-attachments/assets/805322b7-20ce-4ba9-821d-99953cde4597)

### 7. Which small business customer had the highest sales 🏦?
~~~
select top 1 [Customer_Name], Customer_Segment, Sum(Sales) as Total_Sales from [dbo].[KMS Sql Case Study]
where [Customer_Segment] = 'Small Business'
group by [Customer_Name], Customer_Segment
order by Total_Sales desc
~~~
![7](https://github.com/user-attachments/assets/15ecfaea-b787-49ad-8ae8-911aff442363)

### 8. Which Corporate Customer placed the most number of orders in 2009 – 2012 📆?
~~~
select top 1 [Customer_Name], count(Distinct Order_ID) as Total_Orders
from [dbo].[KMS Sql Case Study]
where Customer_Segment = 'Corporate'
and Order_Date between '2009-01-01' and '2012-12-31'
group by Customer_Name
order by Total_Orders Desc
~~~
![8](https://github.com/user-attachments/assets/a00eb105-7437-490f-939e-6bb33bcc2c97)

### 9. Which consumer customer was the most profitable one 🤑?
~~~
select top 1 [Customer_Name], Sum(Profit) as Total_Profit from [dbo].[KMS Sql Case Study]
where [Customer_Segment] = 'Consumer'
group by [Customer_Name]
order by Total_Profit desc
~~~
![9](https://github.com/user-attachments/assets/519ed9a1-3bc3-44a7-b62e-1f5c49ebe1f7)

### 10. Which customer returned items, and what segment do they belong to 📲?
~~~

~~~

### 11. If the delivery truck is the most economical but the slowest shipping method and Express Air is the fastest but the most expensive one, do you think the company appropriately spent shipping costs based on the Order Priority? Explain your answer ✈️
~~~
select [Order_Priority], [Ship_Mode],
sum(Shipping_Cost) as total_shipping_cost_for_priority,
count(Distinct Order_ID) as number_of_orders_for_priority_ship_mode 
from [dbo].[KMS Sql Case Study]
group by [Order_Priority], [Ship_Mode]
order by [Order_Priority] asc, total_shipping_cost_for_priority desc
~~~
![11](https://github.com/user-attachments/assets/7ddb529a-89d8-4582-a699-ffe14688f2e5)

Answer: No, KMS did not appropriately align shipping cost with priority.

Express Air remains the best for high-priority orders, which was underused.
Delivery Truck although slower and cheaper was overused even for urgent orders.
This mismatch results in wasted cost and delayed deliveries.

## INSIGHTS
- Most Sold Category: Office Supplies
- Top Region by Sales: West
- Least Performing Region: Nunavut or Territories
- Most Profitable Segment: Consumer
- Most Costly Shipping Mode: Express Air
- Major Insight: Misalignment between order priority and shipping method caused unnecessary costs.
