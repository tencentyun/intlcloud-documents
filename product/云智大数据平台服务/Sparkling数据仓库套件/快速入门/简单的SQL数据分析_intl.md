## Operation Scenario
This document describes how to use the Sparkling Notebook feature to implement simple SQL data queries and visual data analysis. For more information about data development, see [Data Development](https://cloud.tencent.com/document/product/1002/30555).

## Prerequisites
Before performing data analysis, please make sure that you have created a Sparkling cluster as instructed in [Creating a Cluster](https://cloud.tencent.com/document/product/1002/30551) and imported data into the cluster as instructed in [Data Import](https://cloud.tencent.com/document/product/1002/34144).

## Directions
Go to [Cluster Management](https://sparkling.cloud.tencent.com) and click **Workspace** in the left pane to enter the data development page.

### 1. Creating a Notebook
Click **+** in the upper left corner of the workspace and select **Create a notebook** to create a notebook.
![](https://main.qcloudimg.com/raw/488a8fcb1ec3f7be04d97aba6bf8ad37.png)

### 2. Finding a Database and Data table
a. After entering the following command on the command line, press Shift + Enter or click "Run" in the upper right corner to run the command line to list the names of databases contained in the current cluster.
```
show databases
```
![](https://main.qcloudimg.com/raw/f9462809f8c722ac8087f2b978f0ab23.png)
b. Enter the following command to go to the default database.
```
use default
```
![](https://main.qcloudimg.com/raw/3fa7a16a31a74cab4bd174182a6edd42.png)
c. Enter the following command to list the names of data tables contained in the default database. As you can see, the previously imported data table "new_table" already exists in the Sparkling cluster.
```
show tables
```
![](https://main.qcloudimg.com/raw/e3ee9c1c2d8cab750b92d821fd7bbaa1.png)

### 3. Running a Simple SQL Statement
Run the following command to view the data information in new_table, where the pt column is a list of timestamps added when the data is imported into the Sparkling cluster. The default value is 00:00 the day before the data import date.
```
select * from new_table
```
![](https://main.qcloudimg.com/raw/80ff8ed287fc30028d24d0f557f16f7f.png)

### 4. Analyzing Data Visually
Run the following command to get the number of retrieved rows grouped by "enabled" and create a pie chart of the results as seen in the figure below:
```
select enabled,count(1) from new_table group by enabled
```
![](https://main.qcloudimg.com/raw/2799eac2a99b772c1c09b771b98c9b0c.png)
Run the following command to get the number of retrieved rows grouped by "type" and create a histogram as seen in the figure below. You can click **Settings** there to set the values of keys, groups, and values.
```
select type,count(1) from new_table group by type
```
![](https://main.qcloudimg.com/raw/8e088464e329c30f7a6b9426885a454f.png)
