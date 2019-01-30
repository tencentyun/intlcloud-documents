[//]: # (chinagitpath:XXXXX)

## Operation Scenario
Sparkling allows you to manage and schedule DAG tasks, including notebook development tasks and data ingestion tasks. You can choose whether to turn on a task or execute it immediately and view its execution time and execution details. A notebook development task begins with "notebook_" in its name, while a data ingestion task "datasync_". This documents demonstrates how to manage and execute tasks in the Sparkling console.

## Steps
Go to [Cluster Management](https://sparkling.cloud.tencent.com) and click **Tasks** in the left pane to enter the task management page.

- **Turn on\off a task**
Click the button in the first column on the page to switch the task status. <img src="https://main.qcloudimg.com/raw/d25cb38692eebd853f4b0e44db2d3c06.png"  style="margin:0;"> indicates that the task is turned on, while <img src="https://main.qcloudimg.com/raw/d35010f3ae26248e6e0be5c454db479b.png"  style="margin:0;"> means that the task is turned off. After the page is refreshed, tasks turned off will not be displayed, but they can be retrieved by clicking **Show Paused DAGs** at the bottom left corner.
- **View task details**
Click the second column (DAG) to view the task's DAG details. Click the third column (Component) to view the task details. You will be able to view the information about data source, target table, extraction rule and timed tasks for a Datasync task, and you will be redirected to the Notebook page for a Notebook task.
- **View task scheduling time**
You can view the task's cron code in the fourth column (Schedule) and its last execution time in the seventh column (Last Run). Please note that the time zone in this column is UTC, which is 8 hours behind Beijing time.
- **View task status**
The last task execution status can be viewed in the sixth column (Recent Task).
- **View task execution history**
The eighth column (DAG Runs) shows the number of times the task succeeds and fails and the running status of the task.
- **Execute immediately\refresh a task**
Click the Trigger Dag button in the last column (Links) to manually trigger the task for immediate execution and click the refresh button to refresh the task status.
![](https://main.qcloudimg.com/raw/9d09e148258aafd7a9ef3eb5762e77f0.png)
