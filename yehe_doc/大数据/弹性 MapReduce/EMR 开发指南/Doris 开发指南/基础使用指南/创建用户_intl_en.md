Doris uses the MySQL protocol to communicate. You can connect to a Doris cluster through a MySQL client or MySQL JDBC. When selecting the MySQL client version, you are advised to use a version after 5.1, because usernames of more than 16 characters are not supported before 5.1. This document takes MySQL client as an example to show you the basic usage of Doris through a complete process.

>!Change the Knox password only when resetting the native UI password. Doris' UI authentication password is the same as the cluster password.

## Root User Login and Password Modification
Doris has built-in root and admin users, and the password is the same as the cluster password. After starting the Doris program, you can connect to the Doris cluster through the root or admin user. Use the following command to log in to Doris:
```
mysql -h FE_HOST -P9030 -uroot
```
Parameter description:
- `FE_HOST` is the IP address of any FE node.
- `9030` is the `query_port` configuration in `fe.conf`.

After login, you can modify the root password with the following command:
```
SET PASSWORD FOR 'root' = PASSWORD('your_password');
```

## Creating a User
Create an ordinary user with the following command:
```
CREATE USER 'test' IDENTIFIED BY 'test_passwd';
```

Subsequent login can be done with the following connection command:
```
mysql -h FE_HOST -P9030 -utest -ptest_passwd
```
By default, the newly created ordinary user does not have any permissions. To grant permissions, see [Account Authorization](https://intl.cloud.tencent.com/document/product/1026/40262).
