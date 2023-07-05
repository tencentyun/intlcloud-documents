## Overview 
>? This add-on reduces the chance of various kernel failures triggered by cgroup memory reclamation failures in the user mode. It is applicable only to native kernel defects of CentOS 7.2/7.6. For other image versions, you do not need to install this add-on.


### Add-on Description
Out of Memory (OOM) indicates the programs run with more memory than the maximum memory available because memory cannot be repossessed or is used too much in the application system. When cgroup memory is insufficient, Linux kernel triggers cgroup OOM to kill some processes, so as to repossess some memory to keep continuous operation of the system. As many bugs may occur while Linux kernel (especially the earlier versions such as v3.10) processes cgroup OOM, frequent cgroup OOM occurrence may result in node failures (crash, restart, and unkillable abnormal processes).

OOM-Guard is an add-on provided by TKE for processing container cgroup OOM in user mode. When cgroup OOM occurs, before the kernel kills the container process, OOM-Guard kills the excessive container in the user space. This reduces the chance of various node failures triggered by memory repossessing failures in kernel mode.

Before the OOM threshold is triggered, OOM-Guard writes `memory.force_empty` to trigger relevant cgroup memory repossessing. If `memory.stat` still contains a large amount of cache data, no subsequent processing policies will be triggered. After a container is killed due to cgroup OOM, the add-on reports the `OomGuardKillContainer` event to Kubernetes. You can query the event by running the `kubectl get event` command.

### How It Works
The core concept is to kill the excessive containers in user space before kernel kills the container processes due to cgroup OOM. This reduces the chance of various kernel errors triggered by code branches that encounter repossessing failure of kernel cgroup memory.

OOM-Guard will set "threshold notify" mechanism for memory cgroup to receive notifications from the kernel. For more information, see [threshold notify](https://lwn.net/Articles/529927/).

#### Sample
For example, the memory limit set for a pod is 1000M, OOM-Guard will calculate margin based on the configuration parameters.
```
margin = 1000M * margin_ratio = 20M // the default value of margin_ratio is 0.02
```
In addition, the minimum value of margin is min_margin (1M) and maximum value is max_margin (50M). If it exceeds the limit, min_margin or max_margin is applied.

Calculate the threshold:
```
threshold = limit - margin // i.e. 1000M - 20M = 980M
```
980M is the threshold that is set to the kernel. When the memory used by the pod reaches 980M, OOM-Guard will receive a notification sent by the kernel.

Before threshold is triggered, OOM-Guard writes `memory.force_empty` to trigger relevant cgroup memory repossessing. In addition, if threshold is triggered and `memory.stat` of relevant cgroup still contains a large amount of cache data, the subsequent processing policies will not be triggered. Thus, when cgroup memory reaches the limit, kernel still triggers cgroup OOM.

#### Processing policy applied when threshold is reached
You can control the processing policies by setting the `--policy` parameter. The following three policies are available for now. The default policy is "container".

|Policy | Description|
|---------|---------|
|process | It uses a policy the same as the cgroup OOM killer. It selects a process with the highest value of oom_score inside the cgroup, and kills the process by "SIGKILL" sent from OOM-Guard.| 
|container | It selects a docker container under this cgroup and kills the whole container.| 
|noop | It only records logs but does not take any action.| 

### Kubernetes objects deployed in a cluster

| Kubernetes Object | Type | Required Resources | Namespaces |
| ------------------- | ------------------ | ----------------------- | --------------- |
| oomguard | ServiceAccount | - | kube-system |
| system:oomguard | ClusterRoleBinding |- | - |
| oom-guard | DaemonSet | 0.02-core CPU, 120 MB memory | kube-system |

## Overview 
This add-on is suitable for Kubernetes clusters where the node memory pressure is high and node failures are often caused by business container OOM.

## Limits
- The containerd service socket path is not changed, and the default path of TKE is retained:
   - docker runtime: `/run/docker/containerd/docker-containerd.sock`
   - containerd runtime: `/run/containerd/containerd.sock`
- The mount target of the cgroup memory subsystem is not changed, and the default mount target `/sys/fs/cgroup/memory` is retained.

## How to Use

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. On the **Cluster management** page, click the ID of the target cluster to go to the cluster details page.
3. In the left sidebar, click **Add-on management** to go to the “Add-on list” page.
4. On the **Add-On List** page, click **Create**, and on the displayed **Create an Add-On** page, select **OOM-Guard**.
5. Click **Done** to complete the process.
