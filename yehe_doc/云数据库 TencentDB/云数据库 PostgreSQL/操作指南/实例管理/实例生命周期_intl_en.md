
TencentDB for PostgreSQL instances have many statuses. Instances in different statuses support different operations. This document describes the instance lifecycle.

TencentDB for PostgreSQL instances have the following statuses:
![](https://main.qcloudimg.com/raw/6b7bfa3d39d2971f74b16609ea47c146.svg)

-  **Creating**, **Uninitialized**, and **Initializing** are initial statues. An instance must go through the three statuses before it can be used normally.
-  **Running** and **Executing task** mean that the instance is running normally. Specifically, **Executing task** means that the instance is performing operations, such as modifying its configurations.
-  If a pay-as-you-go instance has overdue payment or is terminated by users, it is **Isolated** and moved into the recycle bin.
-  An instance in the recycle bin can be manually **restored**. After that, it becomes **Running** again.
-  A pay-as-you-go instance will be retained in the recycle bin for up to three days. Three days later, it expires and will be eliminated automatically. Once eliminated, it is deleted completely, and cannot be restored or viewed in the console.
