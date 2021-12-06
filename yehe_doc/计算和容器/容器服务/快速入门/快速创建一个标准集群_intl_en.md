This document describes how to quickly create a container cluster using TKE.


## Step 1. Sign up for a Tencent Cloud Account
If you already have a Tencent Cloud account, ignore this step.
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2F" target="_blank"  style="color: white; font-size:13px;">Click here to sign up for a Tencent Cloud account</a></div>

## Step 2: Topping Up Online
The TKE service itself is currently free of charge, but you will be charged for cloud resources you actually use. What is to be created in this document is a “managed cluster”, and you need to pay for the worker nodes in the cluster, persistent storage, and load balancers bound to your services. For information on related operations, see [Payment Methods](https://intl.cloud.tencent.com/document/product/555/7425).



## Step 3. Authorizing TKE
Open the [Tencent Cloud console](https://console.cloud.tencent.com/), select **Tencent Cloud services** > **Tencent Kubernetes Engine** to enter the TKE console and authorize TKE according to the prompts. If you have already authorized TKE, skip this step.

<div style="background-color:#00A4FF; width: 150px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/tke2/cluster?rid=1" target="_blank"  style="color: white; font-size:13px;">Click here to authorize TKE</a></div>


## Step 4: Creating a Cluster
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/tke2/cluster/create?rid=1" target="_blank"  style="color: white; font-size:13px;">Click here to enter the creation page</a></div>

### Cluster information
On the **Cluster Information** page, enter the cluster name and select the region of the cluster, the cluster network, and container network. Keep other default options unchanged and click **Next**, as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/48966b45ba60fe9116bb58edec3c58dd.png)

 - **Cluster Name**: enter the cluster name. We use “test” as the cluster name in this document.
 - **Region**: select a region closest to you. For example, if you are in “Shenzhen”, please select “Guangzhou”.
 - **Cluster Network**: assign IP addresses within the node network address range to the servers in the cluster. Here we select VPC.
 - **Container Network**: assign IP addresses within the container network address range to the containers in the cluster. Here we select an available container network.


### Selecting a model
On the **Select Model** page, confirm the billing mode, select an availability zone and the corresponding subnet, confirm the node model and click **Next**, as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/ef0eddd2e2a0ea044774c4ee65d0a2ef.png)

- **Node Source**: you can select **Add Node** or **Existing Nodes**. Here we select “Add Node”.
- **Master Node**: you can select from the two cluster modes: **Managed** and **Self-deployed**. Here we select “Managed”.
- **Billing Mode**: you can only select **Pay-as-You-Go**. Here we select “Pay-as-You-Go”.
- **Worker Configuration**: you only need to select an availability zone and the corresponding subnet and confirm the node model. Please keep other default settings unchanged.
  - **Availability Zone**: here we select “Guangzhou Zone 3”.
  - **Node Network**: here we select the subnet of the current VPC.
  - **Model**: here we select “S1.SMALL1 (Standard S1, 1-core 1 GB)”.

### CVM configuration
On the **CVM Configuration** page, select the login method, keep other default settings unchanged, and click **Next**, as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/83501db19590eccb230c482ae37bd3a9.png)

- **Login Method**: you can select **SSH Key Pair**, **Random Password** or **Custom Password**. Here we select “Random Password”.

### Component configurations
On the **Component Configurations** page, you can choose the components you need, including storage, monitoring, image, etc. If you don’t need these components, click **Next** directly. Here we choose not to install components and keep other default settings unchanged.

### Information confirmation
On the **Confirm Info** page, confirm the selected configuration information and billing mode for the cluster and click **Done**, as shown in the figure below:
![](https://qcloudimg.tencent-cloud.cn/raw/bebdbb0524ba191175daa935b9d7d986.png)


You can create your first cluster after paying the bill. Then you can view the managed cluster you create on the [TKE console](https://console.cloud.tencent.com/tke2/cluster?rid=1).

## Step 5: Viewing the Cluster
You can view clusters that have been created in the [cluster list](https://console.cloud.tencent.com/tke2/cluster?rid=1). You can click the cluster ID to enter the details page, and then view the cluster, node, and network information on the “Basic Information” page, as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/0f36c74372186d3efdf1ba2f1751f228.png)




## Step 6: Deleting Clusters
Once started, clusters will start to consume resources. To avoid unnecessary costs, you can follow the steps below to clear all the resources.

1. Select **Cluster** in the left sidebar. On the **Cluster Management** page, select **More** > **Delete** to the right on the raw where the cluster to be deleted is located.
![](https://qcloudimg.tencent-cloud.cn/raw/9431c8e5c0038ec85e1e04edbc217b0c.png)
2. Confirm related information on the “Delete Clusters” pop-up window and click **Confirm** to delete clusters.





## Subsequent Operation: Using a Cluster
Now you know about how to create and delete clusters in TKE after reading this document. You can set workloads and create services in created clusters. Common tasks include:
- [Creating Simple Nginx Service](https://intl.cloud.tencent.com/document/product/457/7851)
- [WordPress with Single Pod](https://intl.cloud.tencent.com/document/product/457/7205)
- [WordPress Service using TencentDB](https://intl.cloud.tencent.com/document/product/457/7447)
- [Building Hello World Service Manually](https://intl.cloud.tencent.com/document/product/457/7204)
- [Building a Simple Web Application](https://intl.cloud.tencent.com/zh/document/product/457/6996)


## Troubleshooting
If you encounter any problem during the whole process, please [submit a ticket](https://console.intl.cloud.tencent.com/workorder) to contact us.
