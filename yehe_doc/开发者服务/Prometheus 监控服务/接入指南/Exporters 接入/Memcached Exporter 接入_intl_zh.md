## 操作场景

在使用 Memcached 过程中需要对 Memcached 运行状态进行监控，以便了解 Memcached 服务是否运行正常，排查 Memcached 故障等。 Prometheus 监控服务提供基于 Exporter 的方式来监控 Memcached 运行状态，并提供了开箱即用的 Grafana 监控大盘。本文为您介绍如何使用 Prometheus 监控服务 Memcached。

## 操作步骤

1. 登录 [ Prometheus 控制台](https://console.cloud.tencent.com/monitor/prometheus)。
2. 在实例列表中，选择对应的 Prometheus 实例。
3. 进入实例详情页，单击**集成中心**。
4. 在集成中心选择 `Memcached` 单击安装进行集成。

### 配置说明

![](https://qcloudimg.tencent-cloud.cn/raw/8d3218bd0419ff314f585d19338e35db.png)

| 名称                       | 描述                                                         |
| -------------------------- | ------------------------------------------------------------ |
| 名称              | 每个集成需要一个唯一名称 |
| 地址                  | 要采集的 Memcached 实例的地址和端口 |
| 标签   | 增加具有业务含义的标签，会自动添加到 Prometheus 的 Label 中 |

### 查看监控

可以通过监控大盘清晰看到如下监控状态：
1. 内存使用率，同时显示已使用的内存和内存总量。
2. 当前的 Get 命令的命中率，同时显示服务运行期间 Get 命令命中和未命中的比例。
3. Memcached 移除旧数据和回收过期数据的速率，同时显示服务运行期间移除和回收的数据总数。
4. Memcached 存储的数据总量。
5. 从网络中读取和写入的字节数。
6. 当前打开的连接数。
7. 服务运行期间 Get 命令和 Set 命令的比例。
8. 当前各命令的产生速率。

![](https://qcloudimg.tencent-cloud.cn/raw/83b448f34e45abbc0636780702642c00.png)

![](https://qcloudimg.tencent-cloud.cn/raw/b12321e5b2747d1e310c4fd24b3d98f5.png)
