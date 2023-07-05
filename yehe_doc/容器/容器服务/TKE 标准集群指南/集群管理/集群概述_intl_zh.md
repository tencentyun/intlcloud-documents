## 集群基本信息
集群是指容器运行所需云资源的集合，包含若干台云服务器、负载均衡器等腾讯云资源。您可以在集群中运行您的应用程序。

## 集群架构

TKE 采用兼容标准的 Kubernetes 集群，包含以下组件：
- Master：用于管控集群的管理面节点。
- Etcd：保持整个集群的状态信息。
- Node：业务运行的工作节点。

## 集群类型

TKE 容器集群支持下述类型：

|集群类型 | 描述 |
|---------|---------|
| 托管集群 | Master、Etcd 腾讯云容器服务管理 |
| 独立集群 | Master、Etcd 采用用户自有主机搭建 |

集群类型详情可参见 [集群模式说明](https://intl.cloud.tencent.com/document/product/457/31417)。


## 集群生命周期
关于 TKE 集群的生命周期，请参见 [集群生命周期](https://intl.cloud.tencent.com/document/product/457/30636)。





## 集群相关操作

- [创建集群](https://intl.cloud.tencent.com/document/product/457/30637)
- [更改集群操作系统](https://intl.cloud.tencent.com/document/product/457/42075)
- [集群扩缩容](https://intl.cloud.tencent.com/document/product/457/30638)
- [连接集群](https://intl.cloud.tencent.com/document/product/457/30639)
- [升级集群](https://intl.cloud.tencent.com/document/product/457/30640)
- [集群启用 IPVS](https://intl.cloud.tencent.com/document/product/457/30641)
- [集群启用 GPU 调度](https://intl.cloud.tencent.com/document/product/457/30642)
- [选择容器网络模式](https://intl.cloud.tencent.com/document/product/457/38966)
- [删除集群](https://intl.cloud.tencent.com/document/product/457/36280)
- [自定义 Kubernetes 组件启动参数](https://intl.cloud.tencent.com/document/product/457/38139)
