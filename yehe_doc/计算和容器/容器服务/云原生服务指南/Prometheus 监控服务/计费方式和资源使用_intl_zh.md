目前使用 Prometheus 监控服务（TMP）时将会在用户的账户下创建 [EKS 集群](https://intl.cloud.tencent.com/document/product/457/34054)、内外网 [负载均衡 CLB](https://intl.cloud.tencent.com/document/product/214) 资源，以及 Prometheus 服务本身的费用，按用户实际使用的云资源收费。本文向您介绍使用 Prometheus 监控服务时资源的使用情况。

## 资源列表

### TMP 实例

TMP 上线了“收费指标采集速率”的能力，您可以用该数值估算监控实例/集群/采集对象/指标等多个维度的预估费用：

1. 登录 [容器服务控制台 ](https://console.cloud.tencent.com/tke2)，选择左侧导航栏中的 **[Prometheus 监控](https://console.cloud.tencent.com/tke2/prometheus2)**。
2. 在 Prometheus 监控列表中，查看“收费指标采集速率”。该指标表示 TMP 实例的收费指标采集速率，根据用户的指标上报量和采集频率预估算出。该数值乘以 86400 则为一天的监控数据点数，根据 [按量计费](https://intl.cloud.tencent.com/document/product/1116/43156) 可以计算预估的监控数据刊例价。
您也可以在“关联集群”、“数据采集配置”、“指标详情”等多个页面查看到不同维度下的收费指标采集速率。

### EKS 集群

每创建一个 Prometheus 监控实例后，会在用户的账户下创建一个按量付费 EKS 集群，用于数据采集。在 [弹性集群列表页](https://console.cloud.tencent.com/tke2/ecluster) 查看资源信息，如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/ef6140a1806a72058732a9e408a30881.png)

#### 注意事项

该 EKS 集群的名称为 Prometheus 监控服务**实例的 ID**，集群描述里面说明为 “Prometheus监控专用，请勿修改或删除”。
![](https://qcloudimg.tencent-cloud.cn/raw/a764cec686ca1c0836a15ceb688ee674.png)

#### 计费

计费方式为**按量计费**，计费详情请参见 EKS [产品定价](https://intl.cloud.tencent.com/document/product/457/34055)。

EKS 集群会按照监控量进行自动扩缩容，监控规模和 EKS 集群费用的关系可参考：

| **用户上报的瞬时 Series 量级** | **预估需要的 EKS 资源** | **对应的刊例价费用/日** |
| ------------------------------ | ----------------------- | ----------------------- |
| <50万                           | 1.25核 1.6GiB           | 0.35美元                   |
| 100万                           | 0.5核1.5GiB*2           | 1.46美元                   |
| 500万                          | 1核3GiB*3               | 2.93美元                    |
| 2000万                         | 1核6GiB*5               | 7.98美元                    |
| 3000万                         | 1核6GiB*8               | 12.77美元                    |

EKS 集群成本示例如下：
  一个新初始化的 Prometheus 实例所用 EKS 集群消耗了：CPU:1.25 核、内存:1.5GiB。预计一天刊例价费用为：0.0319 x 24 + 0.0132 x 24 =  1.0824美 元

### 负载均衡 CLB

使用 Prometheus 服务监控关联集群监控容器服务，常规情况下会在用户账户下创建一个内网 CLB 用于打通采集器与用户集群的网络。

若用户关联了边缘集群，或跨集群关联了未打通网络的集群，支持创建公网的 CLB 进行网络联通，此时会创建一个公网 CLB。

若要使用通过外网访问 Grafana 服务，则需要创建一个相应的公网 CLB。

这些 CLB 资源会收取费用，创建的公网 LB 可在 [负载均衡控制台](https://console.cloud.tencent.com/clb/instance?rid=1) 查看资源信息。

该资源按实际使用量计费，计费详情请参见负载均衡 [标准账户类型计费说明](https://intl.cloud.tencent.com/document/product/214/36998) 文档。

## 资源销毁

目前不支持用户直接在对应控制台删除资源，例如需要在 Prometheus 监控销毁监控实例，对应的所有资源会一并销毁。腾讯云不主动回收用户的监控实例，若您不再使用 Prometheus 监控服务，请务必及时删除监控实例，以免发生资源的额外扣费。
