## Overview
WordPress is a blogging platform developed with PHP. You can use it as a content management system, or use it to create websites on services that support PHP and MySQL databases.

This document describes how to use the official `wordpress` image on Docker Hub to create a publicly accessible WordPress website.


## Prerequisites
>!
>- The `wordpress` image contains all operating environments for WordPress, allowing you to pull and create the service directly.
>- WordPress with a single Pod is used for testing purposes only, and therefore cannot ensure persistent data storage. It is recommended that you use a self-built MySQL or TencentDB to store your data. For more information, see [WordPress Using TencentDB](/doc/product/457/7447). 
>
- You have registered a [Tencent Cloud account](https://intl.cloud.tencent.com/register).
- You have created a cluster. For more information on how to create a cluster, see [Creating a cluster](https://intl.cloud.tencent.com/document/product/457/30637).

## Directions
### Creating a WordPress service
1. Log in to the TKE console and select **[Cluster](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. On the **Cluster Management** page, click the ID of the cluster for which the service is to create to go to the **Deployment** page of the cluster and click **Create**, as shown in the figure below.
![](https://main.qcloudimg.com/raw/1e32ac2e0e8d99315305f1b55034d691.png)
3. On the **Create Workload** page, specify basic information of the workload as instructed in the figure below.
![](https://main.qcloudimg.com/raw/a1c6b34a108a7a24d3f22e7048dec3ef.png)
 - **Workload Name**: enter the name of the workload to create. In this example, `wordpress` is used.
 - **Description**: specify related workload information.
 - **Tag**: specify the key-value pair. The default value is k8s-app = **wordpress** here.
 - **Namespace**: select a namespace based on your requirements.
 - **Type**: select a type based on your requirements.
 - **Volume**: set the volume to which the workload is mounted based on your requirements. For more information, see [Volume Management](https://intl.cloud.tencent.com/document/product/457/30678).
4. Set **Containers in the Pod** as instructed below:
The main parameters are described as follows. You can retain the default values of other parameters.
 - **Name**: enter the custom container name. In this example, `test` is used.
 - **Image**: enter `wordpress`.
 - **Image Tag**: enter **latest**.
 - **Image Pull Policy**: three policies are available. Select a policy as required. In this example, the default policy is used.
   If you do not set any image pull policy and **Image Tag** is left empty or set to `latest`, the `Always` policy is used. Otherwise, the `IfNotPresent` policy is used.
    - **Always**: always pull the image from the remote end.
    - **IfNotPresent**: a local image is used by default. If no local image is available, the image is pulled remotely.
    - **Never**: only use a local image. If no local image is available, an exception occurs.
6. Set the number of Pods for the service as instructed. See the figure below.
![](https://main.qcloudimg.com/raw/649c9a62a29a77d09451e6d0dc487d58.png)
 - **Manual adjustment**: set the number of pods. The number of pods in this example is set to 1. You can click "+" or "-" to change the number of pods.
 - **Auto Adjustment**: the number of pods is automatically adjusted if any of the setting conditions are met. For more information, see [Automatic Scaling Basic Operations](https://intl.cloud.tencent.com/document/product/457/32424).
8. Configure **Access Settings (Service)** for the workload as instructed below:
 - **Service**: select **Enable**.
 - **Service Access**: select **LoadBalancer (public network)**.
 - **Load Balancer**: select according to your requirements.
 - **Port Mapping**: select TCP, and set both the container port and service port to 80.
>! The security group of the cluster to which the service belongs must open the node network and container network to the Internet. It is also required to open ports 30000 to 32768 to the Internet. Otherwise, TKE may be unavailable. For more information, see [TKE Security Group Settings](https://intl.cloud.tencent.com/document/product/457/9084).
9. Click **Create Workload** to create the WordPress service.


### Accessing the WordPress service

You can access the WordPress service using either of the following two methods.

#### Access using the CLB IP address
1. In the left sidebar, click **[Cluster](https://console.cloud.tencent.com/tke2/cluster)** to go to the **Cluster Management** page.
2. Click the ID of the cluster to which the WordPress service belongs and select **Services and Routes** > **Service**.
3. On the service management page, copy the CLB IP address of the WordPress service, as shown in the figure below.
![](https://main.qcloudimg.com/raw/8a8ea1dc181ab31660313ed0883bc980.png)
4. Paste the CLB IP address in the browser and press **Enter** to access the service.

#### Accessing the WordPress service using the service name
Other services or containers in the cluster can access the WordPress service using the service name.

### Verifying the WordPress service
After the service is created, the WordPress server configuration page is displayed when you access the service, as shown in the figure below.
![](https://main.qcloudimg.com/raw/4ccbffc42a7f9381e2595175ea32be65.png)

### More WordPress settings
If the container fails to be created, you can view [Event FAQs](https://intl.cloud.tencent.com/document/product/457/8187) to locate the causes.

