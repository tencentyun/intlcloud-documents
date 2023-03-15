Hue is an open-source Apache Hadoop UI system that evolved from Cloudera Desktop, which Cloudera contributed to the Hadoop project of the Apache Software Foundation. Hue is implemented on the basis of Django, a Python web framework. By using Hue, you can interact with Hadoop clusters in the web-based console on a browser, such as manipulating HDFS data, running MapReduce jobs, executing Hive SQL statements, and browsing HBase databases.

## Accessing Hue WebUI
**To use the Hue component to manage workflows, log in to the Hue console first:**
1. Log in to the [EMR console](https://console.cloud.tencent.com/emr) and click the **ID/Name** of the target cluster in the cluster list to go to the cluster details page. Then, click **Cluster Service**.
2. Find the Hue component on the list page and click **WebUI URL** to go to the Hue page.
3. When logging in to the Hue console for the first time, use the hadoop account and the password set when you created the cluster.
![](https://qcloudimg.tencent-cloud.cn/raw/fe7b2fa224ee12a8a5ded70ccc4a99a7.png)
>! EMR-v2.5.0 and earlier, and EMR-v3.1.0 and earlier are not integrated with OpenLDAP. When you log in to the Hue console for the first time, you must use the root account for login and then create the hadoop account on the WebUI. This is because the default component account upon startup in EMR is hadoop and all subsequent jobs should be submitted by using the hadoop account. For more information about how to create a hadoop account, see the official document of [Hue](https://docs.gethue.com/administrator/administration/ user-management/).


## Managing User Permissions
1. Add a user.
	1. Log in to the [EMR console](https://console.cloud.tencent.com/emr) and add a user on the [User Management](https://intl.cloud.tencent.com/document/product/1026/43326) page.
	2. After adding a user, if you have deployed Ranger in your cluster, you must manually trigger the delivery of the configuration in `ranger-ugsync-site.xml` to restart the EnableUnixAuth service for user synchronization. For more information, see [User Management](https://intl.cloud.tencent.com /document/product/1026/43326). Then, you can go to the Ranger WebUI to set access permissions of the new user.
	3. Find the Hue component on the list page, click **WebUI URL** to go to the Hue page and log in to Hue.
2. Perform permission control.
You can assign different permissions to groups through Hue and add users to groups to get specific permissions.
	1. Click **Groups** at the top of the user management page and then click **Add group** on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/34bd048f7de580e9bff702b29948bbfc.png)
	2. Enter the user group information, select the users to be added to the group, specify the permissions for the group, and click **Add group**.
![](https://qcloudimg.tencent-cloud.cn/raw/c108d30bc0c52547adeb531ee1798d67.png)

## Importing Data
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
	![](https://qcloudimg.tencent-cloud.cn/raw/4cda1ce5eb427e88199f70e0f33c8e81.png)
	2. Enter the information of the target table, click **Libs**, select the MySQL driver, and click **Save**.
	![](https://qcloudimg.tencent-cloud.cn/raw/a3a4734bff7ab835641a3589bbf89fc9.png)

## Job Management
Click the **Jobs** tab on the right to enter the job management page. Then, click a job type tab at the top to view and manage jobs.
![](https://qcloudimg.tencent-cloud.cn/raw/7aaae821f6ebfab18b64da888fa9a053.png)
![](https://qcloudimg.tencent-cloud.cn/raw/7aaae821f6ebfab18b64da888fa9a053.png)

## Table Management
1. Click **Tables** on the right to enter the table management page and view the basic database information.
![](https://qcloudimg.tencent-cloud.cn/raw/058bdbd72391b69a0eae466869a47bf0.png)
2. Click a database to view the information of its tables.
![](https://qcloudimg.tencent-cloud.cn/raw/a14dba986a6192e6246a179560bc790f.png)
3. Click a table to view its details.
![](https://qcloudimg.tencent-cloud.cn/raw/cc89817cc1759903a516db03a3f5abfb.png)
