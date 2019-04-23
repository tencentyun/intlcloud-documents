## Operation Scenario
This document describes how to use the Sparkling Notebook feature to implement simple SQL data queries and visual data analysis. For more information about data development, see [Data Development](https://intl.cloud.tencent.com/document/product/1019/30321).

## Prerequisites
Before performing data analysis, please make sure that you have created a Sparkling cluster as instructed in [Creating a Cluster](https://intl.cloud.tencent.com/document/product/1019/30314) and imported data into the cluster as instructed in [Data Import](https://intl.cloud.tencent.com/document/product/1019/30395).

## Directions
Go to [Cluster Management](https://intl.cloud.tencent.com/login) and click **Workspace** in the left pane to enter the data development page.

### 1. Creating a Notebook
Click **+** in the upper left corner of the workspace and select **Create a notebook** to create a notebook.
![](https://main.qcloudimg.com/raw/532aea20cfdc1629c0e7670ce6ccefdf.png)

### 2. Finding a Database and Data table
a. After entering the following command on the command line, press Shift + Enter or click "Run" in the upper right corner to run the command line to list the names of databases contained in the current cluster.
```
show databases
```
![](https://main.qcloudimg.com/raw/bd4531c052da3f1890b5815c5c85feb7.png)
b. Enter the following command to go to the default database.
```
use default
```
![](https://main.qcloudimg.com/raw/d6e4dbf197fdb49c3e009d1436949257.png)
c. Enter the following command to list the names of data tables contained in the default database. As you can see, the previously imported data table "new_table" already exists in the Sparkling cluster.
```
show tables
```
![](https://main.qcloudimg.com/raw/964a490ce416320a55a041739d8cf636.png)

### 3. Running a Simple SQL Statement
Run the following command to view the data information in new_table, where the pt column is a list of timestamps added when the data is imported into the Sparkling cluster. The default value is 00:00 the day before the data import date.
```
select * from new_table
```
![](https://main.qcloudimg.com/raw/d25431b5e06fb5812b67891008fad7e1.png)

### 4. Analyzing Data Visually
Run the following command to get the number of retrieved rows grouped by "enabled" and create a pie chart of the results as seen in the figure below:
```
select enabled,count(1) from new_table group by enabled
```
![](https://main.qcloudimg.com/raw/36aba2a93a390624a5b5e093dd682016.png)
Run the following command to get the number of retrieved rows grouped by "type" and create a histogram as seen in the figure below. You can click **Settings** there to set the values of keys, groups, and values.
```
select type,count(1) from new_table group by type
```
![](https://main.qcloudimg.com/raw/bcb34a5324104a878e230b3468fa625c.png)
