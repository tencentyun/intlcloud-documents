## Overview
### qGPU overview


qGPU is a GPU sharing technology launched by Tencent Cloud. It can share a GPU card among multiple containers and isolate the vRAM and computing resources among containers. In this way, it ensures business security by using GPU cards at a smaller granularity to increase GPU utilization and reduce costs.
Based on TKE's open-source Nano GPU framework, qGPU can schedule GPU computing power and vRAM at a fine granularity, share a GPU card among multiple containers, and allocate GPU resources across GPU cards. Plus, relying on the powerful underlying isolation technology, it can strongly isolate vRAM and computing power to ensure that business performance and resource use are not affected by GPU sharing.

>? qGPU is currently in beta test. To try it out, please [submit a ticket](https://console.intl.cloud.tencent.com/workorder).

### qGPU features and strengths

The qGPU solution allows multiple containers to share NVIDIA GPU cards by effectively scheduling tasks on such cards. It has the following strengths:

- Flexibility: you can freely configure the GPU vRAM size and computing power proportion.
- Cloud nativeness: standard Kubernetes and NVIDIA Docker solutions are supported.
- Compatibility: there is no need to modify images, replace CUDA libraries, and rewrite business code, and the service can be easily deployed in a way imperceptible to the business.
- High performance: GPU devices are manipulated at the underlying layer, which has efficient convergence and nearly zero loss of throughput.
- Strong isolation: vRAM and computing power can be strictly isolated.

### Solution framework diagram

![](https://qcloudimg.tencent-cloud.cn/raw/671b1e90838586feaeccbbfdf6ed8507.png)

## Notes
- TKE version: v1.14.x or above
- OS: specific Tencent OS 3.1 image
- Model: CVM instances with V100 or T4 cards (CPM instances and more GPU card models will be supported in the future)
- Currently, the latest supported versions of NVIDIA Tesla driver and CUDA are 450.102.04 and 11.3 respectively. To ensure compatibility, we strongly recommend you use the built-in UMD on the nodes instead of installing it repeatedly in Pods.
- qGPU granularity: maximum number of qGPUs (number of Pods) assigned to 1 GPU = number of GPU vRAM size / 4 (for example, 32 GB vRAM can be assigned to up to 8 qGPUs), and at least 1 GB vRAM must be assigned to each qGPU.
- Nodes with the qGPU feature enabled cannot be used as regular GPU nodes, that is, they cannot use the resources of the entire GPU card. We recommend you use the TKE node pool to differentiate and schedule resources.
- If you need to upgrade the Kubernetes master version, please note that:
  - You do not need to set this plugin again for a managed cluster.
  - For a self-deployed cluster, master version upgrade will reset the configurations of all add-ons in the master, which affects the configuration of the qgpu-scheduler add-on as a scheduler extender. Therefore, you need to uninstall the qGPU add-on and install it again.


## Directions

>? As use of qGPU capabilities requires specific images and relevant labels, we strongly recommend you use the TKE node pool capability to group the nodes (nodes in a node pool have the same labels and image attributes). For more information, please see [Creating a Node Pool](https://intl.cloud.tencent.com/document/product/457/35901).


1. Log in to the [TKE console](https://console.qcloud.com/tke2) and select **Cluster** on the left sidebar.
2. On the **Cluster** page, click the target cluster ID to enter the cluster details page;
3. Select **Add-On Management** on the left sidebar to enter the **Add-On List** page.
4. On the **Add-On List** page, select **Create**. On the **Create Add-on** page, select qGPU (GPU isolation component).
5. Click **Parameter Configuration**, and you can set the scheduling policies of qgpu-scheduler.
   - **spread**: multiple Pods will spread among different nodes and GPU cards. The more the remaining resources on a node, the sooner the node will be selected. This policy is applicable to scenarios requiring high availability to avoid placing the replicas of an application on the same device.
   - **binpack**: multiple Pods will use the same node preferentially. This policy is applicable to scenarios with a high GPU utilization.
6. Click **Complete** to create the add-on. After it is successfully installed, you need to prepare GPU resources for the cluster.
7. Prepare GPU resources:
	1. Click **Create Node Pool** and select **qGPU-dedicated market image**:
	![](https://qcloudimg.tencent-cloud.cn/raw/0a5c6b124bbe04dec69e4fdef1e7f089.png)
	After you create a node with the image specified by qGPU, the TKE backend will automatically add the `qgpu-device-enable:"enable"` label to the node. After this label is set, the qgpu-manager DaemonSet will be scheduled to the corresponding node and automatically configure qGPU settings.
	2. Use the advanced configuration of the node pool to set labels so as to specify the qGPU isolation policy (you can enter the full name or abbreviation when entering the label values):
 - Label key: `tke.cloud.tencent.com/qgpu-schedule-policy`.
 - Label value: fixed-share (for more information on the valid values, please see the isolation policy description [table](#table) below).
![](https://qcloudimg.tencent-cloud.cn/raw/ba6baa998467430e728c2c57bd6690fc.png)
 Currently, qGPU supports the following three isolation policies:[](id:table)
<table>
<thead>
<tr>
<th>Label Value</th>
<th>Abbreviation</th>
<th>Parameter</th>
<th>Name</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td nowrap="nowrap">best-effort (default value)</td>
<td>be</td>
<td>Best Effort</td>
<td>Best effort</td>
<td>Default value. The computing power in each Pod is not limited, and as long as there is remaining computing power on a card, it can be used. If N Pods run together and each of them has a heavy load, 1/N computing power will be assigned to each Pod.</td>
</tr>
<tr>
<td>fixed-share</td>
<td>fs</td>
<td>Fixed Share</td>
<td>Fixed share</td>
<td>Each Pod has a fixed computing power share, which cannot be exceeded even when there is idle computing power in the GPU card.</td>
</tr>
<tr>
<td>burst-share</td>
<td>bs</td>
<td>Guaranteed Share with Burst</td>
<td>Guaranteed share with burst</td>
<td>The scheduler ensures that each Pod has a base share of computing power, but once the GPU card has idle computing power, it can be used by Pods. For example, when the GPU card has idle computing power (not assigned to other Pods), a Pod can use the computing power exceeding its base share. Note that if this part of idle computing power used by the Pod is assigned again, the Pod will use its base share again.</td>
</tr>
</tbody></table>
8. Assign GPU resources to the application. By setting the corresponding resources of qGPUs for the container, you can allow Pods to use qGPUs. You can configure this in the console or through YAML:
<dx-tabs>
::: Console
On the **Create Workload** page, directly enter the GPU resource information 
:::
::: YAML
You can use YAML to set qGPU resources:
```yaml
spec:
  containers:
    resources:
      limits:
        tke.cloud.tencent.com/qgpu-memory: "5"
        tke.cloud.tencent.com/qgpu-core: "30"
      requests:
        tke.cloud.tencent.com/qgpu-memory: "5"
        tke.cloud.tencent.com/qgpu-core: "30"
```
Here:
- qGPU resource values in `requests` and `limits` must be the same (according to K8s rules, you can skip the qGPU settings in `requests`, in which case the value in `limits` will be automatically used for it).
- `tke.cloud.tencent.com/qgpu-memory` indicates the size of vRAM (in MB) applied for by the container. **The value must be an integer and cannot be a decimal**.
- `tke.cloud.tencent.com/qgpu-core` indicates the computing power applied for by the container. Each GPU card can provide 100% computing power. **The value of `qgpu-core` must be below 100**. If the set value exceeds the proportion of the remaining computing power, the setting will fail. After it is set, you can get n% the computing power of the GPU card.
:::
</dx-tabs>




## Kubernetes Objects Deployed in Cluster

| Kubernetes Object Name | Type | Requested Resource |Namespace |
|---------|---------|---------|---------|
|qgpu-manager|	DaemonSet|	300 MB memory and 0.2 CPU core for each GPU node |	kube-system|
|qgpu-manager|	ClusterRole	|-|	-|
|qgpu-manager|	ServiceAccount|-|		kube-system|
|qgpu-manager|	ClusterRoleBinding|-|		kube-system|
|qgpu-scheduler|	Deployment	| 800 MB memory and 1 CPU core for a single replica	|kube-system|
|qgpu-scheduler|	ClusterRole|-|		-|
|qgpu-scheduler|	ClusterRoleBinding	|-|	kube-system|
|qgpu-scheduler|	ServiceAccount	|-|	kube-system|
|qgpu-scheduler|	Service|-|		kube-system|

