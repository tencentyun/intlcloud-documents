## Scenario
This document describes how to quickly create an Nginx service in a container cluster.

## Prerequisites
- Complete [Tencent Cloud account registration](https://intl.cloud.tencent.com/register).
- Create a cluster. For more information, see [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637).

## Directions

### Creating Nginx service
1. Log in to the TKE console and select **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. Click the ID of the cluster for which the service is to be created on the Cluster Management page to go to the workload Deployment page of the cluster, and click **Create**. See the figure below.
![](https://main.qcloudimg.com/raw/036baf23123e7291d5fcfb82a2572e53.png)
3. On the Create Workload page, specify the basic information of the workload as instructed. See the figure below.
![](https://main.qcloudimg.com/raw/a1391e5768e6fd5cfe0e6b3c65417a50.png)
  - **Workload Name**: enter the name of the workload to be created. Here, `nginx` is used as an example.
  - **Description**: fill in the related workload information.
  - **Tag**: this is a key value pair, and the tag in this example is set to k8s-app = **nginx** by default.
  - **Namespace**: select a namespace based on your requirements.
  - **Type**: select a type based on your requirements.
  - **Volume**: set up the workload volumes mounted based on your requirements. For more information, see [Volume Management](https://intl.cloud.tencent.com/document/product/457/30678).
4. Configure "Containers in the pod" as instructed. See the figure below.
![](https://main.qcloudimg.com/raw/2ec2c7c803ee61a2d218f17df785636e.png)
Main parameters include:
  - **Name**: enter the name of the container in the pod. Here, “test” is used as an example.
  - **Image**: click **Select an image**, select **DockerHub Image** -> **nginx** in the pop-up window, and then click **OK**.
  - **Image Tag**: use the default value `latest`.
  - **Image Pull Policy**: select one of the three available policies as needed. In this example, the default policy is applied.
    If you do not set any image pull policy and **Image Tag** is left empty or `latest`, the `Always` policy is used. Otherwise, the `IfNotPresent` policy is used.
    - **Always**: the image is always pulled remotely.
    - **IfNotPresent**: a local image is used by default. If no local image is available, the image is pulled remotely.
    - **Never**: a local image is used. If no local image is available, an exception is reported.
5. In the "Number of Pods" section, set the number of pods for the service as instructed. See the figure below.
![](https://main.qcloudimg.com/raw/51c4971952bbd697ca458a415fd1ce21.png)
 - **Manual adjustment**: set the number of pods. The number of pods in this example is set to 1. You can click "+" or "-" to change the number of pods.
 - **Auto Adjustment**: the number of pods is automatically adjusted if any of the setting conditions are met. For more information, see [Service Auto Scaling](https://intl.cloud.tencent.com/document/product/457/32424).
6. Set up the workload access according to the following instructions. See the figure below:   
![](https://main.qcloudimg.com/raw/aedd2d73ab7e5f79218d8194c9b1c249.png)
 - **Service**: check **Enable**.
 - **Service Access**: select **Via Internet**.
 - **Load Balancer**: select according to your requirements.
 - **Port Mapping**: select TCP protocol, and set both the container port and service port to 80.
 >!The security group of the service’s cluster must open the node network and container network to the Internet. It is also required to open ports 30000 to 32768 to the Internet. Otherwise, the problem of TKE being unusable could occur. For more information, see [TKE Security Group Settings](https://intl.cloud.tencent.com/document/product/457/9084).
7. Click **Create workload** to complete the creation of the Nginx service.


### Accessing Nginx service

Ngnix service can be accessed using the following two methods.

#### Accessing Nginx service using **Cloud Load Balancer IP**

1. In the left sidebar, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** to go to the **Cluster Management** page.
2. Click on the Nginx service’s cluster ID and select **Service** -> **Service**.
3. Copy the Nginx service’s cloud load balancer IP from the service management page. See the figure below:
![](https://main.qcloudimg.com/raw/bab54241805b352ae007ece3d130bb4a.png)
4. Enter the cloud load balancer IP in the browser’s address bar and press **Enter** to access the service.

#### Accessing Nginx service using service name

Other services or containers in the cluster can be accessed directly by the service name.

### Verifying Nginx service
When the service is successfully created, you directly enter the Nginx server welcome page when accessing the service. See the figure below:
![](https://main.qcloudimg.com/raw/156e6d3b804e6b214ef7600fee4fa9c1.png)

### More Nginx settings
If creation of the container failed, you can read the [Event FAQs](https://intl.cloud.tencent.com/document/product/457/8187).
