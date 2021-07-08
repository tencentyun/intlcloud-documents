You can connect to a TencentDB for Redis instance by using a client tool, the data management console (DMC), and SDKs supporting various programing languages.

## Preparations
- Prepare a TencentDB for Redis instance. For more information, please see [Creating TencentDB for Redis Instance](https://intl.cloud.tencent.com/document/product/239/37712).
- Prepare a database account. For more information, please see [Managing Account](https://intl.cloud.tencent.com/document/product/239/34590). You can also use the default account directly.
- Configure security group rules for the CVM instance and the TencentDB for Redis instance to allow specific IPs or IP ranges to access the TencentDB for Redis instance. For more information, please see [Configuring Security Group](https://intl.cloud.tencent.com/document/product/239/31945).

## Connecting by Using Client Tool
A CVM instance can be used to access the private network address that is automatically assigned to a TencentDB instance. This connection method relies on the high-speed private network of Tencent Cloud and features low delay. Both instances should be under the same account in the same [VPC](https://intl.cloud.tencent.com/document/product/215/535) in the same region, or both in the classic network.
>?
>- CVM and TencentDB instances in different VPCs (under the same or different accounts in the same or different regions) can be interconnected over private network through [Peering Connection](https://intl.cloud.tencent.com/document/product/553/18827).
>- TencentDB for Redis doesn't support public network address currently. To connect to TencentDB for Redis instances over public network, please see [iptables Forwarding](https://intl.cloud.tencent.com/document/product/239/35905).

### Step 1. Prepare the environment
1. Log in to the Linux CVM instance. For more information, please see [Customizing Linux CVM Configurations](https://intl.cloud.tencent.com/zh/document/product/213/10517).
2. (Taking a CVM instance on CentOS as an example) install the Redis client by running the following command:
```
yum install redis -y
```
If `Complete!` is displayed, the client is installed successfully.

### Step 2. Connect to the instance
#### Password-Free instance
If your instance is password-free, the connection command should be as follows:
```
redis-cli -h IP address -p port
```

#### Password-Protected instance
If your instance is password-protected, the following open-source connection format is supported:
```
redis-cli -h IP address -p port -a password
```

For example, if the password you set is `abcd1234`, the connection command should be as follows:
```
redis-cli -h IP address -p port -a abcd1234
```
>?For instances purchased before January 2018, you need to replace the "password" with "instance ID:password" to access the instance.
>Connection sample: `redis-cli -h IP address -p port -a crs-bkuza6i3:abcd1234`


#### Account-Enabled instance
If you use a [custom account](https://intl.cloud.tencent.com/document/product/239/34590) when connecting, then the authentication method of the custom account is `account name@password`, which acts as the password parameter for accessing TencentDB for Redis:

```
redis-cli -h IP address -p port -a account name@password
```


## Connecting by Using DMC
You can use Tencent Cloud [DMC](https://bj-dmc.cloud.tencent.com/v2/qcloudLogin/login) to access TencentDB for Redis instances, manipulate databases and tables, manage instance sessions, monitor instances in real time, view InnoDB lock waits, and use the SQL window.

## Connecting by Using SDKs
For more information, please see [SDK Connection](https://intl.cloud.tencent.com/document/product/239/7042).

