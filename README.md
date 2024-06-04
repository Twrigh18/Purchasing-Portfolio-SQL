# Purchasing-Portfolio-SQL

<img width="1202" alt="Requistions " src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/6e158e97-b661-415a-9e73-cdb13eb00bc9">


## Procurement Specialist Role
My role title is a Strategic Partnerships Procurement Specialist. My role is to assist departments with purchasing goods and services. I will answer department emails on purchasing related questions and either answer them or guide them to the right person and department. My main job is to process requisitions. Requisition means a request to order the goods or services from the department.
The Job of the purchasing department is to for departments to provide documentation that their purchase complies with the law and the purchasing manual. That is what a procurement method is, and we try to find a procurement method for a department’s purchase. If the departments provide the right documentation, we use a procurement method and then we generate POs for the supplier and have terms and conditions in which the supplier accepts. This role is basically purchasing compliance. There is a Construction and Sourcing team. Before the purchasing reorganization before fiscal year 2023 the teams within Purchasing were 
Goods/Services, Technology, Scientific, and Construction.

## Diving into the Purchasing Requisitions
I am going to talk about the number of requisitions and their amount that have been processed in the past from 2018 year by year going from all purchasing to strategic partnerships which is the team I am in, to specially myself by importing the CSV file into the SQL Database and answer some questions using queries
Note: It is encouraged to zoom into the screenshots

## Pulling and Cleaning the Data
I pulled a report from Workday called Find Requisitions. The result is all the requisition information from 6/1/2018 to 12/31/2023 is presented. That requisition information gets exported into excel in a Excel Worksheet format.
To import the requisition report into SQL, the file format must be in a CSV format. To import CSV files, there are some criteria that must be met in order for the CSV files to be imported to SQL Databases successfully

1.	A Column that uniquely identifies each row
2.	Column Names must have no spaces
3.	Date format must be in this format YYYY-MM-DD
4.	Data that contains numerical values must not have a comma
5.	The CSV file must be UTF-8 not CSV only.




Sample Requisition Report exported into Excel Worksheet Format from Workday below.

<img width="1035" alt="Sample of Original Report Pulled from Workday" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/ab7a081b-2a0b-4739-a27a-1ea38eeb1ee9">
 
The issues with the provided original Excel Worksheet File after I pulled a Requisition Report from Workday
1.	There is no single column that unique identifies each row
2.	Column Names have Spaces
3.	Date format is MM/DD/YYYY instead of YYYY-MM-DD
4.	Data that contain numerical values have a comma
5.	Duplicate Column for Requisition Number
6.	The report criteria and the date before and after and the dates are not needed basically anything above the top of the column names since there columns will be moved up
7.	The Excel File is in Excel Worksheet File format instead of CSV UTF-8 but do this last

## Cleaning the data
* For the no single column that unique identifies each row: I added a new column name called RequistionID. Since this is the column that uniquely identifies each row numbers can not repeat. I added 1 2 3 4 and tapped the lower right square and all the numbers populate all the way until the last number in the 400,000 range. This is used so the primary key can be added in the SQL Database
* For the Column Names have Spaces: I click on each of the column names and just remove the spaces
* For the Date format is MM/DD/YYYY instead of YYYY-MM-DD: I just highlighted the requisition date column and clicked on the number format and selected more number formats and selected custom and I typed YYYY-MM-DD
* For the data that contain numerical values that have commas: I highlighted the total amount column and clicked on the number format and selected general. This replaces the commas in the numerical values. A numeric data type will be used when the report gets imported into SQL
* For the Duplicate Column for Requisition Number: I deleted I highlighted the first column requisitions and selected delete and move to left. I then move the rest of the columns containing the data to the right to add the RequisitionID column.
* The report criteria and the date before and after and the dates: I highlighted the first five rows that contain those report criteria and the before and after dates and selected delete and those rows disappear.

After I did the data cleaning, I saved the Excel Worksheet File.
End Result of the Requisition Report in Excel after Data Cleaning in Excel Worksheet Format
 <img width="1056" alt="Sample of Original Report Pulled from Workday after cleaning" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/d59d5186-2cc2-4ee5-beae-505307d83d51">


The final step is to convert the Excel Worksheet into CSV UTF-8. I went and saved the Excel Worksheet as CSV UTF-8. I recommend after the file is converted is to leave it alone. I did not use the CSV only because there will be issues with successfully importing the csv file. If you need to make changes, do the changes before convert the excel file to any type of CSV format
End Result of the Requisition Report as a CSV UTF-8 File
<img width="982" alt="Sample of Original Report Pulled from Workday after cleaning and coverted to CSV UTF 8" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/838a7c9f-427c-4de1-b175-64dbf52ce891">
 
This file will be used to import into the SQL Database

## Importing the data
SQL Lite is being used for this report. This is what SQLite looks like when it is opened.
<img width="956" alt="SQLlite Front Page" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/170907e0-2d4f-4a54-9045-7774d0d9419d">
 
I created a new database. It is an SQL File. I named it Reqs and saved it somewhere safe where I can access in on my computer. Example I choose the documents and new folder and saved my database file as an SQLite Database File.
<img width="588" alt="New Database File Save" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/e5a385f8-743f-4d77-bd1d-508e2990d7e6">


After I saved the file. The edit table definition pops up. I copied the column names in exact order the same way as it shows up in the CSV UTF 8 File. I named the table Requisitions. I added a primary key and created certain data types that can help with right data being sorted when I start querying. 
<img width="526" alt="Edit Table with Data Types Needed" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/ffb0f9d5-a25e-48ea-8b76-c746257650a0">

End Result of the Requisition Table after being created
 
Now it is time to import. I went to the file tab in SQLite and selected import and Table from CSV file will appear so that will be selected.
<img width="873" alt="File Import option for CSV" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/8dc09b36-bfdd-4e74-9b71-343186bff8b8">
 
The Import CSV file option pops up. I just changed the table name to requisitions the same as originally created. I left everything alone
<img width="1078" alt="Import CSV File Page after selected import CSV from table" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/9f8b8b6f-988a-4d14-b0ea-46ffbe7f768c">
 
Then I selected the requisitions CSV UTF-8 File that I have saved somewhere. A warning pops there is already at table name. Click yes to all. This will ensure a successful import. The data is now successfully imported in less than 5 seconds.
Final Step is to test the query. I used the SELECT * FROM Requisitions; command. It was a success.

 <img width="1621" alt="First Query Testing" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/80fa6b86-c095-4cd5-8c41-c875ea6773a0">


This was the hardest part of learning SQL. I googled a lot. But I am happy that I was able to pull this off. Once done this process is very rewarding and made me become better at creating and understanding SQL and other databases in general.


## Querying
I will be using queries to answer questions. I have created some questions and will answer questions using queries.

## What is the Total Number of Requisitions Overall ? 
<img width="914" alt="Requisitions were processed overall since 2018 " src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/acd60545-7741-4800-9114-0ae196d9eb1e">

In the entire purchasing department, 436971 requisitions have been created since 2018. That is a lot of requisitions.

## What is the Total Amounts of All Requisitions Overall?
<img width="946" alt="Total amount of all the requisitions that were processed " src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/0ac38ed0-d184-4ee1-a544-6c9cd3ec3e5b">

 
The amount from all the requisitions adds up to a total of $4,219,119,102.87. So, all departments at ASU spent a total of around 4 billion dollars since the start of fiscal year 2018.
## How Many Requisitions Were Processed Under $25,000 ?
<img width="1145" alt="Total Number of all Requisitions under $25,000 " src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/b957d8a6-c014-4bda-b5ff-da7db745a189">

 
All Departments submitted 421,945 requisitions that were under $25,000. These requisitions are easy in that they need less documentation so these can be processed very quickly. These take up most of the requisitions overall.
## What is The Total Amount of All Requisitions Under $25,000 ?
<img width="802" alt="Total Amount of All Requisitions under $25,000" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/160911f7-8809-4f7e-aae6-5198af806eea">

 
Departments spent around $638,388,640.23 on orders that are under $25,000.
## How Many Requisitions were Processed Over $25,000 ?
<img width="1184" alt="Total Number of all Requisitions over $25,000 " src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/585e00be-ee23-4dd0-930a-d4c5ee20f32c">

 
All Departments submitted 15,026 requisitions that were over $25,000. Do not let the small number fool you. These orders require more documentation, so these require us to wait for the department to reach back out for the required documentation. These even take longer if the requisitions use federal funding. These take longer to do.
## What Is the Total Amount of All Requisitions Over $25,000 ?
 <img width="803" alt="Total Amount of All Requisitions over $25,000" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/2bba05f4-3985-4b81-bcd8-1e5db309005a">

Departments spent around $3,580,730,462.64 on orders that are over $25,000.


## How Many Requisitions were Processed between $25,000 and $100,000 ?
 <img width="1166" alt="Total Amount of All Requisitions bwt" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/95cceeab-d3e6-4234-ae05-9a0f61ee2ebd">

All Departments submitted 10902 requisitions that were between $25,000 and $100,000. Strategic Partnerships always process these orders, and these are orders that we should always learn and get better at these. They require more documentation and waiting so these most of the time cannot be processed right away so there is a lot of waiting. These are the types of requisitions Strategic Partnerships always prioritizes. MRO teams sometimes do these amounts. The sourcing team never do this amount since they are over $100,000 and rarely construction team process these requisitions.

## How Many Requisitions were Processed Over $100,000 ?
<img width="1172" alt="Total Number of all Requisitions over $100,000" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/e18d2920-c7fa-4920-a641-3fe83957782f">
 
All Departments submitted 4,194 requisitions that were over $100,000. These requisitions require suppliers that have formal solicitations or have a sole source. Departments really have to check if an order is going to go over $100,000

## What Is the Total Amount of All Requisitions Over $100,000 ?
<img width="790" alt="Total Amount of All Requisitions over $100,000" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/2d39745a-535d-418d-8be8-fcb0b764a266">

 
Departments spent around $3,045,686,758.52 on orders that are over $100,000.

## How Many Requisitions were Processed Over $1,000,000 ?
 <img width="1167" alt="Total Number of all Requisitions over $1,000,000 " src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/570a5d30-63be-4a1d-807d-8d57f2976e87">

All Departments submitted 379 requisitions that were over $1,000,000. These are treated as requisitions over $100,000. This is a lot of many so purchasing must be careful and not make any mistakes on these purchases.

## What Is the Total Amount of All Requisitions Over $1,000,000 ?
<img width="788" alt="Total Amount of All Requisitions over $1,000,000" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/8e127586-8ef0-48fa-a323-f73c472a451b">
 
Departments spent around $2,031,538,576.88 on orders that are over $1,000,000.
## What is the Requisition Lowest Amount ?
<img width="934" alt="Requisition Lowest Amount" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/43fd4497-c769-434d-8668-b2d05fc06ad1">
 
The lowest amount on a requisition is -11.96 or around -$12 dollars. This means that the requisition had so many discounts to the point where the supplier gave back the department 12 dollars.
## What Kind of Requisition Is the Lowest Amount ?
<img width="934" alt="Requisition Lowest Amount" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/79eddcf6-c3ea-4ed2-96c6-5f98c6cb4091">

 
This is a pay an invoice requisition. From pulling this up in Workday. This requisition is textbook purchases for student athletes each team like Football Basketball Baseball etc. for SDA. There were around 13 discounts out of 21 different teams that had textbook purchases for student athletes that made the total on the requisition around -12 dollars. Note this is the only requisition with a negative amount.
## What Is the Requisition Highest Amount ?
 <img width="913" alt="Requisition Highest Amount" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/5a46b729-13c2-473d-9118-3a582db3a5d2">

The highest amount on a requisition is $139,066,673. That is a lot of money for a purchase. I am guessing this is a construction purchase
## What Kind of Requisition Is the Highest Amount ?
 <img width="1033" alt="Requisition Highest Amount Type" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/2f58c261-4049-4ed4-9ad6-8adce9ce973b">

This requisition is for construction services for the new building lab called Interdisciplinary Science and Technology Building (ISTB 12) at the Polytechnic campus. There is probably lots of fancy lab equipment that needs to be installed. Anything with science orders is more expensive.
## What is the Average Total Amount of Requisitions Overall ?
 <img width="699" alt="Average Total Amount Of All Requisitions Overall" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/001379b4-dde4-417f-9a94-b93a76ea4901">

Is around $9655.38. This proves most requisitions are low dollar.
## How Many Requisitions and Their Total Amounts Used the Requisition Type of Goods and Services ?
<img width="1177" alt="Total Number of Requisitions that used Goods and Services" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/dd86c0f3-8a80-470a-9e02-63951c83033e">
 
Departments have submitted around 309,641 requisitions totaling around $2,137,782,764.41 that uses the requisition type of Goods and Services. This is an important requisition type. This requisition type generates a purchase order after a requisition gets approved to go to supplier as a contract and the supplier automatically accepts ASU terms and conditions. When a supplier disagrees with some or all of the ASU terms and conditions in the PO, the supplier will create a contracts with their terms and conditions and purchasing will sign off adding ASU terms and conditions and if the supplier still disagrees, the contracts team will specialize in negotiations of the contracts. The purchase order protects ASU and departments if the orders or services go wrong. The total amount for each requisition type is from a query that is coming up.

## How Many Requisitions and Their Total Amounts Used the Requisition Type of Technology ?
<img width="1178" alt="Total Number of Requisitions that used Technology" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/7f876368-d5a5-4d7c-8d3d-4d04d3930561">
 
Departments have submitted around 30,087 requisitions totaling around $593,431,625.50 that uses the requisition type of Technology. Technology operates the same way as using Goods and Services. What makes this requisition type different is that these require security review so these will be provided in requisition before or after approval but are provided before the orders need payment. Pay an invoice of technology purchases has a security review alert so the orders get counted under the requisition type of Pay an Invoice. Sometimes these orders will have suppliers wanting subscription agreements signed so the purchasing department must be very careful with what they agree to because their amounts are more, they have terms for 1 to the max of 5 years and many more supplier terms and conditions. Subscription contracts are the contracts that purchasing must be the most careful on.

## How Many Requisitions and Their Total Amounts Used the Requisition Type of Pay an Invoice ?
 <img width="1097" alt="Total Number of Requisitions that used Pay an Invoice" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/d3990f65-b093-4ac6-b370-0a30b1ccbfe9">

Departments have submitted around 58,498 requisitions totaling around $353,743,777.07 that uses the requisition type of Pay an Invoice. Pay in Invoice is used when a service is done after the fact and the services needed to get paid. In the past, there were many departments that would skip over to using Pay an Invoice used of using Goods and Services generating a PO. This is an issue because if the supplier has any issues, they can point to the PO, but if the PO is not there, then that is on the department. We always want departments for us to generate the PO before creating  a requisition to pay an invoice.

## How Many Requisitions and Their Total Amounts Used Many Requisition Types Instead of the Ones Mentioned Above ?
<img width="1182" alt="Total Number of Requisitions that used other Requsition Type" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/9d74f749-7350-4e81-9845-3dab73337895">
 
Departments have submitted around 38,745 requisitions totaling around $1,134,160,935.89 that uses the requisition types other than Goods and Services, Pay an Invoice, and technology. Construction and MRO team are the ones that use the other requisition types. My team in strategic partnerships will rarely use the Chemical requisition type and those get routed to materials management after approval. The department chooses a requisition type based on the purchases and that requisition will route to a purchasing team based on the requisition type. Departments should always reach out to purchasing if they are not too sure if the requisition type is the right one.
## How Many Requisitions Used the Requisition Type of Pay an Invoice with the Requestors That Start With the Letter J ? 
<img width="1103" alt="Number of reqs that used the requisition type of Pay an Invoice with the requestors that start with the letter J," src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/746c98bd-0077-4e4e-961e-967f4aedeae5">
 
There were 5019 Requisitions were processed answering this question

## How Many Requisitions Used the Requisition Type of Goods and Services with the Requestors That Start with the letter L and the Requisition Amounts That Are Over $25,000 ?
<img width="1108" alt="Number of reqs that used the requisition type of Goods and Services with the requestors that start with L and the requisition amounts that are over $25,000" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/2cdaf561-08cd-461b-b921-a49dd2aaf46e">
 
There were 697 Requisitions were processed answering this question
## How Many Requisitions Used the Requisition Type of Technology with the Requestors That Start with the Letters T, S, C, or P and the Requisition Amounts That Are Over $25,000 ? 
<img width="1180" alt="Number of reqs that used the longest question" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/b606dca5-00ac-4173-8fb8-a3f607c72804">

There were 72019 Requisitions that were processed answering this question

## What are the Different Types of Requisition Types Being Used ?
 
<img width="524" alt="How many different types of Requisition Types being used" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/407a5d02-9d9f-4474-ad01-0b2205131b76">
There are 17 different types of Requisition type is displayed in a table

## What are the Top 17 Requisition Types by Count from Largest to Smallest with Their Total Amounts Included not in Order ?
<img width="966" alt="Different Req types total number of reqs and amount with number in descending order" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/33f90790-dd8f-47d5-a84c-5bc7c369736d">
 
The results match some of the questions of finding how many requisitions were processed using different Requisition Types. The Top 3 Requisition Types by count are Goods and Services, Pay an Invoice, and Technology. My team strategic partnerships and the sourcing team deals with these requisition types the most on a daily basis. MRO team deals with non-stock facilities and inventory replenishment. Chemical and Specialty Gas goes to materials management. Construction team deals with the rest and those require different documentations and requirements based on the purchase

## What are the Top 17 Requisition Type Total Amounts from Largest to Smallest with Their Total Number of Requisitions Included not in Order ?
<img width="914" alt="Different Req types total number of reqs and amount with amount in descending order" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/ca4e2b82-1e9f-4007-a18d-15aaac047697">
 
Goods and Services is on the top since this a requisition type department should always use to generate PO before using Pay in Invoice to pay for the purchase. Many requisition types start appearing near the top that deal with construction due to the nature of their purchases. These purchases absolutely need a Purchase Order generated in order to protect the departments especially with how expensive these purchases order.

## What are the Top Requestors by the Total Number of Requisitions Submitted using HAVING clause?
<img width="580" alt="Top Number of Requestors and the number of requstions they submitted" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/ae6803d0-2fc5-48e4-94ce-c749a590bda5">
 
There are 4875 Different Requesters purchasing dealt with since 2018. They represent different departments across ASU such as SDA, President’s Office, Ira Fulton, WP Carey, Mary Lou, CPMG, Materials Management and many more. The top one works in Materials Management. It is some materials management, but the rest are a variety of departments. Purchasing knows these names by repetition since their titles do not appear in Workday. We must search for their emails personally. It is cool to see what type of order different departments do.

## What is the Total Number of Requisitions per year since 2018 ?
<img width="777" alt="Total Number of all Requisitions per year since 2018" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/e1443796-1286-4c3f-9794-863157e77981">
 
* 2018 – 41652 Requisitions
* 2019 – 85793 Requisitions
* 2020 – 66905 Requisitions
* 2021 – 74310 Requisitions
* 2022 – 82086 Requisitions
* 2023 – 86227 Requisitions

There is a trend with the number of requisitions processes yearly. 2018 is when Workday was first implemented so the number of requisitions is the lowest for that reason. 2019 is the year where the requisitions were processed the most pre pandemic. There were a lot of students enrolled so departments have the funding to spend their money. Purchasing was busy during that year. 2020 is where everything changed. 2020 has the lowest number of requisitions processed. The reason for that huge decline from 2019 is that the pandemic had occurred. ASU had to basically go online, and the university was almost shut down in many ways. Campus was very empty. Because there were not as many students on campus, departments did not really spend as much of their money. As the pandemic started to subside, there number of requisitions started to increase every single year. 2023 has the most requisitions processed. This is the year where the university felt normal before the pandemic.

## What is the Total Amount of all Requisitions per year since 2018 ?
<img width="791" alt="Total Amount of all Requisitions per year since 2018" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/f5d1ea91-710a-4329-8816-8108f091ab00">
 
* 2018 – $348,200,512.82 All Departments spent around 348 million dollars this year in 2018.
* 2019 – $727,505,051.34 All Departments spent around 727 million dollars this year in 2019.
* 2020 – $579,614,994.83 All Departments spent around 580 million dollars this year in 2020.
* 2021 – $674,275,522.28 All Departments spent around 674 million dollars this year in 2021.
* 2022 – $840,200,614.57 All Departments spent around 840 million dollars this year in 2022.
* 2023 – $1,049,170,380.03 All Departments spent around 1 billion dollars this year in 2023.

The trend is just the same as the number of requisitions departments submitted and processed. Department spends lots of money until the pandemic hits in 2020 where ASU is kind of shut down. As the pandemic ends, the spending slowly increases and now in 2023, All departments spend over 1 billion dollars on anything for ASU. I predict all departments will spend even more money in the future.
Conclusion
Since there is no pandemic now, I believe ASU will increase the enrollment. More enrollment means more tuition means more money, meaning departments must purchase things that will go to the purchasing team that will keep us busy. I predict that more requisitions will be processed in 2024 than this year 2023. I believe there will be more Purchase Orders issued in 2024 than 2023. I also believe that departments will spend even more money on Goods/Services, Scientific, Technology, and Construction purchases. I predict every year purchases will increase but more slowly in the long run.

# The Requstions I did since starting at ASU in 2022

## What is the Total Amounts of All Requisitions I did Overall?
SELECT 
 round(SUM(TotalAmount),2)
FROM
 Requisitions
WHERE
 SourcingBuyer = 'Timothy Wright';

 31327779.83
## How Many Requisitions I did that Were Processed Under $25,000 ?
SELECT
 *
FROM
 Requisitions
WHERE
 TotalAmount < '25000.99' AND SourcingBuyer = 'Timothy Wright';
5847
## What is The Total Amount of All Requisitions I did Under $25,000 ?

## How Many Requisitions I did  that were Processed Over $25,000 ?
SELECT
 *
FROM
 Requisitions
WHERE
 TotalAmount > '25001' AND SourcingBuyer = 'Timothy Wright';

290
## What Is the Total Amount of All Requisitions I did Over $25,000 ?


## How Many Requisitions I did  that were Processed Over $100,000 ?
SELECT
 *
FROM
 Requisitions
WHERE
 TotalAmount > '100000' AND SourcingBuyer = 'Timothy Wright';

 0
## What Is the Total Amount of All Requisitions I did Over $100,000 ?

## What is the Requisition Lowest Amount I did?
SELECT
 MIN(TotalAmount) AS [Requisition Lowest Amount]
FROM
 Requisitions
WHERE
 SourcingBuyer = 'Timothy Wright';

zero dollars

## What Is the Requisition Highest Amount I did?
SELECT
 MAX(TotalAmount) AS [Requisition Highest Amount]
FROM
 Requisitions
WHERE
 SourcingBuyer = 'Timothy Wright';
 
99934.84

## What is the Average Total Amount of Requisitions Overall I did ?
SELECT 
 round(AVG(TotalAmount),2) AS [Average Total Amount of Requisitions]
FROM
 Requisitions
WHERE
 SourcingBuyer = 'Timothy Wright';

5104.74
## How Many Requisitions and Their Total Amounts I did Used the Requisition Type of Goods and Services ?
SELECT
 *
FROM
 Requisitions
WHERE
 RequisitionType = '1.Goods and Services' AND SourcingBuyer = 'Timothy Wright';
892
## How Many Requisitions and Their Total Amounts I did Used the Requisition Type of Technology ?
SELECT
 *
FROM
 Requisitions
WHERE
 RequisitionType = 'Technology' AND SourcingBuyer = 'Timothy Wright';
170
## How Many Requisitions and Their Total Amounts I did Used the Requisition Type of Pay an Invoice ?
SELECT
 *
FROM
 Requisitions
WHERE
 RequisitionType = 'Pay an Invoice' AND SourcingBuyer = 'Timothy Wright';
5011
## How Many Requisitions and Their Total Amounts I did Used Many Requisition Types Instead of the Ones Mentioned Above ?
SELECT
 *
FROM
 Requisitions
WHERE
 RequisitionType 
 NOT IN ('1.Goods and Services', 'Technology', 'Pay an Invoice') 
 AND SourcingBuyer = 'Timothy Wright';
64

## What is the Total Number of Requisitions I did per year since I started at ASU ?
SELECT 
 STRFTIME('%Y', RequisitionDate) AS Year, COUNT(*) as [Total Number of Requisitions]
FROM 
 Requisitions
WHERE SourcingBuyer = 'Timothy Wright'
GROUP BY 
 STRFTIME('%Y', RequisitionDate);

2022- 2069 2023 4068
## What is the Total Amount of all Requisitions I did per year  since I started at ASU ?
SELECT 
 STRFTIME('%Y', RequisitionDate) AS Year, 
 round(SUM(TotalAmount),2) as [Total Requisitions Amount]
FROM 
 Requisitions
WHERE SourcingBuyer = 'Timothy Wright'
GROUP BY 
 STRFTIME('%Y', RequisitionDate);
2022 - 5660838.79   2023 - 25666941.04

# Conclusion
