## Problem Description
In daily Ops, if the CPU utilization of a MongoDB database is too high, it will be easy to cause system exceptions; for example, reads/writes slow down, connections are used up, and more connection timeouts occur. A large number of access timeouts will also trigger repeated reconnection and authentication on the client, which may eventually lead to a database crash.
It is very common for MongoDB databases in the production environment to experience a high CPU utilization. This problem is generally caused by SQL exceptions, high traffic, in-memory sort operations, statements without indexes, or improper use of indexes.

When the database performs operations such as query and modification, the CPU will first request data from the storage engine cache:
- If the engine cache has the target data, the CPU will execute the computing task and return the result, which may involve actions requiring high CPU usage such as sorting.
- If the cache does not have the target data, the database will get the data from the disk.
The two data acquisition processes above are called logical read and physical read, respectively. Therefore, poorly performing SQL statements can easily cause the database to generate a lot of logical reads during the execution, resulting in a high CPU utilization. They may also make the database generate a lot of physical reads, resulting in a high IOPS and I/O latency.

## Solution
DBbrain's exception diagnosis feature can easily locate the problem of high CPU utilization, determine the time when the problem occurs, find the specific SQL statement that causes the problem, and give suggestions for fix. Then, you can leverage DBbrain's slow SQL optimization feature based on the suggestions to accurately analyze the statement and avoid similar problems.

- Exception diagnosis: It detects and diagnoses exceptions 24/7 and provides optimization suggestions in real time.
- Slow SQL analysis: It analyzes slow SQL statements of the current instance and provides corresponding optimization suggestions.
- Real-time session: It displays ongoing operations in the current production database for you to handle abnormal operations.

### Option 1 (recommended): Use the "exception diagnosis" feature to troubleshoot database exceptions
The exception diagnosis feature can proactively locate and perform optimization for failures, with no Ops experience required. It can find abnormal situations with high CPU utilization. Based on TencentDB for MongoDB Ops experts' many years of experience and combined with machine learning, big data, and intelligent analysis algorithms, this feature also quickly duplicates the capabilities of senior database experts to empower your MongoDB databases for smart Ops. It can discover almost all exceptions and failures in MongoDB production databases in real time.

The steps are as shown in the example below:
1. Log in to the [DBbrain console](https://console.cloud.tencent.com/dbbrain) and select **Performance Optimization** on the left sidebar. On the displayed page, select the **Exception Diagnosis** tab.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/StQg223_20-en.png)
2. Select (enter or search for) an instance ID in the top-left corner to switch to the target instance.
3. On this page, select **Real-Time**, or select **Historical** and set the time range to be queried. If any failure occurred in this period, you can view its overview information in **Diagnosis Prompt** on the right.
4. Click **View Details** in the **Real-Time Diagnosis** or **Diagnosis Records** section or click an item in the **Diagnosis Prompt** section to enter the **Diagnosis Details** page.
 - Event overview: Includes the diagnosis item name, time range, risk level, duration, and overview.
 - Description: Includes symptom snapshots and performance trends of the exception event or health check event.
 - Intelligent Analysis: Analyzes the root cause of the performance exception to help you locate the specific operation.
 - Optimization Suggestion: Displays optimization suggestions.
5. Select the **Optimization Suggestion** tab to view the optimization suggestions provided by DBbrain for the failure.

### Option 2: Use the "slow SQL analysis" feature to troubleshoot databases/collections leading to high CPU utilization
1. Log in to the [DBbrain console](https://console.cloud.tencent.com/dbbrain) and select **Performance Optimization** on the left sidebar. On the displayed page, select the **Slow SQL Analysis** tab.
2. Select (enter or search for) an instance ID in the top-left corner to switch to the target instance.
3. On this page, select the time period to be queried. If slow SQL statements exist in this period, the time points of occurrence and the number of statements will be displayed in a bar chart in "SQL Statistics".
Click the bar chart, and the information of all corresponding slow SQL statements (those aggregated by template) will be displayed in the list below, and the consumed time distribution of SQL statements in the specified time period will be displayed on the right.
4. You can identify and filter SQL statement execution data in the SQL statement list in the following way:
 1. Sort the SQL statements by average time consumed (or maximum time consumed). Check slow SQL statements. Do not sort the statements by total time consumed, as the data may be affected by a high number of executions.
 2. Then, check the numbers of returned rows and scanned rows.
    - If there is a SQL statement with the same **number of returned rows** and **number of scanned rows**, it is very likely that the full collection has been queried and returned.
    - If there are several SQL statements with a large number of scanned rows but no or few returned rows, it means that the system generated a lot of logical and physical reads. If the volume of the data to be queried is too high and memory is insufficient, the request will generate many physical I/O requests and consume lots of I/O resources. Too many logical reads will occupy too many CPU resources, resulting in high CPU utilization.

### Option 3: Use the "real-time session" feature to kill slow SQL statements
The MongoDB kernel records the currentOp information. DBbrain's real-time session feature enables you to view all the operations being executed in the database and kill specified time-consuming SQL statements. This releases resources such as CPU and disk I/O. In addition, the **Kill Sessions during a Period** option can continuously kill sessions based on specified conditions. If the database is blocked, you can use this option to fix the exception swiftly.

- Kill session:
  - Click **Performance Optimization** > **Real-Time Session** > **Active Session**, select the session to be killed, and kill it.
- Kill sessions during a period:
  - The **Kill Sessions during a Period** option can be configured in dimensions such as database, host, type, and time. There are two trigger mechanisms: **Scheduled stop** and **Manual stop**.  
  - To stop killing sessions during a period, click **Stop** to close upcoming scheduled tasks or terminate manually triggered tasks.

