## Check Details 
In scenarios where multiple sync tasks need to be configured, such as two-way sync, many-to-one sync, and active-active sync, DDL configuration should not form a ring; otherwise, DDL statements will loop in the system, causing errors.

For example, among the three sync tasks (1, 3, and 5) marked by blue lines in the following figure, you can select DDL in up to two of them, and if you select three, a ring will be formed. 

<img src="https://main.qcloudimg.com/raw/273f8bdd817008e04f79a1e5a18d049e.png" style="zoom:40%;" />

## Fix
Modify the sync task configuration. In **Set sync options and objects** > **Data Sync Option** > **SQL Type**, modify the DDL parameter configuration to avoid rings.

