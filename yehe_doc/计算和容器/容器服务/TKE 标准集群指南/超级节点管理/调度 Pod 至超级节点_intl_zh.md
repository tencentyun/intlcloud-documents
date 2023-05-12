
本篇文章主要介绍在容器服务 TKE 集群中，如何调度 Pod 至超级节点，主要有两种调度方式：
- 自动扩容
- 手动调度

### 自动扩容
若集群配置了超级节点，当业务高峰且已有节点资源不足时，会自动调度 Pod 至超级节点，无需购买服务器；业务恢复平稳，自动释放在超级节点中的 Pod 资源，也无需再进行退还机器操作。

如果集群同时开启了 [Cluster Autoscaler](https://intl.cloud.tencent.com/document/product/457/30638) 和超级节点，则会尽量优先将 Pod 调度到超级节点上，而非触发集群节点扩容。如果受上述调度限制影响，Pod 无法调度到超级节点上，则会依然正常触发集群节点扩容。而服务器节点资源充足时，会优先缩容超级节点上的 Pod。


### 手动调度

超级节点支持手动将 Pod 调度至超级节点，默认超级节点会自动添加 Taints 以降低调度优先级，如需手动调度 Pod 到超级节点或指定超级节点，通常需要为 Pod 添加对应的 Tolerations。但并非所有的 Pod 均可以调度到超级节点上，详情请参见 [超级节点调度说明](https://intl.cloud.tencent.com/document/product/457/39760)。为方便使用，您可以在 Pod Spec 中指定 nodeselector 。示例如下：

```yaml
spec:    
    nodeSelector:
      node.kubernetes.io/instance-type: eklet
```

或在 Pod Spec 指定 nodename。示例如下：
```yaml
spec:
   nodeName: $超级节点名称
```

容器服务 TKE 的管控组件会判断该 Pod 是否可以调度到超级节点，若不支持则不会调度到超级节点。

