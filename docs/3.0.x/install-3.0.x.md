title: Installation

# Front End Installation

The frontend installation should be done anytime the central Conductor for Gluent repository will be used along with the Conductor for Gluent Apex application. If using the Conductor for Gluent in the standalone mode, please skip down to the backend installation section.

## Prerequisites
<ul>
<li>Gluent Data Platform 4.1.0+ Installed</li>
<li>Oracle 12.2+ Database (created with DBCA or Manually) <sup>1</sup></li>
<li>Oracle Apex 20.2+<sup>2</sup></li>
</ul>
<u>Note 1: </u>: <i>Apex requires that Oracle Text and JVM options be installed.  No other options are required.</i>

<u>Note 2: </u>: <i>Apex and Conductor for Gluent should be installed into the container database, so be sure to run the alter session command to set the container, e.g. ALTER SESSION SET CONTAINER = XEPDB1. </i>


## Apex 20.2 Setup
Create Tablespace for Apex (if one does not exist)

    SQL>  -- Create Tablespace for Apex - Example
    create tablespace tbs_apex datafile '/opt/oracle/oradata/XE/XEPDB1/tbs_apex01.dbf' size 100m autoextend on maxsize 1000m;

### Copy Apex 20.2 and ORDS to database host
Example Copy to Oracle User Home

    scp apex_20.2_en.zip {oracle user}@{db host}:.
    scp ords-20.4.1.013.1644.zip {oracle user}@{db host}:.

### Remove Existing Apex Software 
Remove Apex from database (if necessary)

    cd $ORACLE_HOME/apex
    
    sqlplus / as sysdba
    
    SQL> -- Disable existing
    EXEC DBMS_XDB.SETHTTPPORT(0);
    SQL> 
    SQL> -- Remove Apex
    @apxremov.sql
    
    PL/SQL procedure successfully completed.
    ... ... ... ...
    ...Application Express Removed
    
    ********************************************************************
    ** You must exit this SQL*Plus session before running apexins.sql **
    ********************************************************************
    SQL> exit

Move original apex software out of the way

    cd $ORACLE_HOME
    mv apex apex.orig
     
### Install Apex
#### Unzip Apex 20.2 software 
example statement if uploaded to user's home directory:

    cd $ORACLE_HOME
    unzip ~/apex_20.2_en.zip
    
#### Install Apex 20.2 in database

    cd $ORACLE_HOME/apex
    sqlplus / as sysdba
    
    SQL> -- Runtime install with 4 parms (apex tbs, apex tbs, temp tbs, image loc)
    @apxrtins.sql tbs_apex tbs_apex temp /i/
    ...set_appun.sql
    
    PL/SQL procedure successfully completed.
    
    ...set_ufrom_and_upgrade.sql
    
    PL/SQL procedure successfully completed.
    
        ... ... ... ... ... ... ... ... ... ...
    
    Thank you for installing Oracle Application Express 20.2.0.00.20
    
    Oracle Application Express is installed in the APEX_200200 schema.
    
    The structure of the link to the Application Express administration services is as follows:
    http://host:port/ords/apex_admin
    
    The structure of the link to the Application Express development interface is as follows:
    http://host:port/ords
    
    timing for: Phase 3 (Switch)
    Elapsed: 00:00:49.96
    timing for: Complete Installation
    Elapsed: 00:06:57.48
    
    PL/SQL procedure successfully completed.
    


#### Change / Setup Apex Administrator

    cd $ORACLE_HOME/apex
    sqlplus / as sysdba
    SQL> -- no parameters
    @apxchpwd.sql
    ...set_appun.sql
    ================================================================================
    This script can be used to change the password of an Application Express
    instance administrator. If the user does not yet exist, a user record will be
    created.
    ================================================================================
    Enter the administrator's username [ADMIN]
    User "ADMIN" does not yet exist and will be created.
    Enter ADMIN's email [ADMIN]
    Enter ADMIN's password []
    Created instance administrator ADMIN.

#### Apex Rest Configuration

    cd $ORACLE_HOME/apex
    sqlplus / as sysdba
    SQL> -- no parameters
    @apex_rest_config.sql

    PL/SQL procedure successfully completed.

        ... ... ... ... ... ... ... ... ... ...

    Session altered.

    PL/SQL procedure successfully completed.

    PL/SQL procedure successfully completed.

#### ORDS

    cd $ORACLE_HOME
    mkdir apex-ords
    cd apex-ords
    unzip ~/ords-20.4.1.013.1644.zip
    cp -r $ORACLE_HOME/apex/images $ORACLE_HOME/apex-ords/.

Sample Installation;

    java -jar ords.war install advanced
    Specify the database connection type to use.
    Enter number for [1] Basic  [2] TNS  [3] Custom URL [1]:
    Enter the name of the database server [localhost]:
    Enter the database listen port [1521]:
    Enter 1 to specify the database service name, or 2 to specify the database SID [1]:
    Enter the database service name:xepdb1
    Enter 1 if you want to verify/install Oracle REST Data Services schema or 2 to skip this step [1]:
    Enter the database password for ORDS_PUBLIC_USER:
    Confirm password:
    Requires to login with administrator privileges to verify Oracle REST Data Services schema.
    
    Enter the administrator username:sys
    Enter the database password for SYS AS SYSDBA:
    Confirm password:
    Connecting to database user: SYS AS SYSDBA url: jdbc:oracle:thin:@//localhost:1521/xepdb1
    
    Retrieving information.
    Enter the default tablespace for ORDS_METADATA [SYSAUX]:tbs_apex
    Enter the temporary tablespace for ORDS_METADATA [TEMP]:
    Enter the default tablespace for ORDS_PUBLIC_USER [SYSAUX]:tbs_apex
    Enter the temporary tablespace for ORDS_PUBLIC_USER [TEMP]:
    Enter 1 if you want to use PL/SQL Gateway or 2 to skip this step.
    If using Oracle Application Express or migrating from mod_plsql then you must enter 1 [1]:
    Enter the PL/SQL Gateway database user name [APEX_PUBLIC_USER]:
    Enter the database password for APEX_PUBLIC_USER:
    Confirm password:
    Enter 1 to specify passwords for Application Express RESTful Services database users (APEX_LISTENER, APEX_REST_PUBLIC_USER) or 2 to skip this step [1]:
    Enter the database password for APEX_LISTENER:
    Confirm password:
    Enter the database password for APEX_REST_PUBLIC_USER:
    Confirm password:
    Enter a number to select a feature to enable:
       [1] SQL Developer Web  (Enables all features)
       [2] REST Enabled SQL
       [3] Database API
       [4] REST Enabled SQL and Database API
       [5] None
    Choose [1]:4
    2021-03-02T01:24:34.126Z INFO        reloaded pools: []
    Installing Oracle REST Data Services version 20.4.1.r0131644
    ... Log file written to /home/oracle/ords_install_core_2021-03-02_012434_00269.log
    ... Verified database prerequisites
    ... Created Oracle REST Data Services proxy user
    Warning: Nashorn engine is planned to be removed from a future JDK release
    ... Created Oracle REST Data Services schema
    ... Granted privileges to Oracle REST Data Services
    ... Created Oracle REST Data Services database objects
    ... Log file written to /home/oracle/ords_install_datamodel_2021-03-02_012445_00226.log
    ... Log file written to /home/oracle/ords_install_apex_2021-03-02_012446_00038.log
    Completed installation for Oracle REST Data Services version 20.4.1.r0131644. Elapsed time: 00:00:12.8

Starting ORDS in Standalone mode:

    java -jar ords.war standalone

## Schema Install
### Create Tablespace
Create tablespace to contain the conductor_for_gluent's repository, for example:

    create tablespace tbs_c4g datafile '+dg_data' size 100M autoextend on next 1M maxsize 100M;

or

    create tablespace tbs_c4g datafile '/u01/app/oracle/oradata/testinst/tbs_c4g01.dbf' size 100M autoextend on next 1M maxsize 1000M;

###Create User and Privileges
Create user conductor_for_gluent with above tablespace as the default tablespace, for example:

    create user conductor_for_gluent identified by "{complex password}" 
    default tablespace tbs_c4g;
    alter user conductor_for_gluent quota unlimited on tbs_c4g;
    grant connect to conductor_for_gluent;
    grant resource to conductor_for_gluent;
    grant create database link to conductor_for_gluent;
    grant create synonym to conductor_for_gluent;
    grant create view to conductor_for_gluent;
    grant select any dictionary to conductor_for_gluent;
    grant select any table to conductor_for_gluent;

### Install and Setup the Objects
The installation SQL scripts are located in <i>install</i> directory where the backend scripts were installed (usually <code>/u01/app/gluent/scripts</code> or <code>/u01/app/gluent/c4g-scripts</code>.  From this directory connect to the apex database (usually <i>c4g_central</i> is the tns name to use:

You can set your environment to use the `tnsnames.ora` file you created during the backend setup. For example:

    cd /u01/app/gluent/c4g-scripts/tns
    export TNS_ADMIN=`pwd`
    cd ../install
    sqlplus /@c4g_central

#### Schema Setup
Run the sql, no parameters - 1 prompt for tablespace

    spool c4g-setup-schema.log
    @c4g-setup-schema.sql
    Tablespace: tbs_c4g
    spool off

#### Source Setup
Run the sql, no parameters

    spool c4g-setup-source.log
    @c4g-setup-source.sql
    spool off

#### Seed Data Setup
Run the sql, no parameters

    spool c4g-setup-seeddata.log
    @c4g-setup-seeddata.sql
    spool off

#### Help Text Setup
Run the sql, no parameters

    spool c4g-setup-helptext.log
    @c4g-setup-helptext.sql
    spool off

## Apex Application Install

    cd /u01/app/gluent/c4g-scripts/tns
    export TNS_ADMIN=`pwd`
    cd ../install
    sqlplus system/{complex_password}@c4g_central

### Create the Workspace

    SQL> -- run the sql, no parameters
    @c4g-apex-workspace.sql


### "Import" the runtime app (sql script)

    SQL> -- run the sql, no parameters
    @c4g-apex-application.sql


## Connecting to Conductor for Gluent

    http://{hostname}:8080/apex/f?p=100:LOGIN_DESKTOP:25119307751525:::::

Default Users
Admin User: c4g_admin
App User: c4g_user

Please contact your Conductor for Gluent provider for password.
 

# Backend Software Installations

## Conductor for Gluent Backend Software Usage Options
The Conductor for Gluent Backend (evolved from AEG Gluent Toolkit) has three possible modes of operation:

<ol>
<li>Standalone mode</li>
<li>Local repository mode</li>
<li>Full Conductor for Gluent Front-end and Back-end with Central Repository</li>
</ol>

The standalone and local repository modes of operation have been around and used in production environments for several years (initial deployment to a production environment in Q1 2017).  Enhancements have been done over the subsequent time period, including the local repository mode.  The central repository integration with Conductor for Gluent frontend was done in 2019.

### Standalone
No additional software is needed or required.  The software just provides a consistent job-oriented method for running gluent offloads.  Jobs are setup through flat "job" files.  Scheduling of the individual jobs requires a cron entry per job.

### Standalone with local repository
Same as standalone.  Additionally, some result information is stored in tables under the gluent_adm schema, such as, tables offloaded, job success, when possible some information on bytes transferred.

### Full Conductor for Gluent with Central Repository
Jobs are configured and scheduled through the front-end software.  A single cron job is required to handle the launching of jobs based on schedule in the central repository.  All information gathered about the job success, partitions offloaded, etc is stored in the central repository.

## Prerequisites
<ul>
<li>Gluent Data Platform 4.1.0+ Installed</li>
<li>Central Repository Database Installed (see C4G Frontend Setup Guide)</li>
</ul>

## Unpack Software
A tar file will be supplied.  The tar file should be unpacked in a directory such as, c4g-scripts or scripts or similar.  For example:

    cd /u01/app/gluent
    mkdir c4g-scripts
    cd c4g-scripts
    tar xf {tar file name}

## Environment File Setup
> <u>Note on split configuration</u>: <i>If gluent is setup in a split configuration, then certain scripts will not function, and certain variables are not set in the environment files.  </i>

### conductor_for_gluent.env
A template for the conductor_for_gluent.env file can be found under the env/templates directory - it is recommended that you copy the template file as a starting point.

<ul>
<li>PATH - This export of the path is to make sure the oraenv script is in the path.</li>
<li>ORACLE_SID - Set this to the Oracle SID of the database which is being offloaded.</li>
<li>ORAENV_ASK - Set for no prompts.</li>
<li>oraenv - script to set the oracle environment.</li>
<li>Unset ORAENV_ASK</li>
<li>As this shell script runs SQL, the SQL_PATH variable is unset, so as not to get possible interference (same name scripts, login.sql files, etc).</li>
<li>OFFLOAD_HOME="/u01/app/gluent/offload" - Update OFFLOAD_HOME to the location of the gluent software offload home.</li>
<li>. $OFFLOAD_HOME/conf/offload.env - DO NOT CHANGE</li>
<li>C4G_REPO</li>
<ul>
<li>NONE - No Repository; standalone mode without a repository</li>
<li>RUNTIME- run a local repository that stores information generated a runtime</li>
<li>FULL - run a central repository that stores information about jobs, schedules, etc.</li>
</ul>
<li>G_ERROR_WORDS - Words and phrases used when determining if a possible error occurred.</li>
<li>TNS_ADMIN - Always set to ${tnsdir} - DO NOT CHANGE</li>
<li>AEG_GLUENT_REPO_SERVICE - service name to be used when connecting to the central repository</li>
<li>AEG_GLUENT_LOCAL_SERVICE - service name to be used when connecting to the local database</li>
<li>dstr - service name used in local repository and standalone mode</li>
</ul>

### run-gluent-job.env
A template for the file can be found under the env/templates directory - it is recommended that you copy the template file as a starting point.

<ul>
<li> PRECREATED_DBS - true or false (defaults to false)  Only add/update if gluent is not allowed to create databases on impala</li>
<li> G_BEGIN_NOTIFY - true or false</li>
<li> G_BEGIN_MAIL_LIST - email addresses space separated in quotes.</li>
<li> G_SUCCESS_NOTIFY - true or false</li>
<li> G_SUCCESS_MAIL_LIST - email addresses space separated in quotes.</li>
<li> G_ERROR_NOTIFY -true or false</li>
<li> G_ERROR_MAIL_LIST - email addresses space separated in quotes.</li>
</ul>

### setup-wallet.env
A template for the file can be found under the env/templates directory - it is recommended that you copy the template file as a starting point.

<ul>
<li>AEG_WALLET_LOCATION=/u01/app/gluent/scripts/tns - update to the location to contain the wallet
</ul>

## Configuration File Setup
If not running in the Central Repository mode, then 2 configuration files can be created to set default offload and present parameters.  

<ul>
<li>offload-defaults.cfg</li>
<li>present-defaults.cfg</li>
</ul>

## User Setup in Local Database for Central Repository Mode

A user is needed in the local database with the following username: CONDUCTOR_FOR_GLUENT

    create user conductor_for_gluent identified by "{complex password}" default tablespace users temporary tablespace temp;

The privileges needed are:

    GRANT CONNECT TO CONDUCTOR_FOR_GLUENT;
    GRANT GLUENT_OFFLOAD_ROLE TO CONDUCTOR_FOR_GLUENT;
    GRANT SELECT ANY DICTIONARY TO CONDUCTOR_FOR_GLUENT;
    GRANT SELECT ANY TABLE TO CONDUCTOR_FOR_GLUENT;
    -- Needed for Conductor for Gluent to do partition maintenance
    GRANT DROP ANY TABLE TO CONDUCTOR_FOR_GLUENT;
    GRANT ALTER ANY TABLE TO CONDUCTOR_FOR_GLUENT;

An alternative to the `ANY TABLE` privilege is to preform the grant(s) on the tables to be offloaded.

## TNS Setup
This is needed for all 3 modes of the backend software.

### TNSNAMES.ORA
A TNSNAMES.ORA file needs to be created in the tns subdirectory.  For the no repository option or the local repository option, one entry for the local DB being offloaded is needed.  For the central repository mode, two entries are needed: one for local DB and a second for the central repository.  Suggested names are as follows:

<ul>
<li>c4g_local</li>
<li>c4g_central</li>
</ul>

Historically, the tns entry was:
<ul>
<li>gluent_conn</li>
</ul>

A sample file is located under the tns/sample directory, showing a simple tns entry.

### Wallet Setup
For Full Conductor for Gluent, run the following:

    ./setup-wallet new c4g_local
    ./setup-wallet add c4g_central

For Standalone or Runtime Repository modes, run the following:
    ./setup-wallet new gluent_conn

## Crontab Setup
Once the backend and frontend software are installed, add a cron entry to run the launch script.  The job should be like the following with the appropriate path specified:

     * * * * * /u01/app/gluent/scripts/bin/launch-gluent-jobs {DB/Container Name} > /u01/app/gluent/scripts/log/launch-gluent-jobs-cron.log 2>&1


