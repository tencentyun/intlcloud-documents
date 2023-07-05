## Overview

### Add-on description

Node-Problem-Detector-Plus is an add-on that monitors the health status of Kubernetes cluster nodes. It runs in the TKE environment as a DaemonSet to help users detect various exceptions on nodes in real time and report the detection results to the upstream Kube-apiserver.

### Kubernetes objects deployed in a cluster



| Kubernetes Object Name | Type | Resource Amount | Namespaces |
| --------------------- | ------------------ | ------------ | --------------- |
| node-problem-detector | DaemonSet | 0.5C 80M | kube-system |
| node-problem-detector | ServiceAccount | -  | kube-system |
| node-problem-detector | ClusterRole | -  | -  |
| node-problem-detector | ClusterRoleBinding | -  | -  |

## Use Cases

Node-Problem-Detector-Plus can be used to monitor the running status of nodes, including kernel deadlocks, OOM, system thread pressure, system file descriptor pressure, and other metrics. It reports such information to the API Server as Node Conditions and Events.
You can estimate the resource pressure of nodes by detecting the corresponding metrics and then manually release or scale out node resources before nodes start draining pods. In this way, you can prevent potential losses resulted from Kubernetes resource repossessing or node unavailability.

## Limits
To use NPD in your cluster, you need to install this add-on in your cluster. The system resources used by NPD containers is restricted to 0.5 CPU core and 80 MB memory.


## Usage


1. Log in to the [TKE console](https://console.qcloud.com/tke2) and select **Cluster** in the left sidebar.
2. On the “**Cluster Management** page, click the ID of the target cluster to go to the cluster details page.
3. In the left sidebar, click **Add-on Management** to go to the **Add-on List** page.
4. On the **Add-on List** page, click **Create** to go to the **Create Add-on** page, and select **NodeProblemDetectorPlus**.
5. Click **Complete**. After the installation is successful, the corresponding node-problem-detector resources are available in your cluster, and the corresponding conditions will be added to Node Conditions.







## Appendix
### Node Conditions

After the NPD plug-in is installed, the following specific Conditions will be added to nodes:

| Condition| Default Value | Description |
| ------------------------- | ------ | ------------------------------------------------------------------------ |
| ReadonlyFilesystem | False | Indicates whether the file system is read-only. |
| FDPressure | False | Queries whether the number of file descriptors of the host reaches 80% of the max value. |
| FrequentKubeletRestart | False | Indicates whether Kubelet has restarted more than 5 times in 20 minutes. |
| CorruptDockerOverlay2 | False | Indicates whether the DockerImage is faulty. |
| KubeletProblem | False | Indicates whether the Kubelet service is Running. |
| KernelDeadlock | False | Indicates whether a deadlock exists in the kernel. |
| FrequentDockerRestart | False | Indicates whether Docker has restarted more than 5 times in 20 minutes. |
| FrequentContainerdRestart | False | Indicates whether Containerd has restarted more than 5 times in 20 minutes. |
| DockerdProblem | False | Indicates whether the Docker service is Running (if the node runtime is Containerd, the value is always False). |
| ContainerdProblem | False | Indicates whether the Containerd service is Running (if the node runtime is Docker, the value is always False). |
| ThreadPressure | False | Indicates whether the current number of threads of the system reaches 90% of the max value. |
| NetworkUnavailable | False | Indicates whether the NTP service status is Running. |
| SerfFailed | False | Detects the node network health status in distributed mode. |
