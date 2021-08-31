## Overview
To learn about how to quickly create WordPress services, you can refer to [Creating a WordPress Service](https://intl.cloud.tencent.com/document/product/457/7205). WordPress services created in this way have the following features:
- Data is written to the MySQL databases running on the same container.
- Services can be quickly launched.
- Databases and storage-type files will be lost if the container is stopped for certain reasons.

Using MySQL databases can ensure permanent storage of data. The databases will continue to run when the pod/container restarts. This document explains how to configure the MySQL database using [TencentDB](https://intl.cloud.tencent.com/product/cdb) and how to create a WordPress service that uses TencentDB.

## Prerequisites
- You have registered a [Tencent Cloud account](https://intl.cloud.tencent.com/register).
- You have created a cluster. For more information on how to create a cluster, see [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637).
>? The database used in the document is [TencentDB for MySQL instance](https://intl.cloud.tencent.com/document/product/236/5147).


### Directions

### Creating a WordPress service
#### Creating a TencentDB instance
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), and click **Create** in the database instance list, as shown in the figure below.
![](https://main.qcloudimg.com/raw/78b43441e5d296e83e2db9246aaddff7.png)
2. Select the configuration to purchase. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/236/5147).
>! The database must be in the same region as that of the cluster. Otherwise, you will unable to connect to the database.

3. After creating the database, you can view it in the [MySQL instance list](https://console.cloud.tencent.com/cdb).
4. Initialize the database. For more information, see [Initializing MySQL Instance](https://intl.cloud.tencent.com/document/product/236/3128).

#### Creating a WordPress service that uses Tencent DB
1. Log in to the TKE console and select **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. On the **Cluster Management** page, click the ID of the cluster for which the service is to create to go to the **Deployment** page of the cluster and click **Create**, as shown in the figure below.
![](https://main.qcloudimg.com/raw/239bfe0c3488c19139c5359b27d24044.png)
3. On the **Create Workload** page, specify basic information of the workload as instructed in the figure below.
![](https://main.qcloudimg.com/raw/3ff74d307b48b793ac121345e7f19154.png)
 - **Workload Name**: the name of the workload to create. Here, `wordpress` is used as an example.
 - **Description**: specify related workload information.
 - **Tag**: specify the key-value pair. The default value is k8s-app = **wordpress** here.
 - **Namespace**: select a namespace based on your requirements.
 - **Type**: select a type based on your requirements.
 - **Volume**: set the volume to which the workload is mounted based on your requirements. For more information, see [Volume Management](https://intl.cloud.tencent.com/document/product/457/30678).
4. Configure **Containers in the pod** as instructed in the figure below.
![](https://main.qcloudimg.com/raw/7e2fccaf2c0168743dc03480cab2a6f3.png)
The main parameters are as follows. Retain the default settings for other parameters.
  - **Name**: enter the custom container name. In this example, `test` is used.
  - **Image**: enter `wordpress`.
  - **Image Tag**: enter `latest`.
  - **Image Pull Policy**: three policies are available. Select a policy as required. In this example, the default policy is used.
If you do not specify an image pull policy, the "Always" policy is used when the image tag is empty or "latest". Otherwise, the IfNotPresent policy is used.
      - **Always**: always pull the image from the remote end.
      - **IfNotPresent**: a local image is used by default. If no local image is available, the image is pulled remotely.
      - **Never**: only use a local image. If no local image is available, an exception occurs.
 - **Environment variable**: enter the following configuration information in sequence.
WORDPRESS_DB_HOST = Private IP address of TencentDB for MySQL
WORDPRESS_DB_PASSWORD = Password entered during initialization
5. Set the number of pods for the service as instructed in the figure below.
![](https://main.qcloudimg.com/raw/06e71d9208795f57159bdaba8eae45b4.png)
 - **Manual adjustment**: set the number of pods. The number of pods in this example is set to 1. You can click "+" or "-" to change the number of pods.
 - **Auto Adjustment**: the number of pods is automatically adjusted if any of the setting conditions are met. For more information, see [Automatic Scaling Basic Operations](https://intl.cloud.tencent.com/document/product/457/32424).
6. Configure **Access Settings (Service)** for the workload as instructed in the figure below.
![](https://main.qcloudimg.com/raw/9d0d2970a6df63f6eb83bbc73deb7178.png)
 - **Service**: select **Enable**.
 - **Service Access**: select **Via Internet**.
 - **Load Balancer**: create or select a load balancer as needed.
  - **Port Mapping**: select TCP, and set both the container port and service port to 80.
 >! The security group of the cluster to which the service belongs must open the node network and container network to the Internet. It is also required to open ports 30000 to 32768 to the Internet. Otherwise, TKE may be unavailable. For more information, see [TKE Security Group Settings](https://intl.cloud.tencent.com/document/product/457/9084).

7. Click **Create workload**.


### Accessing the WordPress service
You can access the WordPress service using either of the following two methods.

#### Accessing the WordPress service using the CLB IP address
1. In the left sidebar, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** to go to the "Cluster Management" page.
2. Click the ID of the cluster to which the WordPress service belongs and choose **Service** > **Service**.
3. On the service management page, copy the CLB IP address of the WordPress service, as shown in the figure below.
![](https://main.qcloudimg.com/raw/f5f9964eacb4752e528ce32d467662a8.png)
4. Paste the CLB IP address in the browser address box and press **Enter** to access the service.

#### Accessing the WordPress service using the service name
Other services or containers in the cluster can access the WordPress service using the service name.

### Verifying the WordPress service
After the service is created, the WordPress server configuration page is displayed when you access the service, as shown in the figure below.
![](https://main.qcloudimg.com/raw/903f45d57c58541433b555d487bd2980.png)

### More WordPress settings
If the container fails to be created, you can view [Event FAQs](https://intl.cloud.tencent.com/document/product/457/8187) to locate the causes.
