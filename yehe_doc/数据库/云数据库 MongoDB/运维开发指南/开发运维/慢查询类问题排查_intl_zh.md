
您在使用 MongoDB 时发现请求延迟明显变长时，可按照如下步骤进行排查：
1. 请检查实例的请求延迟监控指标有无异常。
登录 [MongoDB 控制台](https://console.cloud.tencent.com/mongodb)，单击实例 ID 进入管理页面，在**系统监控**页面，检查实例的监控数据，时延监控指标主要反馈的是从请求到达接入层直至处理完返回客户端的时间。若请求时延较高，则需检查 mongod 上是否有慢日志。

2. 查看当前 mongod 上是否有慢日志。
登录 [MongoDB 控制台](https://console.cloud.tencent.com/mongodb)，单击实例 ID 进入管理页面，在**数据库管理** > **慢日志查询**页面查看实例的慢日志，可选择抽象查询。
请关注：command、COLLSCAN、IXSCAN、keysExamined、docsExamined 等关键字，更多的日志说明请参考 [MongoDB 官网](https://docs.mongodb.com/manual/reference/log-messages/index.html)。
需注意的关键字如下：
 - command 指出慢日志中记录的操作。
 - COLLSCAN 代表该查询进行了全表扫描，IXSCAN 代表进行了索引扫描。更多的字段描述请参考 [MongoDB 官网](https://docs.mongodb.com/manual/reference/explain-results/index.html)。<br>
 - keysExamined 代表索引扫描条目，docsExamined 代表文档扫描条目。keysExamined 和 docsExamined 越大代表没有建索引或者索引的区分度不高。请确认索引的创建字段。
  
3. 请确认是否在前台建索引导致请求被锁住。
如果业务查询所用索引并无问题，请确认当前是否在业务繁忙时段进行了前台建索引操作。当为一个集合创建索引时默认方式为前台方式（background 选项的值为 false）。该操作将阻塞其他的所有操作，直到前台完成索引创建。但如果采用后台方式建索引，则在创建索引期间，MongoDB 依旧可以正常提供读写操作服务，不过，后台建索引方式是有代价的，即后台方式建索引可能会导致索引创建时间变长。具体创建索引的选项请参考 [MongoDB 官网](https://docs.mongodb.com/manual/reference/method/db.collection.createIndex/)。
可通过 currentOp 命令来查看当前建索引的进度，具体的命令如下：
```
db.currentOp(
        {
          $or: [
            { op: "command", "query.createIndexes": { $exists: true } },
            { op: "insert", ns: /\.system\.indexes\b/ }
          ]
        }
        )
```
返回如下图所示，msg 字段代表了当前建索引的进度，locks 字段代表该操作的锁类型，更多锁的说明请参考 [MongoDB 官网](https://docs.mongodb.com/v3.2/reference/database-profiler/)。<br>
![](https://main.qcloudimg.com/raw/355b6c06539ad6a5e3980b90bd200bf0.png)
![](https://main.qcloudimg.com/raw/155583329a2eb2a99575a2b5ce0b8647.png)<br>

4. 检查是否 mongos 负载过高。
时延监控指标主要反馈的是从请求到达接入层直至处理完返回客户端的时间，若已确认 mongod 上没有慢操作，但请求时延较高，可能是 mongos 负载过高导致。造成 mongos 负载高的原因有多种，例如业务瞬间建立大量连接可能会导致 mongos 负载过高，或者，多个分片的数据需要汇总也可能会造成 mongos 负载高。此时可以进行 mongos 重启。重启 mongos 可以在 [控制台](https://console.cloud.tencent.com/mongodb/instance) 实例列表进行。
> !重启 mongos 会导致实例所有的连接在重启的一瞬间中断，业务直接进行重连即可，不存在持续影响业务的可能。
