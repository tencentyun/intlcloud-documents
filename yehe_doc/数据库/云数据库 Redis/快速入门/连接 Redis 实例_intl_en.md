## Overview

This document describes three methods for connecting to a database. After an instance is created and the status is **Running**, you can access it and run Redis commands for read, write, and query.

- Connection via client: You can connect to a TencentDB instance at its automatically assigned private address from a Windows or Linux CVM instance. This connection method utilizes the high-speed private network of Tencent Cloud and features low delay. Both instances should be under the same account and reside in the same [VPC](https://intl.cloud.tencent.com/document/product/215/535) in the same region or reside in the classic network.
> ?
> - CVM and TencentDB instances in different VPCs (under the same or different accounts in the same or different regions) can be interconnected over private network through [Cloud Connect Network](https://intl.cloud.tencent.com/document/product/1003).
> - CVM and TencentDB instances in different VPCs can be connected through the public network address as instructed in [Configuring Public Network Address](https://intl.cloud.tencent.com/document/product/239/43452).
-  Connection via DMC: You can use Tencent Cloud Database Management Center (DMC) to log in to your TencentDB instance to access them, view their key metric information, and run Redis commands.
- Connection via SDK: You can connect to a TencentDB for Redis instance by configuring its private IP, port, instance ID, and password in the SDK for the corresponding programming language. Then, you can manipulate it, get and set its key, and do more.

## Preparations

- Prepare a TencentDB for Redis instance. For more information, see [Creating TencentDB for Redis Instance](https://intl.cloud.tencent.com/document/product/239/37712).
- Prepare a database account and password. For more information, see [Managing Account](https://intl.cloud.tencent.com/document/product/239/34590). You can use the default account or a custom account.
- Configure security group rules for the CVM instance and the TencentDB for Redis instance. For more information, see [Configuring Security Group](https://intl.cloud.tencent.com/document/product/239/31945).
- Obtain the **Private IPv4 Address** for database connection in the **Network Info** section on the **Instance Details** page in the [TencentDB for Redis console](https://console.cloud.tencent.com/redis).

## Connecting via Client Tool
### Connecting from Linux CVM instance
#### Step 1. Prepare the environment

1. Log in to the Linux CVM instance. For more information, see [Customizing Linux CVM Configurations](https://intl.cloud.tencent.com/document/product/213/10517).
2. Taking a CVM instance on CentOS as an example, install the Redis client by running the following command:
```
yum install redis -y
```
If `Complete!` is displayed, the client is installed successfully.

#### Step 2. Connect to an instance
- **Passwordless authentication**
If your instance is passwordless, the connection command is as follows:
```
redis-cli -h IP address -p port
```
Here, the IP address and port are the **Private IPv4 Address** and **Port** obtained in the **Network Info** section on the **Instance Details** page in the [TencentDB for Redis console](https://console.cloud.tencent.com/redis).


- **Access with default account**
To use the default account with a password to access the database, the following open-source connection command is supported:
```
redis-cli -h IP address -p port -a password
```
Here, the IP address and port are the **Private IPv4 Address** and **Port** obtained in the **Network Info** section on the **Instance Details** page in the [TencentDB for Redis console](https://console.cloud.tencent.com/redis).
For example, if the password you set is `abcd1234`, the connection command should be as follows:
```
redis-cli -h IP address -p port -a abcd1234
```
>?To access instances purchased before January 2018, you need to replace the "password" with "instance ID:password".
>Example: `redis-cli -h IP address -p port -a crs-bkuza6i3:abcd1234`

- **Access with custom account**
If you use a [custom account](https://intl.cloud.tencent.com/document/product/239/34590) for connection, the `account name@password` password parameter will be authenticated for accessing TencentDB for Redis:
```
redis-cli -h IP address -p port -a account name@password
```

### Connecting from Windows CVM instance

1. Configure and log in to the Windows CVM instance. For more information, see [Customizing Windows CVM Configurations](https://intl.cloud.tencent.com/document/product/213/10516).
2. In the Windows CVM instance, download the TencentDB for Redis client over the internet and install it.
3. Open the TencentDB for Redis client, configure the instance's private IP address, and click **Test Connection** to connect to the instance.
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td><strong>Name</strong></td>
<td>Name of the connection to the database instance.</td></tr>
<tr>
<td><strong>Address</strong></td>
<td>Enter the <strong>Private IPv4 Address</strong> of the database instance, which can be obtained in the <strong>Network Info</strong> section on the <strong>Instance Details</strong> page in the console.</td></tr>
<tr>
<td><strong>Verification</strong></td>
<td>Enter the password for database instance connection.</td></tr>
</tbody></table>
4. Click <img src="https://qcloudimg.tencent-cloud.cn/raw/23cac0a46eda69586ec354d1b186777a.png" style="zoom:33%;" /> and enter a Redis command in the input box in the bottom-right corner to run it.

## Connection via DMC

1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis).
2. Above the instance list, select the region.
3. In the instance list, find the target instance.
4. Click **Log In** in the **Operation** column.
5. You will be redirected to the login page of the [DMC console](https://bj-dmc.cloud.tencent.com/v2/qcloudLogin/login). Enter the default account password of the target instance and click **Log In**.

6. You can view the instance monitoring information on the **Instance Info** tab on the **Database Management** page.

7. Click the **Command Line** tab and enter a Redis command in the input box at the bottom to run it as shown below:

8. If you are unfamiliar with Redis command parameters, you can select the slot range and database for storing key values in the **Object List** section on the left of the page, click **Create**, select the key data type, click **OK**, edit the key name in the **Key Name** input box, and click **Add element and create key**. Then, enter the corresponding key value and click **OK** in the **Add Element** window. The system will run commands based on the set key and key value.


## Connection via SDK
TencentDB for Redis can be accessed via SDKs for various programming languages, including PHP, Java, Node.js, Python, C, Go, and .NET. For specific samples, see [PHP Connection Example](https://intl.cloud.tencent.com/document/product/239/7042). You can download an SDK client and then connect to a TencentDB for Redis instance by configuring its private IP, port, instance ID, and password as instructed in the sample code.

## FAQs

For more FAQs, see [Connection and Login](https://intl.cloud.tencent.com/document/product/239/18664).
