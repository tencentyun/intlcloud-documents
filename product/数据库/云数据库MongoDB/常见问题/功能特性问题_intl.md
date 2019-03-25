
### How do I obtain the slow log of an instance?
You can use the [Slow Log](https://cloud.tencent.com/document/product/240/30923) feature to get the details of a slow log.

### Does MongoDB support access via a public network?
No. You have to set up a proxy directly to use a public network. You can purchase a CVM and access via a private network.

### Does MongoDB support passwordless access?
For security reasons, passwordless access is not supported by MongoDB.

### How do I set slave database dump?
In mongodump parameters, set readPreference=secondaryPreferred.

### Does TencentDB for MongoDB support adding secondary nodes dynamically?
No.

### What is the difference between TencentDB for MongoDB and client's MongoDB?
For more information, see [Benefits](https://cloud.tencent.com/document/product/240/3545).

### What is the size of oplog? Can I adjust it?
The default oplog capacity is 10% of the instance capacity. You can adjust its size from 10% (min) to 90% (max) of the instance capacity on the console.

### Is oplog included in the purchased capacity?
Since oplog exists inside the MongoDB database, it will occupy part of the purchased capacity (10% by default).

### Which role permissions are available at present?
Only [RoleDBAdminAny and RoleReadWriteAny](https://docs.mongodb.org/v3.0/reference/built-in-roles/) are available, and root is unavailable for now. More roles will become available in the future. We will also open up more convenient and practical console features to replace the need to call for some special permissions.

### What happens if disk usage reaches 100%?
At this point the instance will be banned, in which case it will become read-only, and any connections for write attempt will be closed. Pay attention to your business development and instance usage, and expand capacity as appropriate when capacity usage reaches a certain level.

### Why does the monitor show high memory utilization of MongoDB?
MongoDB uses a greedy strategy to try to allocate available memory for caching to improve performance. For more information, see the [official documentation](https://docs.mongodb.com/manual/faq/storage/).

### Which engines are supported by MongoDB?
WiredTiger engine and Rocks engine.

### Does MongoDB support maintenance window?
No.

### Why is the space not repossessed after data in MongoDB is deleted?
Unless a database or table is deleted directly, the space freed by deleted data will not be repossessed in MongoDB. To repossess the space of the WiredTiger engine, see the [official documentation](https://docs.mongodb.com/manual/faq/storage/).




 

