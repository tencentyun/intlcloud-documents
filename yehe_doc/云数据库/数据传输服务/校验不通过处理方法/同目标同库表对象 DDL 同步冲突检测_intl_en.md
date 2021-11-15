## Check Details 

In scenarios where multiple sync tasks need to be configured, such as many-to-one sync and active-active sync, the same table object cannot receive DDL sync from multiple IDCs; otherwise, such DDL statements may conflict with each other in the target database, causing errors. 

For example, as shown below, databases A and C have tables with the same name to be synced to database B. Then, you can select DDL in only one task between tasks 1 and 4.  

<img src="https://main.qcloudimg.com/raw/273f8bdd817008e04f79a1e5a18d049e.png" style="zoom:40%;" />

## Fix

Modify the sync task configuration. In **Set sync options and objects** > **Data Sync Option** > **SQL Type**, modify the DDL parameter configuration to avoid the situation where the same table object receives DDL sync from multiple IDCs.

