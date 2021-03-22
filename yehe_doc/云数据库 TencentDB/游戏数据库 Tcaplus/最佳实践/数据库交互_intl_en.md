## Best Practices for Game Servers
1. In use cases where not all fields need to be read from or written to, we recommend reading and updating only the required fields to avoid fetching invalid data. This can reduce the size of data transmitted over a network and reduce the number of disk reads and writes.
2. If the data record needs to be returned when a write operation is performed, we recommend setting `result_flag` as needed. For example, if the updated data record is required after an update operation is performed, the `result_flag` should be set to 2. If the data record is not required during a write operation, the `result_flag` is set to 0.
3. For the command words in batch processing tasks, such as `batchget`, `listgetall`, and `getbypartkey`, we recommend getting the data record based on `offest` and `limit`. We recommend setting the `limit` to 200 and enabling multi-package return on the game server.
4. For tables supporting the LIST data type, when a `listaddafter` operation is performed, an enqueue/dequeue rule should be set in case that the list is full. We recommend the rule to add a new record to the front and delete a record from the rear, or vise versa.
5. For tables supporting the LIST data type, a correct index should be passed for `listreplace`, `listdelete`, and `listbatchdelete` operations.
6. Before the game server reads data, make sure that the non-primary key fields of the data record to be read are not empty. For example, when there are three non-primary key fields: A, B and C, if the game server only got A and B, then it indicates that field C is empty. Please check the fields before reading a data record.
7. The game server should control the timeout locally, and we do not recommend determining the timeout based on the response package sent from the game server.
8. When the game server performs traversal, we recommend accessing data from secondary nodes at the storage layer, so as to avoid affecting the performance of primary nodes.
9. We do not recommend performing `memset` operations on large fields to avoid consuming CPU resources. You can set the values of some fields in large data structures to 0 before initialization.
10. When processing requests to TcaplusDB and responses from TcaplusDB, the game server should use the divide-and-conquer method to process partial requests sent to TcaplusDB first and then process responses returned from TcaplusDB.

## Best Practices for System Design
1. Create separate tables for the frequently used fields and the fields on which a one-time atomic operation needs to be performed.
2. When the game server writes data back, we recommend limiting traffic and discretize the data by time.
3. You can modify the table structure while using a table, and a table data conversion plugin is provided.
4. Rollback to the point in time of your cold backup or to an exact time at the table/logging level in all-server/all-region mode is supported.
5. Nodes at the access layer and the storage layer can be dynamically scaled for both all-server/all-region mode and multi-server/multi-region mode. We recommend the multi-server/multi-region mode.
6. Fields with a logical relation should be merged into one table to avoid distributed transaction problems.
7. We recommend enabling the compression feature, including the compression of request/response packages and logs.