# MySQL


## MySQL Database vs. Excel File as a Data Source

- While Excel files can be suitable for smaller datasets and simple analyses, databases become increasingly valuable as data complexity and volume grow. They provide a more robust infrastructure for handling large-scale data analytics and offer better support for the demands of enterprise-level business intelligence and reporting.


## MySQL Database Hosting

### Performance and Scalability

- Databases are designed to handle large amounts of data efficiently. As your dataset grows, the performance of a database tends to be more consistent than that of Excel, which might struggle with large datasets.

- Databases can handle concurrent user access more effectively, making them suitable for environments where multiple users need to query and analyze data simultaneously.

### Data Integrity

- Databases enforce data integrity constraints, ensuring that data adheres to predefined rules (e.g., unique keys, relationships between tables). This helps maintain data accuracy and consistency, reducing the risk of errors.

### Ease of Data Updates

- Databases offer better mechanisms for handling updates and changes to data. With Excel, manual updates and version control can become challenging, whereas databases often provide structured methods for updating and managing data changes.

### Automation and Integration

- Databases can be integrated with other systems and automated processes, facilitating seamless data flow between different parts of your organization. This is often more challenging to achieve with Excel files.

## phpMyAdmin

- phpMyAdmin is a web-based administration tool for managing MySQL databases.

- phpMyAdmin simplifies the management and interaction with MySQL databases by providing a user-friendly web-based interface. It streamlines tasks related to database creation, data manipulation, user access control, and more, making it a valuable tool for both beginners and experienced database administrators.



### Creating tables in MySQL using phpMyAdmin

1. Using the SQL console in phpMyAdmin, I used the following SQL query to create a table for COUNTER Title Master Reports (R5) for 2019.

- Note the name of the table can be whatever you choose. I used the YY as the year so it's easier to edit for different years.

- Remember to define your columns with appropriate data types based on the kind of data you'll be storing (e.g., INT for integers, VARCHAR for variable-length strings, etc.).

```
CREATE TABLE title_master_YY_journals (

Title VARCHAR(50),
Publisher VARCHAR(50),
Publisher_ID VARCHAR(25),
Platform VARCHAR(25),
DOI VARCHAR(25),
Proprietary_ID VARCHAR (25),
ISBN VARCHAR(19),
Print_ISSN VARCHAR(25),
Online_ISSN VARCHAR(25),
Subject VARCHAR(25),
URI VARCHAR(25),
Data_Type VARCHAR(25),
Section_Type VARCHAR(25),
YOP Date,
Access_Type VARCHAR(25),
Access_Method VARCHAR(25),
Metric_Type VARCHAR(25),
Reporting_Period_Total INT,
`19-Jan` INT,
`19-Feb` INT,
`19-Mar` INT,
`19-Apr` INT,
`19-May` INT,
`19-Jun` INT,
`19-Jul` INT,
`19-Aug` INT,
`19-Sep` INT,
`19-Oct` INT,
`19-Nov` INT,
`19-Dec` INT
);

```

![phpMyAdmin Structure Screen shot](https://github.com/AlaoSUL/COUNTER_Reports/blob/main/Images/phpmyAdmin%20-%20structure.png)


### Importing data into tables

1a. Select Database:
- On the left side, you'll see a list of databases. Choose the database into which you want to import the CSV file.
Navigate to the "Import" Tab:

**Once inside the selected database, select the desired table to import since we want to update specific tables. Below are use cases for importing at a database vs table level.** Click on the "Import" tab.

1b. Use Cases:
- Importing into a database is commonly used for tasks like database backup restoration or migration to a new server.
![import database](https://github.com/AlaoSUL/COUNTER_Reports/blob/main/Images/import_database.png)
- Importing into a specific table is useful for tasks like adding new records or updating existing records in a targeted manner.
![import table](https://github.com/AlaoSUL/COUNTER_Reports/blob/main/Images/import_data_table.png)

2. Choose File:
- On the "Import" page, you'll find a section where you can choose a file to import. Click on the "Choose File" button and select the CSV file you want to import from your local machine.

**Note: There is a 32MB file size limit for CSV. You need to compress the CSV file and file name must end in the following format: [filename.csv.zip]**

3. Specify CSV Settings:
- phpMyAdmin will attempt to automatically detect the CSV format. However, you may need to review and adjust the import settings based on your CSV file. This includes specifying the format of the CSV (e.g., CSV using LOAD DATA), field separators, and other options.

![import table settings](https://github.com/AlaoSUL/COUNTER_Reports/blob/main/Images/import_table_settings.png)

- Uncheck the Partial Import options

- Enter 1 in the "Number of rows to skip, starting from the first row" or else the headers will be imported into the table.

- Column names: **If the data in each row of the file is not in the same order as in the database, list the corresponding column names here. Column names must be separated by commas and not enclosed in quotations.**

- The use of backticks around the month abbreviations (e.g., `19-Jan`, `19-Feb`, etc.) is a common convention in databases and data-related contexts, especially when dealing with column or field names. The backticks are often used to denote that the enclosed text is a single identifier or a specific name.

```
Title, Publisher, Publisher_ID, Platform, DOI, Proprietary_ID, ISBN, Print_ISSN, Online_ISSN, Subject, URI, Data_Type, Section_Type, YOP, Access_Type, Access_Method, Metric_Type, Reporting_Period_Total, `19-Jan`, `19-Feb`, `19-Mar`, `19-Apr`, `19-May`, `19-Jun`, `19-Jul`, `19-Aug`, `19-Sep`, `19-Oct`, `19-Nov`, `19-Dec`
```
4. Execute Import:

- Once you've configured the settings, scroll down to the bottom of the page and click on the "Go" button to start the import process.
Verification and Confirmation:

- After the import process completes, phpMyAdmin will display a message indicating whether the import was successful. If there are any errors, they will be reported, and you may need to review your CSV file or import settings.


# Connection of MYSQL to Tableau

## Connect to MySQL server

1. In Tableau Desktop, on the left side of the screen, click on "Connect to Data" to open the Connect pane.

2. Under the "To a Server" section, find and select "MySQL."

3. In the "Server" field, enter the hostname or IP address of your MySQL server.

4. In the "Port" field, enter the port number used by your MySQL server (default is 3306).

5. Specify the database you want to connect to in the "Database" field.

6. If your MySQL server requires authentication, enter your MySQL username and password.

7. Click on the "Sign In" button.

Upon a successful connection, you will see the tables populate on the left side in Tableau. These tables will be the same as those in your phpMyAdmin view.

phpMyAdmin        |   Tableau interface
:----------------:|:-------------------:
![phpMyAdmin table list](https://github.com/AlaoSUL/COUNTER_Reports/blob/main/Images/phpmyAdmin_table%20list.png) | ![tableau server connected](https://github.com/AlaoSUL/COUNTER_Reports/blob/main/Images/tableau_server_connected.png)



## Connect to a Custom SQL Query

Though there are several common reasons why you might use custom SQL, you can use custom SQL to union your data across tables, recast fields to perform cross-database joins, restructure or reduce the size of your data for analysis, etc.

### Combine your tables vertically (union)

1. After connecting to your data, double-click the **New Custom SQL** option on the Data Source Page
![custom SQL](https://github.com/AlaoSUL/COUNTER_Reports/blob/main/Images/custom_SQL_query.png)

2. Enter your query into the text box.

3. When finished, click OK

When you hit OK, the query runs and the custom SQL query appears in the logical layer of the canvas. Only relevant fields from the custom SQL query display in the data grid on the Data Source page.

![custom_SQL_query2](https://github.com/AlaoSUL/COUNTER_Reports/blob/main/Images/custom_SQL_query2.png)


4. Our tables are separated by years so will need to UNION each month for every given year. Thus, the custom SQL query will be extremely long. Here's a snippet:

```
SELECT Title,
Publisher,
YOP,
URI,
Subject,
Access_Type,
Metric_Type,
CAST('2019-01-01' AS DATE) as 'Year 2',
`19-Jan` as 'Num Requests'
FROM title_master_19_journals
UNION ALL
SELECT Title,
Publisher,
YOP,
URI,
Subject,
Access_Type,
Metric_Type,
CAST('2019-02-01' AS DATE) as 'Year 2',
`19-Feb` as 'Num Requests'
FROM title_master_19_journals
UNION ALL
SELECT Title,
Publisher,
YOP,
URI,
Subject,
Access_Type,
Metric_Type,
CAST('2019-03-01' AS DATE) as 'Year 2',
`19-Mar` as 'Num Requests'
FROM title_master_19_journals
UNION ALL....

```

Relevant Fields   |  CAST Function for Year  
:----------------:|:------------------------:
Title, Publisher, YOP, URI, Subject, Access_Type, Metric_Type, `20-Jan` as `Num_Request` |  We needed to create a Date field to accurately represent the given month and year for each table. The COUNTER reports show usage by month so I used 'YYYY-MM-01' as the string to CAST to DATE property called "Year 2."
