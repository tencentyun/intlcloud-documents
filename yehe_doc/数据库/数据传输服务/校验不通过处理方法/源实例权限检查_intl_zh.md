
## 检查详情
检查用户是否具备对数据库的操作权限，具体参考如下对应链接。

- 数据迁移权限要求

   - [MySQL/TDSQL-C/MariaDB/Percona 之间的数据迁移](https://intl.cloud.tencent.com/document/product/571/42645)
   - [MySQL/MariaDB/Percona/TDSQL MySQL 与 TDSQL MySQL 之间的数据迁移](https://intl.cloud.tencent.com/document/product/571/47366)
   -  [PostgreSQL 数据迁移](https://intl.cloud.tencent.com/document/product/571/42640)
   -  [MongoDB 数据迁移](https://intl.cloud.tencent.com/document/product/571/42639)
   -  [SQL Server 数据迁移](https://intl.cloud.tencent.com/document/product/571/42638)

- 数据同步权限要求
   - [MySQL/TDSQL-C/MariaDB/Percona 之间的数据同步](https://intl.cloud.tencent.com/document/product/571/47344)
   - [MySQL/MariaDB/Percona/TDSQL MySQL 与 TDSQL MySQL 之间的数据同步](https://intl.cloud.tencent.com/document/product/571/47350)


- 数据订阅权限要求
   - [MySQL/MariaDB/TDSQL MySQL/TDSQL-C MySQL 数据订阅](https://intl.cloud.tencent.com/document/product/571/47354)    
   - [TDSQL PostgreSQL 版数据订阅](https://intl.cloud.tencent.com/document/product/571/47357)   

## TDSQL PostgreSQL 版检查内容
用户必须拥有 REPLICATION 权限，对应 pg_roles.rolreplication。

用户必须拥有被订阅表的 select 权限，如果是整库订阅，那么用户要拥有该 schema 下所有表的 select 权限。

## 修复方法

用户可能不具备操作权限，请按照检查要求中的对应权限要求对用户进行授权，然后重新执行校验任务。

