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
* **For the no single column that unique identifies each row:** I added a new column name called RequistionID. Since this is the column that uniquely identifies each row numbers can not repeat. I added 1 2 3 4 and tapped the lower right square and all the numbers populate all the way until the last number in the 400,000 range. This is used so the primary key can be added in the SQL Database
* **For the Column Names have Spaces:** I click on each of the column names and just remove the spaces
* **For the Date format is MM/DD/YYYY** instead of YYYY-MM-DD: I just highlighted the requisition date column and clicked on the number format and selected more number formats and selected custom and I typed YYYY-MM-DD
* **For the data that contain numerical values that have commas:** I highlighted the total amount column and clicked on the number format and selected general. This replaces the commas in the numerical values. A numeric data type will be used when the report gets imported into SQL
* **For the Duplicate Column for Requisition Number:** I deleted I highlighted the first column requisitions and selected delete and move to left. I then move the rest of the columns containing the data to the right to add the RequisitionID column.
* **The report criteria and the date before and after and the dates:** I highlighted the first five rows that contain those report criteria and the before and after dates and selected delete and those rows disappear.

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

This was the hardest part of learning SQL. I googled and used AI like ChatGPT a lot. But I am happy that I was able to pull this off. Once done this process is very rewarding and made me become better at creating and understanding SQL and other databases in general.

# Querying
I will be using queries to answer questions. I have created some questions and will answer questions using queries.

## What is the Total Number of Requisitions Overall ? 
<img width="572" alt="Total Number of all Requisitions  since 2018" src="https://github.com/user-attachments/assets/5a9a591c-f024-45e7-b844-d5af24c68397">


In the entire purchasing department, **436971** requisitions have been created since 2018. That is a lot of requisitions.

## What is the Total Amounts of All Requisitions Overall?
<img width="567" alt="Total Amount of all Requisitions since 2018" src="https://github.com/user-attachments/assets/92cf7161-41b7-4126-bf0a-a08719a5149d">


The amount from all the requisitions adds up to a total of **$4,219,119,102.87**. So, all departments at ASU spent a total of around 4 billion dollars since the start of fiscal year 2018.

## How Many Requisitions Were Processed Under $25,000 ?
<img width="1140" alt="Total Number of all Requisitions under $25,000" src="https://github.com/user-attachments/assets/fa0a5ecd-ee78-4f70-a776-42303413b446">


All Departments submitted **421,945** requisitions that were under $25,000. These requisitions are easy in that they need less documentation so these can be processed very quickly. These take up most of the requisitions overall.

## What is The Total Amount of All Requisitions Under $25,000 ?
<img width="668" alt="Total Amount of all Requisitions under $25,000" src="https://github.com/user-attachments/assets/8f3c2be5-c68a-4309-a4ee-9ec49b215b56">


Departments spent around **$638,388,640.23** on orders that are under $25,000.

## How Many Requisitions were Processed Over $25,000 ?
<img width="1175" alt="Total Number of all requisitions over $25,000" src="https://github.com/user-attachments/assets/e304b72f-feec-4c5d-aa4e-5f536bd09760">


All Departments submitted **15,026** requisitions that were over $25,000. Do not let the small number fool you. These orders require more documentation, so these require us to wait for the department to reach back out for the required documentation. These even take longer if the requisitions use federal funding. These take longer to do.

## What Is the Total Amount of All Requisitions Over $25,000 ?
<img width="667" alt="Total Amount of all Requisitions over $25,000" src="https://github.com/user-attachments/assets/73228f37-fb3e-497e-9a26-8d6d5c9d76a4">


Departments spent around **$3,580,730,462.64** on orders that are over $25,000.

## How Many Requisitions were Processed between $25,000 and $100,000 ?


All Departments submitted **10902** requisitions that were between $25,000 and $100,000. Strategic Partnerships always process these orders, and these are orders that we should always learn and get better at these. They require more documentation and waiting so these most of the time cannot be processed right away so there is a lot of waiting. These are the types of requisitions Strategic Partnerships always prioritizes. MRO teams sometimes do these amounts. The sourcing team never do this amount since they are over $100,000 and rarely construction team process these requisitions.

## How Many Requisitions were Processed Over $100,000 ?
<img width="1178" alt="Total Number of all requisitions over $100,000" src="https://github.com/user-attachments/assets/b104914a-86b6-42cd-bb26-1a42cba273bb">

 
All Departments submitted **4,194** requisitions that were over $100,000. These requisitions require suppliers that have formal solicitations or have a sole source. Departments really have to check if an order is going to go over $100,000

## What Is the Total Amount of All Requisitions Over $100,000 ?
<img width="667" alt="Total Amount of all Requisitions over $100,000" src="https://github.com/user-attachments/assets/a2c2719c-8cdc-468f-84bf-41065cfcb08a">


Departments spent around **$3,045,686,758.52** on orders that are over $100,000.

## How Many Requisitions were Processed Over $1,000,000 ?
<img width="1172" alt="Total Number of all requisitions over $1,000,000" src="https://github.com/user-attachments/assets/a6cc765b-849a-4368-9c15-01dde76cbf89">


All Departments submitted **379** requisitions that were over $1,000,000. These are treated as requisitions over $100,000. This is a lot of many so purchasing must be careful and not make any mistakes on these purchases.

## What Is the Total Amount of All Requisitions Over $1,000,000 ?
<img width="775" alt="Total Amount of all Requisitions over $1,000,000" src="https://github.com/user-attachments/assets/6e2eb8f6-29a9-40ea-9a1c-8a8a5b72a448">

 
Departments spent around **$2,031,538,576.88** on orders that are over $1,000,000.

## What is the Requisition Lowest Amount ?
<img width="934" alt="Requisition Lowest Amount" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/43fd4497-c769-434d-8668-b2d05fc06ad1">
 
The lowest amount on a requisition is **-11.96** or around **-$12 dollars**. This means that the requisition had so many discounts to the point where the supplier gave back the department 12 dollars.

## What Kind of Requisition Is the Lowest Amount ?

<img width="983" alt="Requisition Lowest Amount Type" src="https://github.com/user-attachments/assets/5e18bc31-5281-4bc4-be39-0923e4c6c95b">

This is a pay an invoice requisition. From pulling this up in Workday. This requisition is textbook purchases for student athletes each team like Football Basketball Baseball etc. for SDA. There were around 13 discounts out of 21 different teams that had textbook purchases for student athletes that made the total on the requisition around -12 dollars. Note this is the only requisition with a negative amount.

## What Is the Requisition Highest Amount ?
<img width="913" alt="Requisition Highest Amount" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/5a46b729-13c2-473d-9118-3a582db3a5d2">

The highest amount on a requisition is **$139,066,673**. That is a lot of money for a purchase. I am guessing this is a construction purchase

## What Kind of Requisition Is the Highest Amount ?
<img width="1033" alt="Requisition Highest Amount Type" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/2f58c261-4049-4ed4-9ad6-8adce9ce973b">

This requisition is for construction services for the new building lab called Interdisciplinary Science and Technology Building (ISTB 12) at the Polytechnic campus. There is probably lots of fancy lab equipment that needs to be installed. Anything with science orders is more expensive.

## What is the Average Total Amount of Requisitions Overall ?
<img width="672" alt="Average Total Amount of Requisitions Overall " src="https://github.com/user-attachments/assets/5dc020d4-84fb-4a8f-8947-4df1a8c320d7">


Is around **$9655.38**. This proves most requisitions are low dollar.

## How Many Requisitions and Their Total Amounts Used the Requisition Type of Goods and Services ?
<img width="1168" alt="Total Number of Requisitions that used Goods and Services" src="https://github.com/user-attachments/assets/7254216a-4b85-4bf0-b949-abbcc71af29d">

 
Departments have submitted around **309,641** requisitions totaling around $2,137,782,764.41 that uses the requisition type of Goods and Services. This is an important requisition type. This requisition type generates a purchase order after a requisition gets approved to go to supplier as a contract and the supplier automatically accepts ASU terms and conditions. When a supplier disagrees with some or all of the ASU terms and conditions in the PO, the supplier will create a contracts with their terms and conditions and purchasing will sign off adding ASU terms and conditions and if the supplier still disagrees, the contracts team will specialize in negotiations of the contracts. The purchase order protects ASU and departments if the orders or services go wrong. The total amount for each requisition type is from a query that is coming up.

## How Many Requisitions and Their Total Amounts Used the Requisition Type of Technology ?
<img width="1166" alt="Total Number of Requisitions that used Technology" src="https://github.com/user-attachments/assets/3cec89ae-0913-4f62-9b90-42e64df273e7">


 
Departments have submitted around **30,087** requisitions totaling around $593,431,625.50 that uses the requisition type of Technology. Technology operates the same way as using Goods and Services. What makes this requisition type different is that these require security review so these will be provided in requisition before or after approval but are provided before the orders need payment. Pay an invoice of technology purchases has a security review alert so the orders get counted under the requisition type of Pay an Invoice. Sometimes these orders will have suppliers wanting subscription agreements signed so the purchasing department must be very careful with what they agree to because their amounts are more, they have terms for 1 to the max of 5 years and many more supplier terms and conditions. Subscription contracts are the contracts that purchasing must be the most careful on.

## How Many Requisitions and Their Total Amounts Used the Requisition Type of Pay an Invoice ?
<img width="1113" alt="Total Number of Requisitions that used Pay an Invoice" src="https://github.com/user-attachments/assets/7bb09816-f730-40fb-ac6f-117c575b4152">


Departments have submitted around **58,498** requisitions totaling around $353,743,777.07 that uses the requisition type of Pay an Invoice. Pay in Invoice is used when a service is done after the fact and the services needed to get paid. In the past, there were many departments that would skip over to using Pay an Invoice used of using Goods and Services generating a PO. This is an issue because if the supplier has any issues, they can point to the PO, but if the PO is not there, then that is on the department. We always want departments for us to generate the PO before creating  a requisition to pay an invoice.

## How Many Requisitions and Their Total Amounts Used Many Requisition Types Instead of the Ones Mentioned Above ?
<img width="1178" alt="Total Number of Requisitions that used other Requsition Type" src="https://github.com/user-attachments/assets/302fc3c5-3faf-4252-a46a-2d9c305f1905">

 
Departments have submitted around **38,745** requisitions totaling around $1,134,160,935.89 that uses the requisition types other than Goods and Services, Pay an Invoice, and technology. Construction and MRO team are the ones that use the other requisition types. My team in strategic partnerships will rarely use the Chemical requisition type and those get routed to materials management after approval. The department chooses a requisition type based on the purchases and that requisition will route to a purchasing team based on the requisition type. Departments should always reach out to purchasing if they are not too sure if the requisition type is the right one.

## How Many Requisitions Used the Requisition Type of Pay an Invoice with the Requestors That Start With the Letter J ? 
<img width="1111" alt="Total Number of requisitions used the requisition type of Pay an Invoice with the requestors that start with the letter J" src="https://github.com/user-attachments/assets/cf7d1df7-c5a9-4cdc-8825-294c31048605">

 
There were **5019** Requisitions were processed answering this question

## How Many Requisitions Used the Requisition Type of Goods and Services with the Requestors That Start with the letter L and the Requisition Amounts That Are Over $25,000 ?
<img width="1118" alt="Total number of requisitions used the requisition type of Goods and Services with the requestors that start with L and the  requisition amounts that are over $25,000" src="https://github.com/user-attachments/assets/a1b0ead6-b1a0-4f07-b72f-66f43d42deab">

 
There were **697** Requisitions were processed answering this question

## How Many Requisitions Used the Requisition Type of Technology with the Requestors That Start with the Letters T, S, C, or P and the Requisition Amounts That Are Over $25,000 ? 
<img width="1169" alt="TO9A39~1" src="https://github.com/user-attachments/assets/91bca2cb-620b-4481-a629-0d10207297a6">


There were **72019** Requisitions that were processed answering this question

## What are the Different Types of Requisition Types Being Used ?
<img width="524" alt="How many different types of Requisition Types being used" src="https://github.com/user-attachments/assets/f09b3f7f-73ac-48dd-8e3d-2e85506c4c78">


There are **17** different types of Requisition type is displayed in a table

## What are the Top 17 Requisition Types by Count from Largest to Smallest with Their Total Amounts Included not in Order ?

 
The results match some of the questions of finding how many requisitions were processed using different Requisition Types. The Top 3 Requisition Types by count are Goods and Services, Pay an Invoice, and Technology. My team strategic partnerships and the sourcing team deals with these requisition types the most on a daily basis. MRO team deals with non-stock facilities and inventory replenishment. Chemical and Specialty Gas goes to materials management. Construction team deals with the rest and those require different documentations and requirements based on the purchase

## What are the Top 17 Requisition Type Total Amounts from Largest to Smallest with Their Total Number of Requisitions Included not in Order ?

 
Goods and Services is on the top since this a requisition type department should always use to generate PO before using Pay in Invoice to pay for the purchase. Many requisition types start appearing near the top that deal with construction due to the nature of their purchases. These purchases absolutely need a Purchase Order generated in order to protect the departments especially with how expensive these purchases order.

## What are the Top Requestors by the Total Number of Requisitions Submitted using HAVING clause?

 
There are **4875** different Requesters purchasing dealt with since 2018. They represent different departments across ASU such as SDA, President’s Office, Ira Fulton, WP Carey, Mary Lou, CPMG, Materials Management and many more. The top one works in Materials Management. It is some materials management, but the rest are a variety of departments. Purchasing knows these names by repetition since their titles do not appear in Workday. We must search for their emails personally. It is cool to see what type of order different departments do.

## What is the Total Number of Requisitions per year since 2018 ?
<img width="788" alt="Total Number of all Requisitions per year since 2018" src="https://github.com/user-attachments/assets/598dadae-7bad-42a9-aaa7-0603fcc6eab3">

 
* 2018 – 41652 Requisitions
* 2019 – 85793 Requisitions
* 2020 – 66905 Requisitions
* 2021 – 74310 Requisitions
* 2022 – 82086 Requisitions
* 2023 – 86227 Requisitions

There is a trend with the number of requisitions processes yearly. 2018 is when Workday was first implemented so the number of requisitions is the lowest for that reason. 2019 is the year where the requisitions were processed the most pre pandemic. There were a lot of students enrolled so departments have the funding to spend their money. Purchasing was busy during that year. 2020 is where everything changed. 2020 has the lowest number of requisitions processed. The reason for that huge decline from 2019 is that the pandemic had occurred. ASU had to basically go online, and the university was almost shut down in many ways. Campus was very empty. Because there were not as many students on campus, departments did not really spend as much of their money. As the pandemic started to subside, there number of requisitions started to increase every single year. 2023 has the most requisitions processed. This is the year where the university felt normal before the pandemic.

## What is the Total Amount of all Requisitions per year since 2018 ?
<img width="662" alt="Total Amount of all Requisitions per year since 2018" src="https://github.com/user-attachments/assets/2715378b-6334-47a0-af28-d5a78b13cbc0">

 
* 2018 – $348,200,512.82 All Departments spent around 348 million dollars this year in 2018.
* 2019 – $727,505,051.34 All Departments spent around 727 million dollars this year in 2019.
* 2020 – $579,614,994.83 All Departments spent around 580 million dollars this year in 2020.
* 2021 – $674,275,522.28 All Departments spent around 674 million dollars this year in 2021.
* 2022 – $840,200,614.57 All Departments spent around 840 million dollars this year in 2022.
* 2023 – $1,049,170,380.03 All Departments spent around 1 billion dollars this year in 2023.

The trend is just the same as the number of requisitions departments submitted and processed. Department spends lots of money until the pandemic hits in 2020 where ASU is kind of shut down. As the pandemic ends, the spending slowly increases and now in 2023, All departments spend over 1 billion dollars on anything for ASU. I predict all departments will spend even more money in the future.
Conclusion
Since there is no pandemic now, I believe ASU will increase the enrollment. More enrollment means more tuition means more money, meaning departments must purchase things that will go to the purchasing team that will keep us busy. I predict that more requisitions will be processed in 2024 than this year 2023. I believe there will be more Purchase Orders issued in 2024 than 2023. I also believe that departments will spend even more money on Goods/Services, Scientific, Technology, and Construction purchases. I predict every year purchases will increase but more slowly in the long run.











## How Many Requisitions I have Processed since I started at ASU ?
 <img width="1109" alt="Total Number of Requisitions I Processed since Starting at ASU" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/caadfd06-6963-4de8-8188-2e4714d77c6d">

I have processed **6,137** requisitions since starting in the ASU purchasing department. That is a lot of requisitions processed. 

## What Is the Total Amount of All of the Requisitions I Have Processed Since Starting at ASU ?
 <img width="548" alt="Total Amount of All the Requisitions I Processed since Starting at ASU" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/5542917e-87e4-4432-b391-472ed907cdf2">

Departments spent **$24,898,610.91** so around 25 million dollars with the requisitions that I have processed.

## How Many Requisitions That I have Processed That are Under $25,000?  
<img width="1120" alt="Total Number of All the Requisitions I Processed Under 25,000" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/c358d417-0489-482a-9d63-98e04c6f3eac">

I have processed **5,847** requisitions that are $25,000 and under. These represent most of the department’s purchases. I have move away from processing these the longer I work in purchasing. If I do an under $25,000 requisitions, it would be the oldest one first

## What Is the Total Amount of All of the Requisitions I Have Processed That are Under $25,000?
<img width="701" alt="Total Amount of All the Requisitions I Processed Under 25,000" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/165e33b0-70d7-4e09-9472-579f615cbfde">

Departments spent **$15,952,662.19** on purchases that goes to me under $25,000.

##  How Many Requisitions That I have Processed That are Over $25,000? 
<img width="1094" alt="Total Number of All the Requisitions I Processed Over 25,000" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/36ad7506-3088-4bd3-bfe4-20d29a387e49">

I have processed **290** requisitions over $25,000. High dollars requisitions are more time consuming because they require more documentation and if the purchases use federal money, then even more documentation is needed so that the departments justify their purchase. That involves reaching out to the department to obtain more documentation. Processing high dollar requisitions is the biggest priority for the Strategic Partnerships team in that we get trained in how to do these first before going to low dollar. These requisitions have a steeper learning curve with learning which documentation is needed but are easy to master eventually. The hardest part is making sure departments have the right documentations because they don’t always provide what we wanted.

The reason the number is lower because purchasing in general doesn’t get a lot of high dollar requisitions in general. Departments would want a PO generated before creating separate requisitions usually low dollar to pay for invoices in which explains why Purchasing gets so many low dollar requisitions. Also, Strategic Partnerships is a huge team. Including myself there are 6 team members not including higher ups. And the work load gets evenly distributed and everyone in the team knows how to process over $25,000 requisitions. The number of requisitions has increased over time and will continue to increase in the future.


## What Is the Total Amount of All of the Requisitions I Have Processed That Are Over $25,000?
<img width="750" alt="Total Amount of All the Requisitions I Processed Over 25,000" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/abce6bb5-182e-4fd2-acb0-bc7644ac3984">

Departments spent **$15,375,117.64** on purchases that goes to me over $25,000.

## How Many Requisitions That I have Processed That are Over $100,000?
<img width="664" alt="Total Number of All the Requisitions I Processed Over 100,000" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/b79fb5fd-fa2b-4418-abca-4f0764e70aaf">
 
I have processed **zero** requisitions that are over $100,000. The reason for this is because requisitions over $100,000 do not go to our team in Strategic Partnerships. Those over $100,000 requisitions route over to the Sourcing Team in which they exclusively deal with over $100,000 requisitions.

## What Is the Requisition Lowest Amount I did?
<img width="673" alt="Requisition Lowest Amount I did" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/df0939ed-6d23-4ef3-908c-719ae94b9e68">
 
The lowest amount I have done on a requestions is zero dollars. Those requestions can either be a zero-dollar discount, Attachments or anything written the requisition needs to go to the suppler after the purchase order is generated, an agreement need to be signed and sent to the supplier or an agreement term needs to be extended. 

## What Is the Requisition Highest Amount I did?
<img width="714" alt="Requisition Highest Amount I did" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/c2b88baa-8ab3-4782-8989-62e7fc9d34f5">

The lowest amount I have done on a requestions is **$99,934.84** dollars. It is close to $100,000. This is a lot of money. I have seen some requisitions that are exactly $100,000 that reach strategic partnerships. We usually reassign those requisitions to the sourcing team.

## What is the Average Total Amount of Requisitions Overall I did ?
<img width="684" alt="Requisition Average Amount I did" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/0ae8b90a-c50b-441a-b8ef-a3bb82bd06aa">

The average amount I did on requisitions is around **$5,104.74**. This proves a majority of requisitions that come to Strategic Partnerships are under $25,000. 

## How Many Requisitions I Have Processed That Used the Requisition Type of Goods and Services ?
<img width="1115" alt="Total Number of All the Requisitions I Processed Over Using Goods and Services" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/12eceb24-3fbd-4429-bdfc-b2752001ede5">

For the Purchasing Department to generate purchase orders that is needed to go to the supplier that automatically accepts ASU terms and conditions in order to be used as a contract, departments will choose the requisition types of Goods and Services, Chemical, or Technology. I generated **954** Purchase Orders from requisitions that use Goods and Services. Strategic Partnerships don’t get as much requisitions that uses goods and services because departments will sometimes want to purchase to issue Purchase Orders that are of high dollar amounts and then want to pay for each of the goods and services separately with the requisition type of Pay an Invoice.

## How Many Requisitions I Have Processed That Used the Requisition Type of Technology?
<img width="1070" alt="Total Number of All the Requisitions I Processed Over Using Technology" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/d144e1db-a078-4de9-9c01-8d34e46cfe07">

I have processed **170** requisitions that use the requisition type of technology. That means 170 purchase orders have been issued. They are treated the same as goods and services, but they just require a security review while goods and services don’t. 

## How Many Requisitions I Have Processed That Used the Requisition Type of Pay an Invoice ?
<img width="1105" alt="Total Number of All the Requisitions I Processed Over Using Pay an Invoice" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/9d338e11-2f76-455d-8cbd-f9a66700af1b">

A Pay an Invoice requisition type is used for purchases or services that have already happened. Suppliers will provide departments with an invoice and purchasing checks if departments provide an invoice document. I have done **5,011** requisitions that are Pay an Invoice any amounts. Purchasing must approve Pay an Invoice requisition for departments to pay for their purchases. Pay an Invoice is that requestion type that I approved the most. The Pay an Invoice requisitions is the requisition type that our team Strategic Partnerships sees the most. Purchasing always want departments to generate PO before using Pay an Invoice.

## How Many Requisitions I Have Processed That Used Other Requisition Types?
<img width="1108" alt="Total Number of All the Requisitions I Processed Over Using Other Req Types" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/dd91ece9-2a5c-446e-9cc7-403a696c4eb4">

I have processed **64** requisitions of the other requisition types. All the other requestions type route to different teams within Purchasing. The only other requisition type that Strategic Partnerships do is Chemical. These go to material management after approval. The chemical orders are chemicals that are hazardous if people are not careful handling it. These requisitions are rare to see, but are treated just like a Goods and Services Requisitions. 

## How Many Requisitions I Have Processed Every Year?
<img width="752" alt="Total Number of All the Requisitions I Processed Yearly" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/e8f2bbd7-f839-47ba-8980-0f0faf4e5dbd">

* 2022 – 2069 requisitions have been processed by me in 2022
* 2023 – 4068 requisitions have been processed by me in 2023

The trend is that the number of requisitions that I have been processing have increased. As years go on if I still stay in purchasing the number of requisitions that I have processed will plateau and stay close to the same because departments can only submit so many requisitions and I also have more teammates taking on requisitions other than myself.

## What Is the Total Amount for All the Requisitions I Have Processed Per Year ?
<img width="737" alt="Total Amount of All the Requisitions I Processed Yearly" src="https://github.com/Twrigh18/Purchasing-Portfolio-SQL/assets/97319435/0672c635-4679-4e29-8334-a07eb89d1218">

* 2022 – Departments spent $5,660,838.79 so around 5 million dollars with the requisitions that I have processed in 2022.
* 2023 – Departments spent $25,666,941.04 so around 25 million dollars with the requisitions that I have processed in 2023.
  
The trend is that the amounts from the requisitions are increasing every year. In the future the amounts will increase every year since I had taken on higher dollar requisitions.

# Conclusion

Since there is no pandemic now, I believe ASU will increase the enrollment. More enrollment means more tuition means more money, meaning departments must purchase things that will go to the purchasing team that will keep us busy. I predict that more requisitions will be processed in 2024 than this year 2023. I believe there will be more Purchase Orders issued in 2024 than 2023. I also believe that departments will spend even more money on Goods/Services, Scientific, Technology, and Construction purchases. I predict every year purchases will increase but more slowly in the long run.
