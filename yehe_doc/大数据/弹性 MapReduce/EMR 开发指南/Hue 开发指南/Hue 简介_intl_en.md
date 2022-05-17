Hue is an open-source Apache Hadoop UI system that evolved from Cloudera Desktop, which Cloudera contributed to the Hadoop project of the Apache Software Foundation. Hue is implemented on the basis of Django, a Python web framework. By using Hue, you can interact with Hadoop clusters in the web-based console on a browser, such as manipulating HDFS data, running MapReduce jobs, executing Hive SQL statements, and browsing HBase databases.

## Accessing Hue WebUI
**To use the Hue component to manage workflows, log in to the Hue console first as shown below:**
1.Log in to the [EMR console](https://console.cloud.tencent.com/emr), click the **ID/Name** of the target cluster to enter the cluster details page, and click **Cluster Service**.
2. Find the Hue component on the list page and click **WebUI Access Address** to enter the Hue page.
3. When logging in to the Hue console for the first time, use the root account and the password set when you created the cluster.
![](https://qcloudimg.tencent-cloud.cn/raw/fe7b2fa224ee12a8a5ded70ccc4a99a7.png)

>! As the default component account upon start in EMR is Hadoop, you need to create a Hadoop account after logging in to the Hue console with the root account for the first time. All subsequent jobs should be submitted by using the Hadoop account.

## User Permission Management
Log in to Hue with the admin account first.
1. Add a user.
	1. Click **Add user** on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/34bd048f7de580e9bff702b29948bbfc.png)
	2. Enter the user information.
![](https://qcloudimg.tencent-cloud.cn/raw/c108d30bc0c52547adeb531ee1798d67.png)
	3. Enter the user group and other information.
![](https://qcloudimg.tencent-cloud.cn/raw/7935160d1155f554032f9ae0b6b4df7e.png)
	4. Click **Add user**.
![](https://qcloudimg.tencent-cloud.cn/raw/38ecde0380bd216db8c682736cd354fb.png)
2. Perform permission control.
You can assign different permissions to groups through Hue and add users to groups to get specific permissions.
	1. Click **Groups** at the top of the user management page and then click **Add group** on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/6b857c8fa14a766f73b62ff1f9077e92.png)
	2. Enter the user group information, select the users to be added to the group, specify the permissions for the group, and click **Add group**.
![](https://qcloudimg.tencent-cloud.cn/raw/7e3ebc8ca1da824e5da0c622592e9dbb.png)

## Data Import
Hue allows you to import data from a local file, HDFS file, external database, or manually.
![](https://qcloudimg.tencent-cloud.cn/raw/a65e26d2349659cc3d497bfb2c4ac009.png)
1. Import a local file.
	1. Click **Choose file** and select a CSV file. Hue will automatically recognize the delimiter and generate a preview. Click **Next** to import the file to a table.
![](https://qcloudimg.tencent-cloud.cn/raw/2181983dff1198adaee6a5bf1f9a3c52.png)
	2. Enter the table information and click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/45862b537ab26eddde95e6b267f5210a.png)
2. Import an HDFS file.
	1. Select a CSV file from HDFS.
![](https://qcloudimg.tencent-cloud.cn/raw/c85db98b103806a35e8e1363d87c497c.png)
	2. Enter the table information and click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/a26119e9d4356cee5f0689be7ca64ff9.png)
3. Import an external database.
	1. Enter the external database information, click **Test Connection** to get the database information, select the database and table, and click **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/4e7b192e8cbb52970282dd29774ebaaa.png)
	2. Enter the information of the target table, click **Libs**, select the MySQL driver, and click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/a3a4734bff7ab835641a3589bbf89fc9.png)

## Job Management
Click the **Jobs** tab on the right to enter the job management page. Then, click a job type tab at the top to view and manage jobs.
![](https://qcloudimg.tencent-cloud.cn/raw/d0d9f3254368fda9b4044db6055813c0.png)
![](https://qcloudimg.tencent-cloud.cn/raw/7aaae821f6ebfab18b64da888fa9a053.png)

## Table Management
1. Click **Tables** on the right to enter the table management page and view the basic database information.
![](https://qcloudimg.tencent-cloud.cn/raw/058bdbd72391b69a0eae466869a47bf0.png)
2. Click a database to view the information of its tables.
![](https://qcloudimg.tencent-cloud.cn/raw/a14dba986a6192e6246a179560bc790f.png)
3. Click a table to view its details.
![](https://qcloudimg.tencent-cloud.cn/raw/cc89817cc1759903a516db03a3f5abfb.png)
