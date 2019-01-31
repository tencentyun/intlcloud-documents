[//]: # (chinagitpath:XXXXX)

Sparkling provides a data development IDE for data ETL, cleansing and computation and supports task scheduling. Notebook is the core functional component of the IDE and makes it easy to manage tasks.

## Steps
1. Go to [Cluster Management](https://sparkling.cloud.tencent.com) and click **Workspace** in the left pane to enter the data development page.
2. Manage the notebooks.
In the left pane, you can create, refresh, rename or delete a notebook. ![](https://main.qcloudimg.com/raw/4c087c9efd885ec598280341edd1ff3f.png)
3. Edit the execution command.
![](https://main.qcloudimg.com/raw/c435fd5cd293d7cd56f6a340495d5368.png)
   a. Run and view the execution result.
   Enter the SQL statement in the command bar. Run it with the corresponding button in the upper right corner or press Shift+Enter to view its execution result.
   b. Visualize the query result.
   Use the following buttons to visualize the query result, such as drawing a histogram or pie chart.
     ![](https://main.qcloudimg.com/raw/b8e44722879e2fd3505eb68447127777.png)
   c. Download the query result.
   The query result can be downloaded as a .csv or .tsv file.
   d. Add a code snippet.
   Click **Add a code snippet** below to add a new command bar.
   e. Run all commands.
   Click **Run all** in the upper left corner to execute the statements in all the command bars in the current notebook.
     f. Set the timed scheduling.
   Click **Timed scheduling** at the top left corner to pop up the timed scheduling setting box. You can select the interval and define the time. For example, 00:00 daily indicates that the task starts automatically at 00:00 every day. After selecting the regular task duration and concurrent/serial setting, click **OK** to complete the timed scheduling setting. The details of the notebook task can be viewed in the **Tasks** column on the left.
> After the scheduling interval is set, the first execution of the task will be at the start time + one scheduling interval.
>
![](https://main.qcloudimg.com/raw/78554cce688048dbfcc196ad18760000.png)

4. Use the SQL IDE.
You can go to the SQL IDE to view data table information and manage, query or download data.
a. Enter the SQL IDE interface.
In the upper right corner, click <img src="https://main.qcloudimg.com/raw/712bdbcd5c1001d683646a11b0c9557d.png"  style="margin:0;"> to enter the SQL IDE interface.
b. View the data directory.
In the left pane of the SQL IDE interface, you can view all the created and authorized data in the current cluster.
![](https://main.qcloudimg.com/raw/f8d637c722862ba8438660a1a5ea4bae.png)
c. Edit the SQL code.
The SQL editor on the right can be used to edit the code. Currently, SQL supports DDL and DML syntax and is fully compatible with ANSI SQL 2003. After editing, click **Execute** below to view the time used, update time and running result as well as visualize or download the data.
![](https://main.qcloudimg.com/raw/ccfaef11000a8bebcebc4d87358597ba.png)
 




 



