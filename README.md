# VirtuousDataMigration


I worked on this assignment keeping Virtuous as a brand that helps non profits and analyzing data keeping donor related information that you receive from client on scheduled basis. <br>

Attached the SSIS solution (with images),SQL Queries, PowerBI solution is the dataset that I used to implement data analysis,data transformations and visualization <br>

Here are the instructions below <br>

# 1. Data Migration <br> 

I took the mock data set and migrated to three different tables into three tables Contacts , Contacts Methods , Gifts (**refer to the image 6.Populated Tables in SQL Server** ) <br>
<br>
1.I created an SSIS Solution that takes the source file and ingested data into destination tables in SQL Server destination. <br><br>
2.I  scheduled this solution in SQL Server Agent on scheduled basis (daily/monthly/weekly) basis depeding on how we receive data from client  (**refer to the image 5.DATA MIGRATION AUTOMATION IN SQL SERVER AGENT**) <br>
3. As per the analysis using SQL , I found out that there are lot of incosistencies in data and need to do a lot of back filling , merging , filtering of data required before interpreting it . <br>
4. Some examples of inconsistencies are  <br> **a.** Missing the type of Contact (household/company) <br> **b.** The requirement of first name and last name for all the donors <br> **c.** Missing donor contact information of those donors who are present in other tables like Gifts and Contacts <br> **d.** Same donor number for mutiple donors and cleaning htem if they are non existing in Other tables <br> **e.** Categorizing the variable depending on the amount received or donated , contact type <br> **e.** Concatenating first name and last name as donor name <br> **f.** Joining tables to create a single view  table after data cleaning and back filling <br> <br>





