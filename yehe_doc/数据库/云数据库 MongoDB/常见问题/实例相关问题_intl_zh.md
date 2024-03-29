### MongoDB 如何查看实例详情？
在 [实例列表](https://console.cloud.tencent.com/mongodb)，单击实例 ID 可以进入详细信息页面查看实例详情。

### 如何访问 MongoDB 实例？
云数据库 MongoDB 提供多种语言连接方式，如 Shell，PHP，Node.js，Java，Python。
连接示例请参见 [完整的连接说明](https://intl.cloud.tencent.com/document/product/240/7092) 。

### MongoDB 的升级实例规格花费时间与实例已用容量有关吗？
升级实例规格所需的时间取决于实例已用容量，升级期间实例会发生一次切主，切主期间会出现短暂的不可访问，大约十秒左右。

### MongoDB 创建实例的流程？
可通过 [购买页](https://buy.Intl.cloud.tencent.com/mongodb) 按需选择规格大小和时长，单击**立即购买**创建实例。

### 如何在项目中查找 MongoDB 已分配项目的实例？
查找已分配项目的实例，可参考接口 [DescribeDBInstances](https://intl.cloud.tencent.com/document/product/240/34702) 查询实例列表。

### MongoDB 实例的连接数规格是多少？是否支持升级连接数？
请参见 [连接限制说明](https://intl.cloud.tencent.com/document/product/240/31183)，连接数和实例规格相关，可以通过升级规格以获取更大的连接数。

### MongoDB 如何查看实例的慢查询？
您可以使用 [控制台](https://console.cloud.tencent.com/mongodb/instance) 实例管理页面的**数据库管理** > **慢查询管理**功能获取慢查询详情。

### MongoDB 查询可创建的实例规格?
可以通过 [DescribeSpecInfo](https://intl.cloud.tencent.com/document/product/240/34701) 接口查询可创建的实例规格。

### 如何选择副本集实例与分片集群实例?
- **副本集**由一个 Primary 节点和一个或多个 Secondary 节点组成 。如下业务场景，请选择副本集实例。
  - 数据规模不超过实例的总容量。
    您可以在 [创建实例](https://intl.cloud.tencent.com/document/product/240/3551) 时，选择副本集实例的**容量**规格，判断是否满足需求，以选择合适的实例。
  - 写流量少，读流量高的场景。
    您可以扩容从节点解决读流量过高的性能瓶颈。具体操作，请参见 [调整实例节点数量](https://intl.cloud.tencent.com/document/product/240/31192)。
  - 数据库集合非常多，而每个集合中的文档数据量并不大的场景。
  - 如果是多字段随机组合查询场景， 用户随机组合各种查询条件，使用分片集群难以选择合适的片键索引，建议使用副本集。

- **分片集群**相比副本集，突破了数据容量瓶颈、写流量瓶颈限制，具备完善的横向扩展能力。如下业务场景，请选择分片集群实例。 
  - 数据规模预估会超过副本集承载的规模上线。 
    您可以在 [创建实例](https://intl.cloud.tencent.com/document/product/240/3551) 时，查看副本集实例**容量**的最大上限，以选择合适的实例。
  - 写流量超过副本集最大写流量上限的场景。

### 如何设置数据库读操作的优先级？
当业务对数据一致性要求不高时，可以配置读写分离，这样可以减轻主节点的请求压力，同时提升读性能。默认情况下，MongoDB 优先读主节点，如需指定访问从库，客户端可通过设置 Read Preference 来配置读策略。Read Preference 参数，具体取值含义如下：

| 取值               | 含义                                     | 是否默认 |
| ------------------ | ---------------------------------------- | -------- |
| primary            | 只读主节点                               | 是       |
| primaryPreferred   | 主节点优先，如主节点不可用，则读从节点。 | 否       |
| secondary          | 只读从节点，如从节点不可用会报错。       | 否       |
| secondaryPreferred | 从节点优先，如从节点不可用，则读主节点。 | 否       |
| nearest            | 就近读，读网络延迟最低的节点。           | 否       |

设置优先读取从节点可以根据如下示例拼接 URI：
```
mongodb://username:password@IP:27017/admin?readPreference=secondaryPreferred
```

### 如何优化写多数派节点引起的写入性能下降的问题？
**问题描述**
写入数据可以根据业务数据的可靠性要求来选择不同的 Write Concern 策略 。具体信息，可以参见 [MongoDB 官网 Write Concern](https://docs.mongodb.com/manual/reference/write-concern/)。

| 选项          | 描述                                                         | 场景                                 |
| ------------- | ------------------------------------------------------------ | ------------------------------------ |
| {w: 0}        | 对客户端的写入不需要发送任何确认信息                         | 不关注数据完整性                     |
| {w: 1}        | 默认的 writeConcern 选项，数据写入到 Primary 就向客户端发送确认信息 | 兼顾性能与一定程度的数据可靠性       |
| {w: majority} | 数据写入到副本集大多数节点后向客户端发送确认信息             | 数据完整性要求比较高、避免数据回滚 |

对数据可靠性要求比较高时，您可以将 Write Concern 的 `w` 选项设置为 majority，并使用 {j: true} 选项来保证写入时 journal 日志持久化之后才返回给客户端确认信息，可以避免数据回滚的现象，然而写入性能明显下降。

**优化方法**
您可以通过禁用链式复制功能来优化写入性能。假设节点 A(primary)、B 节点(secondary)、C 节点(secondary)，如果 B 节点从 A 节点同步数据，C 节点从 B 节点同步数据，这样 A > B > C 之间就形成了一个链式的同步结构，如下图所示  ：
![](https://qcloudimg.tencent-cloud.cn/raw/5793179daef14afc34df7c702381dcd3.png)
1. MongoDB 多节点副本集可以支持链式复制，执行如下命令确认当前副本集是否支持链式复制。
```
1.	cmgo-xx:SECONDARY> rs.conf().settings.chainingAllowed  
2.	true  
3.	cmgo-xx:SECONDARY> 
```
2. 判断当前副本集节点中是否存在有链式复制情况。您可以查看副本集中每个节点的同步源，如果同步源为 secondary 从节点，则说明副本集中存在链式复制。具体示例如下所示。
```
1.	cmgo-xx:SECONDARY> rs.status().syncSourceHost  
2.	xx.xx.xx.xx:7021  
3.	cmgo-xx:SECONDARY> 
```
3. 执行如下命令，关闭链式复制功能。
```
1.	cfg = rs.config()  
2.	cfg.settings.chainingAllowed = false
3.	rs.reconfig(cfg) 
```

