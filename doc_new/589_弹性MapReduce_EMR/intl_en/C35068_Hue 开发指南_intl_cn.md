## Hue Overview
Hue is an open-source Apache Hadoop UI system that evolved from Cloudera Desktop. Cloudera eventually gifted it to the Hadoop project of Apache Software Foundation. Hue is implemented on the basis of Django, a Python web framework.

By using Hue, you can interact with Hadoop clusters in the web-based console on a browser, such as manipulating HDFS data, running MapReduce jobs, executing Hive SQL statements, and browsing HBase databases.

## Hue Features
- Hive SQL query.
- Hbase data query, modification, and display.
- HDFS access and file browsing.
- Development, monitoring, coordinating, and scheduling of Oozie tasks.

## Log in to the Hue Console
To use the Hue component to manage workflows, log in to the Hue Console first as shown below:
1. Log in to the [EMR Console](https://console.cloud.tencent.com/emr) and select **Component Management** in the left sidebar.
2. Find the Hue component on the list page and click "Native WebUI Access Address" to enter the Hue page.
3. When logging in to the Hue Console for the first time, use the root account and the password set when you created the cluster.
![](https://main.qcloudimg.com/raw/ae62e428871fd46c2ce6509fd31cde63.png)
>As the default component account upon startup in EMR is Hadoop, please create a Hadoop account after logging in to the Hue Console with the root account for the first time. All subsequent jobs should be submitted using the Hadoop account.

## Hive SQL Query
Hue's Beeswax app provides user-friendly and convenient Hive query capabilities, enabling you to select different Hive databases, write HQL statements, submit query tasks, and view results with ease. 
1. At the top of the Hue Console, select **Query** > **Editor** > **Hive**.
![](https://main.qcloudimg.com/raw/bfcd6944a8a8dd70065218885b55f82d.png)
2. Enter the statement to be executed in the statement input box and click the "Execute" icon to execute it.
![](https://main.qcloudimg.com/raw/202878b0b90b42da7317b026e9f2f603.png)

## HBase Data Query
You can use HBase Browser to query, modify, and display data from tables in an HBase cluster.
![](https://main.qcloudimg.com/raw/705ade35d5fe86c27be6aff46235dc02.png)

## HDFS File Browsing
Hue's web UI makes it easy to view files and folders in HDFS and perform operations such as creation, download, upload, copy, modification, and deletion.
1. In the left sidebar in the Hue Console, select **Browsers** > **Files** to browse HDFS files.
![](https://main.qcloudimg.com/raw/b2e05c0c8f05464f0ef1ffe671be1cc3.png)
2. After entering the File Browser, you can perform the operations as shown below:
![](https://main.qcloudimg.com/raw/0dc7e232a81e8900c06adb277b8eaf93.png)

## Oozie Task Scheduling
1. **Prepare workflow data**
Hue's task scheduling is based on workflows. First, create a workflow containing a Hive script with the following content:
```
| create database if not exists hive_sample; | 
| show databases;| 
| use hive_sample;|
| show tables;|
| create table if not exists hive_sample (a int, b string);|
| show tables;|
| insert into hive_sample select 1, "a";|
| select * from hive_sample;|
```
Save the content above as a file named hive_sample.sql. The Hive workflow also requires a hive-site.xml configuration file, which can be found on the cluster node where the Hive component is installed.
The specific path is /usr/local/service/hive/conf/hive-site.xml. Copy the hive-site.xml file, and change the corresponding configuration items to the following values:
```
<property>``  <name>hive.exec.local.scratchdir</name>``  <value>/tmp/hive</value>``</property>``<property>``  <name>hive.downloaded.resources.dir</name>``  <value>/tmp/hive/${hive.session.id}_resources</value>``</property>``<property>``  <name>hive.querylog.location</name>``  <value>/tmp/hive</value>``</property>``<property>``  <name>hive.server2.logging.operation.log.location</name>``  <value>/tmp/hive/tmp/operation_logs</value>``</property>
```
Upload the Hive script file and hive-site.xml to a directory in HDFS, such as /user/hadoop.
2. **Create a workflow**
 1. At the top of the Hue Console, select **Query** > **Scheduler** > **Workflow**.
![](https://main.qcloudimg.com/raw/17e2c9e91bef6c67d7f6721eeb1a490e.png)
 2. Drag a Hive script into the workflow editing page.
![](https://main.qcloudimg.com/raw/128170644bbef8f40743ea0f72a35a0e.png)
 3. Select the Hive script and hive-site.xml files you just uploaded.
![](https://main.qcloudimg.com/raw/1bdf334d89fa1be9fcee003d8328ff4d.png)
 4. After clicking **Add**, you also need to specify the Hive script file in "FILES".
![](https://main.qcloudimg.com/raw/f36e5b22f40b2832f018d0091c8a382c.png)
 5. Click "Save" in the top-right corner and then click the "Execute" icon to run the workflow.
![](https://main.qcloudimg.com/raw/418083ee1956ea3d2faea6afcd520834.png)
3. **Create a scheduled task**
The scheduled task in Hive is "schedule" which is similar to the crontab in Linux. The supported scheduling granularity can be down to the minute level.
 1. Select **Query** > **Scheduler** > **Schedule** to create a schedule.
![](https://main.qcloudimg.com/raw/d0bde8f4b97341f43aaa9ca8ab9b2440.png)
 2. Click **Choose a workflow...** to select a created workflow.
![](https://main.qcloudimg.com/raw/3e9439fc36547531af9e49462e2880dd.png)
 3. Select the execution time, frequency, time zone, start time, and end time of the schedule and click **Save** to save.
![](https://main.qcloudimg.com/raw/097fcba6a4c5c6e27efe342079beae46.png)
4. **Execute the schedule**
 1. Click the "Submit" icon in the top-right corner to submit the schedule.
![](https://main.qcloudimg.com/raw/d42cc1d0d4e2cbe3bdfa77065e5bd8c1.png)
 2. You can view the scheduling status on the monitoring page of the schedulers.
![](https://main.qcloudimg.com/raw/03eca980d7e0cf72b81af89da25f09f2.png)
