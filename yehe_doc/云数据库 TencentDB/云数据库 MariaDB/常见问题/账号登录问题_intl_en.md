
### How do I create an account in TencentDB for MariaDB?
For detailed directions, please see [Creating Accounts](https://cloud.tencent.com/document/product/237/7054).

### How do I access a TencentDB for MariaDB instance over the private network?
Private network access: you can use a CVM instance connected to the network of the TencentDB for MariaDB instance for access over the private network.
For detailed directions, please see [Private Network Access](https://cloud.tencent.com/document/product/237/7056#.E5.86.85.E7.BD.91.E8.AE.BF.E9.97.AE).

### How do I access a TencentDB for MariaDB instance over the public network?
Public network access: on a Windows or Linux server in the public network, install a database client to access the public network address of the TencentDB for MariaDB instance.
For detailed directions, please see [Public Network Access](https://cloud.tencent.com/document/product/237/7056#.E5.A4.96.E7.BD.91.E8.AE.BF.E9.97.AE).

### What should I do if I forgot my TencentDB for MariaDB instance login password?
In the [TencentDB for MariaDB Console](https://console.cloud.tencent.com/tdsql), select "Account Management" on the instance details page and select **More** > **Reset Password** in the "Operation" column to reset the password.

### Can I set the permission of a TencentDB for MariaDB account on a specified field in a specified table to read-only?
The minimum granularity of TencentDB for MariaDB permission settings is table rather than field. This is completely the same as in MySQL.

### In the read-only account scheme for read/write separation of TencentDB for MariaDB, do I need to make special settings in my program?
Yes. You can set accessing the slave through a read-only account in places where the slave can be accessed.

### After read/write separation is enabled for TencentDB for MariaDB, my read-only account does not have the permission to use functions, so it cannot invoke custom functions or stored procedures. How do I change this?
A read-only account does not have the permission to run stored procedures or custom functions. This cannot be changed.


