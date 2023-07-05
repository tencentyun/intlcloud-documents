This document describes how to quickly create a container cluster using TKE.


## Step 1. Sign up for a Tencent Cloud account
Before using TKE, you need to sign up for a [Tencent Cloud account](https://www.tencentcloud.com/account/register?s_url=https%3A%2F%2Fconsole.tencentcloud.com%2Ftke2%2Fcluster%3Frid%3D1) and complete [identity verification](https://www.tencentcloud.com/document/product/378/3629).

## Step 2. Top up online
Cluster management fees and cloud resource fees are charged based on the actual usage of TKE managed clusters with different specifications. For billing modes and prices, see [TKE Billing Overview](https://intl.cloud.tencent.com/document/product/457/45157). In this document, a managed cluster is created. You still need to pay for services such as cluster worker nodes, persistent storage, and CLB instances bound to the service. Before making a purchase, top up your account as instructed in [Payment methods](https://intl.cloud.tencent.com/document/product/555/7425).



## Step 3. Authorize the service
Open the [Tencent Cloud console](https://console.cloud.tencent.com/), select **Tencent Cloud services** > **Tencent Kubernetes Engine** to enter the TKE console and authorize TKE according to the prompts. If you have already authorized TKE, skip this step.

<div style="background-color:#00A4FF; width: 150px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/tke2/cluster?rid=1" target="_blank"  style="color: white; font-size:13px;">Click here to authorize TKE</a></div>


## Step 4. Create a cluster
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/tke2/cluster/create?rid=1" target="_blank"  style="color: white; font-size:13px;">Click here to enter the creation page</a></div>

### Cluster information
On the **Cluster information** page, enter the cluster name and select the region of the cluster, the cluster network, and container network. Keep other default options unchanged and click **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/48966b45ba60fe9116bb58edec3c58dd.png)

 - **Cluster name**: Enter the cluster name. We use "test" as the cluster name in this document.
 - **Region**: select a region closest to you. For example, if you are in “Shenzhen”, please select “Guangzhou”.
 - **Cluster network**: Assign IP addresses within the node network address range to the servers in the cluster. Here we select VPC.
 - **Container network**: Assign IP addresses within the container network address range to the containers in the cluster. Here, we select an available container network.


### Selecting a model
On the **Select model** page, confirm the billing mode, select an availability zone and the corresponding subnet, confirm the node model and click **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/ef0eddd2e2a0ea044774c4ee65d0a2ef.png)

- **Node source**: You can select **Add node** or **Existing nodes**. Here, we select "Add node".
- **Cluster Type**: You can select **Self-deployed Cluster** or **Managed Cluster**. Here we select the latter.
- **Cluster Specification**: Multiple cluster specifications are provided. Here we select **L5**.
- **Billing Mode**: **Pay-as-you-go** is available.
- **Worker configurations**: You only need to select an availability zone and the corresponding subnet and confirm the node model. Keep other default settings unchanged.
  - **Availability Zone**: Here we select **Guangzhou Zone 1**.
  - **Node network**: Here we select the subnet under the current VPC.
  - **Model**: Here we select **SA2.MEDIUM2 (Standard SA2, 2-core 2 GB)**.

### CVM configuration
On the **CVM configuration** page, select the login method, keep other default settings unchanged, and click **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/83501db19590eccb230c482ae37bd3a9.png)

- **Login method**: You can select **SSH key pair**, **Random password** or **Custom password**. Here we select "Random password".

### Add-on configurations
On the **Add-on configurations** page, you can choose the add-ons you need, including storage, monitoring, image, etc. If you don't need them, click **Next**. Here, we choose not to install add-ons and keep other default settings unchanged.

### Information confirmation
On the **Confirm Info** page, confirm the selected configuration information and billing mode for the cluster, read and indicate your consent to the TKE SLA, and click **Done** as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/bebdbb0524ba191175daa935b9d7d986.png)


You can create your first TKE general cluster after making the payment. Then, you can view the created cluster in the [TKE console](https://console.cloud.tencent.com/tke2/cluster?rid=1).

## Step 5. View a cluster
You can view clusters that have been created in the [cluster list](https://console.cloud.tencent.com/tke2/cluster?rid=1). You can click the cluster ID to enter the details page, and then view the cluster, node, network, and API server information on the **Basic Information** page as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/0f36c74372186d3efdf1ba2f1751f228.png)



## Step 6. Delete a cluster
Once started, clusters will start to consume resources. To avoid unnecessary costs, you can follow the steps below to clear all the resources.

1. Select **Cluster** on the left sidebar. On the **Cluster Management** page, select **More** > **Disable Deletion Protection** on the right of the target cluster as shown below:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/iEGX674_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221215175257.png)
2. Select **More** > **Delete** on the right of the cluster as shown below:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Pt9T223_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221215175351.png)
2. Confirm related information in the **Delete clusters** pop-up window and click **Confirm** to delete clusters.



## Subsequent Operation: Using a Cluster
Now you know how to create and delete clusters in TKE. You can set workloads and create services in the clusters. Common tasks include:
- [Creating Simple Nginx Service](https://intl.cloud.tencent.com/document/product/457/7851)
- [WordPress with Single Pod](https://intl.cloud.tencent.com/document/product/457/7205)
- [WordPress Service using TencentDB](https://intl.cloud.tencent.com/document/product/457/7447)
- [Building Hello World Service Manually](https://intl.cloud.tencent.com/document/product/457/7204)
- [Building a Simple Web Application](https://intl.cloud.tencent.com/document/product/457/6996)


## Troubleshooting
For detailed directions on how to create a general cluster in the TKE console, see [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637). If you encounter any problems during the use, [contact us](https://intl.cloud.tencent.com/document/product/457/46720) for assistance.
