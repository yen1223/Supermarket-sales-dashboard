# Supermarket sales Power BI Dashboard Creation Using Kaggle Data

## Introduction
This README provides a detailed walkthrough of creating a Power BI dashboard using the supermarket_sales dataset from Kaggle. The dashboard aims to analyze sales data from January to March 2019 across three cities in Vietnam, offering insights for promotion and category planning.

## Data Acquisition
The dataset used for this project was sourced from Kaggle, specifically the supermarket_sales dataset. This dataset contains 1,000 transactions, 17 columns with info on customer membership, gender, product line, branch, payment method and rating. 

### Steps:
1. Downloaded the dataset from Kaggle
   
2. Performed initial data cleaning in Microsoft Excel before importing into Power BI
   
3. Opened Power Query Editor and created the first table, naming it _Sales Jan 2019-Mar 2019_
   
4. Transformation in Table _Sales Jan 2019-Mar 2019_:
    - Inserted an 'Average price' column by dividing 'Total' by 'Quantity' (despite having a 'Unit price' column)
    - Removed irrelevant columns such as 'cogs', 'gross margin percentage', 'gross income', and 'City'
    - Recoded the 'Customer type' column: replaced 'Member' with '1' and 'Normal' with '0'
    - Recoded the 'Gender' column: replaced 'Male' with '1' and 'Female' with '0'
    - Renamed the 'Product line' column to 'Category'
    - Created a composite 'MemberGender_Key' column from 'Customer type (code)' and 'Gender (code)' to serve as a foreign key for the "Customer type & gender" reference table
      
5. Loaded the same dataset and named table no.2 as _Branch>City_ as a reference table with only columns of 'Branch' and 'City'

6. Created another reference table, named _Customer type & gender_:
    - Started with 'Customer type (code)', 'Gender (code)' columns
    - Created a composite code column of 'MemberGender_Key' to serve as primary key
    - Added new columns of 'Gender' , 'Membership' 'Member&Gender' as description for coded columns

7. Created table, _Category Sales_:
    - Group by 'Total' (sales amount) by 'Product line'
    - Renamed the 'Total' column as 'Category Sales' , 'Product line' column as 'Category'
    - Enabled more detailed info on tooltip by having measure related to the level of category sales

8. Created table, _Calendar_ to define date hierarchies and allow time-based analysis:
    - Created a calendar table of Jan to March 2019
    - Inserted columns of 'Month','Month-Year','Day','Month(no)' as month number
  
9. Built one to many relationships among tables:
    - _Branch>City_ (Branch) 1-* _Sales Jan 2019-Mar 2019_ (Branch)
    - _Customer type & gender_ (MemberGender_Key) 1-* _Sales Jan 2019-Mar 2019_ (MemberGender_Key)
    - _Category Sales_ (Category) 1-* _Sales Jan 2019-Mar 2019_ (Category)
    - _Calendar_ (Date) 1-* _Sales Jan 2019-Mar 2019_ (Date)

![Screenshot](https://github.com/yen1223/Supermarket-sales-dashboard/blob/main/Vietnam%20Supermarket%20Sales%20Data%20Model.png
 "Vietnam Supermarket Sales Data Model")

10. Created measures in table _Sales Jan 2019-Mar 2019_

| Measures🖩            | DAX                                                                | Presented as                            |
|----------------------|--------------------------------------------------------------------|-----------------------------------------|
| Average Sales Amount | `Average Sales Amount = AVERAGE('Sales Jan 2019-Mar 2019'[Total])` | Metric in the form of<br>multi-row card |
| Jan sales            | `Jan sales = CALCULATE(sum('Sales Jan 2019-Mar 2019'[Total]),'Calendar'[Month]="January")`| Monthly category sales in clustered column chart |
| Feb sales            | `Feb sales = CALCULATE(sum('Sales Jan 2019-Mar 2019'[Total]),'Calendar'[Month]="February")`| Monthly category sales in clustered column chart |  
| March sales          | `March sales = CALCULATE(sum('Sales Jan 2019-Mar 2019'[Total]),'Calendar'[Month]="March")`| Monthly category sales in clustered column chart |  
| Mar Sales Growth vs Feb | `Mar Sales Growth vs Feb = DIVIDE(([March sales]-[Feb sales]),[Feb sales])` | Metric in the form of multi-row card;<br>Tooltip on monthly category sales in clustered column chart|
| Mar Sales Growth vs Jan | `Mar Sales Growth vs Jan = DIVIDE(([March sales]-[Jan sales]),[Jan sales])` | Metric in the form of multi-row card;<br>Tooltip on monthly category sales in clustered column chart|
| String_for_cat_button | `String_for_cat_button = If(SELECTEDVALUE('Sales Jan 2019-Mar 2019'[Category], 0) == 0, "See category details", "See details for " & SELECTEDVALUE('Sales Jan 2019-Mar 2019'[Category]))` | Enable string shown on drill through button reflect the filtered value for category|
| String_for_city_button | `String_for_city_button = If(SELECTEDVALUE('Branch>City'[City], 0) == 0, "See branch details", "See details for " & SELECTEDVALUE('Branch>City'[City]))` | Enable string shown on drill through button reflect the filtered value for city|

11. Created 'Time (3 hours)' ,'Time (bins)' columns to be applied on clustered column chart to show sales over time
    
12. Created measures in table _Category Sales_

| Measures🖩            | DAX                                                                | Presented as                            |
|----------------------|--------------------------------------------------------------------|-----------------------------------------|
| Branch contribution | `Branch contribution = sum('Sales Jan 2019-Mar 2019'[Total])/sum('Category Sales'[Category Sales])` | Tooltip on top categories in clustered bar chart to show selected branch contribution to category sales|
| Category Sales Ranking (Jan-Mar) | `Category Sales Ranking (Jan-Mar) = rankx(ALLSELECTED('Sales Jan 2019-Mar 2019'[Category]),CALCULATE(sum('Sales Jan 2019-Mar 2019'[Total])), ,DESC,Dense)` | Tooltip on monthly category sales in clustered column chart|

### 13. Visualisation on summary page: 
![Screenshot](https://github.com/yen1223/Supermarket-sales-dashboard/blob/main/Vietnam%20Supermarket%20Sales%20Dashboard_Summary%20Page.png
 "Vietnam Supermarket Sales Dashboard Summary Page")
 
* Interactive filters with option to drill-through to details page at the back  
* Slicers of 'City', 'Category', 'Time (3 hours)', 'Gender', 'Membership' 
* Enables interaction between charts for further data exploration
* First presented with overview on
     * Sales amount
     * Qty sold
     * % of changes Mar vs Feb
     * % of changes Mar vs Jan
     * Average sales amount 
* Top cities by sales (with contribution %)
* Top categories by sales (with contribution % and average sales $) 
* Category sales over three months (with change %, ranking)
 
### 14. Visualisation on details page filtered by selected city/category: 
![Screenshot](https://github.com/yen1223/Supermarket-sales-dashboard/blob/main/Vietnam%20Supermarket%20Sales%20Dashboard_Details%20Page.png
 "Vietnam Supermarket Sales Dashboard Details Page") 
 
 By default, it displays overall detailed info. This page could offer insights on promotion planning. 
 
* Multi-row cards stated with the filters applied
     * If without filter, typically will show top city/category
* Enables interaction between charts for further data exploration
* Details (in chart sequence):
     * Sales by month shown in matrix (drill down to daily)
     * Trend of customer rating by month
     * Popular hours of customer purchase, payment mode, gender, member type with most sales
     * Trend of category/branch sales by time
     * Category contribution % in piechart for after applying filter on hours of customer purchase,         to find out focus category over different timing of the days at different branches
        * Vice versa, by selecting one or multiple categories, we can observe the timeslot with most           purchase on the selected category
     * Similar interaction can be applied on the chart of payment mode contribution chart (by month)        & member type x gender sales $ chart (by month) when planning collaboration with bank, BNPL          partners and membership programmes

## Conclusion
This README outlines the step-by-step process of using Kaggle data to create an interactive and insightful Power BI dashboard. It demonstrates my ability to effectively handle data analysis, transformation, and visualization tasks, providing actionable insights for business decision-making.
