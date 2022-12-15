
腾讯云边缘容器会向节点数（nodeNum）不超过5个（0 < nodeNum ≤ 5）、大于5个且小于20个（5 < nodeNum < 20）的集群上的命名空间自动应用一组资源配额。您将无法移除这些配额，此资源配额将保护集群控制平面，避免因部署到集群的应用中存在潜在 Bug 而导致其不稳定。

如需检查此配额，您可以执行以下命令：
```
kubectl get resourcequota tke-default-quota -o yaml
```

>! 如需查看给定命名空间的 `tke-default-quota` 对象，请添加 `--namespace` 选项以指定命名空间。

如有特殊场景需要调整配额，请通过 [提交工单](https://console.intl.cloud.tencent.com/workorder/category) 提出配额申请。
