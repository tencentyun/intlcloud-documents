

本篇文章主要介绍在容器服务 TKE 集群中，如何调度 Pod 至超级节点，主要有两种调度方式：
- 自动调度
- 手动调度

## 自动调度

- 如果集群同时开启了 [Cluster Autoscaler](https://intl.cloud.tencent.com/document/product/457/30638) 和按量计费超级节点，则会尽量优先将 Pod 调度到按量计费的超级节点上，而非触发集群节点扩容。如果受调度限制影响，Pod 无法调度到超级节点上，则会依然正常触发集群节点扩容。而服务器节点资源充足时，会优先缩容按量计费超级节点上的 Pod。

## 手动调度

支持用户手动将 Pod 调度至超级节点，默认按量计费的超级节点会自动添加 Taints 以降低调度优先级，如需手动调度 Pod 到超级节点或指定超级节点调度，通常需要为 Pod 添加对应的 Tolerations。但并非所有的 Pod 均可以调度到超级节点上，详情请参见 [超级节点调度说明](https://intl.cloud.tencent.com/document/product/457/39760)。为方便使用，您可以在 Pod Spec 中指定 nodeselector 。示例如下：

```yaml
spec:    
    nodeSelector:
      node.kubernetes.io/instance-type: eklet
```

容器服务 TKE 的管控组件会判断该 Pod 是否可以调度到超级节点，若不支持则不会调度到超级节点。

