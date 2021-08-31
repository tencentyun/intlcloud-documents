## Introduction to TKE

Based on native Kubernetes, Tencent Kubernetes Engine (TKE) is a container-oriented, highly scalable, and high-performance container management service. Compared with a client's container service, TKE has core advantages such as its ease of use, flexible expansion, security, reliability, high efficiency, and low costs. For more information, see [Tencent Kubernetes Engine](https://intl.cloud.tencent.com/document/product/457).

## Overview

As an open source platform for automated container operations, Kubernetes is a mainstream choice for developers. However, the access capability of Kubernetes clusters are not sufficient and cannot meet the requirements of large applications. Using API Gateway as the access layer of Kubernetes can significantly improve the access capability of Kubernetes clusters and empower Kubernetes clusters with advanced capabilities of API Gateway, adapting to more scenarios of more customers.
![](https://main.qcloudimg.com/raw/736f4e705327d4cb5aa42e4e970d1298.svg)

## Prerequisites

You have activated Tencent Cloud services such as API Gateway, TKE, Cloud Load Balancer (CLB), Virtual Private Cloud (VPC), and Cloud Virtual Machine (CVM) and have permission to configure these services, as they will be used during the configuration process.

## Directions

<span id="1"></span>
### Step 1: Create a VPC
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. In the left sidebar, click **Virtual Private Cloud** to access the VPC list page.
3. Click **+ New**. In the pop-up dialog box, set the parameters to create a VPC.
For more information, see [Managing VPC Instances](https://intl.cloud.tencent.com/document/product/215/31805).
 


<span id="2"></span>
### Step 2: Create a CVM
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm).
2. In the left sidebar, click **Instances** to access the CVM instance list page.
3. Click **Create** to access the CVM purchase page.
4. Create a CVM by following the instructions in [Creating Instances via the CVM Purchase Page](https://intl.cloud.tencent.com/document/product/213/4855).
>!When creating a CVM, select the VPC and the subnet created in [Step 1](#1) and retain the default values for the other parameters. In this example, a standard S5 CVM instance is created.

  
 
<span id="3"></span>
### Step 3: Create a TKE cluster in the same VPC
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **Cluster** to access the TKE cluster list page.
3. Click **Create** at the top of the TKE cluster list. On the **Create Cluster** page, create a TKE cluster by following the instructions in [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637).
 >!
>- When configuring the cluster information, set **Cluster network** to the VPC created in Step 1.
>- When selecting a model, set **Node Source** to **Existing nodes** and **Master Node** to **Managed**, and select the CVM created in [Step 2](#2) in the **Worker Configurations** area.
>- Retain the default values for the other parameters.
 
 ![](https://main.qcloudimg.com/raw/91aabf8a50b61cceef077112ecbc5fef.png)

### Step 4: Create a nginx service in the TKE cluster
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2). In the left sidebar, click **Cluster** to access the TKE cluster list page.
2. Click the ID of the TKE cluster created in [Step 3](#3) to access the cluster details page.
3. In the left sidebar, click **Workload** -> **Deployment** to access the deployment list page.
4. Click **Create** at the top of the deployment list page to access the workload creation page.
5. Set the parameters on the workload creation page by following the instructions in [Creating a Simple Nginx Service](https://intl.cloud.tencent.com/document/product/457/7851).
 >!
 >- Select a DockerHub nginx image.
 >- Set **Service Access** to **Via VPC**.
 >- Set **Load Balancer** to **Automatic creation**.
 >- In the **Port Mapping** area, set **Protocol** to **TCP**, and set both **Target Port** and **Port** to 80.
6. Click **Create Workload** to finish creating the Workload. TKE will automatically create the corresponding deployment and service.
	

### Step 5: Create an API Gateway service
1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway).
2. In the left sidebar, click **Service** to access the service list page.
3. Click **Create** at the top of the service list. In the pop-up dialog box, create an API Gateway service by following the instructions in [Creating Services](https://intl.cloud.tencent.com/document/product/628/11787).

### Step 6: Create an API in the API Gateway service
1. In the [API Gateway console](https://console.cloud.tencent.com/apigateway), click **Service** in the left sidebar to access the service list page.
2. Click the name of the created API Gateway service to access the service details page.
3. Click the **Manage API** tab, and then click **Create** to access the API creation page.
4. Enter the frontend configuration, the backend configuration, and the response result, and click **Complete** to finish creating the API.
>!When entering the backend configuration, set **Backend Type** to **HTTP**, **VPC Info** to the VPC created in Step 1, **VPC resources** to **CLB**, and **Backend Path** to **/**.

  

<span id="7"></span>
### Step 7: Open the private IP ranges of API Gateway to the internet
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm). In the left sidebar, click **Security Groups** to access the security group list page.
2. Select a region and click **+ New**. In the pop-up dialog box, set the parameters and click **OK** to create a security group.
	 
3. In the security group list, click the name of the created security group to access the security group details page. Click the **Security Group Rule** tab and then the **Inbound rule** tab to access the inbound rule list.
4. Click **Add a Rule**. In the pop-up dialog box, enter the following 5 private IP ranges of API Gateway: **9.0.0.0/8**, **10.0.0.0/8**, **100.64.0.0/10**, **11.0.0.0/8**, and **30.0.0.0/8**. Set **Protocol port** to **ALL** and **Policy** to **Allow** for the 5 private IP ranges, and click **Completed** to add the 5 inbound rules.
	 
5. Return to the security group details page. Click the **Associate with Instance** tab and then the **Cloud Virtual Machine** tab. Click **Add Instances**. In the pop-up dialog box, associate the created security group with the CVM created in [Step 2](#2) to open the private IP ranges of API Gateway to the internet.

### Step 8: Publish and test the API Gateway service
1. In the [API Gateway console](https://console.cloud.tencent.com/apigateway), click **Service** in the left sidebar to access the service list page.
2. Click the name of the created API Gateway service to access the service details page.
3. Click the **Basic Configuration** tab, and click **Publish** in the upper right corner of the page to publish the service to the **Publish** environment.
4. Request the API created in [Step 6](#6). If the nginx page is displayed, the access is successful.

<img src="https://main.qcloudimg.com/raw/7c2d94c0bfc199305a68df3f0eb0001c.png" width="60%" height="60%">
