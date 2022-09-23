[TOC]
# 概述
TCR Hosts Updater 是 TCR Addon 的子组件之一，用于帮助用户在没有 VPC DNS 服务的地域配置 k8s 集群工作节点的 hosts 文件。
# 原理
![](docs/images/Hosts%20Updater.png)

Hosts Updater 通过挂载 k8s 集群中特定的 `ConfigMaps` 资源为工作负载的 `Volume`，并通过 Linux 系统的 inotify (inode notify) 机制来观察配置文件的变更来更新工作节点的 `/etc/hosts` 文件。
因为需要修改工作节点的 `/etc/hosts` 文件，所以我们通常使用 `Daemonset` 工作负载来部署。并且，需要在每一个需要更新 hosts 的节点上运行。为了能够更广泛的运行到集群内的节点上，我们在 DaemonSet 的 yaml 文件中默认使用了下列污点容忍：

```yaml
      tolerations:
        - key: node-role.kubernetes.io/master
          effect: NoSchedule
        - key: node.kubernetes.io/disk-pressure
          effect: NoSchedule
        - key: node.kubernetes.io/memory-pressure
          effect: NoSchedule
        - key: node.kubernetes.io/network-unavailable
          effect: NoSchedule
        - key: node.kubernetes.io/not-ready
          effect: NoExecute
        - key: node.kubernetes.io/pid-pressure
          effect: NoSchedule
        - key: node.kubernetes.io/unreachable
          effect: NoExecute
        - key: node.kubernetes.io/unschedulable
          effect: NoSchedule
```

# 部署与使用
在部署前，我们需要在准备部署 Hosts Updater 的 `Namespace` 下（如 `kube-system`）新建 `ConfigMaps` 资源 `updater-config`，然后再创建 `DaemonSet`。

如果需要增加或者删除 hosts 条目，编辑 `ConfigMaps` 资源 `updater-config` 即可。`ConfigMaps` 示例如下：
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: updater-config
  namespace: kube-system
data:
  hosts.yaml: |
    - domain: demo.tencentcloudcr.com
      ip: 10.0.0.2
      disabled: false
    - domain: vpc-demo.tencentcloudcr.com
      ip: 10.0.0.2
      disabled: false
```

**注意**：由于使用了 k8s `ConfigMaps Volume`，在编辑了 `updater-config` 后 hosts 文件更新的时间取决于工作节点 kubelet 的 `sync period`（默认值为一分钟）和 `ConfigMaps` 的 `Cache TTL` （默认值为一分钟）。该问题的详细资料请参考 k8s 官方文档 https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/#mounted-configmaps-are-updated-automatically。
