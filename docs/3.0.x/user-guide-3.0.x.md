title: User Guide


# Introduction

Conductor for Gluent is an application to help manage Gluent offloads. The Gluent software works on a per database basis. Conductor has an additional unit above a database called a site. A particular installation of Conductor will have one site with one or more databases to manage. 

The guided flow in Conductor is:
<ol>
<li>Obtain a Gluent Advisor CSV for Conductor file from Gluent</li>
<li>Add Database, after adding a database you will be taken to the Candidate Selection Wizard.</li>
<li>Upload a Gluent Advisor CSV and select one or more tables. On finishing, you will be taken to the Job Wizard.</li>
<li>Name your job, select one or more tables to offload for the job, and schedule the job. </li>
<li>At this point, the job will automatically launch based on the schedule.</li>
</ol>

Note: Once some tables have been added either through the candidate selection page or using the add table wizard, the guided flow will not automatically start when closing the add/edit database page.

It is not mandatory to follow the guided flow. For example, if you do not have a Gluent Advisor CSV for Conductor file, you can add tables through the add table wizard on the Candidate Review page. 


# Login

Enter the Conductor for Gluent Apex URL into your browser. The URL will be something of the form:

	http://{hostname}:{port}/apex/f?p=100

<img src="img/s-00-a-login.png" alt="Login Screen" style="width:400px;height:375px;"><p>
Once the Conductor for Gluent login form is available, then enter your username and password.


# Site

A site is made up of one or more database, for which jobs can be scheduled for offloading data. At the site level, databases can be added to Conductor, defaults can be set for parameters, notifications and the application, and there is a site level overview of some metrics.


## Site Home Page

<img src="img/s-01-a-sitehome.png" alt="Site Home Screen" style="width:800px;height:475px;"><p>

From the site level menu, located on the upper left side of the screen, there are the following choices:

<ol>
<li>Site Home - the site home page</li>
<li>Application Defaults - where you can change settings that affect the way the application operates</li>
</ol>

From the site home:

<ol>
<li>You can manage site level options:</li>
<ul>
<li>Default Offload Parameters</li>
<li>Default Present Parameters</li>
<li>Site Level Notification Options</li>
</ul>
<li>Review metrics at the site level:</li>
<ul>
<li>Count of Jobs by week (Last 28 days) for all databases</li>
<li>Offload Percentage - percentage of data: offloaded, dropped, or not offloaded from all databases</li>
<li>Offloadable Gigabytes of Unselected Advisor Candidates - if an advisor report was uploaded, this is a summary of space from tables which have not been selected</li>
</ul>

<li>Add a New Database - Click on the <i>Add New</i> card from the list.</li>
<li>Select a Database to Manage - Click on one of the database cards, to manage its jobs and tables.</li>
<li>Edit the details of a database - Click on the <i>Edit</i> Link of a database to go to the maintain database details page, where you change its description, icon color, database link information, etc.</li>
</ol>

Buttons:
<ol>
<li>Default Offload Parameters - Click on the button to go to the Manage Default Offload Parameters for Site page.</li>
<li>Default Present Parameters - Depress the button to go to the Manage Default Present Parameters for Site page.</li>
<li>Site Level Notification Options - Click on the button to take you to the Manage Notifications for Site page. </li>
</ol>

Links:
<ol>
<li>Database Name - click on the database name to bring up the database home page where you can manage tables and jobs for the database. </li>
<li>Edit - click on this link to bring up the maintain database details page and edit details about the database. </li>
</ol>


# Databases


## Database Home Page

After clicking on a database on the site home page, you will go to the database home page for that particular database.

<img src="img/s-11-a-dbhome.png" alt="Database Home Screen" style="width:800px;height:475px;"><p>

From the database level menu, located on the upper left side of the screen, there are the following choices:

<ol>
<li>Site Home - the site home page</li>
<li>Database Home - the database home page</li>
<li>Dashboard - Monitor the status of jobs for the database.</li>
<li>Job Maintenance - Add or edit jobs.</li>
<li>Table Review - Add or edit details about tables to be offloaded.</li>
<li>Candidate Selection - Wizard for selecting candidates from a Gluent Advisor CSV for Conductor.</li>
</ol>

At the top of the page are buttons/links to set offload, present and notification parameters at the database level

Followed by some summary information about the database:

<ol>
<li>Advisor Candidates</li>
<ul>
<li># of tables in the advisor report that have not been selected for offload.</li>
<li>Clicking here will take you to the candidate selection wizard.</li>
</ul>
<li>Select Tables</li>
<ul>
<li># of tables that have been selected as candidates for offload.</li>
<li>Clicking here will take you to the table review page.</li>
</ul>
<li>Total Jobs</li>
<ul>
<li># of jobs that have been created.</li>
<li>Clicking here will take you to the job maintenance page.</li>
</ul>
<li>Running Jobs</li>
<ul>
<li># of jobs currently running.</li>
<li>Clicking here will take you to the dashboard.</li>
</ul>
<li>Successful Jobs</li>
<ul>
<li># of jobs that completed successfully.</li>
<li>Clicking here will take you to the dashboard.</li>
</ul>
<li>Jobs in Error State</li>
<ul>
<li># of jobs where an error has occurred.</li>
<li>Clicking here will take you to the dashboard.</li>
</ul>
</ol>

Review metrics at the database level:
<ul>
<li>Count of Jobs by week (Last 28 days) for this database</li>
<li>Offload Percentage - percentage of data: offloaded, dropped, or not offloaded from this database</li>
<li>Offloadable Gigabytes of Unselected Advisor Candidates - if an advisor report was uploaded, this is a summary of space from tables which have not been selected</li>
</ul>

Buttons:
<ol>
<li>Default Offload Parameters - Click on the button to go to the Manage Default Offload Parameters for Database page.</li>
<li>Default Present Parameters - Depress the button to go to the Manage Default Present Parameters for Database page.</li>
<li>Notification - Click on the button to take you to the Manage Notifications for Database page. </li>
<li>Calendar (icon) - Located in the Count of Jobs metric (right-hand side above bars), clicking the button will show a calendar for jobs that have run.</li>
</ol>


## Maintain Database Details


### Add Database

<img src="img/s-10-a-adddb1.png" alt="Maintain Database Details Screen" style="width:800px;height:475px;"><p>

When adding a new database, enter database name, description, and connection method on this page. Then press Add button.

Fields:
<ol>
<li>Name              : Any alpha-numeric identifier used to identify the database. [Required field]</li>
<li>Description       : Any alpha-numeric characters to describe the database. [Required field]</li>
<li>Connection Method : No Connection Allowed -or- DB Link. If DB Link is not specified all details about the tables to be offloaded will need to be manually entered. [Required field]</li>
</ol>

Buttons:
<ol>
<li>Add    : Add the database details to the Conductor for Gluent repository.</li>
<li>Close  : Close the page and go back to the site home.</li>
</ol>


### Edit Database

<img src="img/s-10-b-editdb1.png" alt="Maintain Database Details Screen" style="width:800px;height:475px;"><p>
Any of the fields can be modified. You can switch the color of the database by clicking on the "Database Icon Color" link. Once a color is selected from the pick color screen, be sure to press the "Save" button.

To update the database link information (if that is being used), press on the DB Link Wizard button.

Fields:
<ol>
<li>Name              : Any alpha-numeric identifier used to identify the database. [Required field]</li>
<li>Description       : Any alpha-numeric characters to describe the database. [Required field]</li>
<li>Connection Method : No Connection Allowed -or- DB Link. If DB Link is not specified all details about the tables to be offloaded will need to be manually entered. [Required field]</li>
</ol>

Buttons:
<ol>
<li>Save   : Save the database details to the Conductor for Gluent repository. </li>
<li>Delete : Delete the database details to the Conductor for Gluent repository. </li>
<li>Close  : Close the page. If the database has tables, then you will be directed to the Site home. If the database does not have tables, then you will be directed to the candidate selection wizard. </li>
<li>DB Link Wizard : Open the DB Link Wizard to add/edit the database link.</li>
</ol>

Links:
<ol>
Database Icon Color :  Bring up the page to pick a color for the database icon. Once a color is selected from the pick color screen, be sure to press the "Save" button.
</ol>


### DB Link Wizard


#### DB Link Wizard – Step 1

<img src="img/s-10-c-dblink1.png" alt="DB Link Wizard Step 1 Screen" style="height:475px;"><p>
Enter the host name, port, service name, and password. Press Next to create the database link.

Fields:
<ol>
<li>Host Name    : Fully qualified host name (FQDN) or IP address. [Required field]</li>
<li>TNS Port     : Port for the listener on the host that provides access to the database. [Required field]</li>
<li>Service Name : The TNS service name for the database. [Required field]</li>
<li>Password     : The password of the CONDUCTOR_FOR_GLUENT user for this database. [Required field]</li>
</ol>

Buttons:
<ol>
<li>Cancel   : Cancel the wizard. </li>
<li>Next     : When the next button is depressed, a database link will be (re-)created from the details provided, then you move to the 2nd step of the DB Link Wizard.</li>
</ol>


#### DB Link Wizard – Step 2

<img src="img/s-10-d-dblink2.png" alt="DB Link Wizard Step 2 Screen" style="height:475px;"><p>
Press Test DB Link to verify that the database link is correct. Press Finish if the test is successful. Press the left arrow to go back and correct any of the database link information.

Buttons:
<ol>
<li>Test DB Link : A query will be run with the database link to verify that it completes successfully.</li>
<li>Left Arrow   : Return to Step 1 of the wizard. </li>
<li>Cancel       : Cancel the wizard. </li>
<li>Finish       : When the finish button is hit, the wizard will close.</li>
</ol>


##### Test DB Link

<img src="img/s-10-e-dblink3.png" alt="Test DB Link Screen" style="height:175px;"><p>
When testing the database link, a message will appear in the DB Link Test Results section for success or failure.


# Tables

There are two ways to add tables to the Conductor for Gluent repository:

<ol>
<li>Candidate Selection Wizard - Tables are selected from a Gluent Advisor report. The candidate selection menu option will bring up the candidate selection wizard.</li>
<li>Add Table Wizard - tables are selected from a list of schemas and their tables across a database link based on the privileges provided to the Conductor for Gluent user. The add table wizard button can be found on the table review page.</li>
</ol>


## Candidate Selection Wizard


### Candidate Selection Wizard - Step 1

<img src="img/s-18-1-candidateselection.png" alt="Candidate Selection Wizard Step 1 Screen" style="width:800px;height:475px;"><p>
<u>Step 1 – Select an Advisor Output File</u>: 
Select a file or if this is your second time through, you can use the existing file. Multiple files can be uploaded if a new advisor report CSV is obtained. Press Next to continue.

Fields:
<ul>
<li>When Upload Advisor Output File (CSV) radio option is selected:</li>
<ol>
<li>Advisor Output File - Click into the field to bring up the file browser and select a file.</li>
<li>Date the Advisor was run - It is important to select the correct date, as calculations for the default offload retention is calculated based on this date and information contained in the Gluent Advisor file.</li>
<li>Description - Any alphanumeric description for the file.</li>
</ol>

<li>When Use Current Advisor Output radio option is selected:</li>
<ol>
<li>Current file name - The name of the current file (read only).</li>
</ol>
</ul>

Buttons:
<ol>
<li>Cancel : Cancel the current wizard run.</li>
<li>Next : Upload the advisor file into the Conductor for Gluent repository.</li>
</ol>

<p style="padding: 0 0 30px 0;">
</p>


### Candidate Selection Wizard - Step 2

<img src="img/s-18-2-candidateselection.png" alt="Candidate Selection Wizard Step 2 Screen" style="width:800px;height:475px;"><p>
<u>Step 2 – Select Tables</u>: 
Select one or more tables that you want to offload by clicking on the table's checkbox. Press Next to continue.

Fields:
<ol>
<li>Search : Enter any search string and press enter or hit Go. Once you have searched, you can clear the criteria by hitting the x next to the search term.</li>
</ol>

Buttons:
<ol>
<li>Left Arrow   : Return to Step 1 of the wizard. </li>
<li>Cancel       : Cancel the wizard. </li>
<li>Next : Add the selected tables to the Conductor for Gluent repository.</li>
<li>Magnifying Glass (icon)   : Allows the narrowing of the search to specific field. </li>
<li>Go   : Search for term entered in the search field. </li>
</ol>

<p style="padding: 0 0 30px 0;">
</p>


### Candidate Selection Wizard - Step 3

<img src="img/s-18-3-candidateselection.png" alt="Candidate Selection Wizard Step 3 Screen" style="width:800px;height:475px;"><p>
<u>Step 3 – Table Thresholds</u>: 
The default offload threshold will be determined from the Advisor report. The drop threshold default will be calculated using the application parameter OFFLOAD_DROP_RATIO * offload threshold. Either threshold may be updated if desired. Press Next to continue.

Fields:
<ol>
<li>Offload Threshold : For each date range partitioned table, you can enter a threshold for offloading anything older than the number of days specified. It is defaulted based on the Gluent Advisor Report.</li>
<li>Drop Threshold : For each date range partitioned table, you can enter a threshold for truncating and dropping anything older than the number of days specified. </li>
</ol>

Buttons:
<ol>
<li>Left Arrow   : Return to Step 2 of the wizard. </li>
<li>Cancel       : Cancel the wizard. </li>
<li>Next : Save the values for the table offload and drop thresholds.</li>
</ol>

<p style="padding: 0 0 30px 0;">
</p>


### Candidate Selection Wizard - Step 4

<img src="img/s-18-4-candidateselection.png" alt="Candidate Selection Wizard Step 4 Screen" style="width:800px;height:475px;"><p>
<u>Step 4 – Partition Details</u>: 
If a database link is in use, then the partition details will be automatically loaded from the database into the repository. If no connection is available, the partition details will need to be entered manually. Additionally, a column mask can be selected for numbers that represent dates. Press Finish to complete the wizard.

Fields:
<ol>
<li>Partition Granularity : The partition granularity corresponds to the Gluent Data Platform parameter --partition-granularity. See Gluent Data Platform documentation for details.</li>
<li>Column Mask : The column mask field is a dropdown box that allows selection of a mask on top of number fields when they can be interpreted as a date. </li>
</ol>

Buttons:
<ol>
<li>Left Arrow   : Return to Step 3 of the wizard. </li>
<li>Cancel       : Cancel the wizard. </li>
<li>Finish : Complete the wizard. Be sure to hit the save button if you have modified partition details.</li>
<li>Row Actions (icon) : Located in the Partition Details section, it allows rows to be added, deleted, duplicated, etc.</li>
<li>Save : Save any updates to the partition details. The button is in the Partition Details section.</li>
</ol>


## Table Review Page

<img src="img/s-17-a-tablereview.png" alt="Table Review Screen" style="width:800px;height:475px;"><p>
The table review page allows you to add a new table and view information about the tables that have been selected to offload. The following details about tables are available:

For all tables, you can:

- View chart of Frontend-Backend Space
- View chart of Frontend-Backend Rows
- View table level offload parameters

Additionally, for partitioned tables, you can:

- View and update the offload and drop threshold, as well as, the offload drop action.
- View the partition details

Fields:
<ol>
<li>Candidate Table : Select a table from the list by clicking on it.</li>
</ol>

Buttons:
<ol>
<li>Close       : Close the page and return to the database home page.</li>
<li>Add Table Wizard : Complete the wizard. Be sure to hit the save button if you have modified partition details.</li>
</ol>


### Table Level Offload Parameters Section

<img src="img/s-17-b-tableparms.png" alt="Table Review Screen" style="height:175px;"><p>
Fields:
<ol>
<li>Parameters : A report of all parameters that have been specified for the table.</li>
</ol>
Buttons:
<ol>
<li>Maintain Parameters : Pressing the button will bring up the command parameters page allowing parameters to be added at the table level. See the Command Parameters section for details on adding parameters.</li>
</ol>


### Offload and Drop Thresholds Section

<img src="img/s-17-c-thresholds.png" alt="Table Review Screen" style="height:275px;"><p>
Fields:
<ol>
<li>Table Partition Type : The frontend partitioning type. (read only)</li>
<li>Offload Threshold : Number of days for which a date range (or date masked) should be offloaded. The current date minus the number of days here, will be compared with the partition boundaries.</li>
<li>Drop Threshold : Number of days for which a date range (or date masked) should be truncated and dropped. The current date minus the number of days here, will be compared with the partition boundaries.</li>
<li>Drop Action after Offload : </li>
<ul>
<li>Use Site Default : Use the value specified at the site level in the Application Parameters page.</li>
<li>GENERATE : Generate a script to drop the offloaded partitions after an offload is completed based on Drop Threshold.</li>
<li>AUTO : Drop the offloaded partitions after a table is offload based on Drop Threshold.</li>
<li>MANUAL : Do Nothing after offload is completed.</li>
</ul>
<li>Drop Verify Level :</li>
<ul>
<li>Use Site Default : Use the value specified at the site level in the Application Parameters page.</li>
<li>COUNT    : Before dropping a partition perform a count verification of the frontend partition boundaries against both the backend and frontend. The counts must match before proceeding with a partition drop. </li>
<li>TRUST    : Trust that no modifications (DML) have been performed on the frontend or backend tables before proceeding with a partition drop. No count will be done. </li>
</ul>
</ol>

Buttons:
<ol>
<li>Save : Save any updates to the thresholds, drop action after upload, or drop verify level fields. The button is in the Offload and Drop Thresholds section.</li>
</ol>


### Partition Key Column Details Section

<img src="img/s-17-d-partition.png" alt="Table Review Screen" style="height:175px;"><p>
Fields:
<ol>
<li>Order : The column order for the partition key columns. (read only)</li>
<li>Name : The column name for the partition key columns. (read only)</li>
<li>Granularity : The partition granularity corresponds to the Gluent Data Platform parameter --partition-granularity. See Gluent Data Platform documentation for details. (read only)</li>
<li>Mask : The column mask field is a date format on top of number fields when they can be interpreted as a date. (read only)</li>
</ol>


#### Edit Partition Details Dialog

<img src="img/s-17-e-editpartition.png" alt="Table Review Screen" style="height:175px;"><p>

Fields:
<ol>
<li>Order : The column order for the partition key columns. </li>
<li>Name : The column name for the partition key columns. </li>
<li>Granularity : The partition granularity corresponds to the Gluent Data Platform parameter --partition-granularity. See Gluent Data Platform documentation for details. </li>
<li>Column Mask : The column mask field is a dropdown box that allows selection of a mask on top of number fields when they can be interpreted as a date. </li>
</ol>

Buttons:
<ol>
<li>Close  : Close the page and go back to the table review page.</li>
<li>Add Row :  Add row to the partition key columns. </li>
<li>Save :  Save the changes made to the partition details. </li>
<li>Row Actions (icon) :  It allows rows to be added, deleted, duplicated, etc.</li>
</ol>


## Add Table Wizard

To add a new table, click the Add Table Wizard button located on the table review page.

<img src="img/s-17-f-addtable1.png" alt="Add Table Wizard Screen 1" style="width:350px;height:300;"><p>
When a database link is allowed, the first page of the Add Table Wizard will have select lists for the schemas and table names. When next is hit, the partitioning information will be automatically gathered. 

<p style="padding: 0 0 30px 0;">
When no connection is allowed, you will need to manually enter the correct schema, table_name and partitioning type. 
</p>

<img src="img/s-17-g-addtable2.png" alt="Add Table Wizard Screen 2" style="width:350px;height:300;"><p>
The second page of the Add Table Wizard will be used to specify the Offload and Drop Thresholds for partition tables.

<p style="padding: 0 0 30px 0;">
No information is entered for non-partitioned tables.
</p>

<img src="img/s-17-h-addtable3.png" alt="Add Table Wizard Screen 3" style="width:350px;height:300;"><p>
The third page of the Add Table Wizard is used to specify the partition keys when no connection is allowed. Plus, date masking can be specified for cases where a string or number is used to represent a date.

No information is entered for non-partitioned tables.


# Jobs

The main page for job maintenance contains cards, each with a job on it. Jobs can be selected by clicking on the card. Clicking on the current card allows the editing of details about the job. The job steps are editable in this page. The Job Add Wizard and calendar view are available by pressing the corresponding buttons.

<img src="img/s-19-0-jobhome.png" alt="Jobs Home Screen" style="height:475;"><p>


## Job Page with No Jobs

Before adding any jobs, the screen will show No records found.
<img src="img/s-19-a-jobhome.png" alt="Jobs Home Screen" style="height:230px;"><p>
To start adding jobs, hit the Add Job Wizard button


## Add Job Wizard - Step 1

<u>Step 1: Job Name and Type</u>

The job name can be any alpha-numeric characters. The job description is a free form field. The job type is going to be Normal most of the time. Press Next to continue.

<img src="img/s-19-b-jobwizard1.png" alt="Jobs Wizard Step 1 Screen" style="width:800px;height:425;"><p>

Fields:
<ol>
<li>Job Name : An alpha-numeric name for the job with no spaces or special characters. It must be unique across all databases. </li> 
<li>Job Description : An alpha-numeric description of the job. </li> 
<li>Job Type : Normal is going to be the job type for 99% of the jobs.  A rare case calls for a Duplicate Table job type, when there are duplicate copies of tables that need to be offloaded in multiple schemas. The duplicate job type will be covered in a separate section in Appendix A.  </li>
</ol>

Buttons:
<ol>
<li>Cancel : Cancel the wizard. </li>
<li>Next : The Job will be saved when the next button is depressed, and you will go to Step 2.</li>
</ol>

<p style="padding: 0 0 30px 0;">
</p>


## Add Job Wizard - Step 2

<u>Step 2: Job Steps</u>

Select the step type. Then select the table for the step. Select if the step is enabled or disabled. All steps also have a step comment. Other fields will depend on the step type. Press Next to continue.

<img src="img/s-19-c-jobwizard2.png" alt="Jobs Wizard Step 2 Screen" style="width:800px;height:475px;"><p>

Radio Selector:
<ol>
<li>Next Action:</li>
<ul>
<li>Save below job step and proceed to scheduling - Save the job step and move to Step 3 of the wizard.</li>
<li>Save below job step and add another job step - Save the job step and stay on Step 2 of the wizard.</li>
<li>Save below job step and add parameters for it - Save the job step and go to the command parameters page to add parameters to the job step. After the command parameters page, you will be returned to Step 2 of the wizard.</li>
<li>Do not save below job step and proceed to scheduling - Do not add the job step and move to Step 3 of the wizard.</li>
</ul>
</ol>
Fields:
<ol>
<li>Step Type : </li> 
<ul>
<li> offload - offload oracle tables to backend.  </li>
<li> present - present backend table to oracle </li>
<li> sched_drop_fe_ds - drop offloaded partitions based on specified threshold </li>
<li> sched_gen_drop_fe_ds - generate the statements to drop offloaded partitions based on specified threshold </li>
</ul>
<li>Job Step Class : </li> 
<ul>
<li> ongoing - An offload which would run periodically to offload additional datasets. This job step class should be used for partition tables.</li>
<li> reset - An offload which would reset the table in the backend and re-offload the current values in the frontend. This job step class should be used for non-partitioned tables where a full refresh is done to the backend. <p><b>*** Caution:</b> <i>All backend data will be dropped. DATA LOSS WILL OCCUR if all data is not available in frontend table.</i>
</li>
</ul>
<li>Table : Table for this job step. </li>
<li>Enabled : Yes or No. </li>
<li>Job Step Comment : Any alphanumeric comment about this particular job step. </li>
</ol>

Buttons:
<ol>
<li>Left Arrow : Return to Step 1 of the wizard. </li>
<li>Cancel : Cancel the wizard. </li>
<li>Next : The actions taken when the next button is hit will depend on the Next Action radio selector. </li>
</ol>

<p style="padding: 0 0 30px 0;">
</p>


## Add Job Wizard - Step 3

<u>Step 3: Job Schedule</u>

Jobs can be scheduled on a Monthly, Weekly, Daily, or Hourly basis.  Only jobs with complete information can be enabled.

<img src="img/s-19-d-jobwizard3.png" alt="Jobs Wizard Step 3 Screen" style="height:350;"><p>

Fields:
<ol>
<li>Frequency : </li> 
<ul>
<li> Monthly - Choose the day of the month (1-28), the hour, and the minute the job should run every month. </li>
<li> Weekly - Choose the day of the week, the hour, and the minute the job should run every week. <li>
<li> Daily - Choose the hour and minute the job should run every day. </li>
<li> Hourly - Choose the minute that the job should run every hour. </li>
</ul>
<li>Enabled : Yes or No. </li>
</ol>

Buttons:
<ol>
<li>Left Arrow : Return to Step 2 of the wizard. </li>
<li>Cancel : Cancel the wizard. </li>
<li>Next : The actions taken when the next button is hit will depend on the Next Action radio selector. </li>
</ol>


## Job Page after Adding a Job

Once a job is added, a card can be seen on the page.
<img src="img/s-19-e-jobhome.png" alt="Jobs Home Screen" style="height:330;"><p>
On each card, the following details are shown:
<ul>
<li>Job Name is the title of the card.</li>
<li>Job Mode is the subtitle of the card (execute or verify).</li>
<li>Schedule is the text of the card.</li>
<li>Job Comment is the sub-text of the card.</li>
<li>Enabled/Disabled</li>
<ul>
<li>Enabled jobs will have a Blue circular play icon.</li>
<li>Disabled jobs will have a gray circular pause icon.</li>
</ul>
</ul>


## Job Page with a Job Selected

Clicking on the card, will show the details of the job.
<img src="img/s-19-f-jobhome.png" alt="Jobs Home Screen" style="width:800px;height:475px;"><p>
The currently selected card will have a green border around it. The jobs steps will appear below the job cards section, along with parameters for the currently selected job step. Additionally, the notifications for the job will be shown last in a collapsible section (click the arrow to collapse or expand the section).


### Edit Job Details

Clicking on the currently selected card, will bring up the dialog to edit the job details.
<img src="img/s-19-g-editjob.png" alt="Edit Job Screen" style="height:475px;"><p>

Fields:
<ol>
<li>Job Name : Name of the job can be any alpha numeric characters. No spaces or special characters.</li>
<li>Job Description : Any alpha numeric characters describing the job.</li>
<li>Frequency : </li> 
<ul>
<li> Monthly - Choose the day of the month (1-28), the hour, and the minute the job should run every month. </li>
<li> Weekly - Choose the day of the week, the hour, and the minute the job should run every week. <li>
<li> Daily - Choose the hour and minute the job should run every day. </li>
<li> Hourly - Choose the minute that the job should run every hour. </li>
</ul>
<li>Enabled : Yes or No. </li>
<li>Job Mode :
<ul>
<li>Execute - to execute the job fully. </li>
<li>Verify - to run the job to verify the parameters but not actually offload any data.</li>
</ul>
<li>Job Type : Normal is going to be the job type for 99% of the jobs.  A rare case calls for a Duplicate Table job type, when there are duplicate copies of tables that need to be offloaded in multiple schemas. The duplicate job type will be covered in a separate section in Appendix A.  </li>
</ol>

Buttons:
<ol>
<li>Cancel : Cancel the dialog. </li>
<li>Delete : Delete the job if there are no job steps. </li>
<li>Save : Save the changes to the job. </li>
</ol>


### Job Steps Section

In the Job Steps section, you can directly edit the job step fields. The parameters for the job step can be added, updated, or deleted by clicking on the step's maintain link.
<img src="img/s-19-j-jobsteps.png" alt="Edit Job Steps" style="height:150px;"><p>
Fields:
<ol>
<li>Step# : A numeric value to order the steps for execution. </li>
<li>Table Id : The table for this step. </li>
<li>Job Step Class : </li> 
<ul>
<li> ongoing - An offload which would run periodically to offload additional datasets. This job step class should be used for partition tables.</li>
<li> reset - An offload which would reset the table in the backend and re-offload the current values in the frontend. This job step class should be used for non-partitioned tables where a full refresh is done to the backend. <p><b>*** Caution:</b> <i>All backend data will be dropped. DATA LOSS WILL OCCUR if all data is not available in frontend table.</i>
</li>
</ul>
<li>Step Type : </li> 
<ul>
<li> offload - offload oracle tables to backend.  </li>
<li> present - present backend table to oracle </li>
<li> sched_drop_fe_ds - drop offloaded partitions based on specified threshold </li>
<li> sched_gen_drop_fe_ds - generate the statements to drop offloaded partitions based on specified threshold </li>
</ul>
<li>Enabled : Yes or No. </li>
<li>Job Step Comment : Any alphanumeric comment about this particular job step. </li>
<li>Backend Table : Only used for present commands. </li>
<li>Offload Specification : The value can be used for some specialized offload methods:</li>
<ul>
<li>
Retention based on # partitions: Specify a "P" with a number, and Conductor will offload partitions beyond the number specified. e.g., if 6 is specified and there are 12 partitions, Conductor will specify a "--less-than-value" parameter that results in partitions 7-12 being offloaded (if they have not been offloaded already).
</li>
<li>
Specific --less-than-value: Specify a "L" with a value, and Conductor will supply the value in the --less-than-value parameter when offloading.
</li>
</ul>
<li>Parameters : Link to maintain parameters for the job step. </li>
</ol>

Links:
<ol>
<li>Maintain : Pressing the button will bring up the command parameters page allowing parameters to be added at the job step level. See the Command Parameters section for details on adding parameters.</li>
</ol>

Buttons:
<ol>
<li>Cancel : Cancel the dialog. </li>
<li>Delete : Delete the job if there are no job steps. </li>
<li>Save : Save the changes to the job. </li>
</ol>


## Future Job Calendar

Displays jobs that will run based on their projected schedule in a calendar view.
<img src="img/s-19-z-futurecalendar.png" alt="Jobs Future Calendar Screen" style="width:800px;height:475px;"><p>

Buttons:
<ol>
<li>Close : Close the dialog. </li>
<li>Left Arrow (icon) : Move backward by month. </li>
<li>Right Arrow (icon) : Move forward by month. </li>
<li>Today : Go to Today on the calendar. </li>
<li>Month : Month view. </li>
<li>Week : Week view. </li>
<li>Day : Day view. </li>
<li>List : View as a list. </li>
</ol>


# Dashboard

The dashboard allows for monitoring of jobs.
<img src="img/s-20-a-dashboard.png" alt="Dashboard Screen" style="width:800px;height:475px;"><p>

<u>Job States</u>: The donut graph shows a summary by state of the jobs. The state pieces can be clicked on to drill down into the run job details.

<u>Recent Jobs</u>: The 10 most recent jobs. Drilldown to the run job details by clicking on the job id. Also, the job name can be selected to drill down to the job details.

Fields:
<ol>
<li>Auto-Refresh Interval : Dropdown allowing a selection to set an auto-refresh interval. </li>
</ol>

Buttons:
<ol>
<li>Close : Close the page. Takes you back to the Database Home. </li>
<li>Refresh : Refresh the page manually. </li>
<li>Calendar (icon) : Opens the job calendar dialog. </li>
</ol>

Links:
<ol>
<li>Piece of Job State Donut : Pressing one of the state pieces will bring up the run job details page for all jobs with the state. </li>
<li>Job Id : Pressing the link will bring up the run job details page for the job with that job id and with that job state. </li>
<li>Job Name : Pressing the link will take you to the job maintenance page. </li>
</ol>


## Job Calendar

Displays jobs that have run in a calendar view.
<img src="img/s-20-c-calendar.png" alt="Jobs Future Calendar Screen" style="width:800px;height:475px;"><p>
Hovering on a job will show the start and end time for the job. Clicking on the job will bring up the run job details page for the job id.

Buttons:
<ol>
<li>Close : Close the dialog. </li>
<li>Left Arrow (icon) : Move backward by month. </li>
<li>Right Arrow (icon) : Move forward by month. </li>
<li>Today : Go to Today on the calendar. </li>
<li>Month : Month view. </li>
<li>Week : Week view. </li>
<li>Day : Day view. </li>
<li>List : View as a list. </li>
</ol>


# Run Job Details

The run job details page shows the details of a run job. 
<img src="img/s-21-a-runjobs.png" alt="Run Job Details Screen" style="width:800px;height:475px;"><p>


## Sections


Sections:
<ol>
<li>Run Jobs : Run job level details. </li>
<li>Run Job Steps : Details on each run job step. </li>
<li>Command Details : Commands are those job steps executing an actual Gluent Data Platform command. </li>
</ol>


#### Run Jobs Section

Fields:
<ol>
<li>Id - internal job id (read only)</li>
<li>Job Name (read only)</li>
<li>Job Mode (read only)</li>
<li>Run Job State - dropdown to allow a job in error state to be aborted, resumed, or restarted. [Only if run job in ERROR state]</li>
<li>Start Timestamp (read only)</li>
<li>Finish Timestamp (read only)</li>
<li>Description (read only)</li>
</ol>

Buttons:
<ol>
<li>Refresh (icon) : Refresh the section. </li>
<li>Save : Save change to Run Job State field. [Only if run job in ERROR state] </li>
</ol>


#### Run Job Steps Section

Fields:
<ol>
<li># - internal step number (read only)</li>
<li>State - internal run job state (read only)</li>
<li>Step Type (read only)</li>
<li>Step Table</li>
<li>Job Step Offload Spec - internal offload specification details (read only)</li>
</ol>

Buttons:
<ol>
<li>Refresh (icon) : Refresh the section. </li>
</ol>


#### Command Details Section

Fields:
<ol>
<li>Id - internal command id (read only)</li>
<li>Start Timestamp (read only)</li>
<li>Finish Timestamp (read only)</li>
<li>Status (read only)</li>
<li>Status Details (read only)</li>
<li>Log File Name - Gluent Data Platform log file name (read only)</li>
</ol>

Buttons:
<ol>
<li>Refresh (icon) : Refresh the section. </li>
</ol>


## Handling a Job in Error State

A job can be updated from error state on the run job details page. The run job details page can be accessed by:
<ol>
<li> Clicking on the job_id link for a job in error state from the Recent Jobs list.
<img src="img/s-22-a-job-list.png" alt="Job in Error" style="width:200px;height:125px;"><p>
</li>
<li> Selecting one or more jobs in error state by selecting the Error donut piece.
<img src="img/s-22-a-error-donut.png" alt="Error Donut" style="width:200px;height:175px;"><p>
</li>
</ol>


Once the job is up in the run job details page, double-click on the Run Job State field.

<img src="img/s-22-c-jobstate-field.png" alt="Job State Field" style="width:200px;height:100;"><p>

This will allow access to the dropdown list to handle the job. The options shown will be:

<img src="img/s-22-d-jobstate-dropdown.png" alt="Job State Dropdown" style="width:200px;height:125px;"><p>

Here is what each option will do:

<ol>
<li>
Abort the Job Run - Change the state of the job to aborted. The run job cannot be resumed or started once this is done. The job will run from the beginning on the next scheduled run.
</li>
<li>
ERROR in Job Run - Leave the job in error state. A job in error state will not run on its next scheduled date/time.
</li>
<li>
Resume the Job - Job will run at the start of the next minute. The job will resume where it left off with the same job settings as when the job started. This option would be used when job was affected by outside forces. For example, a network outage caused the job to fail because it could not connect to the backend.
</li>
<li>
Rewrite the Job File and Resume the Job - Job will run at the start of the next minute. Before resuming where it left off, the job will rewrite the job file to pick up any changes to job parameters or other job step information that has been updated. This option would be used in cases where an additional parameter is needed or something else about the job was specified incorrectly.
</li>
</ol>

# Command Parameters

Command parameters are Gluent Data Platform parameters that can be specified to be used by offload or present commands executed by Conductor for Gluent.  They can be specified at different levels of operation:

<ul>
<li> Site Level - Parameters will be used for every offload or present command executed across all the databases.  </li>
<li> Database Level - Parameters will be used for every offload or present command executed for that specific database.  </li>
<li> Table Level - Parameters will be used for every offload or present command executed for that specific table.  </li>
<li> Job Step Level - Parameters will be used for every offload or present command executed for that specific job step.  </li>
</ul>

<img src="img/s-02-a-siteoffload.png" alt="Site Level Offload Screen" style="width:800px;height:475px;"><p>

In the above example screen, the command parameters are being maintained for offload commands at the site level.


## Add Command Parameter

Here is the flow of adding a parameter.


#### Before adding a parameter to a job step

<img src="img/s-02-a-addparm-before.png" alt="Job Step Level Parm Before Screen" style="width:800px;height:200;"><p>
Hit the Add Parameter button.


#### Add Parameter: Initial Screen

<img src="img/s-02-b-addparm-blank.png" alt="Job Step Level Parm Before Screen" style="width:800px;height:350px;"><p>
Click on the dropdown


#### Add Parameter: Dropdown list

<img src="img/s-02-c-addparm-dropdown.png" alt="Job Step Level Parm Before Screen" style="width:800px;height:350px;"><p>
Select a parameter from the dropdown list.


#### Add Parameter: Specify value

<img src="img/s-02-d-addparm-value.png" alt="Job Step Level Parm Before Screen" style="width:800px;height:350px;"><p>
If the parameter requires a value, that is entered and then hit Add button.


#### After adding a parameter to a job step

<img src="img/s-02-e-addparm-after.png" alt="Job Step Level Parm Before Screen" style="width:800px;height:225px;"><p>
Once the parameter is added, it will show up in the report for that job step.


# Job Notifications

The implementation of notifications is different than that of parameters. It is not an accumulation but an override system:

<ol>
<li>Job Level - Job notifications override any notifications at the database or site level. </li>
<li>Database Level - Database level notification will be used when there are no notifications set at the job level.</li>
<li>Site Level - Values entered at the site level will be used when there are no notifications at the database level and at the job level.  </li>
</ol>

Notifications are sent at the following points of a job:

<ol>
<li> When Job Begins</li>
<li> When Job Succeeds</li>
<li> If Job has an Error</li>
</ol>

Notifications can be enabled and disabled.

<img src="img/s-04-a-jobnotifications.png" alt="Site Level Notifications Screen" style="width:800px;height:475px;"><p>

Fields:
<ol>
<li>Email Addresses for Notifications when Job Begins </li>
<li>Enabled toggle for Notifications when Job Begins </li>
<li>Email Addresses for Notifications when Job Succeeds </li>
<li>Enabled toggle for Notifications when Job Succeeds </li>
<li>Email Addresses for Notifications if Job has an Error </li>
<li>Enabled toggle for Notifications if Job has an Error </li>
</ol>

Buttons:
<ol>
<li>Close - Close the dialog.  </li>
<li>Delete - Delete the notifications.  </li>
<li>Save - Save any changes made to the notifications.  </li>
</ol>


# Application Defaults

<img src="img/s-05-a-appparms.png" alt="Application Parameters Screen" style="width:800px;"><p>
The application defaults are parameters that affect the way the Conductor for Gluent functions. Here is a list of the parameters and how they work:

- CREATE_BACKEND_DB – Controls whether the parameter –create-backend-db will be included on offload commands. If the backend system allows the gluent user to create databases, then it should be set to YES. If the backend system does not allow the gluent user to create databases, then set to NO. 
- DROP_VERIFY_EXPIRY – (for future use)
- DROP_VERIFY_LEVEL – Controls the default value for the DROP_VERIFY_LEVEL on tables.
<ul>
<li>COUNT    : Before dropping a partition perform a count verification of the frontend partition boundaries against both the backend and frontend. The counts must match before proceeding with a partition drop. </li>
<li>TRUST    : Trust that no modifications (DML) have been performed on the frontend or backend tables before proceeding with a partition drop. No count will be done. </li>
</ul>
The DROP_VERIFY_LEVEL can be over-ridden at the table level.
- JOB_LAUNCH_INTERVAL – Controls the granularity of the drop down for minutes in the job scheduler. If set to 1, you can specify any minute of the hour (0-59). If you specify 15, you can specify 0, 15, 30, 45. 
- OFFLOAD_DROP_RATIO – Controls the default value for the DROP_THRESHOLD on tables. The value in this field will be multiplied with the OFFLOAD_THRESHOLD to determine the default for the DROP_THRESHOLD. 
- OFFLOAD_DROP_ACTION – This is the site-wide default for whether an offload job step should attempt to
<ul>
<li>GENERATE : Generate a script to drop the offloaded partitions after an offload is completed based on Drop Threshold.</li>
<li>AUTO     : Drop the offloaded partitions after a table is offload based on Drop Threshold.</li>
<li>MANUAL   : Do Nothing after offload is completed.</li>
</ul>
The OFFLOAD_DROP_ACTION can be over-ridden at the table level.

Double-click in the Value field to edit the parameter value.


# Appendix A


## Duplicate Table Job

When there are duplicate copies of tables that need to be offloaded in multiple schemas. An example of this would be if a company had a schema per client with the same tables under each schema. 

A Duplicate Table Job is added through the <i>Add Job Wizard</i>, however, only step 1 is entered. After completing step 1, you will be taken back to the main job maintenance page. Once you select the job, you can start adding elements to the configuration. The different types of elements in a configuration are:

<ol>
<li>Duplicate</li>
<ul>
<li>Enter duplicate table details.</li><li>Only a table name is specified (no schema/owner), as there are multiple duplicate tables across the database</li><li> The duplicate element will look for the specified table name across all schemas in the database.</li>
</ul>
<li>Include</li>
<ul>
<li>Enter the details for a specific table that should be included in the job.</li><li>Enter a full table name with owner/schema and table names specified.</li>
</ul>
<li>Exclude</li>
<ul>
<li>Enter the details for a specific table that should be excluded in the job.</li><li>Enter a full table name with owner/schema and table names specified.</li>
</ul>
</ol>

<u>Example</u><p>
A call center company has one schema for each client that they service through their call center. Under each of those client schemas, they have a CALL_DETAILS table which needs to be offload. In addition, they have a training schema, which has a CALL_DETAILS table that should not be offloaded. The configuration elements for this scenario are:

<ul>
<li>Duplicate, CALL_DETAILS</li>
<li>Exclude, TRAINING.CALL_DETAILS</li>
</ul>

<p style="padding: 0 0 30px 0;">
This will result in a job being generated based on the frequency desired that will have all the CALL_DETAILS tables except the one from the TRAINING schema. 
</p>

