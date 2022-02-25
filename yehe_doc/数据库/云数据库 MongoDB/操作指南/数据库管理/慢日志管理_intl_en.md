You can view and analyze the slow logs generated during database operations in the TencentDB for MongoDB console for targeted database performance optimization. 

## Background
- Slow logs are often used as the basis for optimizing business operations in MongoDB. For more information, see [Database Profiler](https://docs.mongodb.com/manual/tutorial/manage-the-database-profiler/). 
- The system provides two query methods as described below:
  - Query statistics: slow logs for the specified time period are queried, and the query results are aggregated and analyzed by command (operation) type.
  - Query details: a specific operation command is specified to query slow logs, and the query results are displayed in a list displaying the execution durations and log details.

## Version Description
Currently, TencentDB for MongoDB 4.2, 4.0, 3.6, and 3.2 support slow log management.

## Notes
- The system logs operations with an execution time of more than 100 ms.
- The slow logs are retained for 7 days. The time span for a single query cannot exceed 1 day.
- Only the first 10,000 slow logs can be queried. If the query is slow, you can narrow down the query time period.

## Prerequisites
- You have [applied for a TencentDB for MongoDB instance](https://intl.cloud.tencent.com/document/product/240/3551).
- The TencentDB for MongoDB replica set or sharded instance is in **Running** status.

## Directions
### Querying slow log
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Replica Set Instance** or **Sharded Instance**. The directions for the two types of instances are similar.
3. Above the instance list on the right, select the region.
4. In the instance list, find the target instance.
5. Click the target instance ID to enter the **Instance Details** page.
6. Select the **Database Management** > **Slow Log Query** tab.
7. On the **Slow Log Query** tab, select a **query method** to query slow logs.
  - **Query statistics**: select a **query time period**, set the **time consumed** threshold, and click **Query**.
  - **Query details**:
    1. Select the specific executed command to be queried in **Executed Command**.
    2. Select a **query time period**, set the **time consumed** threshold, and click **Query**.
8. View and analyze the slow logs.
  - A **statistics query** result contains four fields:
    - **Query Method**: statistics query.
    - **Sample Command**: output statements aggregated in the command type dimension. You mainly need to refer to the command when troubleshooting problems.
    - **Average Execution Time (ms)**: average execution time (in ms) of operations aggregated in the command type dimension.
    - **Total**: total occurrences of operations aggregated in the command type dimension.
![](https://main.qcloudimg.com/raw/07a66dab61f3842de50b400faf3b08d5.png)
  - A **details query** result contains three fields:
    - **Query Method**: details query.
    - **Time Consumed**: execution time of the business command (in ms).
    - **Log Details**: details of the business command.
![](https://main.qcloudimg.com/raw/e063ea622dbd6bb8b73d4b488a33d2ae.png)

### Slow log management
#### Viewing slow log request statement
1. On the **Slow Query Management** page, you can view the slow log request statements.
2. In the search box in the top-right corner, enter the information to be queried for search.
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Query Statement</td><td>Query statement.</td></tr>
<tr>
<td>Op Type</td><td>Operation type.</td></tr>
<tr>
<td>Node Location</td><td>Node of the executed operation.</td></tr>
<tr>
<td>Namespace</td><td>Namespace of the database table.</td></tr>
<tr>
<td>Executed Time</td><td>Time consumed.</td></tr>
<tr>
<td>Details</td><td>Details of the executed statement.</td></tr>
</tbody></table>

#### Batch killing
1. On the **Slow Query Management** page, select the slow log request statements to be cleared.
2. Click **Batch Kill** above the list.
3. In the **Note** pop-up window, read the prompt carefully.
4. Click **OK**.

### Downloading slow log file
1. On the **Slow Log Download List** page, you can view current slow log files.
2. Find the file to be downloaded and click **Download** in the **Operation** column.

## Related APIs
| API | Description |
| ----------------------- | ------------------------------------------------------------ |
| DescribeSlowLogs        | [Gets slow log information](https://intl.cloud.tencent.com/document/product/240/36929) |
| DescribeSlowLogPatterns | [Gets slow log statistics](https://intl.cloud.tencent.com/document/product/240/36930) |

