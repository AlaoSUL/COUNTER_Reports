# COUNTER_Reports

### What is COUNTER?

Since its inception in 2002, Counting Online Usage Networked Electronic Resources (COUNTER) has been focused on providing a code of practice that help ensure librarians have access to consistent, comparable, and credible usage reporting for their online scholarly information. The COUNTER Code of Practice provides guidance on data elements to be measured and definitions of these data elements, as well as guidelines for output report content and formatting and requirements for data processing and auditing. To have their usage statistics and reports designated COUNTER compliant, content providers MUST provide usage statistics that conform to the current Code of Practice.

Project COUNTER’s mission “COUNTER exists to develop and maintain the standard for counting and reporting the use of electronic resources. It will ensure that content providers can implement the code of practice efficiently and that their library customers and users will receive relevant usage reports in the format they need.”

COUNTER's standardized usage reports allow libraries to:

- Compare usage easily across different publisher platforms & vendors and reports/formats are standard
- Assess user activity, in relationship to their content & improve user experience
- Inform renewal and new purchasing decisions
- Justify budget spend to their stakeholders
- Inform faculty/power-users about the value & use of current library resources
- Derive “cost-per-use” for content

### Whom is COUNTER for?

The COUNTER Code of Practice helps librarians demonstrate the value of electronic resources by facilitating the recording and reporting of online resource usage stats in a consistent and credible way.

The implementation of the Code of Practice helps publishers and vendors support their library customers and provide statistics comparable with those of their competitors.

### COUNTER Release 5 (R5)

As of January 2022, [Release 5.0.2](https://cop5.projectcounter.org/en/5.0.2/) will be the current Code of Practice and the requirement for COUNTER compliance.

### Additional resources

[Friendly Guides updated for Release 5.0.2](https://www.projectcounter.org/friendly-guides-release-5/)

Release 5 Manual for Librarians --> The PDFs are located in the [COUNTER Module folder](https://github.com/AlaoSUL/COUNTER_Reports/tree/main/COUNTER%20Modules)

In the manual you will see:

- the key metrics that show user activity on a platform
- most importantly, how to calculate usage per book or journal
- the main COUNTER reports and how to use them
- how to track trends by comparing the correct figures between Release 4 and Release 5 reports

#### Books: Understanding metrics and standard views

It explains:

- Item Metrics
- Title Metrics
- Calculating cost per use
- Reports
- Hourly sessions
- Automatic time-outs

#### Journals: Understanding metrics and standard views

It explains:

- Item Metrics
- Calculating cost per use
- Reports
- Sessions
- Trend data
- Open Access usage

#### Database reports

It explains:

- Metrics
- Different Types of Databases
- Searches
- Sessions
- The Database Master Report and its Standard Views
- Comparing between Release 4 and Release 5

#### Comparing Counts between Release 4 and Release 5

- We look at examples of the new Release 5 Standard Views, and compare them to the corresponding
Release 4 reports.
- Highlight the new metric types so that you can see how they affect cost-per-use calculations
- Offer new possibilities for the usage analysis


### Equivalence between R4 and R5 Reports

| Release 4 | Release 5 | Metric Type (R5) |
| --- | --- | --- |
| Journal Report 1 (Full-text article requests, excluding GOA) | Journal Usage by Access Type TR_J3 | Total_Item_Requests |
| Journal Report 1 GOA (Gold OA Full-text article requests) | Journal Usage by Access Type TR_J3 | Total_Item_Requests |
| Journal Report 2 (Access Denied)| Journal Access Denied TR_J2 | No_License |
| Journal Report 5 | Title Master Report TR | Total_Item_Requests |
| Database Report 1 (Total searches, result clicks, and record views) | Database Search and Item Usage DR_D1 | Regular Searches (R4) and Searches_Regular |
| Database Report 2 (Access Denied) | Database Access Denied DR_D2 | Access Denied: concurrent/simultaneous user license limit exceeded (R4)/Limit_Exceeded (R5) and Access denied: content item not licenced / No_License (R5) |
| Platform Report | Platform Master Report PR | Searches-federated and automated (R4) and Searches_Automated and Searches_Federated |
| Book Report 1 (Title requests)  | Book Requests TR_B1 | Unique_Item_Requests |
| Book Report 2 (Section requests) | Book Request TR_B1 | Total_Item_Requests |
| Book Report 3 (Access Denied) | Book Access Denied TR_B2 | No_License |
| Multimedia Report 1 | Item Master Report IR | Total_Item_Requests |

## Where do I get the COUNTER reports?

- We have a technical specialist from the acquisitions department who pull these reports and organizes the Excel files onto a shared Google drive. I can easily find the reports and download them. Shout out to James!

- Unfortunately, R4 reports are deprecated so some publishers will be missing a year or two of stats.

- Otherwise, COUNTER Sushi is an API to allow developers to retrieve all possible reports.

### COUNTER reports Documentation

Please visit their site for more information on the scope of COUNTER

- [Technical Specification for COUNTER](https://cop5.projectcounter.org/en/5.0.2/03-specifications/index.html#specifications)

- [COUNTER reports](https://cop5.projectcounter.org/en/5.0.2/04-reports/index.html#reports)

- [Delivery of COUNTER reports](https://cop5.projectcounter.org/en/5.0.2/05-delivery/index.html#delivery)

- [COUNTER Sushi](https://www.projectcounter.org/counter-sushi/)

## Data Cleaning - How to Format Release 4 and Release 5 reports

- Data cleaning is a painstaking, yet most important process of data analysis. Luckily, COUNTER reports provides a consistent report layout. However, there are several nuances among these reports in order to merge/concatenate the R4 and R5 reports. Here are the steps that I took to clean Release 4 and Release reports.

### Modules Used

- Pandas: a fast, powerful, flexible and easy to use open source data analysis and manipulation tool

- Functools: provides useful features that make it easier to work with high order functions (a function that returns a function or takes another function as an argument ). With these features, you can reuse or extend the utility of your functions or callable object without rewriting them.

#### Journal Report - Full Text Article Requests

###### Journal Report 1 (R4)

- Notable Columns: Journal (Title) | Publisher | Print ISSN | Reporting Period Total | Reporting Period HTML | Reporting Period PDF | Jan-YY to Dec-YY

![jr1](https://github.com/AlaoSUL/COUNTER_Reports/blob/main/Images/Elsevier_j1r4.PNG)

- The first 7 rows are general information which is not pertinent to our analysis so we must skip these rows. While reading in the Excel files, I used the skip_rows argument to start at Row 8 or index 7 (Python index starts at 0) to get the headers correctly into the first row.

- Additionally, some reports have a total entry as the first row after the headers. I used iloc(), an index-based selection technique to exclude this row since it's not useful in our analysis.

- Created an Access_Type column (present in TR_J3) to distinguish controlled --> Access_Type: "Controlled"

- Essentially, the end goal is to combine the Journal 1, Journal 1 GOA, and Journal Access TR_J3 reports into one dataset.

###### Journal Report 1 GOA (R4)

- Same columns as the Journal 1 report except usage data is for Gold Open Access (GOA) Articles only

- Created an Access Type column (present in TR_J3) to distinguish GOA --> Access_Type: "OA_Gold"

- This additional column is necessary to distinguish between controlled and GOA articles and analyze usage within the same month/year.


![el_goa1](https://github.com/AlaoSUL/COUNTER_Reports/blob/main/Images/Else_GOAp1.PNG)
![el_goa2](https://github.com/AlaoSUL/COUNTER_Reports/blob/main/Images/Else_GOAp2.PNG)

##### Journal Usage by Access Type TR_J3 (R5)

- Notable Columns: Title | Publisher | Print_ISSN | Online_ISSN | Access_Type | Metric Type | Reporting_Period_Total | Jan-YY to Dec-YY

![tr_j3](https://github.com/AlaoSUL/COUNTER_Reports/blob/main/Images/tr_j3r5.PNG)

- Contrary to R4, R5's first 13 rows are general information so I extended the skip_row range to index 13.

##### Code Snippet of data cleaning steps for TR_J3

![dcjr1](https://github.com/AlaoSUL/COUNTER_Reports/blob/main/Images/dcjr1.PNG)

- Similar to R4, some reports have a total entry so I used iloc() to exclude this line.

- Renamed a few columns for the dataframes to merge correctly: Title --> Journal | Print_ISSN --> Print ISSN | Online_ISSN --> Online ISSN

- Created a list of dataframes

- Concatenate vertically (axis = 0) using columns found in all dataframes

- Fill NaN values from previous years: There will be NaN values since month/year columns will be extended to the right (wider). We will fill these columns with 0 as there cannot be usage in future dates.

##### Combine JR1/GOA and TR_J3

![combinej1](https://github.com/AlaoSUL/COUNTER_Reports/blob/main/Images/combine_elsevier.PNG)

##### Issue with generated Excel file from above

![fileloadeddate](https://github.com/AlaoSUL/COUNTER_Reports/blob/main/Images/dateissue.PNG)

![dataissue1](https://github.com/AlaoSUL/COUNTER_Reports/blob/main/Images/datetime_issue.PNG)
![dataissue2](https://github.com/AlaoSUL/COUNTER_Reports/blob/main/Images/datetime_issue2.PNG)
- COUNTER reports expresses the month/year columns in this format "YYYY-MM-DD 00:00:00". The datatype shows as an int64 but I am unable to convert
to datetime since leading zeros in a integer are no longer permitted. The column cannot be recognized when the column field is put as a string.

- The current workaround is a bit manual until I find a more efficient way to solve this data incompatibility.

- In the export Excel file, I converted the headers into a short date format "Jan-YY" or "Jan-15" which makes it more digestible when imported
into Tableau.


#### Merging Journal Reports with Subject Fields (E.G Elsevier)

- As part of our analysis, we wanted to incorporate subject categories/disciplines to merge with our journal and book usage. We can drill down to see trends among categories/disciplines from year to year.

- The six publishers are Cambridge, Elsevier, Sage, SpringerNature, Taylor & Francis, and Wiley.

- I was able to find [Elsevier Journal w Subjects via Google Searches](https://phdtalks.org/2021/05/download-elsevier-journal-list-with-impact-factor-2021-pdf-xls.html)

- Accuracy of Elsevier List: Out of 37,450 rows, there were 68 entries with no corresponding subject fields which represents only 0.18% of the data. As a result, the list had 99.82% of Elsevier journals used between 2015-2021 at Stanford University.

- Upon request, Cambridge, Sage, and Wiley provided these lists.

- SpringNature has an [API](https://dev.springernature.com/) that allows developers to access the data.

### Using Digital Object Identifier (DOI) to scrape subject/discipline information

- Each Title Master report contains a DOI column that can be transformed into a URL link (adding https://[doi here].org)

- Using BeautifulSoup, a Python package for parsing XML and HTML, I wrote a for loop to iterate over each DOI and extract the nested tag with the subject information.    

- Please refer to this notebook for detailed documentation.


#### Standardizing Subjects Among Publishers 

##### How to merge with the final reports

- The merge can be accomplished with a VLOOKUP in Excel. The columns needed will be ISSN (Journals) or ISBN (Books) with Top Level, Primary Level, and Secondary Level fields.
