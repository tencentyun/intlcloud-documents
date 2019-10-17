## Operation Scenario
WordPress is a blogging platform developed with PHP. You can use it as a content management system, or use it to create websites on services that support PHP and MySQL databases.

This document describes how to use the `tutum/wordpress` image to create a publicly accessible WordPress website.


##  Prerequisites
>!
>- The `tutm/wordpress` image includes all operating environments for WordPress, allowing you to pull and create the service directly.
>- Creating WordPress with single pod is for testing purposes only, and persistent data storage cannot be ensured. It is recommended that you use a self-built MySQL or TencentDB to store your data. For more information, please see [WordPress Using TencentDB](/doc/product/457/7447). 
>
- Complete [Tencent Cloud account registration](https://intl.cloud.tencent.com/register).
- Create a cluster. For details on how to create a cluster, see [Creating a cluster](https://intl.cloud.tencent.com/document/product/457/30637).

## Steps
### Creating WordPress Service
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** to go to the **Cluster Management** page.
3. Click on the cluster ID for which the service is to be created, and go to the Deployment details page. Select **Create**. See the figure below:
![](https://main.qcloudimg.com/raw/236918b1a3c7c502fcd110da0971e74b.png)
4. Set up the workload basic information on the **Create Workload** page according to the following instructions. See the figure below:
 - **Workload Name**: The name of the workload to be created. Here, `wordpress` is used as an example.
 - **Description**: Fill in the related workload information.
 - **Tag**: Key = value. This is a key value pair, and the tag in this example is set by default as k8s-app = **wordpress**.
 - **Namespace**: To be selected based on your requirements.
 - **Type**: To be selected based on your requirements.
 - **Volume**: Set up the workload volumes mounted based on your requirements. For more details, see [Volume Management](https://intl.cloud.tencent.com/document/product/457/30678).
 ![](https://main.qcloudimg.com/raw/d2b3c89b8770a0bfd06cc39f20ead90d.png)
5. Set up **Containers in Pod** according to the following instructions. See the figure below:
 - **Name**: Enter the custom container name. Here, `test` is used as an example.
 - **Image**: Enter `tutum/wordpress`.
 - **Image Tag**: Enter `latest`.
 >! Keep default settings for other options.
 >
![](https://main.qcloudimg.com/raw/cf064d1b2bd1a61781a75800e3fbbae0.png)
7. Set up the service’s pod number according to the following instructions. See the figure below:
 - **Manual adjustment**: Set the number of pods. The number of pods in this example is set as 1. You can click **+** or **-** to change the number of pods.
 - **Auto adjustment**: Automatically adjust the number of pods if any of the setting conditions are met. For more details, see [Service auto scaling](https://intl.cloud.tencent.com/document/product/457/14209).
 ![](https://main.qcloudimg.com/raw/10129daba44bfa7d7573c968cab8c4a4.png)
8. Configure the workload **access settings (service)** according to the following instructions. See the figure below:
 - **Service**: Check **Enable**.
 - **Service Access**: Select **Via Internet**.
 - **Load balancer**: Select according to your requirements.
 - **Port mapping**: Select TCP protocol, and set both the container port and service port to 80.
 ![](https://main.qcloudimg.com/raw/3f722201e228c2bebc63cad0ea3d76c7.png)
>! The security group of the service’s cluster must open the node network and container network to the Internet. It is also required to open ports 30000 to 32768 to the Internet. Otherwise, the problem of TKE being unusable could occur. For more details, see [TKE Security Group Settings](https://intl.cloud.tencent.com/document/product/457/9084).
9. Click **Create workload** to complete the creation of the wordpress service.


### Accessing WordPress Service

WordPress service can be accessed using the following two methods.

#### Accessing WordPress Service Through Cloud Load Balancer IP
1. In the left sidebar, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** to go to the **Cluster Management** page.
2. Click on the WordPress service’s cluster ID and select **Service** > **Service**.
3. Enter the service management page and copy the WordPress service’s load balancer IP. See the figure below:
![](https://main.qcloudimg.com/raw/204793d204a733e7c4c8b2cea5e96dce.png)
4. Enter the load balancer IP in the browser’s address bar and press **Enter** to access the service.

#### Accessing Service Using Service Name
Other services or containers in the cluster can be accessed directly by the service name.

### Verifying WordPress Service
When the service is successfully created, you can directly enter the WordPress server configuration page when accessing the service. See the figure below:
![](https://main.qcloudimg.com/raw/4ccbffc42a7f9381e2595175ea32be65.png)

### More WordPress Settings
If creation of the container failed, you can read the [Event FAQs](https://intl.cloud.tencent.com/document/product/457/8187).

