Before using the TDSQL-C for MySQL, you need to have 2 accounts, namely the Tencent Cloud console account and the database account. These two accounts are used to access the console and your database, respectively. This document describes the information of the two accounts.

## Tencent Cloud Console Account
Before starting using Tencent Cloud services, you need to register a Tencent Cloud account first. Then you can log in to the Tencent Cloud website or console with the account. For detailed directions, see [Signing Up](https://intl.cloud.tencent.com/document/product/378/17985).

## Database Account
When TDSQL-C for MySQL cluster is created, the system will retain the default account. In addition, you can also create a custom account as needed to allocate and manage databases conveniently.

### Default account

| Default System Account | Host | MySQL 5.7 | MySQL 8.0 | Description |
|---------|---------|---------|---------|---------|
| root | % | &#10003; | &#10003; | Admin account, which has permissions to perform all operations. |
| mysql.sys | localhost | &#10003 |&#10003 | The account used to manage and access the system's built-in `sys` database, through which you can quickly understand the metadata information of the system. |
| mysql.session | localhost | - |&#10003  | The account used by internal plugins to access the server. |
| mysql.infoschema | localhost | - |&#10003 | The account used to manage and access the system's built-in `information_schema` database. |

<dx-alert infotype="alarm" title="">
To avoid database problems, we recommend you not delete the default account.
</dx-alert>

### Non-default account
In addition to the default account, you can create other database accounts in the console as needed. For more information, see [Creating Account](https://www.tencentcloud.com/document/product/1098/44612)
