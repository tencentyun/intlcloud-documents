

### 垂直切分

一个数据库由很多表构成，每个表对应着不同的业务。垂直切分是指按照业务功能将表进行分类，分布到不同的数据库上。



### 单表

单表指主要用于存储一些无需分片的表。该表的数据全量存在第一个物理分片中，所有该类型的表都放在第一个物理分片中，语法和使用方法和 MySQL 完全一样，您可以把他理解为一个非分布式的表。

### DDL

参见 [数据库模式定义语言](#ddl1)

### DML

参见 [数据库操纵语言](#dml1)



### 分表

分表指原有数据量极大的表，需要切分到多个数据库节点，这样每个物理分片都有一部分数据，所有物理分片构成了完整的数据。
<span id="shardkey1"></span>
### 分表键

TDSQL 通过采用分表键求模的方案进行分表。
<span id="tdsql1"></span>
### TDSQL MySQL版

TDSQL MySQL版（TDSQL for MySQL，TDSQL）是部署在腾讯云上的一种支持自动水平拆分、Shared Nothing 架构的分布式数据库。分布式数据库即业务获取的是完整的逻辑库表，而后端会将库表均匀的拆分到多个物理分片节点。TDSQL 默认部署主备架构，提供容灾、备份、恢复、监控、迁移等全套解决方案，适用于 TB 或 PB 级的海量数据库场景。



### 广播表

广播表又名小表广播功能，设置为广播表后，该表的所有操作都将广播到所有物理分片中，每个分片都有该表的全量数据。
<span id="OLAP1"></span>
### 联机分析处理

联机分析处理（On-Line Analytical Processing），是数据仓库系统的主要应用，支持复杂的分析操作，侧重决策支持，并且提供直观易懂的查询结果。
<span id="OLTP1"></span>
### 联机事务处理

联机事务处理（On-Line Transaction Processing），是传统的关系型数据库的主要应用，主要是基本的、日常的事务处理，例如银行交易。



### OLAP

参见 [联机分析处理](#OLAP1)

### OLTP

参见 [联机事务处理](#OLTP1)



### Percona

Percona 完全兼容 MySQL 协议，且功能和性能上较 MySQL 有显著的提升。目前 TDSQL 已支持 Percona 5.7 版本。

### Proxy

TDSQL 通过 Tproxy 实现自动分库分表逻辑，管理底层的多个物理数据库实例，对客户端提供唯一的兼容 MySQL 数据库服务端口。



### 强同步

强同步是一种基于 MySQL 协议的异步多线程强同步复制方案。

### 全局唯一数字序列

全局唯一数字序列简称 sequence，使用的是 unsigned long 类型，8个字节长，目前 TDSQL 可以保证该字段全局唯一和有序递增。



### shardkey

参见 [分表键](#shardkey1)

### 水平切分

水平切分指按照某种规则，将一个表的数据分散到多个物理独立的数据库服务器中，形成“独立”的数据库“分片”。多个分片共同组成一个逻辑完整的数据库实例。
<span id="dml1"></span>
### 数据库操纵语言

数据库操纵语言（Data Manipulation Language），命令是 SELECT、UPDATE、INSERT、DELETE。

<span id="ddl1"></span>
### 数据库模式定义语言

数据库模式定义语言（Data Definition Language），主要的命令有 CREATE、ALTER、DROP 等。



### TDSQL

参见 [TDSQL MySQL版](#tdsql1)
