# MySQL to Tableau


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
