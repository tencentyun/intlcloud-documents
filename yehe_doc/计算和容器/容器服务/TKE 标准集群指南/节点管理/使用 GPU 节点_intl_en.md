## Overview
If your business involves scenarios such as deep learning and high-performance computing, you can use TKE to support the GPU feature, which can help you quickly use a GPU container.
There are many ways to create a GPU CVM instance:
- [Create a GPU CVM instance](#createGPUService)
- [Add an existing GPU CVM instance](#addGPUService)
- [Create a node pool](https://intl.cloud.tencent.com/document/product/457/35901)


## Usage Limits
- You need to select the GPU model for the added node. You can have the GPU driver automatically installed as needed. For more information, see [GPU Driver](#newGPUService).
- TKE supports GPU scheduling only if the Kubernetes version of the cluster is later than **1.8.\***.
- By default, GPUs are not shared among containers. A container can request one or more GPUs, but not part of a GPU.
- The **master node** in a self-deployed cluster currently does not support the GPU model setting.

## Directions

[](id:createGPUService)
### Creating GPU CVM instance

For more information, see [Adding a Node](https://intl.cloud.tencent.com/document/product/457/30652). When creating a GPU, you should pay special attention to the following parameters:
#### Model
On the **Select Model** page, set **Model** in **Node Model** to GPU.

#### GPU driver, CUDA version, and cuDNN version[](id:newGPUService)
After setting the model, you can select the GPU driver version, CUDA version, and cuDNN version as needed.
<dx-alert infotype="explain" title=" ">

- If you select **Automatically install GPU driver on the backend**, it will be installed automatically during system start, taking 15–25 minutes.
- The supported driver versions are determined by both the operating system and the GPU model.
- If you do not select **Automatically install GPU driver on the backend**, the GPU driver will be installed by default for some operating systems of earlier versions to ensure the normal use. The complete default driver version information is as shown below:
<table>
<thead>
<tr>
<th>Operating System</th>
<th>Default Driver Version Installed</th>
</tr>
</thead>
<tbody><tr>
<td>CentOS 7.6, Ubuntu 18, Tencent Linux2.4</td>
<td>450</td>
</tr>
<tr>
<td>CentOS 7.2 (not recommended)</td>
<td>384.111</td>
</tr>
<tr>
<td>Ubuntu 16 (not recommended)</td>
<td>410.79</td>
</tr>
</tbody></table>
</dx-alert>




#### MIG
With multi-instance GPU (MIG) enabled, an A100 GPU will be divided into seven separate GPU instances to help you improve the GPU utilization when multiple jobs are running. For more information, see [NVIDIA Multi-Instance GPU User Guide](https://docs.nvidia.com/datacenter/tesla/mig-user-guide/index.html).
<dx-alert infotype="notice" title=" ">
To use the MIG feature, make sure the following conditions are met:
<li>The GPU model is GT4.</li>
<li>You have selected **Automatically install GPU driver on the backend** in the console and configured the GPU, CUDA, and cuDNN versions.</li>
</dx-alert>






[](id:addGPUService)
### Adding existing GPU CVM instance

For detailed directions, see [Adding a Node](https://intl.cloud.tencent.com/document/product/457/30652). When adding a node, you should pay attention to the following:
- On the **Select Node** page, select an existing GPU node as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/134239c5fde42c8082d4cb76699125f1.png)
- Configure the automatic installation of the GPU driver and MIG as needed.

