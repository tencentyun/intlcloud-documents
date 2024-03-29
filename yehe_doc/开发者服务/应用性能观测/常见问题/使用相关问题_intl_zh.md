
### 之前使用 Skywalking，如何迁移到应用性能观测？
应用性能观测服务已兼容 Skywalking 协议，如果您已经在使用 Skywalking，您只需要替换上报 Token 和地址，即可在腾讯云上监控您的服务。


### Go 语言上报应用性能监控，资源管理中显示有上报量，但是应用列表没有数据，链路追踪的服务端也没有看到数据，该如何解决？
需要在代码中配置 span.kind 这个标签，Value值需标注服务是 server 端还是 client 端。
span.kind 用来区分是服务端客和户端的关系，拓扑依据需要依赖这些关系绘制。若没有配置，应用列表的拓补图数据会为空。
![](https://main.qcloudimg.com/raw/ff6795585b9a1b19bf92dfc8e3f1c851.jpg)

### 有数据上报成功，但是有些服务在APM拓补图上显示灰色，为什么？
如果一个服务在所选时间段内没有收到请求，我们从“服务提供者”的视角会认为这个服务不活跃，将该服务显示为灰色。

### 为什么只有 trace 数据，无 metric 数据？
大概率是 span.kind 上报的有问题，APM 只抓取 **client**、**server**、**consumer**、**producer** 四种 span.kind，请确保您的 span.kind 类型在这四种里。

### 应用性能观测的平均错误率是如何计算？
平均错误率 = 所有错误 span 的总和 ÷ 总请求数。
平均错误率是根据 span 来计算的， 任意一个 span 出现错误都将会被标记为错误状态。在应用性能观测中 error 和  status.code  代表 span 的错误状态。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/yNQ8010_2.png)

>? APM 后期会支持自定义错误数统计方式。

### APM 选择内网上报时，ping APM 内网上报地址不通，如何处理？
1. 服务器所在地域是否与 APM 业务系统所选地域相同。
2. 尝试是否能 Ping 通服务器地址和端口，若不能请提交工单联系我们。
