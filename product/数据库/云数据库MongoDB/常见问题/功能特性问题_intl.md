
### How do I obtain the slow log of an instance?
You can use the [Slow Log](https://cloud.tencent.com/document/product/240/30923) feature to get the details of a slow log.
### Does MongoDB support access via a public network?
No. However, when you are using a public network, you can access MongoDB with proxy and CVM, which provides a private network for you to connect.
### Does MongoDB require a password to access?
For security reasons, MongoDB does require a password to access
### How do I create a dump of replica set slave?
In mongodump parameters, set readPreference=secondaryPreferred.
### Can I add secondary nodes to TencentDB for MongoDB?
No.
### What is the difference between TencentDB for MongoDB and self-hosted MongoDB?
For more information, see [Benefits](https://cloud.tencent.com/document/product/240/3545).
### What is the size of oplog? Can I adjust it?
By default, oplog capacity is 10% of the instance capacity. You can adjust the number to a value between 10% (min) and  90% (max) on the console.
### Is oplog included in the purchased capacity?
Since oplog is built in the MongoDB, it will take at least 10% of the purchased capacity (10% by default).
### Which role permissions are currently available?
Only [RoleDBAdminAny and RoleReadWriteAny](https://docs.mongodb.org/v3.0/reference/built-in-roles/) are available, and root is unavailable for now. More roles may become available in the future. We will offer more user-friendly consoles for permission management.
### What happens if disk memory usage is 100 %?
The instance will be blocked, meaning that you can only read the instance, and any attempts to write operation will be disconnected. Pay attention to the instance usage, and expand the capacity as needed.
### Why MongoDB uses too much memory?
MongoDB aggressively allocates available cache memory to improve performance. For more information, see the [official documentation](https://docs.mongodb.com/manual/faq/storage/).
### Which engines are supported by MongoDB?
WiredTiger engine and Rocks engine.
### Does MongoDB support maintenance window?
No.
### Why can’t I reclaim disk space after the data was removed in MongoDB?
Unless you delete or remove databases or tables directly, you do not reclaim disk space for MongoDB to reuse freed space. To reclaim the space of the WiredTiger engine, see the [official documentation](https://docs.mongodb.com/manual/faq/storage/).
