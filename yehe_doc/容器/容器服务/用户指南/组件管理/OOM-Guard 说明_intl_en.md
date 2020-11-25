## Overview

### Add-on description
OOM-Guard is an add-on provided by TKE for handling container cgroup out-of-memory (OOM) in user mode. Because the process by which the Linux kernel handles cgroup OOM has many bugs, frequent cgroup OOM can often incur node failures (crash, restart, and unkillable abnormal processes). When cgroup OOM occurs, before the kernel kills the container process, OOM-Guard can kill the limit-exceeding container in the user space, reducing the chance of various kernel failures triggered by code branches that fail to be repossessed by the kernel cgroup memory.

Before the OOM threshold is triggered, OOM-Guard writes `memory.force_empty` to trigger-related cgroup memory repossessing. After the repossession, if `memory.stat` shows a sufficient cache capacity, no subsequent processing policies will be triggered. After a container is killed due to cgroup OOM, the add-on reports the `OomGuardKillContainer` event to Kubernetes. You can query the event by running the `kubectl get event` command.

## Kubernetes Objects Deployed in a Cluster

| Kubernetes Object Name | Type | Default Resource Consumption | Namespaces |
| ------------------- | ------------------ | ----------------------- | --------------- |
| oomguard | ServiceAccount | - | kube-system |
| system:oomguard | ClusterRoleBinding | - | - |
| oom-guard | DaemonSet | 0.02-core CPU and 120-MB memory | kube-system |

## Use Cases
This add-on is suitable for Kubernetes clusters where the node memory pressure is high and business container OOM often incur node failures.

## Limits
- The containerd service socket path is not changed, and the default path of TKE is retained:
   - docker runtime: `/run/docker/containerd/docker-containerd.sock`
   - containerd runtime: `/run/containerd/containerd.sock`
- The mount target of the cgroup memory subsystem is not changed, and the default `/sys/fs/cgroup/memory` mount target is retained.

## Usage

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and select **Cluster** in the left sidebar.
2. On the "Cluster Management" page, click the ID of the target cluster to go to the cluster details page.
3. In the left sidebar, click **Add-On Management** to go to the "Add-On List" page.
4. On the "Add-On List" page, click **Create**. On the "Create an Add-On" page that appears, select **OOM-Guard**.
5. Click **Finish** to install the add-on.
