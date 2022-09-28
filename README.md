# VirtuousDataMigration


I worked on this assignment keeping Virtuous as a brand that helps non profits and analyzing data keeping donor related information that you receive from client on scheduled basis. <br>

Attached the SSIS solution (with images),SQL Queries, PowerBI solution is the dataset that I used to implement data analysis,data transformations and visualization <br>

Here are the instructions below <br>

# 1. Data Migration <br> 

I took the mock data set and migrated to three different tables into three tables Contacts , Contacts Methods , Gifts (**refer to the image 6.Populated Tables in SQL Server** ) <br>
<br>
1.I created an SSIS Solution that takes the source file and ingested data into destination tables in SQL Server destination. <br><br>
2.I  scheduled this solution in SQL Server Agent on scheduled basis (daily/monthly/weekly) basis depeding on how we receive data from client  (**refer to the image 5.DATA MIGRATION AUTOMATION IN SQL SERVER AGENT**) <br>

# 2. Data Transformations <br> 
3. As per the analysis using SQL , I found out that there are lot of incosistencies in data and need to do a lot of back filling , merging , filtering of data required before interpreting it . <br>
4. Some examples of inconsistencies are  <br> **a.** Missing the type of Contact (household/company) <br> **b.** The requirement of first name and last name for all the donors <br> **c.** Missing donor contact information of those donors who are present in other tables like Gifts and Contacts <br> **d.** Same donor number for mutiple donors and cleaning htem if they are non existing in Other tables <br> **e.** Categorizing the variable depending on the amount received or donated , contact type <br> **e.** Concatenating first name and last name as donor name <br> **f.** Joining tables Contacts and Contact Details and then merging with the table Gifts to create a single view  table after data cleaning and back filling <br> <br>

**Solution <br>

I used Power BI to implement data transformations and data modeling .<br>
Some of the data modelling which I implemented on the aggreagted Contact View and Gifts table are as follows <br>

a. Created a calculated column and implemented a DAX function to create a Donor Name <br>
**Donor Name = CONCATENATE(CONCATENATE(Gifts[donors_first_name]," "),Gifts[donors_last_name]) **<br>

b. Implemented State Name using the State code provided in the table  <br>

**State Abbreivation = SWITCH(Gifts[State], "AL", "Alabama", "AK", "Alaska", "AZ", "Arizona", "AR", "Arkansas"
, "CA", "California", "CO", "Colorado", "CT", "Connecticut", "DE", "Delaware"
, "FL", "Florida", "GA", "Georgia","HI", "Hawaii", "ID", "Idaho", "IL", "Illinois", "IN", "Indiana", "IA", "Iowa", "KS", "Kansas"
, "KY", "Kentucky", "LA", "Louisiana", "ME", "Maine", "MD", "Maryland", "MA", "Massachusetts", "MI", "Michigan", "MN", "Minnesota"
, "MS", "Mississippi", "MO", "Missouri", "MT", "Montana", "NE", "Nebraska", "NV", "Nevada", "NH", "New Hampshire", "NJ", "New Jersey"
, "NM", "New Mexico", "NY", "New York", "NC", "North Carolina", "ND", "North Dakota", "OH", "Ohio", "OK", "Oklahoma", "PA", "Pennsylvania"
, "OR", "Oregon", "RI", "Rhode Island", "SC", "South Carolina", "SD", "South Dakota", "TN", "Tennessee", "UT", "Utah", "VT", "Vermont", "VA", "Virginia"
, "WA", "Washington", "WV", "West Virginia", "WI", "Wisconsin", "WY", "Wyoming","TX", "Texas","DC", "District of Columbia", "GU", "Guam", "PR", "Puerto Rico", "VI", "Virgin Islands","Unknown State" )** <br>

c. Implemented contact type using the below DAX functions 
**Contact Type = IF(Gifts[Contacts_View.Contact Type] = "Household" ,"Household", IF(Gifts[Contacts_View.Contact Type] = "Company", "Company","Unknown"))**<br>

d. Implemented Amount Received or donated based on Amount Received using below DAX Function <br>

**Received/Donated = IF(Gifts[amount_received] < 0 ,"Donated","Received") **<br>

###### *Note:: I implemented it in Power BI as I want to show it off in the visual format easily .However I initially implemented these transformations in SQL for initial analysis to check the validity of data available. <br><br>

**Example <br>**
The JOIN Function in SQL is equivalent to Merge in POWER BI <br>
The IN function in SQL is equivalent to Multifilter /Adavanced filterin in PowerBI <br>
Merging and backfilling the data can be implemented through CTE function and using CASE State ments <br>


# 3. Data Visualization <br> 

Implemented below tabs using PowerBI 

#### Existing Donor Details <br>

This tab in PowerBI display with the donor information and contact details. I also categorized these contact absed on the deceased donors  <br> <br>

![1  Visualize Existing Donor Details](https://user-images.githubusercontent.com/12963112/192724177-a34708b3-67fd-498f-8c8c-95b8351b60e4.png) <br>

##### Donor Gifts <br> 

This tab gives us the information by Total Gifts Received , Amount Received and Gift Ids . Also the bar chart for Total Gifts Received can be drill down to the Gifts <br>

##### Amount Received Trend by Donor <br>

This tab gives the total amount received by these donors over month .

##### Amount Gift per State <br>

This tab gives the amount per state and city and bar chart can be drill down through Donor Name 


