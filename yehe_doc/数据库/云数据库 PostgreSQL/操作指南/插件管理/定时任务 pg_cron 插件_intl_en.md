
pg_cron is a simple cron-based job scheduler for PostgreSQL 10 and later. It runs in the database as an extension and uses common cron syntax to schedule and execute database commands directly in the database.

This document describes how to use the pg_cron extension of PostgreSQL.

## Enabling pg_cron Extension
1. To use pg_cron, [submit a ticket](https://console.cloud.tencent.com/workorder/category) to add it to the `shared_preload_libraries` parameter of your database. Modifying this parameter requires an instance restart; therefore, do so during off-peak hours.

2. After the parameter is modified, enter the `postgres` database and run the following command with the admin account:
```
CREATE EXTENSION pg_cron;
```

3. Currently, pg_cron can execute scheduled jobs only in the `postgres` database. You can run scheduled jobs in other databases as instructed in [Setting Scheduled Job for Other Databases](#wpjhzy).


4. By default, after pg_cron is created, its configuration data and job execution can be configured only by the admin. If you want to use another user account to configure or run pg_cron, grant the account the cron metadatabase permission by running the following command:
```
postgres=> GRANT USAGE ON SCHEMA cron TO other-user;
```
This permission grants another user the permission to access cron metadata to schedule and cancel cron jobs. To successfully execute a cron job, the user needs the permission to access objects in the job. If the user doesn't have such permission, the job will fail, and an error will be displayed in `postgresql.log`.
In the following sample code, the user doesn't have the permission to access the `pgbench_accounts` table:
```
2020-12-08 16:41:00 UTC::@:[30647]:ERROR: permission denied for table pgbench_accounts
2020-12-08 16:41:00 UTC::@:[30647]:STATEMENT: update pgbench_accounts set abalance = abalance + 1
2020-12-08 16:41:00 UTC::@:[27071]:LOG: background worker "pg_cron" (PID 30647) exited with exit code 1
```
Below are other messages in the `cron.job_run_details` table:
```
postgres=> select jobid, username, status, return_message, start_time from cron.job_run_details where status = 'failed';
jobid |  username  | status |                   return_message                    |          start_time
-------+------------+--------+-----------------------------------------------------+-------------------------------
   143 | unprivuser | failed | ERROR: permission denied for table pgbench_accounts | 2020-12-08 16:41:00.036268+00
   143 | unprivuser | failed | ERROR: permission denied for table pgbench_accounts | 2020-12-08 16:40:00.050844+00
   143 | unprivuser | failed | ERROR: permission denied for table pgbench_accounts | 2020-12-08 16:42:00.175644+00
   143 | unprivuser | failed | ERROR: permission denied for table pgbench_accounts | 2020-12-08 16:43:00.069174+00
   143 | unprivuser | failed | ERROR: permission denied for table pgbench_accounts | 2020-12-08 16:44:00.059466+00
(5 rows)
```

## pg_cron Scheduled Job Configuration
pg_cron provides three main operations: adding and deleting jobs and viewing job information.

### cron.schedule() function
This function is used to schedule a cron job. Jobs are scheduled in the `postgres` database initially by default. This function returns a bigint value indicating the job identifier. To schedule a job in other databases in a TencentDB for PostgreSQL instance, refer to the example in [Setting Scheduled Job for Other Databases](#wpjhzy).
This function has two syntax formats:

**Syntax**
```
cron.schedule (job_name,
    schedule,
    command
);

cron.schedule (schedule,
    command
);
```

**Parameters**

| Parameter | Description | 
|---------|---------|
| job_name | cron job name, which can be left empty. | 
| schedule | cron job schedule text, which is in the standard cron format. | 
| command | Text of the command to be executed. | 

**Sample**
```
postgres=> SELECT cron.schedule ('test','0 10 * * *', 'VACUUM pgbench_history');
 schedule
----------
      145
(1 row)

postgres=> SELECT cron.schedule ('0 15 * * *', 'VACUUM pgbench_accounts');
 schedule
----------
      146
(1 row)
```
`schedule` uses the standard cron syntax. Here, `*` indicates to run the job at the specified time, and specific numbers indicate to run the job at the time specified by the numbers.
```
# Format: minute  hour  day of month  month  day of week
# week (0 - 6) = sun,mon,tue,wed,thu,fri,sat
# Example of job definition:
# .---------------- minute (0 - 59)
# |  .------------- hour (0 - 23)
# |  |  .---------- day of month (1 - 31)
# |  |  |  .------- month (1 - 12) OR jan,feb,mar,apr ...
# |  |  |  |  .---- day of week (0 - 6) (Sunday=0 or 7) OR sun,mon,...,sat
# |  |  |  |  |
# *  *  *  *  * 
```

### cron.unschedule() function
This function is used to delete a cron job. You can pass in a `job_name` or `job_id`. Make sure that you own the policy corresponding to the `job_id` passed in. This function returns a boolean value indicating success or failure.

This function uses the following syntax format:
**Syntax**
```
cron.unschedule (job_id);

cron.unschedule (job_name);
```

**Parameters**

| Parameter | Description | 
|---------|---------|
| job_id | Job ID returned by the `cron.schedule` function during cron job scheduling. | 
| job_name | Name of the cron job scheduled by the `cron.schedule` function. | 

**Sample**
```
postgres=> select cron.unschedule(108);
 unschedule
------------
 t
(1 row)

postgres=> select cron.unschedule('test');
 unschedule
------------
 t
(1 row)
```

### pg_cron tables
The following tables are used to schedule jobs and record job execution methods.

| Table | Description | 
|---------|---------|
| cron.job | It contains the metadata of each scheduled job. Most interactions with this table are implemented by using the `cron.schedule` and `cron.unschedule` functions.<br>Note that we recommend you not directly grant the permission to update or insert data into this table. |
| cron.job_run_details | It contains the historical information of previously scheduled jobs. It is very useful for checking the statuses, returned messages, and start/end times of executed jobs.<br>To prevent this table from growing continuously, clear it regularly. |

## Setting pg_cron Scheduled Job
1. If you want to perform the `VACUUM` operation on a specified table at the selected time, use the `cron.schedule` function to schedule a job. For example, you can run `VACUUM FREEZE` on the specified table at 22:00 (GMT) every day. The number returned by the scheduling statement indicates the current job ID.
```
SELECT cron.schedule('manual vacuum', '0 22 * * *', 'VACUUM FREEZE pgbench_accounts');
 schedule
----------
1
(1 row)
```
2. This function has three input parameters: the job name (string), the cron scheduling syntax, and the specific SQL statement to be executed.


## Viewing pg_cron Scheduled Job
After scheduling a job, you can view it in the `cron.job` table by running the following statement:
```
SELECT * FROM cron.job;

jobid | schedule   |  command  | nodename  | nodeport | database | username | active 
-------+------------+-----------+-----------+----------+----------+----------+--------
    1 | 0 22 * * * |   VACUUM ... | localhost |     5432 | postgres | test     | t
```

## Deleting pg_cron Scheduled Job
If a scheduled job is no longer needed, you can run the following statement to delete it:
```
SELECT cron.unschedule(1);

 unschedule
------------
          t
```

## Viewing the Execution History of Scheduled Job
After running the above sample code, you can check the job status and execution result in the `cron.job_run_details` table as follows:
```
postgres=> select * from cron.job_run_details;
 jobid | runid | job_pid | database | username | command | status | return_message | start_time | end_time
-------+-------+---------+----------+----------+----------------------------------------+-----------+----------------+-------------------------------+-------------------------------
 1 | 1 | 3395 | postgres | adminuser| vacuum freeze pgbench_accounts | succeeded | VACUUM | 2020-12-04 21:10:00.050386+00 | 2020-12-04 21:10:00.072028+00
(1 row)
```

## Clearing pg_cron Record Table
1. The `cron.job_run_details` table contains the records of historical cron jobs, which may get very large over time. We recommend you clear it regularly. For example, it may be sufficient to retain the records of jobs in the past week for troubleshooting.

2. In the following sample code, the `cron.schedule` function is used to schedule the job of clearing records in the `cron.job_run_details` table at 00:00 every day and retaining only records of jobs in the past seven days.
```
SELECT cron.schedule('0 0 * * *', $$DELETE 
    FROM cron.job_run_details 
    WHERE end_time < now() – interval '7 days'$$);
```

## Disabling pg_cron Records	
- To completely disable writing any content into the `cron.job_run_details` table, set the `cron.log_run` parameter to `off` in the console.
If you do so, the pg_cron extension will no longer write data to this table and will only generate errors in the `postgresql.log` file. You can view all error messages in the error logs in the console.

- Run the following command to check the value of the `cron.log_run` parameter.
```
postgres=> SHOW cron.log_run;
```

## [Setting Scheduled Job for Other Databases](id:wpjhzy)

By default, all metadata of pg_cron is stored in the `postgres` database. To run a scheduled job for objects in another database, perform the following operations:

1. To perform the `VACUUM` operation on a table in the `test` database, you first need to use the admin account of pg_cron to run the `cron.schedule` function in the `postgres` database to schedule a job.
```
postgres=> SELECT cron.schedule('test manual vacuum', '29 03 * * *', 'vacuum freeze test_table');
```
2. Run the following command with the admin account to set the database of the schedule job to the target database. Note that `jobid` must be the `jobid` returned in step 1.
```
postgres=> UPDATE cron.job SET database = 'test' WHERE jobid = 106;
```
3. Query the `cron.job` table to verify the operation result.
```
postgres=> select * from cron.job;
 jobid | schedule | command | nodename | nodeport | database | username | active | jobname
-------+-------------+----------------------------------------+-----------+----------+-----------+-----------+--------+-------------------------
 2 | 29 03 * * * | vacuum freeze test_table | localhost | 8192 | test | adminuser | t | database1 manual vacuum
 1 | 59 23 * * * | vacuum freeze pgbench_accounts | localhost | 8192 | postgres | adminuser | t | manual vacuum
(2 rows)
```

## [pg_cron Parameters](id:pgcs)
Parameter used to control the behaviors of the pg_cron extension are as listed below:

| Parameter | Description | 
|---------|---------|
| cron.database_name | pg_cron metadatabase. | 
| cron.host | Name of the host to connect to PostgreSQL, which cannot be modified. | 
| cron.log_run | Specifies whether to record all executed jobs into the `job_run_details` table. Valid values: `on`, `of`. | 
| cron.log_statement | Specifies whether to record all cron statements into logs before running them. Valid values: `on`, `off`. | 
| cron.max_running_jobs | Maximum number of concurrent jobs. To run more jobs, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance. | 
| cron.use_background_workers	| Specifies to use backend workers instead of client sessions. You cannot modify the value. | 

You can run the following SQL command to display these parameters and their values:
```
postgres=> SELECT name, setting, short_desc FROM pg_settings WHERE name LIKE 'cron.%' ORDER BY name;
```
