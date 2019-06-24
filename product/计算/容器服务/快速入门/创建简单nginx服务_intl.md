This document shows how to quickly create an "nginx" service in a container cluster.

## Prerequisites
To create an "nginx" service, you must create a cluster first. For more information on how to create a cluster, please see [Create Cluster](https://cloud.tencent.com/document/product/457/9091).

## Procedure
1. Log in to [TKE Console](https://console.cloud.tencent.com/ccs).
2. Click **Service** in the left navigation bar, and click **+ New** in the service list page.
![](https://main.qcloudimg.com/raw/4502f16f8f98ec47f41fac37c314b844.png)
3. Enter basic service information.
 - **Service name**: The name of the service to be created, which is comprised of lowercase letters, numbers and "-". It starts with a lowercase letter and ends with a lowercase letter or a number. In this example, the name is "nginx".
 - **Region**: Select the closest region based on your location.
 - **Cluster**: Select an appropriate cluster and Namespace.
 - **Service description**: Service information. This information is displayed on the **Service Information** page.
 ![](https://main.qcloudimg.com/raw/8542522ecba3ac1127b1008a33da87d1.png)
4. Select an image. Enter the name of the running container, which is "nginx" here. Click **Select Image**.
![](https://main.qcloudimg.com/raw/b34ca7f7bce7a4958507ee7cf4b54c9c.png)
Click **DockerHub Image**, and select "**nginx**". Click **OK**.
![](https://main.qcloudimg.com/raw/8c6653ed8d909a8791a0f696a6492e69.png)
Version (Tag): latest. By default, the latest version is used for TKE.
![](https://main.qcloudimg.com/raw/4361066a76a77d2d4edf1ae6ff3928ee.png)
5. Configure port mapping. Set both container port and service port to 80.
![](https://main.qcloudimg.com/raw/54c8d5786d0959091878089b9a42d171.png)
6. Click **Create Service** to complete the creation of "nginx" service.
>**Note**: Keep default settings for other options.

## Accessing "nginx" Service
1. Click **Service Information** on the service page to check the load balancer ID and load balancer IP. 
![](https://main.qcloudimg.com/raw/8372310f0fb138c71eb4548b5a4af209.png)
![](https://main.qcloudimg.com/raw/3480dd888a89edc654796d44affccabe.png)
2. Access "nginx" service by the following ways.
 - Use load balancer IP.
 - Use **domain name**.
 Copy the domain name by clicking **Load Balance** -> **TCP/UDP** in the left navigation bar of the container console to access the service.
 ![](https://main.qcloudimg.com/raw/b7b26e65be95126f827a129f0f67b52a.png)
 - Other services or containers in the cluster can be accessed directly by the service name.
3. Go to "nginx" server's default welcome page.
![](//mc.qcloudimg.com/static/img/a3cbbc5c902bd162210a4615c0955f19/image.png)

