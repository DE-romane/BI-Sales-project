# Sales Insights and Performance Project

Welcome to the **End-to-End Power BI Sales Dashboard Project**. 

![sales Dashboard2](https://github.com/DE-romane/BI-Sales-project/assets/70475916/7b76ccf6-f273-4b33-88bc-ab01d8960c9a)

![Sales Dashboard](https://github.com/DE-romane/BI-Sales-project/assets/70475916/df29fa73-0643-4bd7-8d07-fc401dab2e26)



## Table of Contents

1. [Objective of the Sales Dashboard / Business Problem](#objective-of-the-sales-dashboard--business-problem)
2. [Steps to Follow for an End-to-End Power BI Project](#steps-to-follow-for-an-end-to-end-power-bi-project)
    - [Import Data](#Import-Data)
    - [Power Query – Data Extract, Transform & Load](#power-query--data-extract-transform--load)
    - [Create a Date Table](#create-a-date-table)
    - [Create Data Model in Power BI Desktop](#create-data-model-in-power-bi-desktop)
    - [Develop Reports in Power BI Desktop](#develop-reports-in-power-bi-desktop)
    - [Implementing DAX Calculations](#implementing-dax-calculations)
3. [Conclusion of Power BI Sales Dashboard Project](#conclusion-of-power-bi-sales-dashboard-project)
4. [Download Power BI Project PBIX File & Excel Dataset](#download-power-bi-project-pbix-file--excel-dataset)

## Objective of the Sales Dashboard / Business Problem

The objective of this report is to analyze and present comprehensive insights into sales, profit, orders, profit margin, and various comparisons. The goals are to:

- Calculate and display the **Total Sales** for the selected period.
- Calculate and visualize the **Total Profit**.
- Analyze the **Number of Orders** placed during the selected period.
- Calculate and visualize the **Profit Margin Percentage**.
- Compare **Sales by Product** with the previous year.
- Compare **Sales by Month** with the previous year.
- Display the **Top 5 Cities** based on sales.
- Compare **Profit by Channel** with the previous year.
- Analyze **Sales by Customer** and compare with the previous year.
- Create **Slicers** for Date, City, Product, and Channel.

## Steps to Follow for an End-to-End Power BI Project

### Import Data

Load data from Data/Sales Analysis Report.xlsx

### Power Query – Data Extract, Transform & Load

Use the Power Query Editor in Power BI to clean and transform the data. This involves removing duplicates, handling missing values, merging datasets, and creating calculated columns.

### Create a Date Table

To work with DAX time intelligence functions

Ensure to turn off Auto Date/Time for new files in Power BI Options Settings to improve performance.

```DAX
DAX DateTable = 
ADDCOLUMNS (
    //CALENDAR(DATE(2020,1,1), DATE(2024,12,31)),
    CALENDARAUTO(),
    "Year", YEAR([Date]),
    "Quarter", "Q" & FORMAT(CEILING(MONTH([Date])/3, 1), "#"),
    "Quarter No", CEILING(MONTH([Date])/3, 1),
    "Month No", MONTH([Date]),
    "Month Name", FORMAT([Date], "MMMM"),
    "Month Short Name", FORMAT([Date], "MMM"),
    "Month Short Name Plus Year", FORMAT([Date], "MMM,yy"),
    "DateSort", FORMAT([Date], "yyyyMMdd"),
    "Day Name", FORMAT([Date], "dddd"),
    "Details", FORMAT([Date], "dd-MMM-yyyy"),
    "Day Number", DAY ( [Date] )
)
```

### Create Data Model in Power BI Desktop

Design and create a data model representing the relationships between different tables. Establish proper relationships, define keys.

![data model](https://github.com/DE-romane/BI-Sales-project/assets/70475916/477bafd9-5a14-475e-87d1-2dfa854662e4)

### Develop Reports in Power BI Desktop

 create reports based on data model. Add visualizations such as charts, tables, and maps. Apply filters, slicers, and drill-through functionalities.

**Creating Visuals:**

- Create Slicers – Date, City, Product, and Channel
- Create Dax measures
- Create Visuals:
- 1) Sales By Product and Comparing it with last year’s Sales.
- 2) Sales By Month and Comparing it with last year’s Sales.
- 3) Sales of top 5 Cities
- 4) Compare Profit by channel with Previous year’s Profit
- 5) Sales By Customer and Comparing it with last year’s Sales
 - 6) Create Cards for Sales, Profit, Profit Margin & Product Sold
### Implementing DAX Calculations

Use DAX to create calculated columns, measures, and tables for complex calculations and aggregations.

```dax
// Measures

//Measures Total Sales
Sales = SUM(Sales_Data[Sales])

//Measures Previous Year Toal Sales
Sales PY = CALCULATE([Sales], SAMEPERIODLASTYEAR(DateTable[Date]))

//Diffrence Between Current Year Sales & Previous Year Sales
Sales vs PY = [Sales] - [Sales PY]

//Percentage Increase or Decrease in sales year on year (YOY%)
Sales vs py % = DIVIDE([Sales vs PY],[Sales],0)

Products Sold = SUM(Sales_Data[Order Quantity])
Profit = SUM(Sales_Data[Profit])
Profit LY = CALCULATE([Profit], SAMEPERIODLASTYEAR(DateTable[Date]))
Profit Vs LY = [Profit] - [Profit LY]
Profit vs LY % = [Profit Vs LY] / [Profit]
Profit Margin = DIVIDE([Profit], [Sales], 0)
Total Cost = SUM(Sales_Data[Total Cost])
```

## Conclusion of Power BI Sales Dashboard Project

### Conclusion for the Year 2019:

- Sales decreased by more than 10%.
- There is a drop in sales of all the top 7 Products.
- 4 Customers are leading to a drop in sales.
- The profit margin in the Export channel is higher.
