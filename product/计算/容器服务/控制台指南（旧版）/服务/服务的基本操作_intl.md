## Creating Service
1. Log in to the **Tencent Cloud TKE console**.
2. Click **Service** in the left navigation bar, and click **New** in the service list page.
![](https://main.qcloudimg.com/raw/8478242ffb1a155095abb25bcda136b2.png)
3. Configure basic service information.
 - **Service Name**: The name of the service to be created, which has a length limited to 63 characters comprised of lowercase letters, numbers and "-". It starts with a lowercase letter and ends with a lowercase letter or a number.
 - **Region**: Select the region where the service is deployed.
 - **Cluster**: Select a cluster to run your service. You need to select a running cluster with available CVMs in it.
 - **Service description**: Information of created service. This information is displayed in **Service Information** page.
![](https://main.qcloudimg.com/raw/6a0fbf1c2214fa9a5e7dd0a5c7a4126b.png)
4. Configure volume.
Click **Add Volume** when you specify a specific path to which a container is mounted.
>**Note:**
>If no source path is specified, a temporary path is assigned by default.

 - **Type**: Four types of volumes are supported: local disk, cloud disk, NFS disk, and configuration file. 
 - **Name**: Volume name.
 - **Path**: Specify the path to which a container is mounted.
 ![](https://main.qcloudimg.com/raw/e2a1df83e3561bbe3797b29a00b0c1a3.png)
5. Configure a container.
 - **Name**: The name of the container to be created, with a length limited to 63 characters.
 - **Image**: Click **Select Image** to create a service under My Images, My Favorites, TencentHub Image, DockerHub Image or other images.
 - **Tag**: The default image tag for TKE. If you need to use a different image tag, click tag display window to select one.
![](https://main.qcloudimg.com/raw/c9fd82080b33af2c31195578c270d832.png)
6. Other settings
 -  **Number of pods**: A pod consists of one or more relevant containers. You can specify the number of pods by clicking + or -.
 -  **Service access method**: The method for accessing a service determines the network attribute of this service. Different access methods offer different network capabilities. For more information about the four access methods, please see [Configuration of Service Access Methods](https://intl.cloud.tencent.com/document/product/457/9098).
![](https://main.qcloudimg.com/raw/37f7769806da7e4b8733647cbd439505.png)
7. Click **Create Service** to complete the creation process.

## Updating the Number of Pods
1. Click **Services** in the left navigation bar of TKE console to enter the service list, and click **Update Number of Pods**.
![](https://main.qcloudimg.com/raw/8bd546e918cae8b9ab56b8a3888d4b22.png)
2. You can specify the number of pods by clicking + or -. Click **OK** after the configuration is completed.
![](https://main.qcloudimg.com/raw/2ac540ab8deb40f3d8c7884abff05577.png)

## Updating Service
1. Click **Services** in the left navigation bar of TKE console to enter the service list, and click **Update Service**.
![](https://main.qcloudimg.com/raw/0718ff67e32f5096c345ceab944622a4.png)
2. Click **Start Update**.
Two updating methods are available.
 -  **Rolling update**: Update pods one by one, which allows you to update the service without interrupting the business.
 -  **Quick update**: Directly close all current pods, and launch the same number of new pods.

## Redeployment
Redeployment is to redeploy the containers under a service and pull a new image.
1. Click **Services** in the left navigation bar of TKE console to enter the service list, and click **More** -> **Redeploy**.
![](https://main.qcloudimg.com/raw/5d0847e49c8a2ff37f5816f494e4b95f.png)
2. Click **OK**.
![](https://main.qcloudimg.com/raw/e179c624bd597adb4a4c438415569466.png)

## Deleting Service
1. Click **Services** in the left navigation bar of TKE console to enter the service list, and click **More** -> **Delete**.
![](https://main.qcloudimg.com/raw/30f8fe02b60ab3b9cf374e786ba6f403.png)
2. Click **OK**.
![](https://main.qcloudimg.com/raw/df2ce4b0830b3c209a462f6a1018b0b6.png)
>**Note**:
>Deleting the service will delete all the pods and public network load balancers under the service. Back up your data in advance.




