# Sales Performance & Profitability Dashboard (Power BI)

An interactive Power BI dashboard that analyses sales performance, year-over-year trends, discount impact and profitability.

> **Note:** Built on a practice dataset. The findings do not represent actual company performance.

## Business Problem
Sales and profit are declining compared with last year. The goal is to find what is going wrong, where it is happening, and what needs further investigation.

## Dataset
- 1,800 order records (practice dataset)
- Columns: Order_ID, Order_Date, Customer_ID, Region, Sales_Channel, Category, Product, Quantity, Sales, Cost, Profit, Discount_Rate
- 10 rows had blank Profit values, so Total Profit is calculated as `Sales - Cost`

## Key Findings (2026 YTD vs. same period last year)
- Sales declined by **11.6%**, profit decreased by **15.8%**
- Profit margin fell by **1.5 pp** to **29.4%**
- **South** had the highest sales, **East** the lowest
- Next step: investigate product mix and discount patterns in weaker regions before making pricing recommendations

## Dashboard Features
- KPI cards: Total Sales, Total Profit, Profit Margin %, Total Orders, Average Order Value, each with a vs-last-year indicator
- Monthly sales trend: 2026 vs 2025
- Sales by Category and Sales by Channel
- Pareto chart: Total Sales and Cumulative Sales % by Product
- Margin % by Discount Rate
- Region x Category matrix
- Custom tooltip page and region drill-through page
- What-if analysis to test discount scenarios
- Slicers: Year, Region, Sales Channel

## Key DAX Measures
```DAX
Total Sales = SUM(Sales[Sales])

Total Profit = SUM(Sales[Sales]) - SUM(Sales[Cost])

Profit Margin % = DIVIDE([Total Profit], [Total Sales])

Sales LY = CALCULATE([Total Sales], SAMEPERIODLASTYEAR(DateTable[Date]))

Sales vs LY % = DIVIDE([Total Sales] - [Sales LY], [Sales LY])

Cumulative Sales % =
VAR CurrentSales = [Total Sales]
VAR CumSales =
    CALCULATE([Total Sales], FILTER(ALLSELECTED(Sales[Product]), [Total Sales] >= CurrentSales))
VAR AllSales = CALCULATE([Total Sales], ALLSELECTED(Sales[Product]))
RETURN DIVIDE(CumSales, AllSales)
```


## Tools
Power BI Desktop, DAX, Excel

## Files
- `Sales_Dashboard.pbix`: Power BI report
- `sales_practice_dataset.xlsx`: practice dataset

## About Me
Devadharshini K | 2026 CSE graduate | Looking for Data Analyst / BI roles

