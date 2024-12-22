# Supermarket sales Power BI Dashboard Creation Using Kaggle Data

## Introduction
This README provides a walkthrough of the process I followed to create a Power BI dashboard using a dataset from Kaggle. The goal of this dashboard is to analyze a Vietnam supermarket sales Jan-Mar 2019 in 3 different cities and provide insights into promotion and category planning. 

## Data Acquisition
The dataset used for this project was sourced from Kaggle, specifically the supermarket_sales dataset. This dataset contains 1,000 transactions, 17 columns with info on customer membership, gender, product line, branch, payment method and rating. 

### Steps:
1. Downloaded the dataset from Kaggle
2. Performed initial data cleaning in Microsoft Excel before importing into Power BI
### Created 4 tables with relationship and _data transformation_ before establishing relationship:
3. Opened up the Power Query Editor and named first table as "Sales Jan 2019-Mar 2019"
   
4. Transformation in Table _"Sales Jan 2019-Mar 2019"_:
    - Inserted the 'Average price' column with division of 'Total' over 'Quantity' (although there is 'Unit price' column)
    - Removed irrelevant columns i.e. 'cogs', 'gross margin percentage', 'gross income', 'City'
    - Recoded the 'Customer type' column to replace the value 'Member' with '1' and 'Normal' with '0'
    - Recoded the 'Gender' column to replace the value 'Male' with '1' and 'Female' with '0'
    - Renamed the 'Product line' column to 'Category'
    - Created composite code column 'MemberGender_Key' from 'Customer type (code)' and'Gender (code)' as a foreign key to connect with reference table "Customer type & gender" 
      later
      
5. Loaded the same dataset and named table no.2 as "Branch>City" as a reference table with only columns of 'Branch' and 'City'

6. Created another reference table, named _"Customer type & gender"_:
    - Started with 'Customer type (code)', 'Gender (code)' columns
    - Created a composite code column of 'MemberGender_Key' to serve as primary key
    - Added new columns of 'Gender' , 'Membership' 'Member&Gender' as description for coded columns

7. Created table, _"Category Sales"_:
    - Group by 'Total' (sales amount) by 'Product line'
    - Renamed the 'Total' column as 'Category Sales' , 'Product line' column as 'Category'

8. Created table, _"Calendar"_:
    - Created a calendar table of Jan to March 2019
    - Inserted columns of 'Month','Month-Year','Day','Month(no)' as month number
      
9. Built one to many relationships among tables:
    - _Branch>City_ (Branch) 1-* _Sales Jan 2019-Mar 2019_ (Branch)
    - _Customer type & gender_ (MemberGender_Key) 1-* _Sales Jan 2019-Mar 2019_ (MemberGender_Key)
    - _Category Sales_ (Category) 1-* _Sales Jan 2019-Mar 2019_ (Category)
    - _Calendar_ (Date) 1-* _Sales Jan 2019-Mar 2019_ (Date)
      
### Data transformation after establishing one-to-many relationships: 
10. Created measures in table "Sales Jan 2019-Mar 2019":
    - 'Average Sales Amount' : average of 'Total'
    - 'Feb sales' : sum of 'Total' ,filter 'Month'=February    **(AFTER TBC SMOOTH THEN CONTINUE HERE)**
      
11. Created measure in table "Category Sales":
    - 'Branch contribution' : divide sum of 'Total' sales amount (From "Sales Jan 2019-Mar 2019") by sum of 'Category Sales'
    - 'Category Sales Ranking (Jan-Mar)' : sum of 'Total' sales amount (From "Sales Jan 2019-Mar 2019") in descending order



    


...

## Conclusion
This README outlines my process of using Kaggle data to create an interactive and insightful Power BI dashboard. This demonstrates my ability to handle data analysis, transformation, and visualization tasks effectively.
