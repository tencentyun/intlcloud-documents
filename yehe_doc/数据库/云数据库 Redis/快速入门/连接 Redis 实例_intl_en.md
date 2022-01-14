You can connect to a TencentDB for Redis instance using a client tool, the database management center (DMC), and SDKs supporting various programing languages.

## Preparations
- Prepare a TencentDB for Redis instance. For more information, see [Creating TencentDB for Redis Instances](https://intl.cloud.tencent.com/document/product/239/37712).
- Prepare a database account. For more information, see [Managing Accounts](https://intl.cloud.tencent.com/document/product/239/34590). You can also use the default account directly.
- You have configured security group rules for the CVM instance and the TencentDB for Redis instance to allow specific IPs or IP ranges to access the TencentDB for Redis instance. For more information, see [Configuring Security Groups](https://intl.cloud.tencent.com/document/product/239/31945).

## Connecting Using a Client Tool
A CVM instance can be used to access the private address that is automatically assigned to a TencentDB instance. This connection method relies on the high-speed private network of Tencent Cloud and features low delay. Both instances should be under the same account in the same [VPC](https://intl.cloud.tencent.com/document/product/215/535) in the same region, or both in the classic network.
>?
>- CVM and TencentDB instances in different VPCs (under the same or different accounts in the same or different regions) can be interconnected over private network through [Cloud Connect Network](https://intl.cloud.tencent.com/document/product/1003).
>- CVM and TencentDB instances in different VPCs can be connected through the public network address as instructed in [Configuring the Public Network Address](https://intl.cloud.tencent.com/document/product/239/43452).

### Step 1. Prepare the environment
1. Log in to the Linux CVM instance. For more information, see [Customizing Linux CVM Configurations](https://intl.cloud.tencent.com/document/product/213/10517).
2. Taking a CVM instance on CentOS as an example, install the Redis client by running the following command:
```
yum install redis -y
```
If `Complete!` is displayed, the client is installed successfully.

### Step 2. Connect to the instance
#### Password-free instance
If your instance is password-free, the connection command should be as follows:
```
redis-cli -h IP address -p port
```

#### Password-protected instance
If your instance is password-protected, the following open-source connection command is supported:
```
redis-cli -h IP address -p port -a password
```

For example, if the password you set is `abcd1234`, the connection command should be as follows:
```
redis-cli -h IP address -p port -a abcd1234
```
>?To access instances purchased before January 2018, you need to replace the "password" with "instance ID:password".
>Example: `redis-cli -h IP address -p port -a crs-bkuza6i3:abcd1234`


#### Account-enabled instance
If you use a [custom account](https://intl.cloud.tencent.com/document/product/239/34590) for connection, the `account name@password` password parameter will be authenticated for accessing TencentDB for Redis:
```
redis-cli -h IP address -p port -a account name@password
```

## Connecting Using DMC
You can use Tencent Cloud [DMC](https://bj-dmc.cloud.tencent.com/v2/qcloudLogin/login) to access TencentDB for Redis instances, manipulate databases and tables, manage instance sessions, monitor instances in real time, view InnoDB lock waits, and use the SQL window.

## Connecting Using SDKs
For more information, see [SDK Connection](https://intl.cloud.tencent.com/document/product/239/7042).

