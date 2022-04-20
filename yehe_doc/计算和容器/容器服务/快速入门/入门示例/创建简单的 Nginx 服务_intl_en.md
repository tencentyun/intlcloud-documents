## Overview
This document describes how to quickly create an Nginx service in a container cluster.

## Prerequisites
- You have registered a [Tencent Cloud account](https://intl.cloud.tencent.com/register).
- You have created a cluster. For more information on how to create a cluster, see [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637).

## Directions

### Creating Nginx service
1. Log in to the TKE console and select **[Cluster](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. On the **Cluster Management** page, click the ID of the cluster where the service will be created to go to the **Deployment** page of the cluster, as shown in the figure below:
![](https://main.qcloudimg.com/raw/036baf23123e7291d5fcfb82a2572e53.png)
3. Click **Create** on this page. For more information, see [Creating a Deployment](https://intl.cloud.tencent.com/document/product/457/30662).
4. On the "Create Workload" page, specify the basic information of the workload as instructed. See the figure below.
![](https://main.qcloudimg.com/raw/a1391e5768e6fd5cfe0e6b3c65417a50.png)
  - **Workload Name**: take nginx as an example in this document.
  - **Description**: fill in the related workload information.
  - **Label**: in this example, the default value of the label is k8s-app = **nginx**.
  - **Namespace**: select a namespace based on your requirements.
  - **Type**: take **Deployment (deploy Pods in an extensible manner)** as an example.
  - **Volume**: set the volume to which your workload will be mounted based on your requirements. For more information, see [Instructions for Other Storage Volumes](https://intl.cloud.tencent.com/document/product/457/30678).
5. Configure "Containers in the Pod" as instructed. See the figure below:
![](https://main.qcloudimg.com/raw/2ec2c7c803ee61a2d218f17df785636e.png)
The main parameters are described as follows:
  - **Name**: enter the name of the container in the pod. Here, “test” is used as an example.
  - **Image**: click **Select Image**, select **DockerHub Image** > **Nginx** in the pop-up, and click **OK**.
  - **Image Tag**: use the default value `latest`.
  - **Image Pull Policy**: choose from **Always**, **IfNotPresent** and **Never** as needed. In this document, we use the default policy.
6. In **Number of Instances**, set the number of instances for the service according to the following information. In this document, we choose **Manual Adjustment** and set the instance number to one. See the figure below:
![](https://main.qcloudimg.com/raw/51c4971952bbd697ca458a415fd1ce21.png)
7. Specify the access mode of the workload, as shown in the following figure.   
![](https://main.qcloudimg.com/raw/aedd2d73ab7e5f79218d8194c9b1c249.png)
 - **Service**: select **Enable**.
 - **Service Access**: select **Via Internet**.
 - **Load Balancer**: select according to your requirements.
 - **Port Mapping**: select TCP, and set both the container port and service port to 80.
>! The security group of the service’s cluster must open the node network and container network to the Internet. It is also required to open ports 30000 to 32768 to the Internet. Otherwise, the problem of TKE being unusable could occur. For more details, see [TKE Security Group Settings](https://intl.cloud.tencent.com/document/product/457/9084).
8. Click **Create workload** to complete the creation of the Nginx service.


### Accessing Nginx service

Ngnix service can be accessed using the following two methods.

#### Accessing Nginx service using **Cloud Load Balancer IP**

1. In the left sidebar, click **[Cluster](https://console.cloud.tencent.com/tke2/cluster)** to go to the **Cluster Management** page.
2. Click on the Nginx service’s cluster ID and select **Service** > **Service**.
3. On the service management page, copy the CLB IP address of the Nginx service. See the figure below.
![](https://main.qcloudimg.com/raw/bab54241805b352ae007ece3d130bb4a.png)
4. Paste the CLB IP address in the browser and press **Enter** to access the service.

#### Accessing Nginx service using service name

Other services or containers in the cluster can access the WordPress service using the service name.

### Verifying Nginx service
When the service is successfully created, you directly enter the Nginx server welcome page when accessing the service. See the figure below:
![](https://main.qcloudimg.com/raw/156e6d3b804e6b214ef7600fee4fa9c1.png)

### More Nginx settings
If the container fails to be created, you can view [Event FAQs](https://intl.cloud.tencent.com/document/product/457/8187) to locate the causes.
