
TencentDB for PostgreSQL instances have many status. Instances in different status support different operations. This document describes the instance lifecycle.

TencentDB for PostgreSQL instances have the following status:
![](https://main.qcloudimg.com/raw/db9949e44ed6ea29b599b89ee732e1a4.png)

- **Creating** is the initial status of instances, and instances can be used normally after creation.
-  **Running** and **Executing task** mean that the instance is running normally. Specifically, **Executing task** means that the instance is performing operations, such as modifying its configurations.
-  If a monthly subscribed instance expires or a pay-as-you-go instance has overdue payment or is terminated by users, it is **Isolated** and moved into the recycle bin.
- You can manually **Restore** an instance from the recycle bin. After that, it becomes **Running** again.
-  A pay-as-you-go instance will be retained in the recycle bin for up to three days. Three days later, it expires and will be eliminated automatically. Once eliminated, it is deleted completely, and cannot be restored or viewed in the console.
