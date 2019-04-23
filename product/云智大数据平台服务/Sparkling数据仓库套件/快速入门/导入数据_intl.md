## Operation Scenario
This document describes how to import all the data in TencentDB for MySQL into a new Sparkling cluster. Sparkling supports a variety of data import methods and scheduled import. For more information, see [Data Integration](https://intl.cloud.tencent.com/document/product/1002/30554).

## Prerequisites
A MySQL database instance has been created in the [TencentDB for MySQL console](https://intl.cloud.tencent.com/login), and the data you want to import has been stored in the instance. It is recommended that the database and Sparkling cluster be located in the same region to ensure the stability and speed of access.
For more information about MySQL database operations, see [Getting Started with TencentDB for MySQL](https://intl.cloud.tencent.com/product/cdb).

## Directions
Go to [Cluster Management](https://intl.cloud.tencent.com/login) and click **Data** in the left navigation pane to enter the data ingestion page. Follow the steps below to complete the data ingestion from RDBMS:
![](https://main.qcloudimg.com/raw/c390a66727655a0bd909b8660214424c.png)

### 1. Configuring a Data Source
Take importing the data in the default data table "metrics" in the default database "sys" in the MySQL instance as an example. Configure the data source as shown in the figure below, where you should select the MySQL region for "Region". The MySQL instance ID can be found in the [MySQL console](https://intl.cloud.tencent.com/login), and the APP ID can be found in [Account Info](https://intl.cloud.tencent.com/login).
![](https://main.qcloudimg.com/raw/961028b8abfef987a1e67da0702f459c.png)
>? Click **Test Connectivity** to verify whether it can be connected to the database where the data table to be ingested resides. After the system prompts that "Data connection is good", click **Next** to complete the data source configuration.

### 2. Previewing Data
You can preview the field information in the data table on the "Data Preview" page. By default, five rows of data are extracted for preview. If there are no issues with the preview, click **Next**.
![](https://main.qcloudimg.com/raw/1fb275f0f8ac8485caeb7feedb985d32.png)

### 3. Configuring a Target
After completing the setup as shown in the figure below, you can create a table named "new_table", where the fields should be set as all the fields in the "metrics" table and the storage format as PARQUET.
![](https://main.qcloudimg.com/raw/9b0a541954369b51e0ee76ceac86f82b.png)

### 4. Configuring an Extraction Task
The example in this document imports the data through a single full import task. For more import methods, see [Data Integration](https://cloud.tencent.com/document/product/1002/30554).
![](https://main.qcloudimg.com/raw/8ecaf4c7c6cf3242eb13ef8ae5e6b755.png)

### 5. Previewing
You can view the current set data source, data preview, target table, and task scheduling on the "Preview" page. If there are no issues, click **Done** to complete the data import task setup. Click **OK** in the pop-up dialog box to go to the task management page.
![](https://main.qcloudimg.com/raw/8494ed9c1eb06cc15d9a3bc3d9af9f95.png)
