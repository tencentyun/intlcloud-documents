Slow logs in MongoDB are often used as a basis for business operation optimization. For more information on slow logs, see [official documentation](https://docs.mongodb.com/manual/tutorial/manage-the-database-profiler/). TencentDB for MongoDB provides you with an interface to query slow logs.

>! The system records the operations of which the execution time exceeds **100 ms**.
> The slow logs are retained for 7 days. It is recommended to limit the interval between queries to 1 day.
> Only the first 10,000 slow logs can be queried. If the query is slow, you can decrease the time range for query.

### Query Methods 

The system provides two query methods, as described below:

-  **Query statistics**: Aggregate query analysis conducted based on the "command" operation type.
-  **Query details**: Details of the slow log within a specified time period.


### Query Results

The result contains four fields:
-  Query method: It is consistent with the method selected by the user. It is "Query statistics" in this case.
-  Sample statement: The statement outputted with the "command" type as the aggregation dimension. Users mainly refer to the "command" type when troubleshooting problems.
-  Average execution time (unit: ms): The average execution time (in ms) of operations aggregated in the dimension of the "command" type.
-  Total number of times: The total occurrences of operations aggregated in the dimension of the "command" type.
 ![](https://main.qcloudimg.com/raw/310550632811abdeca6cea2fd398c17b.png)


The result contains three fields:
-  Query method: It is consistent with the method selected by the user. It is "Query statistics" in this case.
-  Time consuming: The execution time of the business command (in ms).
-  Log details: The details of the business command.
![](https://main.qcloudimg.com/raw/210e70d3dc1003c2c52ddc9baa290e65.png)

