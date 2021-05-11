title: Release Notes

# 2.2.12

- Table dropdown only shows tables from selected DB
- Now able to add parameters at table level
- Key column specification can be edited
- Transfer details are being gathered on offload
- Incrmental improvements:
	- error handling
	- wording on a few frontend screens
	- updated charts

### Upgrade Instructions

- cd {C4G_INSTALLATION_LOCATION}
- tar --overwrite -xpf conductor_for_gluent-2.2.11.tar.bz2
- export TNS_ADMIN={C4G_INSTALLATION_LOCATION}/tns
- sqlplus /@{C4G_REPOSITORY_SERVICE_NAME}
	- @install/c4g-update-schema-2.2.12.sql
	- @install/c4g-apex-application.sql
	- @install/c4g-setup-source.sql

# 2.2.11

- Corrected sizing calculation with Oracle, Hadoop, Elgible, Dropped bars on all charts
- Table names will now only show for current database instead of all databases
- Corrected query sort order on Bytes Comparison and Space Recovery charts on the dashboard
- Corrected problem in output from the get_col_spec_details procedure
- Corrected issue with offload details not being collected
- Incremental improvements to the frontend, including:
	- Color conisistency for charts
	- Column sort available on dataset (partition) reports
	- Auto-refresh on dashboard
	- Percent completion on job list

### Upgrade Instructions

- cd {C4G_INSTALLATION_LOCATION}
- tar --overwrite -xpf conductor_for_gluent-2.2.11.tar.bz2
- export TNS_ADMIN={C4G_INSTALLATION_LOCATION}/tns
- sqlplus /@{C4G_REPOSITORY_SERVICE_NAME}
	- @install/c4g-update-schema-2.2.11.sql
	- @install/c4g-apex-application.sql
	- @install/c4g-setup-source.sql

# 2.2.10

- Change to directory/file structure and naming:
	- gui renamed to install
	- all templates for files have been placed in a templates subdirectory in respective location for consistency
- Corrected issue where column partitioning information was not being gathered on a duplicate job types
- Incremental improvements to the frontend

### Upgrade Instructions

- cd {C4G_INSTALLATION_LOCATION}/..
- mv {C4G_INSTALLATION_LOCATION} {C4G_INSTALLATION_LOCATION}.`date +"%Y%m%d"`
- tar -xpf conductor_for_gluent-2.2.10.tar.bz2
- cp {C4G_INSTALLATION_LOCATION}.`date/tns/*.ora {C4G_INSTALLATION_LOCATION}.`date/tns/.
- cp {C4G_INSTALLATION_LOCATION}.`date/tns/*wallet* {C4G_INSTALLATION_LOCATION}.`date/tns/.
- cp {C4G_INSTALLATION_LOCATION}.`date/env/*.env {C4G_INSTALLATION_LOCATION}.`date/env/.
- export TNS_ADMIN={C4G_INSTALLATION_LOCATION}/tns
- sqlplus /@{C4G_REPOSITORY_SERVICE_NAME}
	- @install/c4g-apex-application.sql
	- @install/c4g-setup-source.sql

# 2.2.9

- Changes to database interaction to have it be a co-process (only connect once to database)

### Upgrade Instructions

- cd {C4G_INSTALLATION_LOCATION}
- tar -xf conductor_for_gluent-upgrade-2.2.9.tar.bz2
- sqlplus conductor_for_gluent/{password}@{C4G_REPOSITORY_SERVICE_NAME}
- @gui/c4g-apex-application.sql
- @gui/c4g-setup-source.sql

# 2.2.8

- Optimization of some SQL calls
- Improvements in help text

### Upgrade Instructions

- cd {C4G_INSTALLATION_LOCATION}
- tar -xf conductor_for_gluent-upgrade-2.2.8.tar.bz2
- sqlplus conductor_for_gluent/{password}@{C4G_REPOSITORY_SERVICE_NAME}
- @gui/c4g-apex-application.sql
- @gui/c4g-setup-source.sql
- @gui/c4g-setup-helptext.sql

# 2.2.7

- Changed DB Details Apex screen to handle loopback connection for DB LINK
- Changed Incremental Update Flag from a selection dropdown to an autocomplete text field
- Fixed issue with database level parameters not being included in offload/present commands
- Reduced length of variable name to less than 30 characters
- Corrected issue with job not exiting on error in certain cases

### Upgrade Instructions

- cd {C4G_INSTALLATION_LOCATION}
- tar -xf conductor_for_gluent-upgrade-2.2.7.tar.bz2
- sqlplus conductor_for_gluent/{password}@{C4G_REPOSITORY_SERVICE_NAME}
- @gui/c4g-apex-application.sql
- @gui/c4g-setup-source.sql

----------

# 2.2.6

- Add license/copyright info

----------

# 2.2.5

- Corrected command parameters, so they take into account gluent version at DB, Table and Job Step levels
- Add feature to limit cmd parameters that show at Site and DB levels that do not make sense (e.g. ones that specify columns)
- Command parameters are available for Gluent versions 2.11 - 3.4
- launch-guent-job updated so it will only attempt to launch jobs for it's database install
- Continued improvement the processing when recording information about Oracle and Hadoop Datasets
- Improvements to debug mode and logging

----------

# 2.2.3

- Incremental improvment in the processing details about Oracle Datasets

----------

# 2.2.2

- Lengthen columns from 30 to 128 for long naming support
- Correct issue in calendar
- GUI improvements

----------

# 2.2.1

- Renamed table and associated objects to get the length of them to fit in 30 characters.

----------

# 2.2.0

- Ability to add a new table adhawk rather than uploading an advisor report
- Column making works on char/varchar2 data types
- A generate drop statements or actual drop statements can be scheduled as a job step for partition maintenance of offloaded table data based on a Drop Threshold.
- GENERATE option added to OFFLOAD_DROP_ACTION application parameter to generate drop partition statements but not run them.
- Added column to Oracle Dataset Report that shows which partitions are eligible for dropping
- Metrics added on the Site Home and Database Home screens

### Known Issues

- Composite Partitions Keys do not work properly for the partition maintenance features.

----------

# 2.1.3

- Template Files updated to correctly reflect the changes in environment variables in release 2.1.0
- Help Text installation is working without manual intervention
- Documentation Website added - https://swnerd.github.io/c4g-doc/

