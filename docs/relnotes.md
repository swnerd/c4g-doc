title: Release Notes

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

