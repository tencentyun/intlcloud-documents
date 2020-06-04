## 云硬盘的典型应用场景
### 去本地化
- **高性能高可靠数据存储**：云硬盘可高效地支持云服务器热迁移，提前避免物理故障带来的业务中断。云硬盘提供三份数据冗余，具备完善的数据备份、快照、数据秒级恢复能力。云硬盘适用于高负载、核心关键业务系统。
- **弹性扩容**：云硬盘可在同一可用区内自由挂载、卸载，无需关闭/重启云服务器。云硬盘的容量可弹性配置，按需扩容。
![](https://main.qcloudimg.com/raw/1cdbb7fadac1aa88d823eba12a106522.png)

### 海量数据分析
典型的 Spark-HDFS 离线数据分析框架对于磁盘的读写 RDD read/write、shuffle write 都是顺序 I/O，只有 shuffle read I/O 是随机 I/O，顺序 I/O 比例高达95%。云硬盘的多线程并发吞吐性能优秀，高效支持 Hadoop-Mapreduce、HDFS、Spark，TB/PB 级数据的离线处理。
多磁盘并发，单 HDFS 集群可达到1GB/s的吞吐性能。
小红书、巨人网络、饿了么、Yoho!BUY 有货、微票儿等大企业已在云硬盘上广泛开展数据分析、挖掘、商业智能等大数据实践。
![](https://main.qcloudimg.com/raw/4be675dc660f05c9a7fcd35d9e83973d.png)
**部署环境**：12Core 40GB RAM 云服务器5台，模拟离线数据分析1.5TB数据量。
**测试性能**：

- 每台云服务器各挂载1块1TB普通云盘，5块普通云盘提供500MB/s的读取速度，50分钟读取到内存。
- 每台云服务器各挂载1块1TB SSD 云硬盘，25分钟读取到内存。

### 核心数据库
SSD 云硬盘适合对 I/O 性能要求高，同时对数据可靠性要求也高的场景。尤其适合如 PostgreSQL、MySQL、Oracle、SQL Server 等中大型关系数据库应用、对数据可靠性要求高的 I/O 密集型等核心业务系统以及对数据可靠性要求高的中大型开发测试环境。
SSD 云硬盘完美兼顾了数据可靠性与高性能表现，已为英魂之刃、问道、Yoho!BUY 有货、微票儿、小红书等大企业提供可靠支持。
![](https://main.qcloudimg.com/raw/a826f514194aad6d398069b00ab817da.png)
**部署环境**：4Core 8GB RAM 云服务器4台，分别挂载1块800G的 SSD 云硬盘，部署 MySQL version 5.5.42。
**测试性能**：用 sysbench 模拟 OLTP 性能测试，测试集为1千万条记录，TPS 可达1616，QPS 达29000，单盘足以支撑每秒上万人的在线同时交易。



## 典型业务场景 I/O 模型
- **整点数据落盘**
![](https://main.qcloudimg.com/raw/11e16a3ee744c3cdd313de199b461881.png)
- **高负载 OLTP 业务**
![](https://main.qcloudimg.com/raw/a835908f6a9bcaf8407a299607d33dee.png)
- **周期性超高负载**
![](https://main.qcloudimg.com/raw/66b6e76d8cc2d477698a21e12cffff8d.png)
- **持续高顺序读写**
![](https://main.qcloudimg.com/raw/f08c8eb9b38a1bf0a94cec35fea5538e.png)
