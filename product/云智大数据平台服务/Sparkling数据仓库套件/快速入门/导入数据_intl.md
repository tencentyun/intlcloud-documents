## Operation Scenario
This document describes how to import all the data in TencentDB for MySQL into a new Sparkling cluster. Sparkling supports a variety of data import methods and scheduled import. For more information, see [Data Integration](https://cloud.tencent.com/document/product/1002/30554).

## Prerequisites
A MySQL database instance has been created in the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), and the data you want to import has been stored in the instance. It is recommended that the database and Sparkling cluster be located in the same region to ensure the stability and speed of access.
For more information about MySQL database operations, see [Getting Started with TencentDB for MySQL](https://cloud.tencent.com/product/cdb/getting-started).

## Directions
Go to [Cluster Management](https://sparkling.cloud.tencent.com) and click **Data** in the left navigation pane to enter the data ingestion page. Follow the steps below to complete the data ingestion from RDBMS:
![](https://main.qcloudimg.com/raw/a0c3027c3d8c98f5adedc52484706605.png)

### 1. Configuring a Data Source
Take importing the data in the default data table "metrics" in the default database "sys" in the MySQL instance as an example. Configure the data source as shown in the figure below, where you should select the MySQL region for "Region". The MySQL instance ID can be found in the [MySQL console](https://console.cloud.tencent.com/cdb), and the APP ID can be found in [Account Info](https://console.cloud.tencent.com/developer).
![](https://main.qcloudimg.com/raw/040c813d491b9558344fe3211b77a711.png)
>? Click **Test Connectivity** to verify whether it can be connected to the database where the data table to be ingested resides. After the system prompts that "Data connection is good", click **Next** to complete the data source configuration.

### 2. Previewing Data
You can preview the field information in the data table on the "Data Preview" page. By default, five rows of data are extracted for preview. If there are no issues with the preview, click **Next**.
![](https://main.qcloudimg.com/raw/18d9add9962bfa70794d41a84707b2c3.png)

### 3. Configuring a Target
After completing the setup as shown in the figure below, you can create a table named "new_table", where the fields should be set as all the fields in the "metrics" table and the storage format as PARQUET.
![](https://main.qcloudimg.com/raw/59d25533b344aeb18e05ca36a2241f64.png)

### 4. Configuring an Extraction Task
The example in this document imports the data through a single full import task. For more import methods, see [Data Integration](https://cloud.tencent.com/document/product/1002/30554).
![](https://main.qcloudimg.com/raw/1f9d9b1956f848e515a63be198fc06c2.png)

### 5. Previewing
You can view the current set data source, data preview, target table, and task scheduling on the "Preview" page. If there are no issues, click **Done** to complete the data import task setup. Click **OK** in the pop-up dialog box to go to the task management page.
![](https://main.qcloudimg.com/raw/f4ea850b9c35a44dcbc7594ab910c575.png)
