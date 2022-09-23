## Scenario

If your business involves scenarios such as deep learning and high-performance computing, you can use TKE to support the GPU feature, which can help you quickly use a GPU container.
You can enable GPU scheduling in multiple ways:

- [Adding a GPU node to the cluster](#addGPUNodesatCluster)
 - [Creating a GPU instance](#createGPUServer)
 - [Adding an existing GPU instance](#addGPUServer)
- [Creating a GPU service container](#createGPUServiceContainer)
 - [Creating a GPU service container in the console](#consoleCreate)
 - [Creating a GPU service container by using an application or kubectl command](#appOrKubectlCreate)

## Prerequisites

You have logged in to the [TKE console](https://console.cloud.tencent.com/tke2).

## Notes

- GPU scheduling is supported only when the Kubernetes version of the cluster is **1.8.\*** or later.
- GPUs are not shared among containers. A container can request one or more GPUs, but not part of a GPU.
- We recommend that you use the GPU feature together with affinity scheduling.

## Directions

<span id="addGPUNodesatCluster"></span>

### Adding a GPU node to a cluster

You can add a GPU node in either of the following ways:

- [Creating a GPU instance](#createGPUServer)
- [Adding an existing GPU instance](#addGPUServer)

<span id="createGPUServer"></span>

#### Creating a GPU instance

1. Click **[Clusters](https://console.cloud.tencent.com/tke2/cluster?rid=4)** in the left sidebar to go to the "Cluster Management" page.
2. Click **Create a Node** for the cluster in which the GPU instance is to be created.
3. On the "Select the Model" page, select **GPU Model** as the instance "Family" and select "GPU Compute GN2" as the "Model".
4. Complete the remainder of the process as instructed.

 >? During CVM configuration, TKE automatically performs the initial processes such as GPU driver installation based on the selected model, and you can ignore the basic image. 

<span id="addGPUServer"></span>

#### Adding an existing GPU instance

1. Click **[Clusters](https://console.cloud.tencent.com/tke2/cluster?rid=4)** in the left sidebar to go to the "Cluster Management" page.
2. Click **Add Existing Node** for the cluster in which an existing GPU instance is to be added.
3. On the "Select Nodes" page, select an existing GPU node and click **Next**.
4. Complete the remainder of the process as instructed.

 >? During CVM configuration, TKE automatically performs the initial processes such as GPU driver installation based on the selected model, and you can ignore the basic image.

<span id="createGPUServiceContainer"></span>

### Creating a GPU service container

You can create a GPU service container in either of the following ways:

- [Creating a GPU service container in the console](#consoleCreate)
- [Creating a GPU service container by using an application or kubectl command](#appOrKubectlCreate)

<span id="consoleCreate"></span>

#### Creating a GPU service container in the console

1. Click **[Clusters](https://console.cloud.tencent.com/tke2/cluster?rid=4)** in the left sidebar to go to the "Cluster Management" page.
2. Click the ID or name of the cluster for which the workload is to be created to go to the cluster management page for this workload.
3. Select a workload type under "Workload" to go to the corresponding information page. For example, choose **Workload** > **DaemonSet** to go to the DaemonSet information page.
4. Click **Create** to go to the "Create Workload" page.
5. Specify information such as the workload name and namespace as instructed. 
6. Click **Create Workload** to create the workload.

<span id="appOrKubectlCreate"></span>

#### Creating a GPU service container by using an application or kubectl command

You can add a GPU field in the YAML file by using an application or kubectl command.