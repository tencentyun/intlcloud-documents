
### How do I create an account in TencentDB for MariaDB?
For more information, please see [Managing Account](https://intl.cloud.tencent.com/document/product/237/7054).

### How do I access a TencentDB for MariaDB instance over the private network?
Use a CVM instance connected to the network of the TencentDB for MariaDB instance to access the private IP of the MariaDB instance. For more information, please see [Accessing Instance > Private network access](https://intl.cloud.tencent.com/document/product/237/7056).

### How do I access a TencentDB for MariaDB instance over the public network?
Install a database client on a Windows or Linux server in the public network to access the public IP of the TencentDB for MariaDB instance. For more information, please see [Accessing Instance > Public network access](https://intl.cloud.tencent.com/document/product/237/7056).

### What should I do if I forgot my TencentDB for MariaDB instance login password?
Log in to the [TencentDB for MariaDB console](https://console.cloud.tencent.com/mariadb), click an instance ID/name, and enter the instance management page. On the **Account Management** tab, locate the desired account in the account list, and select **More** > **Reset Password** in the **Operation** column.

### Can I set the permission of a TencentDB for MariaDB account on a specified field in a specified table to read-only?
No. The minimum granularity of TencentDB for MariaDB permission settings is table rather than field. This is completely the same as in MySQL.

### In the read-only account scheme for read/write separation of TencentDB for MariaDB, do I need to make special settings in my program?
Yes. You can set accessing the replica server through a read-only account in business modules where your need to read data only from the replica server.

### After read/write separation is enabled for TencentDB for MariaDB, my read-only account does not have the permission to use functions, so it cannot invoke custom functions or stored procedures. How do I change this?
A read-only account does not have the permission to run stored procedures or custom functions. This cannot be changed.
