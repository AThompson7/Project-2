![Seattle Airbnb](https://storage.googleapis.com/kaggle-datasets-images/393/804/669cd834cb82eb3f7fbded566dd02e92/dataset-cover.jpeg)
# **Project 2 - Seattle Airbnb**
The aim of this project is to investigate patterns of more or less successful airbnb locations within the Seattle, Washington area. The two .csv files were joined on the “listing_id” and “id” columns respectively. Numerous data factors were cleaned and taken into consideration such as zip code, accommodation, host status, price and reviews rating. Relationships between the data can be investigated in PostgreSQL to potentially glean new insights into the statistically relevant operations of Seattle airbnbs.

## **Members**
Jose Sandoval  &emsp; &emsp; Vanessa Kemp<br>
Nick Taheri   &emsp; &emsp; &emsp;  Aidan Thompson

## **Step 1: Extraction**
Two .csv files were utilized for this project. The files are located within the ‘Resource’ folder which were both acquired from https://www.kaggle.com/datasets/airbnb/seattle.

Originally, the Kaggle dataset also included a reviews.csv file. It was decided that for the purposes of our analysis the reviews.csv file should not be used as it contained qualitative data such as reviewer names of airbnb's and their review comments. Data such as this would be difficult to draw any conclusions from and make comparisons to the other tables. 

To extract the data, Jupyter Notebook was used and pandas's read_csv function was used to load the raw csvs from our Resources folder into an initial data frame.

## **Step 2: Transform**
Each of the .csv files were examined for relevance and usability to achieve the project’s target. The following lists the columns of each .csv file which were chosen to be cleaned using Pandas/Jupyter Notebooks.

•         	**calendar.csv** : The listing_id, available and price columns.
   ~~~~python	
   calendar_file = "Resources/calendar.csv"
   calendar_df = pd.read_csv(calendar_file, encoding="utf8")
   ~~~~
•         	**listings.csv** : The  id, host_response_rate, host_acceptance_rate, host_is_superhost, zipcode, price, number_of_reviews, review_scores_rating, property_type, room_type, accommodates, square_feet, weekly_price and monthly_price columns.
   ~~~~python
   listings_file = "Resources/listings.csv"
   listings_df = pd.read_csv(listings_file, encoding="utf8")
   ~~~~

Detailed steps to clean and transform each .csv file:

1. Import Dependencies

•  Import Pandas  
•  from sqlalchemy import create_engine  
•  from sqlalchemy import inspect  

2. Create the path to the .csv file

3. Read the .csv file into a data frame

4. Create a copy with only the desired columns with .copy()

5. Delete rows with missing information using .dropna()

6. Delete all duplicates with .drop_duplicates() 

7. View the data frame to ensure successful cleaning

8. Ascertain data types of columns with .dtypes

9. Convert columns to usable data types 

•  Convert the date column to datetime with pd.to_datetime()  
•  Convert the string ‘price’ column to float using .astype(float)  
•  To convert the string ‘weekly_price’, ‘monthly_price’ and 'price' to numeric values, remove the currency signs with .replace() then convert to numeric using pd.to_numeric  
•  Convert  ‘accommodates’ and ‘square_feet’ with pd.to_numeric  

10. Replace the NaN values in calendar.csv using .fillna(‘$0’)

11. Filter the zipcode column with .str.len() == 5 to filter out invalid zipcodes not equal to 5 characters

12. Check the .csv data types have been successfully altered with .dtypes

## **Step 3: Load**

The process of loading data frames into pgAdmin4 is accomplished in Jupyter Notebooks. 

Establish connection to a local database.

Convert the data frames using .to_sql(). To confirm, query each data frame with pd.read_sql_query.head().

Perform SQL joins of the data frames on the listing_id column.
df = r””” SELECT df1.column_name, df2.column_name, df3.column_name, df4.column_name
FROM df1
JOIN df2 ON df1 = df2 
JOIN df3 ON df1 = df3 
JOIN df4 ON df1 = df4”””

Check the join is successful using pd.read_sql_query.head().

The engine uploads the SQL data.

The created SQL schema has four tables each focused on sub-categories of data:<br>
 •	'calendar'<br>
 •	'listings_host'<br>
 •	'listings_reviews'<br>
 •	'type_and_price'<br>
 
 Note: A postgresSQL protocol was employed to fulfill credentials requirements.

## Final Table
![AirBnb](Images/project.png)

The final database contains all of the cleaned and transformed columns. Utilizing SQL syntax in Jupyter Notebooks with the df = r”””code””” method or using pgAdmin4, the joined data frame is ready for querying. 
