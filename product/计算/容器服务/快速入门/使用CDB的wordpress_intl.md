In [WordPress with Single Pod](https://intl.cloud.tencent.com/document/product/457/7205), we described how to quickly create a WordPress service. The data of WordPress with single pod is written to the MySQL database running in the same container, which can ensure quick start but may incur an issue, that is, if the container is stopped for some reason, the database and storage-related files will be lost.

This document explains how to configure the MySQL database to make sure that it continue running when the pod/container restarts. Persistent data storage can be achieved by using [CDB](https://console.cloud.tencent.com/cdb).

## Prerequisites
You need to create a cluster first. For more information on how to create a cluster, please see [Basic Operations of Cluster](https://intl.cloud.tencent.com/document/product/457/9091).

## Procedure
### Step 1: Create a CDB
1. Log in to the [VPC Console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click the ID/name (e.g. vpc-xxxxx) on the VPC list page.
![](https://main.qcloudimg.com/raw/6a920e1417bdb8c45ba051f97713a82b.png)
3. On the VPC Details page, select **MySQL** in the database directory, and click **Add** on the right.
![](https://main.qcloudimg.com/raw/c4c4c11d25736adfc105ca3a0f684d24.png)
4. Select the configuration to purchase, and complete the payment. For more information, please see [Database MySQL](https://intl.cloud.tencent.com/document/product/236).
5. The purchased MySQL will appear in the MySQL instance list.
![](https://main.qcloudimg.com/raw/74a49caf041b5ef539ce94610154d001.png)
6. Initialize the MySQL instance. Click **Initialize** under the **Operation** column on the right side.
![](https://main.qcloudimg.com/raw/a1524f1ecb9dd5a7aeb53d158a0fe7b0.png)
7. Configure initialization parameters, and then click **OK** to start initialization.
 - **Supported character set**: Select the character set supported by the MySQL database.
 - **Case-sensitivity of the table name**: Whether the table name is case sensitive. Default is "Yes".
 - **Custom port**: Database access port. Default is 3306.
 - **Root account password**: The default user name for the new MySQL database is "root". This is used to set the password of the root account.
 - **Confirm password**: Enter the password again.
 ![](https://main.qcloudimg.com/raw/dadb15cb38483e99ed38a4985957b216.png)
8. The status of the target MySQL instance becomes **Running**, which indicates it has been initialized successfully.
![](https://main.qcloudimg.com/raw/4a3d28bb54b9811f642754eafe930976.png)

### Step 2: Create WordPress service
1. Log in to the [Tencent Cloud TKE console](https://console.cloud.tencent.com/ccs).
2. Click **Service** in the left navigation bar, and click **New** in the service list page.
![](https://main.qcloudimg.com/raw/41599cc9561c312c3fe2c0efab92f43e.png)
3. Configure basic service information.
 - **Service Name**: The name of the service to be created, which is comprised of lowercase letters, numbers and "-". It starts with a lowercase letter and ends with a lowercase letter or a number.
 - **Region**: Select the closest region based on your location.
 - **Cluster**: Select a cluster to run your service. You need to select a running cluster with available CVMs in it.
 - **Service description**: Information of the created service. This information is displayed on the **Service Information** page.
![](https://main.qcloudimg.com/raw/3f56c16e137498692de2370549d070ac.png)
4. Click **Display Advanced Settings** under the running container. In the drop-down list, click **New Variable** under Environment Variables. Enter:
WORDPRESS_DB_HOST = Address of CDB for MySQL
WORDPRESS_DB_PASSWORD = Password entered during initialization
![](https://main.qcloudimg.com/raw/aa72c7bbd6ea390de37e48eab4c4e5bb.png)
5. Configure port mapping. Set both container port and service port to 80.
![](https://main.qcloudimg.com/raw/16ce1c921fe665395fc7c56b0157b3e0.png)
6. Click **Create Service** to complete the creation of the WordPress service.

## Accessing WordPress Service
1. Click **Service Information** on the service page to check the load balancer IP.
![](https://main.qcloudimg.com/raw/0ec3abf5923b299929ce870ed4375a61.png) 
2. Enter the IP in the browser to access the service.
![Alt text](https://main.qcloudimg.com/raw/fe522cc3fc29e278b37efae5a1b0150b.png)

