### 自建 Prometheus如何迁移到 Prometheus 监控服务？[](id:question1)

在自建 Prometheus 的配置文件中加一个 Remote Write 配置指向到 Prometheus 监控服务即可进行迁移，详情请参见 [自建 Prometheus 迁入](https://intl.cloud.tencent.com/document/product/1116/43213) 。

### 请问 Grafana 能支持批量导出导入 Dashboard 吗？

目前只能通过 API 导出，详情请参见 [HTTP API Reference](https://grafana.com/docs/grafana/latest/http_api/)。

### 一个 exporter 数据太多了怎么办？

prometheus 服务能支持这种场景，但是不建议在 exporter 暴露特别多的 metrics，exporter 本身和 prometheus agent 会消耗比较多的内存。建议暴露一些关键指标，不要在指标的 label 中使用用户 id,url 等参数信息。

### 如何使用 Prometheus 监控服务监控两个不同 VPC 下的集群？
1. 通过[云联网](https://intl.cloud.tencent.com/document/product/215/40089)打通两个集群之间的 VPC 网络，即可在 Prometheus 集成两个不同 VPC 下的集群。
2. 在其中一个集群 [安装Agent](https://intl.cloud.tencent.com/document/product/1116/43180)，并通过 Nginx 代理，remote write 目标地址到 Prometheus 实例。

### 原生的容器服务如何接入 Prometheus？  
暂不支持，可通过自建数据，在自建 Prometheus 的配置文件中加一个 Remote Write 配置指向到 Prometheus 监控服务即可，参考文档 [自建 Prometheus 迁入](https://intl.cloud.tencent.com/document/product/1116/43213)。

###  Prometheus 接口创建告警规则，告警周期的参数要怎么设置?

在新建 Labels 参数中加 `key=_interval_  value=1m/5m/10m/15m/30m/60m` 即可。


### 重建实例会丢失数据吗？
数据存储在腾讯云的时序数据库（TencentDB for CTSDB）上，重建实例数据不会丢失。但由于重建期间无法正常上报数据，数据会出现断点情况。

### Prometheus实例重建后，产生数据量飙升，这是正常的吗？
短时间内的波动是正常的，重建后会有重试操作，所以数据量短时间看起来是有较大的波动。


### Prometheus 集成中心-Mysql 集成，可以批量添加 MySQL 实例吗？
暂不支持，目前只能一个一个添加。

### Prometheus 创建的弹性集群（EKS）的安全组在那里可以查看?
[私有网络(VPC)-](https://console.cloud.tencent.com/vpc/vpc?rid=1)->安全->安全组-->以当前 Prometheus 实例 ID 为关键词搜索即可查看。

### pod monitor 是否可以配置多个抓取？
可以，只需保证 port name 相同、 label 相同即可。

### （Prometheus 监控服务 pushgateway 用法）如果多个实例的客户端 push 同个 job 但不同 label 指标时，会有指标覆盖的情况，如何处理？
通过 groupingkey 可以解决这个问题，代码示例如下：

```
if err := push.New("http://$IP:$PORT", "db_backup").
        BasicAuth("$APPID", "$TOKEN").
        Collector(completionTime).
        Grouping("instance", "$INSTANCE"). 
```
