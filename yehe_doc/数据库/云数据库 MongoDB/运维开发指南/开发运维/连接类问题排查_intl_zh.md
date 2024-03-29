
您在使用 MongoDB 的过程中经常会遇见两类连接问题，下面介绍可以参考的排查思路。

## 连接使用率高
若您在使用过程中发现实例的连接使用率高，可参考如下步骤来排查问题。
1. 确认业务是否使用了连接池。
MongoDB 的服务模型是每个网络连接由一个单独的线程（ one-thread-per-connection ）来处理，当网络连接数太多时，过多的线程会导致上下文切换开销变大，同时内存开销也会上涨。每次请求都建立连接和鉴权会极大的影响性能。因此，要限制实例的连接数且连接使用完毕需要释放，推荐业务使用连接池。同时，MongoDB 各个语言的 Driver 基本都会封装一个对象，应该在使用时构造一个全局的对象，然后在后续的请求中使用该全局对象来发送请求给实例。Driver 的对象有默认连接池大小，也可以在构造对象时指定 maxPoolSize 选项来设置连接池大小。

2. 如果已经设置了连接池，请检查业务是否有突发异常。
 - 请确认业务是否有发布变更，代码逻辑缺陷导致建立大量连接。
 - 请检查是否有连接泄漏，在相关 CVM 上统计检查连接数是否异常。
 - 请确认业务是否有大量真实突发请求。

3. 请检查是否有慢查询导致连接被占用。
 - 若确认业务无异常，请检查索引是否有异常，例如之前建立的索引被误删等。
 -  若索引无异常，请检查当前是否有大量慢查询。慢查询导致连接一直占用未被释放，因此会建立更多的连接。
登录 [MongoDB 控制台](https://console.cloud.tencent.com/mongodb)，单击实例 ID 进入管理页面，在**数据库管理** > **慢日志查询**页面查看实例的慢日志，可选择抽象查询。
请关注：command、COLLSCAN、IXSCAN、keysExamined、docsExamined 等关键字，更多的日志说明请参考 [MongoDB 官网](https://docs.mongodb.com/manual/reference/log-messages/index.html)， 
   需注意的关键字如下：
    - command 指出慢日志中记录的操作。
    - COLLSCAN 代表该查询进行了全表扫描，IXSCAN 代表进行了索引扫描。更多的字段描述请参考 [MongoDB 官网](https://docs.mongodb.com/manual/reference/explain-results/index.html)。
    - keysExamined 代表索引扫描条目，docsExamined 代表文档扫描条目。keysExamined 和 docsExamined 越大代表没有建索引或者索引的区分度不高。请确认索引的创建字段。

4. 请确认是否在前台建索引导致请求被锁住。
若业务查询所用索引并无问题，请确认当前是否在业务繁忙时段进行了前台建索引操作。当为一个集合创建索引时默认方式为前台方式（ background 选项的值为 false ）。该操作将阻塞其他的所有操作，直到前台完成索引创建。但如果采用后台方式建索引，则在创建索引期间，MongoDB 依旧可以正常的提供读写操作服务，但后台建索引方式是有代价的，即后台方式建索引可能会导致索引创建时间变长。具体创建索引的选项请参考 [MongoDB 官网](https://docs.mongodb.com/manual/reference/method/db.collection.createIndex/)。<br>
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

65. 评估实例配置是否满足业务要求。
若经过使用连接池和建立区分度高的索引之后从控制台监控上看业务的连接使用率仍然很高，则可能是实例的配置已经不能满足业务实际需要导致。此时，需要您根据自身业务模型，流量峰值、 QPS 和 TPS 等要求来评估实际需要的实例规格配置并根据需要升级实例。

## 连接拒绝 
若在实际使用过程中出现了连接拒绝，请参考如下步骤排查问题。

1. 确认实例连接使用率是否达到100%。
登录 [MongoDB 控制台](https://console.cloud.tencent.com/mongodb)，在系统监控页面，查看连接数和连接使用率监控指标。
若实例连接使用率100%，请排查自身业务是否有异常，另一方面紧急情况可以通过在控制台重启 mongos 来快速释放连接。
>! 重启 mongos 会导致实例所有的连接在重启的一瞬间中断，业务直接进行重连即可，不存在持续影响业务的可能。若重启后业务连接数迅速增加又导致连接使用率100%，则说明业务确实存在大量有效连接，不属于连接泄漏的场景。此时需要业务首先排查产生大量连接的原因，可参考连接使用率高问题的排查方法。

2. 确认用户名与密码是否错误。
请确保用户名和密码正确，如有错，请登录 [MongoDB 控制台](https://console.cloud.tencent.com/mongodb)，单击实例 ID 进入管理页面，在**数据库管理** > **账号管理**页面修改。

3. 确认 Mongoshell 版本。
为保障鉴权成功，请安装 Mongo Shell 3.0及以上版本。安装步骤请参考 [官方文档](https://docs.mongodb.com/v3.2/installation/)。

4. 确认认证库是否正确。
>!在官网控制台创建的用户其认证库均为 admin，因此用户登录时需要制定认证库为 admin。用命令行创建的用户，例如在 test 库下建立的用户登录时指定的认证库为 test。

