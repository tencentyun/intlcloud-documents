## Operation Scenario

If your business involves scenarios such as deep learning and high-performance computing, you can use TKE to support the GPU feature, which can help you quickly use a GPU container. If you need to activate the GPU feature, you can apply by [submitting a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=350&source=0&data_title=ÈÝÆ÷·þÎñTKE&step=1).
There are multiple ways to enable GPU scheduling:
- [Adding a GPU node to the cluster](#addGPUNodesatCluster)
 - [Creating a GPU CVM instance](#createGPUServer)
 - [Adding an existing GPU CVM instance](#addGPUServer)
- [Creating a GPU service container](#createGPUServiceContainer)
 - [Creating in the console](#consoleCreate)
 - [Creating through an application or kubectl command](#appOrKubectlCreate)

## Prerequisites

You are logged in to the [TKE console](https://console.cloud.tencent.com/tke2).

## Considerations
- GPU scheduling is supported only if the Kubernetes version of the cluster is above **1.8.\***.
- GPUs are not shared among containers. A container can request one or more GPUs. However, it cannot request a portion of one GPU.
- It is recommended to use the GPU feature together with affinity scheduling.

## Directions

<span id="addGPUNodesatCluster"></span>
### Adding a GPU Node to a Cluster

There are two ways to add a GPU node:
- [Creating a GPU CVM instance](#createGPUServer)
- [Adding an existing GPU CVM instance](#addGPUServer)

<span id="createGPUServer"></span>
#### Creating a GPU CVM Instance

1. In the left sidebar, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster?rid=4)** to go to the cluster management page.
2. In the row of the cluster for which to create a GPU CVM instance, click **Create a node**.
3. On the "Select a model" page, set the "Instance family" to "**GPU model**" and select "GPU compute type" for "Instance type". See the figure below:
![](https://main.qcloudimg.com/raw/4cb5eb503fb90aecc83911c84390bedf.png)
4. Follow the on-screen prompts to complete the creation.
 >? When selecting on the "CVM configuration" page, TKE will automatically perform the initial processes such as GPU driver installation according to the selected model, and you do not need to care about the basic image. 

<span id="addGPUServer"></span>
#### Adding an Existing GPU CVM Instance

1. In the left sidebar, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster?rid=4)** to go to the cluster management page.
2. In the row of the cluster for which to add an existing GPU CVM instance, click **Add an existing node**.
3. On the "Select a node" page, select the existing GPU node and click **Next**. See the figure below:
![](https://main.qcloudimg.com/raw/cd222f6e694f281662ccc8df289816c6.png)
4. Follow the on-screen prompts to complete the addition.
 >? When selecting on the "CVM configuration" page, TKE will automatically perform the initial processes such as GPU driver installation according to the selected model, and you do not need to care about the basic image.

<span id="createGPUServiceContainer"></span>
### Creating a GPU Service Container

There are two ways to create a GPU service container:
- [Creating in the console](#consoleCreate)
- [Creating through an application or kubectl command](#appOrKubectlCreate)

<span id="consoleCreate"></span>
#### Creating in the Console

1. In the left sidebar, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster?rid=4)** to go to the cluster management page.
2. Click the ID/name of the cluster where Workload needs to be created to enter the cluster management page.
3. Under "Workload", select a workload type to go to the corresponding information page. For example, select "Workload" > "DaemonSet" to go to the DaemonSet information page. See the figure below:
![](https://main.qcloudimg.com/raw/73b214fcb0cf26e569310894dd44c512.png)
4. Click **Create** to go to the "Create a workload" page.
5. Set the workload name, namespace and other information as instructed. In "GPU limit", set the GPU quantity limit. See the figure below:
![](https://main.qcloudimg.com/raw/a768a0610894587528573f959277ab9f.png)
6. Click **Create a workload** to complete the creation.

<span id="appOrKubectlCreate"></span>
#### Creating Through an Application or kubectl Command

You can add a GPU field in the YAML file through an application or kubectl command. See the figure below:
![](https://main.qcloudimg.com/raw/2f2b3a751fd4bc0a3d443d7495fb1050.png)

