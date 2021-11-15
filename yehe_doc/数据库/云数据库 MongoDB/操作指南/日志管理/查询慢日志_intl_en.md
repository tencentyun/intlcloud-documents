Slow logs are often used as the basis for optimizing business operations in MongoDB. For more information on slow logs, please see [Database Profiler](https://docs.mongodb.com/manual/tutorial/manage-the-database-profiler/). You can query slow logs in the [TencentDB for MongoDB Console](https://console.cloud.tencent.com/mongodb).

>?
>- The system logs operations with an execution time of more than 100 ms.
>- The slow logs are retained for 7 days. You are recommended to limit the query time range within 1 day.
>- Only the first 10,000 slow logs can be queried. If the query is slow, you can narrow down the query time range.


Log in to the [TencentDB for MongoDB Console](https://console.cloud.tencent.com/mongodb) and click an instance ID to enter the instance management page. Select **Database Management** > **Slow Log Query**.

#### Query Methods 
The system provides two query methods as described below:
- Query statistics: aggregate query analysis conducted based on the `command` (operation) type.
- Query details: details of the slow logs within a specified time period.

#### Query Results
The statistics query result contains four fields:
- Query Method: it is consistent with the method selected by the user, which is "Query statistics" in this case.
- Sample Statement: the statement output with the `command` type as the aggregation dimension. You mainly need to refer to the `command` type when troubleshooting problems.
- Average Execution Time (ms): the average execution time (in ms) of operations aggregated in the dimension of the `command` type.
- Total: the total occurrences of operations aggregated in the dimension of the `command` type.
![](https://main.qcloudimg.com/raw/07a66dab61f3842de50b400faf3b08d5.png)


A details query result contains three fields:
- Query Method: it is consistent with the method selected by the user, which is "Query statistics" in this case.
- Time Consumed: the execution time of the business command (in ms).
- Log Details: the details of the business command.
![](https://main.qcloudimg.com/raw/e063ea622dbd6bb8b73d4b488a33d2ae.png)
