You can analyze MongoDB slow operation logs to improve your database performance. For more information, see [official documentation](https://docs.mongodb.com/manual/tutorial/manage-the-database-profiler/). TencentDB for MongoDB provides you with an interface to query slow operation logs.

>! By default, the slow operation threshold is **100 milliseconds**. Databases with a profiling level of 1 will profile operations slower than the threshold.
> The slow operation logs are kept for 7 days. It is recommended to limit the interval between queries to 1 day.
> You can query only the first 10,000 slow operation logs. If the query is slow, you can narrow down the time range.
### Query Types
The system provides two types of query, as described below:

-  **Query statistics**: **Query statistics**: Analysis of aggregation "command".
-  **Query details**: Details of the slow log within a specified time period.


### Query Results

The result of query statistics contains four fields:
-  Query method: It is consistent with the method selected by the user. It is "Query statistics" in this case.
-  Sample statement: The statement returned by aggregation  "command". Users can refer to the "command" when troubleshooting problems.
-  Average execution time (unit: ms): The average execution time (in ms) of the aggregation "command".
-   Total number of logs: The count of the aggregation “command”.
 ![](https://main.qcloudimg.com/raw/310550632811abdeca6cea2fd398c17b.png)


The result of query details contains three fields:
-  Query method: It is consistent with the method selected by the user. It is "Query statistics" in this case.
-  Time consuming: The execution time of the command (in ms).
-  Log details: The details of the command.
![](https://main.qcloudimg.com/raw/210e70d3dc1003c2c52ddc9baa290e65.png)
