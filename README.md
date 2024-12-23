# Supermarket sales Power BI Dashboard Creation Using Kaggle Data

## Introduction
This README provides a detailed walkthrough of creating a Power BI dashboard using the supermarket_sales dataset from Kaggle. The dashboard aims to analyze sales data from January to March 2019 across three cities in Vietnam, offering insights for promotion and category planning.

## Data Acquisition
The dataset used for this project was sourced from Kaggle, specifically the supermarket_sales dataset. This dataset contains 1,000 transactions, 17 columns with info on customer membership, gender, product line, branch, payment method and rating. 

### Steps:
1. Downloaded the dataset from Kaggle
2. Performed initial data cleaning in Microsoft Excel before importing into Power BI
### Created 4 tables with relationship and _data transformation_ before establishing relationship:
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

** tbc feedback after 5-8 **    
9. Built one to many relationships among tables:
    - _Branch>City_ (Branch) 1-* _Sales Jan 2019-Mar 2019_ (Branch)
    - _Customer type & gender_ (MemberGender_Key) 1-* _Sales Jan 2019-Mar 2019_ (MemberGender_Key)
    - _Category Sales_ (Category) 1-* _Sales Jan 2019-Mar 2019_ (Category)
    - _Calendar_ (Date) 1-* _Sales Jan 2019-Mar 2019_ (Date)
      
### Data transformation after establishing one-to-many relationships: 
10. Created measures in table _Sales Jan 2019-Mar 2019_:
    - 'Average Sales Amount' : average of 'Total', shown as metric in form of multi-row card
    - 'Jan sales' : sum of 'Total' ,filter 'Month'=January
    - 'Feb sales' : sum of 'Total' ,filter 'Month'=February
    - 'Mar sales' : sum of 'Total' ,filter 'Month'=March
    - 'Mar Sales Growth vs Feb' : divide difference of 'Mar sales'and 'Feb sales' by 'Feb sales'
    - 'Mar Sales Growth vs Jan' : divide difference of 'Mar sales'and 'Jan sales' by 'Jan sales'
    - 'String_for_cat_button' : to enable string shown on drill through button reflect the filtered value for category
    - 'String_for_city_button' : to enable string shown on drill through button reflect the filtered value for city 
11. Created 'Time (3 hours)' ,'Time (bins)' to be applied on clustered column chart to show sales over time
12. Created measure in table _Category Sales_:
    - 'Branch contribution' : divide sum of 'Total' sales amount (From "Sales Jan 2019-Mar 2019") by sum of 'Category Sales', in percentage %
    - 'Category Sales Ranking (Jan-Mar)' : sum of 'Total' sales amount (From "Sales Jan 2019-Mar 2019") in descending order, in integer format

### Visualisation on summary page: 
13. Interactive filters with option to drill-through to details page at the back
14. 'City', 'Category', 'Time (3 hours)', 'Gender', 'Membership' slicers
15. Overview on Sales amount, Qty sold, % of changes Mar vs Feb, % of changes Mar vs Jan, Average sales amount 
16. Top cities by sales (with contribution %)
17. Top categories by sales (with contribution % and average sales $) 
18. Category sales over three months (with change %, ranking)
 
### Visualisation on details page filtered by selected city/category: 
19. Multi-row card on top show the filter applied (if without filter, by default showing top city/category in total sales amount)
20. Interactive dashboard on same page for further filters 
21. Sales by month shown in matrix (may breakdown to daily)
22. Rating by month
23. Hours, payment mode, member type with most sales
24. Category/branch sales by time
25. Category contribution % by applying filter on hours
26. Payment mode (contribution %), member type sales $ by month

## Conclusion
This README outlines my process of using Kaggle data to create an interactive and insightful Power BI dashboard. This demonstrates my ability to handle data analysis, transformation, and visualization tasks effectively.
