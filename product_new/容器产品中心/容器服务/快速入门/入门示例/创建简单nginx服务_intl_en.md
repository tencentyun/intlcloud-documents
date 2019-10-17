## Operation Scenario
This document shows how to quickly create an `nginx` service in a container cluster.

##  Prerequisites
>- Complete [Tencent Cloud account registration](https://intl.cloud.tencent.com/register).
>- Create a cluster. For details on how to create a cluster, see [Creating a cluster](https://intl.cloud.tencent.com/document/product/457/30637).

## Steps

### Creating Nginx Service

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** to go to the **Cluster Management** page.
3. Click on the cluster ID for which the service is to be created, and go to the Deployment page. Select **Create**. See the figure below:
![](https://main.qcloudimg.com/raw/036baf23123e7291d5fcfb82a2572e53.png)
4. Set up the workload basic information on the **Create Workload** page according to the following instructions. See the figure below:
 - **Workload Name**: Enter the name of the workload to be created. Here, `nginx` is used as an example.
 - **Description**: Fill in the related workload information.
 - **Tag**: Key = value. This is a key value pair, and the tag in this example is set by default as k8s-app = **nginx**.
 - **Namespace**: To be selected based on your requirements.
 - **Type**: To be selected based on your requirements.
 - **Volume**: Set up the workload volumes mounted based on your requirements. For more details, see [Volume Management](https://intl.cloud.tencent.com/document/product/457/30678).
![](https://main.qcloudimg.com/raw/a1391e5768e6fd5cfe0e6b3c65417a50.png)
5. Set up **Containers in pod**. Enter the name of the container in the pod. In this example, `test` is used.
6. Click **Select Image** (keep other settings as default). See the figure below:
 ![](https://main.qcloudimg.com/raw/2ec2c7c803ee61a2d218f17df785636e.png)
Select **DockerHub Image** > **nginx** in the pop-up box and click **OK**. See the figure below:
![](https://main.qcloudimg.com/raw/25bcb76882dbfb54ff9fe2390fc5a06b.png)
6. Set up the service’s pod number according to the following instructions. See the figure below:
 - **Manual adjustment**: Set the number of pods. The number of pods in this example is set as 1. You can click **+** or **-** to change the number of pods.
 - **Auto adjustment**: Automatically adjust the number of pods if any of the setting conditions are met. For more details, see [Service auto scaling](https://intl.cloud.tencent.com/document/product/457/14209).
 ![](https://main.qcloudimg.com/raw/51c4971952bbd697ca458a415fd1ce21.png)
7. Set up the workload access according to the following instructions. See the figure below:   
 - **Service**: Check **Enable**.
 - **Service Access**: Select **Via Internet**.
 - **Load balancer**: Select according to your requirements.
 - **Port mapping**: Select TCP protocol, and set both the container port and service port to 80.
 ![](https://main.qcloudimg.com/raw/aedd2d73ab7e5f79218d8194c9b1c249.png)
 > The security group of the service’s cluster must open the node network and container network to the Internet. It is also required to open ports 30000 to 32768 to the Internet. Otherwise, the problem of TKE being unusable could occur. For more details, see [TKE Security Group Settings](https://intl.cloud.tencent.com/document/product/457/9084).
8. Click **Create workload** to complete the creation of the nginx service.


### Accessing Nginx Service

Ngnix service can be accessed using the following two methods.

#### Accessing Nginx Service Using **Cloud Load Balancer IP**

1. In the left sidebar, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** to go to the **Cluster Management** page.
2. Click on the Nginx service’s cluster ID and select **Service** > **Service**.
3. Copy the Nginx service’s cloud load balancer IP from the service management page. See the figure below:
![](https://main.qcloudimg.com/raw/bab54241805b352ae007ece3d130bb4a.png)
4. Enter the cloud load balancer IP in the browser’s address bar and press **Enter** to access the service.

#### Accessing Nginx Service Using Service Name

Other services or containers in the cluster can be accessed directly by the service name.

### Verifying Nginx Service
When the service is successfully created, you can directly enter the nginx server configuration page when accessing the service. See the figure below:
![](https://main.qcloudimg.com/raw/37246241fe0abd1d3796c080b1661217.png)

### More Nginx Settings
- If creation of the container failed, you can read the [Event FAQs](https://intl.cloud.tencent.com/document/product/457/8187).

