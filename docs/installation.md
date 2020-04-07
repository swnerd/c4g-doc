title: Installation

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
<li>Gluent Software Installed</li>
<li>Cloudera with Impala only</li>
<li>parquet-tools available in the path of the edge node for the ssh user when using Full Conductor for Gluent Front-end and Back-end with Central Repository - usually found in /var/lib/alternatives.</li>
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
<li>HADOOP_HOST - defaults to the HDFS_CMD_HOST</li>
<li>HADOOP_SSH_USER - set to the target user on hadoop for ssh</li>
<li>G_ERROR_WORDS - Words and phrases used when determining if a possible error occurred.</li>
<li>TNS_ADMIN - Always set to ${tnsdir} - DO NOT CHANGE</li>
<li>AEG_GLUENT_REPO_SERVICE - service name to be used when connecting to the central repository</li>
<li>AEG_GLUENT_LOCAL_SERVICE - service name to be used when connecting to the local database</li>
<li>dstr - service name used in local repository and standalone mode</li>
<li>impala_node - automatically determined but can be overridden</li></li>
<li>IMPALA_SHELL_CMD - command with options need to run impala-shell</li>
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
<li>WALLET_ENTRY - the wallet entry you want to setup (corresponds to a TNS service name)
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

     * * * * * /u01/app/gluent/scripts/bin/launch-gluent-jobs > /u01/app/gluent/scripts/log/launch-gluent-jobs-cron.log 2>&1


# Front End Installation

## Prerequisites
<ul>
Oracle 12+ Database (created with DBCA or Manually)
</ul>
<u>Note</u>: <i>Apex requires that Oracle Text and JVM options be installed.  No other options are required.</i>

## Apex 19.2 Setup
Create Tablespace for Apex (if one does not exist)

    SQL>  -- Create Tablespace for Apex - Example
    create tablespace tbs_apex datafile '/u01/app/oracle/oradata/testinst/tbs_apex01.dbf' size 100m autoextend on maxsize 1000m;

### Copy Apex 19.2 to database host
Example Copy to Oracle User Home

    scp apex_19.2_en.zip {oracle user}@{db host}:.

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
#### Unzip Apex 19.2 software 
example statement if uploaded to user's home directory:

    cd $ORACLE_HOME
    unzip ~/apex_19.2_en.zip
    
#### Install Apex 19.2 in database

    cd $ORACLE_HOME/apex
    sqlplus / as sysdba
    
    SQL> -- Runtime install with 4 parms (apex tbs, apex tbs, temp tbs, image loc)
    @apxrtins.sql tbs_apex tbs_apex temp /i/
    ...set_appun.sql
    
    PL/SQL procedure successfully completed.
    
    ... ... ... ...
    PL/SQL procedure successfully completed.
    
    
    
    
    Thank you for installing Oracle Application Express 19.2.0.00.18
    
    Oracle Application Express is installed in the APEX_190200 schema.
    
    The structure of the link to the Application Express administration services is as follows:
    http://host:port/pls/apex/apex_admin (Oracle HTTP Server with mod_plsql)
    http://host:port/apex/apex_admin     (Oracle XML DB HTTP listener with the embedded PL/SQL gateway)
    http://host:port/apex/apex_admin     (Oracle REST Data Services)
    
    The structure of the link to the Application Express development interface is as follows:
    http://host:port/pls/apex (Oracle HTTP Server with mod_plsql)
    http://host:port/apex     (Oracle XML DB HTTP listener with the embedded PL/SQL gateway)
    http://host:port/apex     (Oracle REST Data Services)
    
    timing for: Phase 3 (Switch)
    Elapsed: 00:00:08.39
    timing for: Complete Installation
    Elapsed: 00:06:24.88
    
    PL/SQL procedure successfully completed.


#### Change / Setup Apex Administrator

    cd $ORACLE_HOME/apex
    sqlplus / as sysdba
    SQL> -- no parameters
    @apxchpwd.sql
    ...set_appun.sql
    ================================================================================
    This script can be used to change the password of an Application Express instance administrator. If the user does not yet exist, a user record will be created.
    ================================================================================
    Enter the administrator's username [ADMIN]
    User "ADMIN" does not yet exist and will be created.
    Enter ADMIN's email [ADMIN] {specify email address}
    Enter ADMIN's password [] 
    Created instance administrator ADMIN.

#### Enable Embedded PL/SQL Gateway and other configuration items

    cd $ORACLE_HOME/apex
    sqlplus / as sysdba
    SQL> -- one parameter is oracle_home 
    @apex_epg_config.sql /u01/app/oracle/product/12.2.0/dbhome_1
    
    PL/SQL procedure successfully completed.
    ... ... ... ...
    PL/SQL procedure successfully completed.
    
    Commit complete.
    
    alter user anonymous identified by {complex password} account unlock;
    alter user xdb identified by {complex password} account unlock; 
    
    EXEC DBMS_XDB.SETHTTPPORT(8080);
    
    BEGIN
        DBMS_NETWORK_ACL_ADMIN.APPEND_HOST_ACE(
            host => '*',
            ace => xs$ace_type(privilege_list => xs$name_list('connect'),
                               principal_name => 'APEX_180200',
                               principal_type => xs_acl.ptype_db));
    END;
    /
    -- Below script contents can be found in Appendix A of this document
    @xdbconfig_anonymous.sql
     
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
The installation SQL scripts are located in <i>gui</i> directory where the backend scripts were installed (usually <code>/u01/app/gluent/scripts</code> or <code>/u01/app/gluent/c4g-scripts</code>.  From this directory connect to the apex database (usually <i>c4g_central</i> is the tns name to use:

You can set your environment to use the `tnsnames.ora` file you created during the backend setup. For example:

    cd /u01/app/gluent/c4g-scripts/tns
    export TNS_ADMIN=`pwd`
    cd ../gui
    sqlplus system/{complex password}@c4g_central

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
    commit;
    spool off

<u>Note</u>: <i> Be sure to commit after running the script.  </i>


#### Help Text Setup
Run the sql, no parameters

    spool c4g-setup-helptext.log
    @c4g-setup-helptext.sql
    commit;
    spool off

<u>Note</u>: <i> Be sure to commit after running the script.  </i>

## Apex Application Install
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
 

# Appendix A - xdbconfig_anonymous.sql

    DECLARE
      l_configxml XMLTYPE;
      l_value VARCHAR2(5) := 'true';
    BEGIN
      l_configxml := DBMS_XDB.cfg_get();
      IF l_configxml.existsNode('/xdbconfig/sysconfig/protocolconfig/httpconfig/allow-repository-anonymous-access') = 0 THEN
        -- Add config element
        begin
          SELECT
            insertChildXML(
              l_configxml
              , '/xdbconfig/sysconfig/protocolconfig/httpconfig'
              , 'allow-repository-anonymous-access'
              , XMLType('<allow-repository-anonymous-access xmlns="http://xmlns.oracle.com/xdb/xdbconfig.xsd">'
                  || l_value
                  || '</allow-repository-anonymous-access>')
              , 'xmlns="http://xmlns.oracle.com/xdb/xdbconfig.xsd"'
            )
            INTO l_configxml
            FROM dual;
          exception
            when others then
              dbms_output.put_line( 'insert' ); -- '
              raise;
        end;
        DBMS_OUTPUT.put_line('xdbconfig for anonymous now inserted.');
      ELSE
        -- Update existing config element.
        begin
          SELECT
            updateXML(
              DBMS_XDB.cfg_get()
              , '/xdbconfig/sysconfig/protocolconfig/httpconfig/allow-repository-anonymous-access/text()'
              , XMLType('<allow-repository-anonymous-access xmlns="http://xmlns.oracle.com/xdb/xdbconfig.xsd">'
                  || l_value
                  || '</allow-repository-anonymous-access>')
              , 'xmlns="http://xmlns.oracle.com/xdb/xdbconfig.xsd"'
            )
              INTO l_configxml
              FROM dual;
          exception
            when others then
              dbms_output.put_line( 'update'); -- '
              raise;
        end;
        DBMS_OUTPUT.put_line('xdbconfig for anonymous now updated.');
      END IF;
      DBMS_XDB.cfg_update(l_configxml);
      DBMS_XDB.cfg_refresh;
    END;
    /
