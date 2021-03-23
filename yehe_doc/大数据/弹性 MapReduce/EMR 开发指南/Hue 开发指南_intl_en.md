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
1. Log in to the [EMR Console](https://console.cloud.tencent.com/emr) Click the ID/name of the target cluster to go to the cluster details page, and then click **Cluster Services**.
2. Find the Hue component on the list page and click **WebUI Access Address** to enter the Hue page.
3. When logging in to the Hue Console for the first time, use the root account and the password set when you created the cluster.
![](https://main.qcloudimg.com/raw/ae62e428871fd46c2ce6509fd31cde63.png)
>As the default component account upon startup in EMR is Hadoop, please create a Hadoop account after logging in to the Hue Console with the root account for the first time. All subsequent jobs should be submitted by using the Hadoop account.

## Hive SQL Query
Hue's Beeswax app provides user-friendly and convenient Hive query capabilities, enabling you to select different Hive databases, write HQL statements, submit query tasks, and view results with ease. 
1. At the top of the Hue Console, select **Query** > **Editor** > **Hive**.
![](https://main.qcloudimg.com/raw/bfcd6944a8a8dd70065218885b55f82d.png)
2. Enter the statement to be executed in the statement input box and click **Execute** to execute it.
![](https://main.qcloudimg.com/raw/f0f36e1a049ee72ef5ce79ac7d93574b.png)

## HBase Data Query
You can use HBase Browser to query, modify, and display data from tables in an HBase cluster.
![](https://main.qcloudimg.com/raw/23e332d0abd935823a3de21168d08d4f.png)

## HDFS File Browsing
Hue's web UI makes it easy to view files and folders in HDFS and perform operations such as creation, download, upload, copy, modification, and deletion.
1. In the left sidebar in the Hue Console, select **Browsers** > **Files** to browse HDFS files.
![](https://main.qcloudimg.com/raw/1c544585871ec81d0630632ef33804e2.png)
2. After entering the **File Browser**, you can perform the operations as shown below:
![](https://main.qcloudimg.com/raw/0b9ec60bd7643f943aaeb48a465b678d.png)

## Oozie Task Scheduling
1. **Prepare workflow data**
Hue's task scheduling is based on workflows. First, create a workflow containing a Hive script with the following content:
```
 create database if not exists hive_sample; 
 show databases;
 use hive_sample;
 show tables;
 create table if not exists hive_sample (a int, b string);
 show tables;
 insert into hive_sample select 1, "a";
 select * from hive_sample;
```
Save the content above as a file named hive_sample.sql. The Hive workflow also requires a hive-site.xml configuration file, which can be found on the cluster node where the Hive component is installed. Upload the Hive script file and hive-site.xml to a directory in HDFS, such as `/user/hadoop`.
Upload the Hive script file and hive-site.xml to a directory in HDFS, such as `/user/hadoop`.
2. **Create a workflow**
 - Switch to the hadoop user. At the top of the Hue Console, select **Query** > **Scheduler** > **Workflow**.
![](https://main.qcloudimg.com/raw/17e2c9e91bef6c67d7f6721eeb1a490e.png)
 - Drag a Hive script into the workflow editing page.
>!This document uses the installation of Hive v1 as an example, and the configuration parameter is HiveServer1. If it is deployed with other Hive versions (i.e., configuring configuration parameters of other versions), an error will be reported.
>
![](https://main.qcloudimg.com/raw/128170644bbef8f40743ea0f72a35a0e.png)
 - Select the Hive script and hive-site.xml files you just uploaded.
![](https://main.qcloudimg.com/raw/1bdf334d89fa1be9fcee003d8328ff4d.png)
 - After clicking **Add**, you also need to specify the Hive script file in "FILES".
![](https://main.qcloudimg.com/raw/f36e5b22f40b2832f018d0091c8a382c.png)
 - Click **Save** in the top-right corner and then click **Execute** to run the workflow.
![](https://main.qcloudimg.com/raw/3c7f79c50b40772240ed52135ec0b00d.png)
3. **Create a scheduled task**
The scheduled task in Hive is "schedule" which is similar to the crontab in Linux. The supported scheduling granularity can be down to the minute level.
 - Select **Query** > **Scheduler** > **Schedule** to create a schedule.
![](https://main.qcloudimg.com/raw/d0bde8f4b97341f43aaa9ca8ab9b2440.png)
 - Click **Choose a workflow...** to select a created workflow.
![](https://main.qcloudimg.com/raw/3e9439fc36547531af9e49462e2880dd.png)
 - Select the execution time, frequency, time zone, start time, and end time of the schedule and click **Save** to save.
![](https://main.qcloudimg.com/raw/6dfbaa89d2545c9aa4f8b3d8c1b4fadb.png)
4. **Execute the schedule**
 - Click **Submit** in the top-right corner to submit the schedule.
![](https://main.qcloudimg.com/raw/cdcce33e1f79c032028956f27958412d.png)
 - You can view the scheduling status on the monitoring page of the schedulers.
![](https://main.qcloudimg.com/raw/29da2913272ddce9d3b534ee7d026b22.png)
