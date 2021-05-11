
## Overview

### Add-on description

GPU Manager is an all-in-one GPU manager. It is implemented based on the Kubernetes Device Plugin system. This manager provides features such as assigning shared GPUs, querying GPU metrics, and preparing GPU-related devices before running a container. It supports your use of GPU devices in Kubernetes clusters.

### Add-on features
- **Topology assignment**: provides an assignment feature based on GPU topology. When you assign an application with more than one GPU card, this feature can select the fastest topology link method to assign the GPU device.
- **GPU sharing**: allows you to submit tasks with less than one GPU card, and guarantees QoS.
- **Query of application GPU metrics**: you can access the `/metric` path of the CVM port (port 5678 by default) to provide the GPU metric collection feature for Prometheus. You can also access the `/usage` path to query the status of readable containers.

### Kubernetes objects deployed in a cluster


| Kubernetes Object Name | Type | Recommended Resource Reservation | Namespaces |
| --------------------- | ---------- | ------ | ------------ |
| gpu-manager-daemonset | DaemonSet | 1-core CPU and 1-GiB memory for each node | kube-system |
| gpu-quota-admission | Deployment | 1-core CPU and 1-GiB memory for each node | kube-system |

## Use Cases

When the GPU application is running in a Kubernetes cluster, it can prevent the waste of resources caused by requesting a whole card in scenarios such as AI training, enabling full utilization of resources.

## Limits
- This add-on is implemented through Kubernetes Device Plugin. It can be directly used on clusters with Kubernetes version 1.10 and later.
-  Each GPU card is split into 100 shares. The GPU usage can be a decimal value from 0.1 to 0.9 or an integer. VRAM resources are assigned memory capacities in the minimum unit of 256 MiB.
- To use GPU-Manager, the cluster must contain GPU model nodes.



## Usage

### Installing the add-on
1. Log in to the [TKE console](https://console.qcloud.com/tke2) and select **Cluster** in the left sidebar.
2. On the **Cluster Management** page, click the ID of the target cluster to go to the cluster details page.
3. In the left sidebar, click **Add-On Management** to go to the "Add-On List" page.
4. On the "Add-On List" page, click **Create**. On the "Create an Add-On" page that appears, select **GpuManager**.
5. Click **Finish** to create the add-on.



### Creating fine-grained GPU workloads
After the GpuManager add-on is successfully installed, you can use the following two methods to create fine-grained GPU workloads.

#### Method 1: Creating in the TKE console
1. Log in to the TKE console and select **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. Select the cluster for which you want to create the GPU application to go to the workload management page. Then, click **Create**.
3. On the "Create a Workload" page, configure the configuration items as needed. You can configure a fine-grained GPU workload in **GPU Resources**, as shown in the figure below:
![](https://main.qcloudimg.com/raw/d1bd71b3b773a69fab38a408369cca8c.png)

#### Method 2: Creating through YAML
>? When submitting, use YAML to configure GPU resource usage for the container. For core resources, you must enter `tencent.com/vcuda-core` in "resource". For VRAM resources, you must enter `tencent.com/vcuda-memory` in "resource".

The following shows a YAML example:
- A P4 device using 1 card:

```
apiVersion: v1
kind: Pod
...
spec:
containers:
 - name: gpu
resources:
tencent.com/vcuda-core: 100
```

- An application using 5-GiB VRAM and 0.3 cards:

```
apiVersion: v1
kind: Pod
...
spec:
containers:
 - name: gpu
resources:
tencent.com/vcuda-core: 30
tencent.com/vcuda-memory: 20
```

