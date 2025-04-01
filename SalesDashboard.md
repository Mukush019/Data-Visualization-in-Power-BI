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
-  Which product categories and sub-categories provide the highest sales and profit, and which ones do we need to market?

## Data Analysis
