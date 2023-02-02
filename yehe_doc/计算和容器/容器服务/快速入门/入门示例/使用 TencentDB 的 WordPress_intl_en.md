## Overview
To learn about how to quickly create WordPress services, you can refer to [Creating a WordPress Service](https://www.tencentcloud.com/document/product/457/7205). WordPress services created in this way have the following features:
- Data is written to the MySQL databases running on the same container.
- Services can be quickly launched.
- Databases and storage-type files will be lost if the container is stopped for certain reasons.

Using MySQL databases can ensure permanent storage of data. The databases will continue to run when the pod/container restarts. This document explains how to configure the MySQL database using TencentDB and how to create a WordPress service that uses TencentDB.

## Prerequisites
- You have registered a [Tencent Cloud account](https://intl.cloud.tencent.com/account/register).
- You have created a standard TKE cluster. For more information, see [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637).
>? The database used in the document is [TencentDB for MySQL instance](https://intl.cloud.tencent.com/document/product/236/5147).
>

## Directions

### Creating a WordPress service
#### Creating a TencentDB instance
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), and click **Create** in the database instance list, as shown in the figure below.
![](https://main.qcloudimg.com/raw/78b43441e5d296e83e2db9246aaddff7.png)
2. Select the configuration to purchase. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/236/5147).
>!The database must be in the same region as that of the cluster. Otherwise, you will be unable to connect to the database.
>
3. After creating the database, you can view it in the [MySQL instance list](https://console.cloud.tencent.com/cdb).
4. Initialize the database. For details, see [Initializing MySQL database](https://intl.cloud.tencent.com/document/product/236/37785).

#### Creating a WordPress service that uses Tencent DB
1. Log in to the TKE console and select **[Cluster](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. On the **Cluster Management** page, click the ID of the target cluster to go to the cluster details page.
3. On the **Workload** > **Deployment** page, click **Create**. For more information, see [Creating a Deployment](https://intl.cloud.tencent.com/document/product/457/30662).
4. On the **Create Deployment** page, specify basic information of the workload as instructed in the figure below.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/9uSg439_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221223182910.png)
 - **Workload Name**: enter the name of the workload to create. In this example, `wordpress` is used.
 - **Description**: specify related workload information.
 - **Labels**: the default value is `k8s-app = wordpress` in this example.
 - **Namespace**: select a namespace based on your requirements.
 - **Volume**: set the volume to which the workload is mounted based on your requirements. For more information, see [Volume Management](https://intl.cloud.tencent.com/document/product/457/30678).
5. Configure "Containers in the Pod" as instructed. See the figure below:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/npAd465_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221223183029.png)
The main parameters are described as follows:
  - **Name**: enter the name of the container in the pod. Here, “test” is used as an example.
  - **Image**: click **Select Image**, select **DockerHub Image** > **wordpress** in the pop-up window, and click **OK**.
  - **Image Tag**: use the default value `latest`.
  - **Image Pull Policy**: choose from **Always**, **IfNotPresent** and **Never** as needed. In this document, we use the **default policy** as an example.
  - **Environment variable**: enter the following configuration information in sequence.
WORDPRESS_DB_HOST = Private IP address of TencentDB for MySQL
WORDPRESS_DB_PASSWORD = Password entered during initialization
6. In **Number of Instances**, set the number of instances for the service according to the following information. In this document, we choose **Manual Adjustment** and set the instance number to one. See the figure below:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/xJde374_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221223183140.png)
7. Specify the access mode of the workload, as shown in the following figure.   
![](https://staticintl.cloudcachetci.com/yehe/backend-news/QStR744_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221223183336.png)
 - **Service**: select **Enable**.
 - **Service Access**: select **LoadBalancer (public network)**.
 - **Load Balancer**: select according to your requirements.
 - **Port Mapping**: select TCP, and set both the container port and service port to 80.
>! The security group of the service’s cluster must open the node network and container network to the Internet. It is also required to open ports 30000 to 32768 to the Internet. Otherwise, the problem of TKE being unusable could occur. For more details, see [TKE Security Group Settings](https://intl.cloud.tencent.com/document/product/457/9084).
8. Click **Create Deployment**.



### Accessing the WordPress service
You can access the WordPress service using either of the following two methods.

#### Accessing the WordPress service using the CLB IP address
1. In the left sidebar, click **[Cluster](https://console.cloud.tencent.com/tke2/cluster)** to go to the **Cluster Management** page.
2. Click the ID of the cluster to which the WordPress service belongs and choose **Services and Routes** > **Service**.
3. On the service list page, copy the CLB IP address of the WordPress service, as shown in the figure below.
![](https://main.qcloudimg.com/raw/f5f9964eacb4752e528ce32d467662a8.png)
4. Paste the CLB IP address in the browser and press **Enter** to access the service.

#### Accessing the WordPress service using the service name
Other services or containers in the cluster can access the WordPress service using the service name.

### Verifying the WordPress service
After the service is created, the WordPress server configuration page is displayed when you access the service, as shown in the figure below.
![](https://main.qcloudimg.com/raw/903f45d57c58541433b555d487bd2980.png)

### More WordPress settings
If the container fails to be created, you can view [Event FAQs](https://intl.cloud.tencent.com/document/product/457/8187) to locate the causes.
