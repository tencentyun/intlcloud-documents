## 命名空间

Namespace=QCE/DOCKER

##  监控指标

| 指标中文名 | 指标英文名         | 单位   | 指标含义                    | 维度                  |
| ------- | ----------------- | ---- | ------------------------- | ------------------------- |
| 实例网络入带宽 | PodInBandwidth  | Mbps | 同一实例内容器共享网络，实例（pod）的网络入带宽 | clusterId、serviceName、namespace、podName |
| 实例网络出带宽 | PodOutBandwidth | Mbps | 同一实例内容器共享网络，实例（pod）的网络出带宽 | clusterId、serviceName、namespace、podName |
| 实例网络入流量 | PodInFlux       | MB   | 同一实例内容器共享网络，实例（pod）的网络入流量 | clusterId、serviceName、namespace、podName |
| 实例网络出流量 | PodOutFlux      | MB   | 同一实例内容器共享网络，实例（pod）的网络出流量 | clusterId、serviceName、namespace、podName |
| 实例网络入包量 | PodInPackets    | 个/s  | 同一实例内容器共享网络，实例（pod）的网络入包量 | clusterId、serviceName、namespace、podName |
| 实例网络出包量 | PodOutPackets   | 个/s  | 同一实例内容器共享网络，实例（pod）的网络出包量 | clusterId、serviceName、namespace、podName |

> ?每个指标对应的统计粒度（Period）可取值不一定相同，可通过 [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) 接口获取每个指标支持的统计粒度。

##  各维度对应参数总览

| 参数名称                       | 维度名称    | 维度解释                                                     | 格式                                           |
| ------------------------------ | ----------- | ------------------------------------------------------------ | ---------------------------------------------- |
| Instances.N.Dimensions.0.Name  | clusterId   | 集群 ID 的维度名称                                            | 输入 String 类型维度名称：clusterId              |
| Instances.N.Dimensions.0.Value | clusterId   | 具体的集群 ID，[查询集群列表](https://intl.cloud.tencent.com/document/product/457/32025) 接口中返回的 clusterId（集群的 ID）字段 | 输入集群具体 ID，例如：disk-test               |
| Instances.N.Dimensions.1.Name  | serviceName | 服务维度名称                                                 | 输入 String 类型维度名称：serviceName            |
| Instances.N.Dimensions.1.Value | serviceName | 具体的服务名称，请使用 [Kunbernetes API](https://kubernetes.io/zh/docs/concepts/overview/kubernetes-api/) 查询具体的 serviceName | 输入具体服务名称，例如：test                  |
| Instances.N.Dimensions.2.Name  | namespace   | 命名空间的维度名称                                           | 输入 String 类型维度名称：namespace              |
| Instances.N.Dimensions.2.Value | namespace   | 具体的命名空间名称，请使用 [Kunbernetes API](https://kubernetes.io/zh/docs/concepts/overview/kubernetes-api/) 查询具体的 namespace | 输入命名空间具体名称，例如：default           |
| Instances.N.Dimensions.3.Name  | podName     | 实例的维度名称                                               | 输入 String 类型维度名称：podName                |
| Instances.N.Dimensions.3.Value | podName     | 具体的实例名称，请使用 [Kunbernetes API](https://kubernetes.io/zh/docs/concepts/overview/kubernetes-api/) 查询具体的 name | 输入实例具体名称，例如：test-3488000495-nj6s9 |

## 入参说明

查询容器服务实例维度监控数据，入参取值例如下：

&Namespace=QCE/DOCKER
&Instances.N.Dimensions.0.Name=clusterId
&Instances.N.Dimensions.0.Value=集群 ID
&Instances.0.Dimensions.1.Name=namespace
&Instances.0.Dimensions.1.Value=命名空间
&Instances.0.Dimensions.2.Name=serviceName
&Instances.0.Dimensions.2.Value=服务器名称
&Instances.0.Dimensions.3.Name=podName
&Instances.0.Dimensions.3.Value=实例名称

