# Payment Optimization and Customer Behavior Analysis of Justus Café Customers
![Justus Café](cafe.jpg)
## Introduction
Justus Café is experiencing mixed payment adoption across different transaction values, with heavy cash usage leading to long queues during peak hours. By analyzing customer payment behaviors, item preferences, and sales trends, this project provides actionable insights to:
- Improve transaction efficiency
- Enhance customer experience
- Identify upselling and revenue optimization opportunities
  
## Data Sources
Café Sales Data: The primary dataset used for this is analysis is the "dirty_cafe_sales.csv" dataset obtained from Kaggle, containing information about the sales made by Justus Café. The dataset consist of 10000 rows and 12 columns.

## Business Questions
- What is the highest selling product by transaction count?
- What day of the week records the highest sales?
- How do payment methods (cash, credit card, digital wallet) vary across low-value (<= $4) and high-value (>= $20) transactions?
- What incentives could shift payment preferences toward faster methods?
- What upselling opportunities exist to improve customer spend?
- Which months and quarters generate the most revenue?
- What payment methods are preferred across different customer categories?
- What is the highest revenue-generating product, and what is the location preference?
- Which channel (in-store vs. takeaway) produces the most sales?
- Do sales peak during weekdays or weekends?
## Tools Used
- MS Excel
- Power Query – data cleaning & transformation
- Power Pivot (Star Schema) – fact & dimension modeling
- DAX – revenue, transaction count, averages
- Pivot Tables & Dashboards – interactive visuals
## Data Cleaning and Transformation
The raw dataset contained missing, inconsistent, and incorrect values. The data cleaning was done using the power query editor. First the rows with no transaction date, no location and no payment methods were removed. The sales data in some instances had price without quantity, quantity without price, sales amount with price but no quantity. Since sales amount equals price times quantity. I created the following If condition logic: 
// This formula calculates the unit price when missing, using total spent divided by quantity
Price Column
```
m
= if [Price Per Unit] = null or [Price Per Unit] = "" or [Price Per Unit] = "UNKNOWN" or [Price Per Unit] = "ERROR" then 
   (if [Quantity] <> null and [Total Spent] <> null 
   then Number.From([Total Spent]) / Number.From([Quantity]) 
   else "Unknown") 
else try Number.From([Price Per Unit]) otherwise "Unknown"
```
\\ This formula calculates the total amount spent when missing, using price multiplied by quantity
Sales Amount
```
m
= if [Total Spent] = null or [Total Spent] = "" or [Total Spent] = "UNKNOWN" or [Total Spent] = "ERROR" then 
   (if [New_Price] <> "Unknown" and [New_Quantity] <> "Unknown" 
   then Number.From([New_Quantity]) * Number.From([New_Price]) 
   else "Unknown") 
else try Number.From([Total Spent]) otherwise "Unknown"
```
The applied steps can be found in ![Applied_Steps](Applied_Steps.png). 

\\ This formula classifies day into weekday or weekend
Day Classification
```
m
= if Date.DayOfWeek([Transaction Date]) = 0 or Date.DayOfWeek([Transaction Date]) = 6 
   then "Weekend" 
   else "Weekday"
```







