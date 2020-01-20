
## Overview

### Add-on description

GPU Manager is an all-in-one GPU manager. It is implemented based on the Kubernetes Device Plugin system. This manager provides features such as assigning shared GPU, querying GPU metrics, and preparing GPU-related devices before running a container. It supports your use of GPU devices in Kubernetes clusters.

### Add-on features
- **Topology assignment**: provides an assignment feature based on GPU topology. When you assign an application with more than one GPU card, it can select the fastest topology link method to assign the GPU device.
- **GPU sharing**: allows you to submit tasks with less than one GPU card, and supplies QoS assurance.
- **Querying application GPU metrics**: You can access the `/metrics` path of the CVM port (by default this is 5678) to provide GPU metrics collection feature for Prometheus, and can access the `/usage` path to perform state querying of readable containers.

### Kubernetes objects deployed in a cluster

Deploying GPU-Manager Add-on in a cluster will deploy the following Kubernetes objects in the cluster:

| Kubernetes Object Name             | Type                       | Default Resource Occupation | Namespaces |
| --------------------- | ---------- | ------ | ------------ |
| gpu-manager-daemonset | DaemonSet  | /      | kube-system  |
| gpu-quota-admission   | Deployment | /      | kube-system  |

## Use cases

When the GPU application is running in a Kubernetes cluster, it can prevent the waste of resources caused by requesting a whole card in scenarios such as AI training, allowing full utilization of resources.

## Limits
- This add-on is implemented through Kubernetes Device Plugin. It can be directly used on clusters of Kubernetes version 1.10 and above.
-  Each GPU card is split into 100 shares. The usage of GPU can only be a between 0.1 to 0.9, or an integer. VRAM resources are assigned memory with 256MiB as the smallest unit.
- To use GPU-Manager, the cluster must contain GPU model nodes.

## Usage

### Installing the add-on
1. Log in to the [TKE Console](https://console.cloud.tencent.com/tke2), and select **Add-ons** in the left sidebar.
2. On the top of the **Add-ons** management page, select the region and the cluster for installing GPU-Manager, and click **Create**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/d087e46c782e0fe391bb0abd7d2af71d.png)
3. In the **Create Add-on** page, select **GPU Manager**, and click **Complete** to install it.



### Creating fine-grained GPU workloads
After GPU-Manager is successfully installed, you can use the following two methods to create fine-grained GPU workloads.

#### Method 1: creating through the TKE Console
1. Log in to the TKE Console and select **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. Select the cluster for which you want to greate the GPU applicaiton, go to the workload management page, and click **Create**.
3. In the **Create Workload** page, complete configuration as needed. You can configure a fine-grained GPU workload in **GPU Limits**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/1158f1e99e049a83c48692e19ae6aa6b.png)


#### Method 2: creating through YAML
>When submitting, use YAML to set the GPU resource usage for the container. This resource must have `tencent.com/vcuda-core` entered in “resources”. The VRAM resources must be written in “resources” as `tencent.com/vcuda-memory`.

A YAML example is as follows:
- P4 device using 1 card:
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
- 5GiB VRAM application using 0.3 cards:
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
