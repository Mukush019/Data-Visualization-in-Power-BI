# **Sales Dashboard** 
---
## Project Overview
A company seeks to optimize sales strategies, increase profits, and improve on customer engagement but lacks insights into key revenue drivers, product performance, and customer behaviors. This project aims to uncover opportunities for strategic growth, cost reduction, and targeted marketing by analyzing sales trends, demographic patterns, geographic distribution, and product category efficiency.
## Data Sources 
The primary dataset used for this project is "sales_data" [View the data](https://docs.google.com/spreadsheets/d/1Pyd4bmOhPAGTKe0WP55vAXPNJ9zRj3nPmvesxblrCjs/edit?usp=sharing).
The data contains:
- *Date information*
  - Date
  - Day
  - Month
  - Year
- *Demographic Information*
   - Customer_Age
   - Age_Group
   - Customer_Gender
- *Geographic Information*
   - Country
   - State
- *Product Information*
   - Product_Category
   - Sub_Category
   - Product
- *Sales Information*
   - Order_Quantity
   - Unit_Cost
   - Unit_Price
   - Profit
   - Cost
   - Revenue
## Tools
This project was done in *Power BI Desktop* **ONLY**
[Download Here](https://www.microsoft.com/en-us/download/details.aspx?id=58494)
## Data Cleaning and Preparation
- Data loading and inspection
- Data formatting
   - Dimension Modelling
     The data contained only one table with a combination of dimensions and measures. All this was done in Power Query in Power BI. This step involves the creation of a star schema. The steps taken were as follows:
      1. Duplicating the original table.
      2. Removing unnecessary columns, *ONLY* leaving relevant columns for that dimension table. i.e, Customer Table only has Customer Age, AgeGroup, and Customer Gender
      3. Adding a *Primary Key* for the dimension table using the Index Column option in Power BI. A DAX was also used to make the Primary Key dimension specific.
         
         ```dax
         "Customer_ID" = "Cust_" & Text.PadStart(Text.From([Index]),3,"0")
         ```
      4. The final step involved merging the dimension table with the fact table.
    The final result was a **Star Schema**.
    *Dimension Table* - Customer_Table
                      - Product_Table
                      - Date Table
                      - Country_Table
    *Fact Table* - Sales_Fact_Table
## Exploratory Data Analysis
EDA involved exploring the sales data to answer key questions, such as:
- What is the total revenue?
- Describe the revenue growth rate both annually and quarterly
- How does the profit margin vary?
- Has customer spending increased or decreased over the years?
- What are the top 5 products in terms of revenue and profit?
- What is the country-wise contribution regarding orders, revenue, and profit?
-  How do sales vary depending on age?
-  In which months do we have peak sales?
-  Which product categories and sub-categories provide the highest sales and profit, and which do we need to market?

## Data Analysis
A time series analysis was done to come up with the KPIs. The following measures and DAX were used in the visualization of the various key performance indicators:
- Total Sales
  ```dax
    Total Revenue = SUM(sales_Fact_Table[Revenue])
  ```
- Total profit
```dax
Total Profit = SUM(sales_Fact_Table[Profit])
```
- Average order value
```dax
  Average Order Value = DIVIDE(
    [Total Revenue],
    COUNTROWS(sales_Fact_Table)
)
```
- Current Year Sales
```dax
Current Year Revenue = TOTALYTD(
                                [Total Revenue],
                                DATESYTD('Date'[Date])
)
```
- Current Quarter Sales
```dax
Current Quarter Sales = TOTALQTD(
                                [Total Revenue],
                                DATESQTD('Date'[Date])
)
 ```
- Previous Year Sales
```dax
  Previous Year Revenue = CALCULATE(
                                    [Total Revenue],
                                    PREVIOUSYEAR(
                                        DATESYTD('Date'[Date])
                                    )
                                )
```
Previous Quarter Sales
```dax
Previous QTD Sales = CALCULATE(
                        [Total Revenue],
                        PREVIOUSQUARTER(
                            DATESQTD('Date'[Date])
                        )
                        )
```
- Annual and Quarterly Growth Rate
```dax
Yearly Growth Rate = DIVIDE(([Current Year Revenue]-[Previous Year Revenue]),[Previous Year Revenue])
```
```dax
Quarterly Revenue Growth = DIVIDE(([Current Quarter Sales]-[Previous QTD Sales]),[Previous QTD Sales])
```
- Profit Margin
```dax
F-Profit Margin = DIVIDE(
                       [Total Profit],
                       [Total Revenue]
)
```
The following DAX was used in creating age ranges that were used in the histogram 
```dax
NewAgeGroup = 
VAR LowerBound = FLOOR(Customer_Table[Customer_Age],10)  
RETURN
     LowerBound & "-" & (LowerBound+9)
```

## Results and Findings
This analysis results are summarized as follows:
- The company's total sales from 2011-2016 is $ 108,756,685.
- The annual sales dropped by 9.41% in 2016. However, it is worth noting that according to the data, 2016 was not over yet. We have sales data from January to July.
- The quartely sales also dropped significantly. As already stated, the 2016 FY is not over yet. Since the company experienced a sharp decline in sales in July, this has contributed to the significant drop in quarterly sales.
- The company recorded a significant improvement in profitability.
- In the country-wise analysis, the United States tops the list in terms of order quantity, sales, and profit. Something worthy to note is that even though Canada has a significantly higher order quantity compared to the United Kingdom, the United Kingdom records more sales and profit compared to Canada.
- Customers between the ages of 30 and 39 contribute a significantly high share of revenue for the company, while customers aged 80-89 contribute the least to the company's revenue. The company's peak season is June, when it records the highest revenue before dropping sharply in July, then rising consistently in November and December.
- The bikes product category records the highest sales and profit but significantly low order quantity. Accessories have the highest order quantity but not high sales and revenue. Clothing product category has average order quantity but significantly low sales and revenue.

## Recommendation

