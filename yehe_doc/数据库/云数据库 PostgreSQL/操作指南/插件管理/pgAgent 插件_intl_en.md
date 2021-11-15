This document describes how to implement automatic job execution in TencentDB for PostgreSQL through the pgAgent feature.

## Overview
If your business needs to perform specified actions in the database at scheduled times, such as clearing redundant data, updating materialized views, performing VACUUM FULL, and executing DML, this can be implemented in PostgreSQL through:
- The crontab feature of Linux
- The pgAgent feature of pgAdmin

pgAgent is an extension in the pgAdmin tool imported in pgAdmin III v1.4. It is mainly used as a PostgreSQL job scheduling agent and capable of running multi-step batch or shell scripts and SQL jobs on complex schedules. 
It should be noted that pgAgent requires the support of certain database tables and objects, so you need to install it first.



## Directions
### Configuring pgAgent 
1. [Log in to the TencentDB for PostgreSQL instance](https://intl.cloud.tencent.com/document/product/409/34626) and create your business database.
2. Run the following statement in the database where you need to enable the pgAgent feature:
```
psql > create extension pgagent;
CREATE EXTENSION
```
3. After the configuration is completed, you need to start the job scheduler through the pgAgent tool.
[Log in to the CVM instance](https://intl.cloud.tencent.com/document/product/213/10517) (we recommend you put the CVM and TencentDB for PostgreSQL instances in the same VPC). Choose the pgAgent version according to the actual database version. This document uses v11.8 as an example to install pgagent_11 available [here](https://download.postgresql.org/pub/repos/yum/11/redhat/rhel-8.0-x86_64/).
4. After pgAgent is installed, run the following statement to start the job scheduler:
>?Please use the command according to the actually installed version of pgAgent. For example, if v10 is installed, the command should be `pgagent_10`.
>
```
pgagent_11 hostaddr=IP dbname=database user=username port=port password=password
```
5. After successful execution, there is no echo, but you can use the following command to check whether the process is started successfully:
```
Run this statement, and if there is a `pgagent` process, it has been started successfully.
# ps -ef |grep pgagent
root      158553       1  0 Oct30 ?        00:00:15 pgagent_11 hostaddr=IP dbname=database user=username port=port password=password
```

### Configuring pgAgent Jobs through pgAdmin
1. Log in to the [TencentDB for PostgreSQL console](https://console.cloud.tencent.com/postgres), click an instance name in the instance list to enter the instance details page, and enable the public network access.
2. Open pgAdmin 4 and access your TencentDB for PostgreSQL instance at the public network access address. At this time, you can see pgAgent Jobs on the page.
![](https://main.qcloudimg.com/raw/9c12d37faee93b1db78c07e5aefaed58.png)
3. On the pgAdmin page, right-click and select **pgAgent Jobs** > **Create** > **Create Jobs** to create a scheduled job.
4. On the **General** page, configure the basic job information.
![](https://main.qcloudimg.com/raw/5f6d1e2ac7fd354fb55e78652a5d6c67.png)
5. Enter the **Steps** tab and configure the job that needs to be executed at the scheduled time. To do so, click **+** in the top-right corner to add a step, name it, and then configure the SQL statement to be executed on the **Code** tab.
![](https://main.qcloudimg.com/raw/63e2391908ba7e2be23716659442c97c.png)
6. Enter the **Schedules** page and configure the scheduling information for job execution:
 1. On the **General** tab below, configure the effective time of the job.
![](https://main.qcloudimg.com/raw/b952b05c3d757036cd82f1d7527fa4be.png)
 2. On the **Repeat** tab below, configure a crontab-style schedule.
![](https://main.qcloudimg.com/raw/ff1346df822c218fc0fd9fc6d8ece5f6.png)
 3. After configuring the execution time, you can also configure the time when the job should not be executed on the **Exceptions** tab.
7. Finally, click **Save**, and this job will be automatically executed according to the configuration.
