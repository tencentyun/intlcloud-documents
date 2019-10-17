## Operation Scenario
The examples in [WordPress with Single Pod](/doc/product/457/7205) show how to quickly create WordPress services. The WordPress services created in this way have the following features: 

- The data is written to the mySQL database running on the same container. 
- Services can be quickly launched.
- Databases and storage-type files will be lost if the container is stopped for certain reason.

Using MySQL databases can ensure the permanent storage of data. The databases will continue to run when the pod/container restarts. This document explains how to configure MySQL database using [TencentDB](https://intl.cloud.tencent.com/product/cdb) and how to create a WordPress service that using TencentDB.

##  Prerequisites
- Complete [Tencent Cloud account registration](https://intl.cloud.tencent.com/register).
- Create a cluster. For details on how to create a cluster, see [Creating a cluster](https://intl.cloud.tencent.com/document/product/457/30637).
>?The database used in the document is a [MySQL instance](https://intl.cloud.tencent.com/document/product/236/5147).
>

## Steps

### Creating WordPress Service
#### Creating TencentDB
1. Log in to the [TencentDB MySQL console](https://console.cloud.tencent.com/cdb), and click **Create** in the database instance list. See the figure below:
![](https://main.qcloudimg.com/raw/19726071d60c533349252a5c46caca8b.png)
2. Select the configuration to purchase. For details, see [TencentDB MySQL](https://intl.cloud.tencent.com/document/product/236/5147).
>! The region of the database must be the same as that of the cluster, otherwise you will not be able to connect to the database.
>
3. After successfully creating the database, you can view it in [MySQL instance list](https://console.cloud.tencent.com/cdb).
4. Initialize the database. For details, see [Initializing MySQL database](https://intl.cloud.tencent.com/document/product/236/3128).

#### Creating a WordPress Service that Using Tencent DB
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** to go to the Deployment page and select **Create**. See the figure below:
![](https://main.qcloudimg.com/raw/7da31921c38569dc3a3bf367019d5129.png)
3. Set up the workload basic information on the **Create Workload** page according to the following instructions. See the figure below:
 - **Workload Name**: The name of the workload to be created. Here, `wordpress` is used as an example.
 - **Description**: Fill in the related workload information.
 - **Tag**: Key = value. This is a key value pair, and the tag in this example is set by default as k8s-app = **wordpress**.
 - **Namespace**: To be selected based on your requirements.
 - **Type**: To be selected based on your requirements.
 - **Volume**: Set up the workload volumes mounted based on your requirements. For more details, see [Volume Management](https://intl.cloud.tencent.com/document/product/457/30678).
 ![](https://main.qcloudimg.com/raw/73a22932a9354f294697de7c87ff098c.png)
5. Set up **Containers in Pod** according to the following instructions. See the figure below:
  - **Name**: Enter the custom container name. Here, `test` is used as an example.
  - **Image**: Enter `wordpress`.
  - **Image Tag**: Enter `latest`.
 - **Environment variable**: Enter the following configuration information in sequence.
WORDPRESS_DB_HOST = Private IP for cloud database MySQL
WORDPRESS_DB_PASSWORD = Password entered during initialization
>! Keep default settings for other options.
>
![](https://main.qcloudimg.com/raw/f90c2362c30130625460d927570f1bf3.png)
5. Set up the service’s pod number according to the following instructions. See the figure below:
 - **Manual adjustment**: Set the number of pods. The number of pods in this example is set as 1. You can click **+** or **-** to change the number of pods.
 - **Auto adjustment**: Automatically adjust the number of pods if any of the setting conditions are met. For more details, see [Service auto scaling](https://intl.cloud.tencent.com/document/product/457/14209).
 ![](https://main.qcloudimg.com/raw/10129daba44bfa7d7573c968cab8c4a4.png)
6. Configure the workload **Access settings (service)** according to the following instructions. See the figure below:
 - **Service**: Check **Enable**.
 - **Service Access**: Select **Via Internet**.
 - **Load balancer**: Select according to your requirements.
  - **Port mapping**: Select TCP protocol, and set both the container port and service port to 80.
 ![](https://main.qcloudimg.com/raw/3f722201e228c2bebc63cad0ea3d76c7.png)
 >! The security group of the service’s cluster must open the node network and container network to the Internet. It is also required to open ports 30000 to 32768 to the Internet. Otherwise TKE service may be unavailable. For more details, see [TKE Security Group Settings](https://intl.cloud.tencent.com/document/product/457/9084).
>
6. Click **Create workload** to complete the creation of the `WordPress` service.


### Accessing WordPress Service
WordPress service can be accessed using the following two methods.

#### Accessing WordPress Service Through Cloud Load Balancer IP
1. In the left sidebar, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** to go to the **Cluster Management** page.
2. Click on the WordPress service’s cluster ID and select **Service** > **Service**.
3. Enter the service management page and copy the WordPress service’s cloud load balancer IP. See the figure below:
![](https://main.qcloudimg.com/raw/204793d204a733e7c4c8b2cea5e96dce.png)
4. Enter the cloud load balancer IP in the browser’s address bar and press **Enter** to be able to access the service.

#### Accessing Service Using Service Name
Other services or containers in the cluster can be accessed directly by the service name.

### Verifying WordPress Service
When the service is successfully created, you can directly enter the WordPress server configuration page when accessing the service. See the figure below:
![](https://main.qcloudimg.com/raw/903f45d57c58541433b555d487bd2980.png)

### More WordPress Settings
If creation of the container failed, you can read the [Event FAQs](https://intl.cloud.tencent.com/document/product/457/8187).
