数据传输服务 DTS 提供基于 binlog 的增量数据订阅功能，仅需几步简单操作，即可订阅云数据库 TencentDB 的增量更新数据。

数据订阅 Kafka 版支持通过 Kafka 客户端直接消费数据。通过数据订阅功能您可以轻松实现源库的增量数据变更订阅，方便您搭建云数据库和异构系统之间的数据同步，如缓存更新，ETL（数据仓库技术）实时同步，业务异步解耦等。

## 前提条件
- 已准备好待订阅的腾讯云数据库 MySQL 、云数据库 MariaDB 或 TDSQL MySQL版，并且各数据库版本符合要求，请参见 [数据订阅支持的数据库](https://intl.cloud.tencent.com/document/product/571/42663)。
- 已在源端实例中开启 binlog。
- 已在源端实例中创建订阅帐号，需要帐号权限如下：REPLICATION CLIENT、REPLICATION SLAVE、PROCESS 和全部对象的 SELECT 权限。
具体授权语句如下：
```
create user ‘迁移账号’ IDENTIFIED BY '账号密码';
grant SELECT, REPLICATION CLIENT,REPLICATION SLAVE,PROCESS on *.* to '迁移账号'@'%';
flush privileges;
```

## 约束限制
- 订阅的消息内容目前默认保存时间为最近1天，超过保存时间的数据会被清除，请用户及时消费，避免数据在消费完之前就被清除。
- 数据消费的地域需要与订阅实例的地域相同。
- 对 MySQL、MariaDB、TDSQL MySQL 的数据订阅，当前不支持 geometry 相关的数据类型。 

## TDSQL MySQL版 数据订阅说明

- 数据订阅源是 TDSQL MySQL版 时，不支持直接执行授权语句授权，所以订阅帐号的权限需要在 [TDSQL 控制台](https://console.cloud.tencent.com/tdsqld) 单击实例名，进入帐号管理页中添加。
订阅账号所需要的权限即上述授权语句中所示权限，对于为订阅账号进行`__tencentdb__`的授权操作，在控制台修改权限弹窗中选择对象级特权，勾选所有权限即可。
- 数据订阅源是 TDSQL MySQL版 时，不支持实例创建两级分区的分表。如果实例在订阅任务发起前已经存在两级分区的分表，则校验任务不通过；如果实例在订阅任务运行中创建了两级分区分表，则订阅任务会报错暂停。
关于两级分区信息请参见 [两级分区](https://intl.cloud.tencent.com/document/product/1042/38142)。
- 数据订阅源是 TDSQL MySQL版 的订阅任务，各个分片的 DDL 操作都会被订阅并投递到 Kafka，所以对于一个分表的 DDL 操作，会出现重复的 DDL 语句。例如，实例 A 有3个分片，订阅了一个分表 tableA，那么对于表 tableA 的 DDL 语句会订阅到3条。
- Kafka 中的每条消息的消息头中都带有分片信息，以 key/value 的形式存在消息头中，key 是 ShardId，value 是 SQL 透传 ID，请参见 [分片管理](https://console.cloud.tencent.com/tdsqld)，可根据 SQL 透传 ID 区分该消息来自哪个分片。

## 支持订阅的 SQL 操作
|  类型      | 数据变更                    | 结构变更                                                    | 数据+结构变更 |
| ------ | --------------------------- | ----------------------------------------------------------- | ------------- |
| 全实例 | DML：INSERT、UPDATE、DELETE | DDL：CREATE DATABASE、CREATE TABLE、ALTER TABLE、DROP TABLE | DML+DDL       |
| 数据库 | DML：INSERT、UPDATE、DELETE | DDL：CREATE TABLE、ALTER TABLE、DROP TABLE    | DML+DDL       |
| 数据表 | DML：INSERT、UPDATE、DELETE | DDL：ALTER TABLE、DROP TABLE             | DML+DDL       |

## 操作步骤
1. 登录 [DTS 控制台](https://console.cloud.tencent.com/dts/dss)，在左侧导航选择**数据订阅**，单击**新建数据订阅**。
2. 在新建数据订阅页，选择相应配置，单击**立即购买**。
 - 计费模式：支持包年包月和按量计费。
 - 地域：地域需与待订阅的数据库实例订阅保持一致。
 - 数据库：目前支持 MySQL、Percona、MariaDB，请根据具体数据库类型进行选择。
 - 版本：选择 **kafka 版**，支持通过 Kafka 客户端直接消费。
 - 订阅实例名称：编辑当前数据订阅实例的名称。
3. 购买成功后，返回数据订阅列表，单击**操作**列的**配置订阅**对刚购买的订阅进行配置，配置完成后才可以进行使用。
![](https://qcloudimg.tencent-cloud.cn/raw/06b74af952a12f7e60a7df707c957d0c.png)
4. 在配置数据库订阅页面，选择相应配置，单击**下一步**。
 - 实例：选择对应数据库实例，只读实例和灾备实例不支持数据订阅。
 - 数据库帐号：添加订阅实例的帐号和密码，帐号具有订阅任务需要的权限，包括 REPLICATION CLIENT、REPLICATION SLAVE、PROCESS 和全部对象的 SELECT 权限。
![](https://qcloudimg.tencent-cloud.cn/raw/c1bbe02a47a94a2955a30e0c53bb61cb.png)
5. 在订阅类型和对象选择页面，选择订阅类型，单击**保存配置**。
 - 订阅类型，包括数据更新、结构更新和全实例。
    - 数据更新：订阅选择对象的数据更新，包括数据 INSERT、UPDATE、DELETE 操作。
    - 结构更新：订阅实例中全部对象的结构创建、修改和删除。
    - 全实例：包括该订阅实例的全部对象的数据更新和结构更新。
 - Kalfa 分区策略：选择按表名分区，按表名+主键分区。
 - 使用自定义分区策略：用户根据自己的需求自定义分区。
>?订阅对象会过滤掉系统库表和命名为“test”的数据库。因为 DTS 不支持系统库表的订阅，而命名为“test”的数据库被 DTS 认为是测试数据，所以都会被过滤掉。
>
![](https://qcloudimg.tencent-cloud.cn/raw/2965c8182bd59e73e4a54dbfc7b5e1ca.png)
6. 在预校验页面，预校验任务预计会运行2分钟 - 3分钟，预校验通过后，单击**启动**完成数据订阅任务配置。
>?如果校验失败，请根据失败提示在待订阅实例中进行修正，并重新进行校验。
>
![](https://qcloudimg.tencent-cloud.cn/raw/43d8d91b937eccd3d65312ed9f4ed0d2.png)
7. 单击启动后，订阅任务会进行初始化，预计会运行3分钟 - 4分钟，初始化成功后进入**运行中**状态。
8. [新增消费组](https://intl.cloud.tencent.com/document/product/571/39534)，数据订阅 Kafka 版支持用户创建多个消费组，进行多点消费。数据订阅 Kafka 版消费依赖于 Kafka 的消费组，所以在消费数据前需要创建消费组。 
9. 订阅实例进入运行中状态之后，就可以开始消费数据。Kafka 的消费需要进行密码认证，具体示例请参考 [数据消费 Demo](https://intl.cloud.tencent.com/document/product/571/39538)，我们提供了多种语言的 Demo 代码，也对消费的主要流程和关键的数据结构进行了说明。
