## Overview
This document describes how to quickly create a Nginx service in a container cluster.

## Prerequisites
- You have [signed up for a Tencent Cloud account](https://www.tencentcloud.com/account/register).
- You have [created a cluster](https://intl.cloud.tencent.com/document/product/457/30637).

## Directions

### Creating a Nginx service
1. Log in to the TKE console and select **[Cluster](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. On the **Cluster Management** page, click the target cluster ID to enter the **Basic Information** page.
3. On the **Workload** > **Deployment** page, click **Create**. For more information on parameters, see [Deployment Management](https://intl.cloud.tencent.com/document/product/457/30662).
4. On the **Create Deployment** page, specify the basic information of the workload as shown below:
![](https://main.qcloudimg.com/raw/a1391e5768e6fd5cfe0e6b3c65417a50.png)
  - **Workload Name**: Here, it is `nginx`.
  - **Description**: Enter the workload information.
  -  **Label**: Here, the default value is `k8s-app = nginx`.
  - **Namespace**: Select a namespace as needed. The default value is `default`.
  - **Volume**: Set the volume to which your workload will be mounted based on your requirements. For more information, see [Instructions for Other Storage Volumes](https://intl.cloud.tencent.com/document/product/457/30678).
5. Configure "Containers in the Pod" as instructed. See the figure below:
![](https://main.qcloudimg.com/raw/2ec2c7c803ee61a2d218f17df785636e.png)
The main parameters are described as follows:
  - **Name**: Enter the name of the container in the Pod. Here, `test` is used as an example.
  - **Image**: Click **Select Image**, select **DockerHub Image** > **nginx** in the pop-up window, and click **Confirm**.
  - **Image Tag**: Use the default value `latest`.
  - **Pull Image from Remote Registry**: Three policies (`Always`, `IfNotPresent`, and `Never`) are available. Select a policy as required. In this example, **the default policy is used**.
6. In **Number of Instances**, set the number of instances for the service according to the following information. In this document, we choose **Manual Adjustment** and set the instance number to one. See the figure below:
![](https://main.qcloudimg.com/raw/51c4971952bbd697ca458a415fd1ce21.png)
7. Specify the access mode of the workload, as shown in the following figure.   
![](https://main.qcloudimg.com/raw/aedd2d73ab7e5f79218d8194c9b1c249.png)
 - **Service**: select **Enable**.
 - **Service Access**: select **LoadBalancer (public network)**.
 - **Load Balancer**: select according to your requirements.
 - **Port Mapping**: select TCP, and set both the container port and service port to 80.
>! The security group of the service’s cluster must open the node network and container network to the Internet. It is also required to open ports 30000 to 32768 to the Internet. Otherwise, the problem of TKE being unusable could occur. For more details, see [TKE Security Group Settings](https://intl.cloud.tencent.com/document/product/457/9084).
8. Click **Create workload** to complete the creation of the Nginx service.


### Accessing the Nginx service

Ngnix service can be accessed using the following two methods.

#### Accessing the Nginx service using the **load balancer IP**

1. In the left sidebar, click **[Cluster](https://console.cloud.tencent.com/tke2/cluster)** to go to the **Cluster Management** page.
2. Click the target cluster ID and select **Services and Routes** > **Service**.
3. On the Service list page, copy the load balancer IP of the Nginx service as shown below:
![](https://main.qcloudimg.com/raw/bab54241805b352ae007ece3d130bb4a.png)
4. Paste the CLB IP address in the browser and press **Enter** to access the service.

#### Accessing the Nginx service using the service name

Other services or containers in the cluster can access the WordPress service using the service name.

### Verifying the Nginx service
When the service is successfully created, you directly enter the Nginx server welcome page when accessing the service. See the figure below:
![](https://main.qcloudimg.com/raw/156e6d3b804e6b214ef7600fee4fa9c1.png)

### More Nginx settings
If the container fails to be created, you can view [Event FAQs](https://intl.cloud.tencent.com/document/product/457/8187) to locate the causes.
