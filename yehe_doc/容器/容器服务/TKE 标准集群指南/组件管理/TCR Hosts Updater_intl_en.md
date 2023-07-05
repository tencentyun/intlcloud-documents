[TOC]
# Overview
TCR Hosts Updater, a component of TCR Addon, helps you deploy the hosts file on K8s cluster worker nodes in regions without VPC DNS service.
# How It Works
![](docs/images/Hosts%20Updater.png)

Hosts Updater mounts a specific `ConfigMaps` in the K8s cluster as the `Volume` of a worker node, watches the changes of the config file via inotify (inode notify) of Linux OS, and updates the `/etc/hosts` file of the worker node accordingly. 
As we need to edit the `/etc/hosts` file of the worker node, `Daemonset` workload is usually used for deployment, and it should be run on each node that you need to update hosts. To allow the DaemonSet workload runs on nodes in the cluster as many as possible, the following tolerations are set in the YAML file of the DaemonSet: 

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

# Deployment and Usage
Before the deployment, please create a `ConfigMaps` resource named `updater-config` under `Namespace` of Host Updater (e.g. `kube-system`), and then create `DaemonSet`.

To add or delete entries in hosts, simply edit the `updater-config`. See below for examples:  
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

**Note**: As K8s `ConfigMaps Volume` is used, after the modification of `updater-config`, the effective time of the hosts update depends on the `sync period` of worker node kubelet (default to 1 min) and the `Cache TTL` of `ConfigMaps` (default to 1 min). For details, see https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/#mounted-configmaps-are-updated-automatically.
