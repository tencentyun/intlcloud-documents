### How do I get the slow logs of an instance?
You can use the [Slow Log Query](https://intl.cloud.tencent.com/document/product/240/31454) feature to get the slow log details.

### Does MongoDB support access over the public network?
No. You have to set up a proxy to use the public network. You can purchase a CVM instance and access over a private network.

### Does MongoDB support password-free access?
For security reasons, MongoDB does not support password-free access.

### How do I set secondary database dump?
In mongodump parameters, set `readPreference=secondaryPreferred`.

### Does TencentDB for MongoDB support adding secondary nodes dynamically?
No.

### What is the difference between TencentDB for MongoDB and self-created MongoDB?
For more information, please see [Strengths](https://intl.cloud.tencent.com/document/product/240/3545).

### What is the size of oplog? Can I adjust it?
The default oplog size is 10% of the instance capacity. You can adjust it between 10% (minimum) and 90% (maximum) of the instance capacity in the console.

### Is oplog included in the purchased capacity?
As oplog exists inside the MongoDB database, it will occupy a part of the purchased capacity (10% by default).

### What role permissions are available currently?
Only [RoleDBAdminAny and RoleReadWriteAny](https://docs.mongodb.org/v3.0/reference/built-in-roles/) are available, and root privileges are unavailable for now. More roles will become available in the future. We will also open up more convenient and practical console features to eliminate the need to call for some special permissions.

### What will happen if disk utilization reaches 100%?
At this point, the instance will be blocked and become read-only, and any connections for write attempts will be closed. Please pay attention to your business development and instance usage and expand the capacity as appropriate when capacity usage reaches a certain level.

### Why does the monitor show high memory utilization in MongoDB?
MongoDB uses a greedy policy to try to allocate available memory for caching to improve performance. For more information, please see [FAQ: MongoDB Storage](https://docs.mongodb.com/manual/faq/storage/).

### Which engines are supported by MongoDB?
WiredTiger engine and Rocks engine are supported currently.

### Does MongoDB support maintenance window?
No.

### Why is the space not reclaimed after data in MongoDB is deleted?
Unless a database or table is dropped directly, the space freed by deleted data will not be reclaimed in MongoDB. To reclaim the space of the WiredTiger engine, please see [FAQ: MongoDB Storage](https://docs.mongodb.com/manual/faq/storage/).
