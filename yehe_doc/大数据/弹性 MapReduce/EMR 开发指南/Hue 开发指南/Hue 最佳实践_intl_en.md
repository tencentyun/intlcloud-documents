This document describes how to use Hue.
## Hive SQL Query
Hue's Beeswax app provides user-friendly and convenient Hive query capabilities, enabling you to select different Hive databases, write HQL statements, submit query tasks, and view results with ease.
1. At the top of the Hue console, select **Query** > **Editor** > **Hive**.
 ![](https://qcloudimg.tencent-cloud.cn/raw/48a2fbc6dacc28ea8e0f8e7d6e321d47.png)
2. Enter the statement to be executed in the statement input box and click **Run** to run it.
 ![](https://main.qcloudimg.com/raw/f0f36e1a049ee72ef5ce79ac7d93574b.png)

## HBase Data Query, Modification, and Display
You can use HBase Browser to query, modify, and display data from tables in an HBase cluster.
 ![](https://main.qcloudimg.com/raw/23e332d0abd935823a3de21168d08d4f.png)

## HDFS Access and File Browsing
Hue's web UI makes it easy to view files and folders in HDFS and perform operations such as creation, download, upload, copy, modification, and deletion.
1. On the left sidebar in the Hue console, select **Browsers** > **Files** to browse HDFS files.
![](https://main.qcloudimg.com/raw/1c544585871ec81d0630632ef33804e2.png)
2.	Perform various operations.
 ![](https://main.qcloudimg.com/raw/0b9ec60bd7643f943aaeb48a465b678d.png)

## Oozie Job Development
1. Prepare workflow data: Hue's job scheduling is based on workflows. First, create a workflow containing a Hive script with the following content:
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
Save the above content as a file named `hive_sample.sql`. The Hive workflow also requires a `hive-site.xml` configuration file, which can be found on the cluster node where the Hive component is installed. The specific path is `/usr/local/service/hive/conf/hive-site.xml`. Copy the `hive-site.xml` file and then upload the Hive script file and `hive-site.xml` to a directory in HDFS, such as `/user/hadoop`.

2. Create a workflow.
	1. Switch to the `hadoop` user. At the top of the Hue console, select **Query** > **Scheduler** > **Workflow**.
![](https://qcloudimg.tencent-cloud.cn/raw/b1b9b6361124538cb755efb3fc1d90b3.png)
	2. Drag a Hive script into the workflow editing page.
>!This document uses the installation of Hive v1 as an example, and the configuration parameter is `HiveServer1`. If it is deployed with other Hive versions (i.e., configuring configuration parameters of other versions), an error will be reported.

![](https://qcloudimg.tencent-cloud.cn/raw/27cbec2a4f30fc937f34a5d086b496b4.png)
	3. Select the Hive script and `hive-site.xml` files you just uploaded.
![](https://qcloudimg.tencent-cloud.cn/raw/251b3efbd9bb7057945cfc1ac0f1aab7.png)
	4. Click **Add** and specify the Hive script file in `FILES`.
![](https://qcloudimg.tencent-cloud.cn/raw/38e9a81097f76194047f0d302d39ab2a.png)
	5. Click **Save** in the top-right corner and then click **Run** to run the workflow.
![](https://main.qcloudimg.com/raw/3c7f79c50b40772240ed52135ec0b00d.png)

3. Create a scheduled job.
The scheduled job in Hive is "schedule", which is similar to the crontab in Linux. The supported scheduling granularity can be down to the minute level.
	1. Select **Query** > **Scheduler** > **Schedule** to create a schedule.
![](https://qcloudimg.tencent-cloud.cn/raw/c45fd5b062e78750aab55b7ba466975b.png)
	2. Click **Choose a workflow** to select a created workflow.
![](https://qcloudimg.tencent-cloud.cn/raw/5d20d799a91dbc105e4eadd9d2365bf7.png)
	3. Select the execution time, frequency, time zone, start time, and end time of the schedule and click **Save**.
![](https://main.qcloudimg.com/raw/6dfbaa89d2545c9aa4f8b3d8c1b4fadb.png)

4. Create a scheduled job.
	1. Click **Submit** in the top-right corner to submit the schedule.
![](https://qcloudimg.tencent-cloud.cn/raw/be86060e81eac2fe1842c58e9bf57dd3.png)
	2. You can view the scheduling status on the monitoring page of the schedulers.
![](https://main.qcloudimg.com/raw/29da2913272ddce9d3b534ee7d026b22.png)

## Notebook Query and Comparative Analysis
Notebooks can quickly build access requests and queries and put the query results together for comparative analysis. It supports five types: Hive, Impala, Spark, Java, and Shell.
1. Click **Editor**, **Notebook**, and **+** to add the required query.
![](https://qcloudimg.tencent-cloud.cn/raw/09d6b44c6517d1a3204f6fdb517e075f.png)
2. Click **Save** to save the added notebook and click **Run** to run the entire notebook.
![](https://qcloudimg.tencent-cloud.cn/raw/75eb474e274a7555a3baec6cb1deaf61.png)

