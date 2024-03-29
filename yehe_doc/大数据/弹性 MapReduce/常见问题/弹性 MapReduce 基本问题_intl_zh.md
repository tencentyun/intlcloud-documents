### 如何查看任务日志？
可登录任意一台 EMR 服务器执行以下命令查看任务日志：
```
yarn logs -applicationId application_1507732460084_0057
```
>!需以 Hadoop 用户身份执行该命令。如果是其他用户的任务可以添加参数`-appOwner username`。

如需查看任务异常原因可通过以下命令实现：
```
yarn logs -applicationId application_1507732460084_0057|grep -A20 Exception
```

### 如何调整集群计算资源？
集群计算资源由 `yarn-site.xml` 中的以下两项配置决定：
``` xml
<property>
  <name>yarn.nodemanager.resource.cpu-vcores</name>
  <value>4</value>
</property>
<property>
  <name>yarn.nodemanager.resource.memory-mb</name>
  <value>14745</value>
</property>
```
默认情况下 cpu-vcores 等于机器的 CPU 核数，memory-mb 等于机器内存的91%，可以根据实际情况作出调整，如果设置太大则存在机器宕机的风险。

### 如何处理任务执行时内存溢出？
提交 MR 任务或者通过 Hive 执行 SQL 脚本时发生内存溢出可以通过设置以下参数处理：
```
set mapreduce.map.java.opts=-Xmx4096m;
set mapreduce.reduce.java.opts=-Xmx4096m;
```

可以根据计算需要调整内存参数，如果是 Hive 也可写在 `~/.hiverc` 文件下，提交的时候会自动执行。

### 如何预估集群规模？
假设您的一次运算以 SQL 执行为例，如果想要在确定的时间里查询到结果需要的 vcore 为64个，内存为128GB，业务要求一次要支持10个并发，那么需要的资源为 vcore 640个，内存1280GB，假设采用24核48GB的设备，那么需要的计算设备量为：1280 / 48约等于27台。

### 如何设置 Hive 的 fetch 查询？
Hive 默认查询如下：
``` sql
select * from tablename where a=’1’ limit 10;
```
默认查询不会启动计算任务，您可以通过添加 `set hive.fetch.task.conversion=none` 参数开启分布式查询。

### 如何选择集群存储介质？
EMR 集群支持如下存储介质，普通本地盘、SSD 本地盘、普通云硬盘，SSD 云硬盘以及对象存储 COS，您可以根据实际需要来选择存储介质：
- 如果您的应用场景是大规模数据仓库分析，对时延不是那么敏感，建议您使用 COS 作为底层存储。
- 如果您非常熟悉 HDFS 而且使用 COS 迁移成本过高，您也可以使用普通云盘。
- 如果您的应用是海量列式数据库 Hbase，需要高效写入和查询，建议您使用本地 SSD 盘或者 SSD 云硬盘。

### EMR 集群能通过外网登录么？
开启公网 IP 可以登录集群，详情请参考 [登录集群](https://intl.cloud.tencent.com/document/product/1026/31101) 文档。

### EMR 集群支不支持开启 ldap 认证？
ldap 认证是根据产品版本决定的，2.3.0版本及以上支持，默认开启，暂不支持关闭。2.3.0版本以下不支持。

### common 节点是否支持扩容？
common 节点暂不支持扩容。

### EMR 是否支持升级 ClickHouse 版本？
目前 EMR 产品中，ClickHouse 集群中已有三个发行版，且每个发行版中 ClickHouse 均有升级，详情请参考 [版本概述](https://intl.cloud.tencent.com/document/product/1026/31095)。

### 大数据相关组件在弹性 MapReduce 页面选择后会自动安装好吗？
控制台可直接安装组件。


### EMR 的 hdfs 默认开启 webhdfs 吗？
默认开启 webhdfs。

### EMR 是否支持修改所属项目？
弹性 MapReduce 不支持修改所属项目，如果该问题对您的业务造成影响，您可以申请技术 [工单](https://console.cloud.tencent.com/workorder/category) 支持。

### MapReduce 节点中可以运行后端 jar 包吗？
创建集群时可以使用引导操作来设定自定义的引导脚本来实现，可分别设置在节点初始化后、集群启动前、集群启动后三个时间节点执行；操作文档参见 [引导操作](https://intl.cloud.tencent.com/document/product/1026/34521) 。


### 如何根据业务场景选择集群规格？
EMR 集群提供六种集群类型，可根据实际业务需要选择集群类型，详情可参考 [业务评估](https://intl.cloud.tencent.com/document/product/1026/31098)。









