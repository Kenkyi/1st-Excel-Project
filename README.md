# 1st-Excel-Project
This Excel project analyzes the sales data of electronics from 2016 to 2021 and creates a dashboard using exploratory analysis.tory analysis.

# Introduction
This project analyzes the total sales of electronics over the years from 2016 to 2021. It explores the countries with the highest sales, the most popular items in terms of sales, and key performance indicators (KPIs) such as total sales, the total number of orders, profit margin, profit percentage, and revenue growth.

# Background

Motivated by the desire to identify sales trends and patterns, this project was created to focus on four main KPIs, four charts, and three slicers.

# Questions I Wanted to Answer Through the Data Model and Dashboard
1.	Was the sales trend constant over the period?
2.	What is the seasonality of the sales trend?
3.	Which product category generated the most revenue?
4.	Does the age group of customers impact sales?
5.	Which country has the highest number of customers and the highest revenues?

# Tools Used
•	Excel: The primary tool for creating charts, graphs, and dashboards.
•	Pivot Table: A tool for performing analysis, grouping, and pivoting to examine data.
•	Power Query: Used to automate calculations within Excel.
•	DAX: Used for advanced calculations on pivot tables.

# Dataset
The dataset was sourced from Maven Analytics. It covers the period from 2016 to 2021, with data for January and February of 2021 included. The most meaningful insights come from annual comparisons between 2016 and 2020.

## Example Formulas
 # To Calculate Days to Deliver, Profit, and Customer Age
```
= Table.AddColumn(#"Sorted Rows", "days_to_deliver", each Duration.Days([DeliveryDate] - [OrderDate]), Int64.Type)  
= Table.AddColumn(#"Sorted Rows", "profit", each [ProductPrice] - [ProductCost], type number)  
= Table.AddColumn(#"Changed Type1", "customer_age", each Number.RoundDown(Duration.Days(DateTime.LocalNow() - [CustomerDOB]) / 365.25))
```
# To Group Customer Age Groups
```
= DATEDIFF([CustomerDOB], TODAY(), YEAR) - IF(OR(MONTH(TODAY()) < MONTH([CustomerDOB]), AND(MONTH(TODAY()) = MONTH([CustomerDOB]), DAY(TODAY()) < DAY([CustomerDOB]))), 1, 0)
```

```
=  
SWITCH(
    TRUE(),
    'Transactions'[customer_age] < 18, "Teens (Under 18)",
    'Transactions'[customer_age] >= 18 && 'Transactions'[customer_age] <= 24, "Young Adults (18-24)",
    'Transactions'[customer_age] >= 25 && 'Transactions'[customer_age] <= 44, "Adults (25-44)",
    'Transactions'[customer_age] >= 45 && 'Transactions'[customer_age] <= 64, "Middle-aged (45-64)",
    'Transactions'[customer_age] >= 65, "Seniors (65+)",
    "Other"
)
```
# To Calculate Profit Percentage
=DIVIDE(AVERAGE([ProductPrice]) - AVERAGE([ProductCost]), AVERAGE([ProductCost]))


# What I Learned from the Project
## •	The highest total sales occurred in Q4 of 2019, with $5,768,124. Every year, February and Q4 consistently bring the highest sales values.
## •	The majority of the company’s customers are located in the United States.
## •	In terms of age groups, people over the age of 65 accounted for nearly 40% of the company’s sales during the period.
## •	When comparing online and in-store sales, 80% of the sales came from in-store purchases. However, there was no significant difference between customer gender in terms of sales; both genders contributed equally.
## •	Over the six-year period, there were 62,884 total orders, with 2019 having the highest number of orders at 21,611.
## •	In terms of product categories, ‘Computers’ generated the highest percentage of sales, while ‘Music, Movies, and Audiobooks’ had the highest profit margin.
