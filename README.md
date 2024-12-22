# Supermarket sales Power BI Dashboard Creation Using Kaggle Data

## Introduction
This README provides a walkthrough of the process I followed to create a Power BI dashboard using a dataset from Kaggle. The goal of this dashboard is to analyze a Vietnam supermarket sales Jan-Mar 2019 in 3 different cities and provide insights into promotion and category planning. 

## Data Acquisition
The dataset used for this project was sourced from Kaggle, specifically the supermarket_sales dataset. This dataset contains 1000 transactions, 17 columns with info on customer membership, gender, product line, branch, payment method and rating. 

### Steps:
1. Downloaded the dataset from Kaggle
2. Performed initial data cleaning in Microsoft Excel before importing into Power BI
### Power Query Editor - Table no.1 "Sales Jan 2019-Mar 2019":
3. Opened up the Power Query Editor and inserted the 'Average price' column with division of 'Total' over 'Quantity' despite existence of 'Unit price' column
4. Removed irrelevant columns i.e. 'cogs', 'gross margin percentage', 'gross income', 'City'
5. Recoded the 'Customer type' column to replace the value 'Member' with '1' and 'Normal' with '0'
6. Recoded the 'Gender' column to replace the value 'Male' with '1' and 'Female' with '0'
7. Renamed the 'Product line' column to 'Category'
### Power Query Editor - Table no.2 "Branch>City":
8. Loaded the same dataset and updated the column with correct data types
9. Created the reference table of 'Branch' & 'City'
### Power Query Editor - Table no.3 "Customer type & gender": 
10. Created new reference table with columns of "Customer type (code)", "Gender (code)", "Member&Gender" as description column
11. Updated the columns with correct data types
### Power Query Editor - Table no.4 "Category Sales": 
12. Group by "Total" by "Product line" and renamed as "Category Sales"
13. Renamed the 'Product line' column to 'Category'


...

## Conclusion
This README outlines my process of using Kaggle data to create an interactive and insightful Power BI dashboard. This demonstrates my ability to handle data analysis, transformation, and visualization tasks effectively.
