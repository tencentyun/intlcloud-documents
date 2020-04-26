## Scenario
WordPress is a blogging platform developed with PHP. You can use it as a content management system, or use it to build websites based on a service architecture that supports PHP and MySQL databases.

This document describes how to use the official `wordpress` image on Docker Hub to build a public WordPress website.


## Prerequisites
>
>- The `wordpress` image contains all runtime environments for WordPress, and you can directly pull these resources to create a service.
>- WordPress with a single pod is used for testing purposes only, and therefore data may not be stored permanently. We recommend that you build your own MySQL or TencentDB database to store your data. For more information, see [WordPress Using TencentDB](https://intl.cloud.tencent.com/document/product/457/7447). 
>
- You have [registered for a Tencent Cloud account](https://intl.cloud.tencent.com/register).
- You have created a cluster. For more information on how to create a cluster, see [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637).

## Directions
### Creating a WordPress service
1. Log in to the TKE console and click **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. On the "Cluster Management" page, select the ID of the cluster to create the service and go to the "Deployment" page of the workload in the cluster. Then, click **Create**, as shown in the following figure.
![](https://main.qcloudimg.com/raw/1e32ac2e0e8d99315305f1b55034d691.png)
3. On the "Create Workload" page, specify the basic information of the workload as instructed. See the figure below.
![](https://main.qcloudimg.com/raw/a1c6b34a108a7a24d3f22e7048dec3ef.png)
 - **Workload Name**: enter the name of the workload. In this example, the name is `wordpress`.
 - **Description**: specify the related information of the workload.
 - **Tag**: specify the key-value pair. In this example, the default value is k8s-app = **wordpress**.
 - **Namespace**: select a namespace as required.
 - **Type**: select a type as required.
 - **Volume**: set the workload volume to mount. For more information, see [Volume Management](https://intl.cloud.tencent.com/document/product/457/30678).
4. Configure **Containers in Pod** as instructed. See the figure below.

The following describes the main parameters. You can keep the default values of other parameters.
 - **Name**: enter the custom container name. In this example, the name is `test`.
 - **Image**: enter `wordpress`.
 - **Image Tag**: enter `latest`.
 - **Image Pull Policy**: select one of the three available policies as required. In this example, the default policy is applied.
If you do not set any image pull policy and leave **Image Tag** empty or set it to `latest`, the `Always` policy is used. Otherwise, the `IfNotPresent` policy is used.
    - **Always**: always fetch the image remotely.
    - **IfNotPresent**: use a local image by default. Fetch the image remotely if no local image is available.
    - **Never**: only use a local image. An exception occurs if no local image is available.
6. Set the number of pods for the service as instructed. See the figure below.
![](https://main.qcloudimg.com/raw/649c9a62a29a77d09451e6d0dc487d58.png)
 - **Manual adjustment**: specify the number of pods. In this example, it is set to 1. You can click "+" or "-" to change the number of pods.
 - **Auto adjustment**: automatically adjust the number of pods if any of the set conditions is met. For more information, see [Automatic Scaling for Basic Operations](https://intl.cloud.tencent.com/document/product/457/32424).
8. Configure **Access Settings (Service)** for the workload as instructed. See the figure below.
![](https://main.qcloudimg.com/raw/be7ada723be03bb14f9d528aa15a0f58.png)
 - **Service**: select "Enable".
 - **Service Access**: select "Public Network Access".
 - **Load Balancer**: create or select a load balancer as required.
 - **Port Mapping**: select the TCP protocol, and set both the container port and service port to port 80.
>The node network, container network, and ports 30000 to 32768 in the security group of the cluster which the service belongs to must be opened to Internet. Otherwise, TKE may be unavailable. For more information, see [TKE Security Group Settings](https://intl.cloud.tencent.com/document/product/457/9084).
9. Click **Create Workload** to create the WordPress service.


### Accessing the WordPress service

You can access the WordPress service with either methods.

#### Access with CLB IP address
1. In the left sidebar, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** to go to the "Cluster Management" page.
2. Click the ID of the cluster that the WordPress service belongs to and choose **Service** > **Service**.
3. On the service management page, copy the CLB IP address of the WordPress service, as shown in the following figure.
![](https://main.qcloudimg.com/raw/8a8ea1dc181ab31660313ed0883bc980.png)
4. Paste the CLB IP address in the address bar of the browser and press Enter to access the service.

#### Access with service name
Other services or containers in the cluster can use the service name to directly access the WordPress service.

### Verifying the WordPress service
The WordPress service is created successfully if you are directed to the WordPress server configuration page when you try to access the service, as shown in the following figure.
![](https://main.qcloudimg.com/raw/4ccbffc42a7f9381e2595175ea32be65.png)

### More WordPress settings
If the container cannot be created, you may search [Event FAQs](https://intl.cloud.tencent.com/document/product/457/8187) for a solution.

