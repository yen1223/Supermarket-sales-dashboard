# Supermarket sales Power BI Dashboard Creation Using Kaggle Data

## Introduction
This README provides a walkthrough of the process I followed to create a Power BI dashboard using a dataset from Kaggle. The goal of this dashboard is to analyze a Vietnam supermarket sales Jan-Mar 2019 in 3 different cities and provide insights into promotion and category planning. 

## Data Acquisition
The dataset used for this project was sourced from Kaggle, specifically the supermarket_sales dataset. This dataset contains 1000 transactions, 17 columns with info on customer membership, gender, product line, branch, payment method and rating. 

### Steps:
1. Downloaded the dataset from Kaggle
2. Performed initial data cleaning in Microsoft Excel before importing into Power BI
### Table no.1 "Sales Jan 2019-Mar 2019":
3. Opened up the Power Query Editor and inserted the 'Average price' column with division of 'Total' over 'Quantity' despite existence of 'Unit price' column
4. Removed irrelevant columns i.e. 'cogs', 'gross margin percentage', 'gross income', 'City'
5. Recoded the 'Customer type' column to replace the value 'Member' with '1' and 'Normal' with '0'
6. Recoded the 'Gender' column to replace the value 'Male' with '1' and 'Female' with '0'
7. Renamed the 'Product line' column to 'Category'
8. Created composite code column 'MemberGender_Key' from 'Customer type (code)'& 'Gender (code)' as a foreign key to connect with reference table "Customer type & gender" later
9. Created one to many relationships with tables
    - Customer type & gender (MemberGender_Key) 1-* Sales Jan 2019-Mar 2019 (MemberGender_Key)
    - Calendar (Date) 1-* Sales Jan 2019-Mar 2019 (Date)
    - Branch>City (Branch) 1-* Sales Jan 2019-Mar 2019 (Branch)
    - Category Sales (Category) 1-* Sales Jan 2019-Mar 2019 (Category)
10. Created measures:
    - 'Average Sales Amount' with average of 'Total'
    - 'Feb sales' with sum of 'Total' filter 'Month'=February (AFTER TBC SMOOTH THEN CONTINUE HERE)
... TBC need rearranged the table creation sequence to make the flow smooth TBC.....
### Table no.2 "Branch>City":
8. Loaded the same dataset and updated the column with correct data types
9. Created the reference table of 'Branch' & 'City'
10. Created measure of 'Branch contribution' by dividing sum of 'Total' sales amount (From "Sales Jan 2019-Mar 2019") by sum of 'Category Sales'
11. Created measure of 'Category Sales Ranking (Jan-Mar)' with sum of 'Total' sales amount (From "Sales Jan 2019-Mar 2019") in descending order
### Table no.3 "Customer type & gender": 
10. Created new reference table with columns of 'Customer type (code)', 'Gender (code)', 'Member&Gender' as description column
11. Updated the columns with correct data types
12. Added new columns of 'Gender'& 'Membership' as description for coded columns
13. Created composite code column 'MemberGender_Key' from 'Customer type (code)'& 'Gender (code)' as the primary key
### Table no.4 "Category Sales": 
12. Group by 'Total' by 'Product line' and renamed as 'Category Sales'
13. Renamed the 'Product line' column to 'Category'
### Table no.5 "Calendar": 
14. Created a calendar table of Jan to March 2019
15. Inserted columns of 'Month','Month-Year','Day','Month(no)'
16. Connected this table with 'Date' column of primary table no.1 "Sales Jan 2019-Mar 2019"


    


...

## Conclusion
This README outlines my process of using Kaggle data to create an interactive and insightful Power BI dashboard. This demonstrates my ability to handle data analysis, transformation, and visualization tasks effectively.
