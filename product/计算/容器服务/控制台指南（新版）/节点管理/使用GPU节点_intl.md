## Operation Scenario

If your business involves scenarios such as deep learning and high-performance computing, you can use TKE to support the GPU feature, which can help you quickly use a GPU container. If you need to activate the GPU feature, you can apply by [submitting a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=350&source=0&data_title=ÈÝÆ÷·þÎñTKE&step=1).
There are two ways to create a GPU CVM instance:
- [Creating a GPU CVM instance](#createGPUService)
- [Adding an existing GPU CVM instance](#addGPUService)


## Usage Restrictions

- The GPU support has to be activated separately by [submitting a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=350&source=0&data_title=ÈÝÆ÷·þÎñTKE&step=1) for application.
- For the added node, you should select a GPU model and an GPU-related image.
- TKE supports GPU scheduling only if the Kubernetes version of the cluster is above **1.8.\***.
- GPUs are not shared among containers. A container can request one or more GPUs. However, it cannot request a portion of one GPU.

## Steps

<span id="createGPUService"></span>
### Creating a GPU CVM Instance

For detailed steps, see [Creating a Cluster](https://cloud.tencent.com/document/product/457/32189). During the creation process, please note the following two points:
- On the "Select a model" page, set "Model" in "Node model" to a GPU model. See the figure below:
![](https://main.qcloudimg.com/raw/c56c36c18d72a34206a3ae1ae9686e7f.png)
- On the "CVM configuration" page, TKE will automatically perform the initial processes such as GPU driver installation according to the selected model, and you do not need to care about the basic image. 

<span id="addGPUService"></span>
### Adding an Existing GPU CVM Instance

For detailed steps, see [Adding an Existing Node](https://cloud.tencent.com/document/product/457/32203#addExistingNode). During the addition process, please note the following two points:
- On the "Select a node" page, select the existing GPU node. See the figure below:
![](https://main.qcloudimg.com/raw/9f06c1b1b02a649ae85a6c2c4a3ffe81.png)
- On the "CVM configuration" page, TKE will automatically perform the initial processes such as GPU driver installation according to the selected model, and you don't need to take care of the basic image.

