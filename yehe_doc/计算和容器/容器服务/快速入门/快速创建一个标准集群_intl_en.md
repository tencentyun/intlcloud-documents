This document describes how to quickly create a container cluster in TKE.


## Step 1. Sign up for a Tencent Cloud Account
If you already have a Tencent Cloud account, ignore this step.
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://intl.cloud.tencent.com/zh/document/product/378/17985" target="_blank"  style="color: white; font-size:13px;">Sign up for Tencent Cloud</a></div>

## Step 2. Topping Up Online
The TKE service itself is currently free of charge, but you will be charged for cloud resources you actually use. What is to be created in this document is a managed cluster, and you need to pay for the worker nodes in the cluster, persistent storage, and load balancers bound to your services. For information on related operations, see [Payment Methods](https://intl.cloud.tencent.com/document/product/555/7425).



## Step 3. Authorizing TKE
Open the [Tencent Cloud console](https://console.cloud.tencent.com/), select **Tencent Cloud services** > **Tencent Kubernetes Engine** to enter the TKE console and authorize TKE according to the prompts. If you have already authorized TKE, skip this step.

<div style="background-color:#00A4FF; width: 150px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/tke2/cluster?rid=1" target="_blank"  style="color: white; font-size:13px;">Authorize</a></div>


## Step 4. Creating a Cluster
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/tke2/cluster/create?rid=1" target="_blank"  style="color: white; font-size:13px;">Create a cluster</a></div>

### Cluster information
On the **Cluster Information** page, enter the cluster name and select the region of the cluster, the cluster network, and container network. Keep other default options unchanged and click **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/48966b45ba60fe9116bb58edec3c58dd.png)

 - **Cluster Name**: Enter the cluster name, such as `test`.
 - **Region**: Select the region closest to your end user.
 - **Cluster Network**: Select a VPC. IP addresses within the VPC IP range are assigned to servers in the cluster. .
 - **Container Network**: Select an available contaienr network. IP addresses within the container network IP range are assigned to the containers in the cluster. 


### Selecting a model
On the **Select Model** page, confirm the billing mode, select an availability zone and the corresponding subnet, confirm the node model and click **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/ef0eddd2e2a0ea044774c4ee65d0a2ef.png)

- **Node Source**: Choose **Add Node**.
- **Master Node**: Choose **Managed**.
- **Billing Mode**: It defaults to **Pay-as-You-Go**. 
- **Worker Configurations**: Select an availability zone and the corresponding subnet and confirm the node model. Keep other default settings unchanged.
  - **Availability Zone**: Select an AZ.
  - **Node Network**: Select the subnet of the current VPC.
  - **Model**: Select a model, such as “S1.SMALL1 (Standard S1, 1-core 1 GB)”.

### CVM configuration
On the **CVM Configuration** page, select the login method, keep other default settings unchanged, and click **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/83501db19590eccb230c482ae37bd3a9.png)

- **Login Method**: Options include **SSH Key Pair**, **Random Password** or **Custom Password**. **Random Password** is used in this document.

### Component configurations
On the **Component Configurations** page, you can choose the components you need, including storage, monitoring, image, etc. If you don’t need these components, click **Next** directly. Here we choose not to install components and keep other default settings unchanged.

### Information confirmation
On the **Confirm Information** page, confirm the selected configuration information and billing mode for the cluster and click **Complete**.
![](https://qcloudimg.tencent-cloud.cn/raw/bebdbb0524ba191175daa935b9d7d986.png)


Make the payment and create a cluster. Then you can view the managed cluster you create in the [TKE console](https://console.cloud.tencent.com/tke2/cluster?rid=1).

## Step 5: Viewing the Cluster
You can view clusters that have been created in the [cluster list](https://console.cloud.tencent.com/tke2/cluster?rid=1). You can click the cluster ID to enter the details page, and then view the cluster, node, and network information on the **Basic Information** page.
![](https://qcloudimg.tencent-cloud.cn/raw/0f36c74372186d3efdf1ba2f1751f228.png)




## Step 6: Deleting Clusters
Once started, clusters will start to consume resources. To avoid unnecessary costs, you can follow the steps below to clear all the resources.

1. Select **Cluster** in the left sidebar. On the **Cluster Management** page, select **More** > **Delete** for the cluster to delete.
![](https://qcloudimg.tencent-cloud.cn/raw/9431c8e5c0038ec85e1e04edbc217b0c.png)
2. Confirm related information on the **Delete Clusters** pop-up window and click **Confirm** to delete clusters.





## Working with a Cluster
Refer to the documents below for common cluster operations:
- [Creating Simple Nginx Service](https://intl.cloud.tencent.com/document/product/457/7851)
- [WordPress with Single Pod](https://intl.cloud.tencent.com/document/product/457/7205)
- [WordPress Service using TencentDB](https://intl.cloud.tencent.com/document/product/457/7447)
- [Building Hello World Service Manually](https://intl.cloud.tencent.com/document/product/457/7204)
- [Building a Simple Web Application](https://intl.cloud.tencent.com/zh/document/product/457/6996)


## Troubleshooting
If you encounter any problem during the whole process, please [submit a ticket](https://console.intl.cloud.tencent.com/workorder) to contact us.
