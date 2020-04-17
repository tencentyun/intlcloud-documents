
A CVM instance can be used to access the private address that is automatically assigned to a TencentDB instance. This connection method relies on the high-speed private network of Tencent Cloud and features low delay. Both instances should be under the same account and reside in the same [VPC](https://intl.cloud.tencent.com/document/product/215/535) in the same region or reside in the basic network.
>CVM and TencentDB instances in different VPCs (under the same or different accounts in the same or different regions) can be interconnected over the private network through [Peering Connection](https://intl.cloud.tencent.com/product/pc).

## Environment Preparations
1. Log in to a Linux CVM instance. For more information, please see [Configuring Linux CVM](https://intl.cloud.tencent.com/document/product/213/2936).
2. Taking a CVM instance on CentOS as an example, Install the Redis client by running the following command:
```
yum install redis -y
```
If `Complete!` is displayed, it means the Redis client is installed successfully.

## Instance Connection
### Password-free instance
If your instance is password-free, the connection command should be as follows:
```
redis-cli -h IP address -p port
```

### Password-protected instance
If your instance is password-protected, the following open-source connection format is supported:
```
redis-cli -h IP address -p port -a password
```

For example, if the password you set is `abcd1234`, then the connection command should be as follows:
```
redis-cli -h IP address -p port -a abcd1234
```
>For instances purchased before January 2018, you need to replace the "password" with "instance ID:password" to access it. For example:
>`redis-cli -h IP address -p port -a crs-bkuza6i3:abcd1234`
>

## Connection Sample
For examples of each connection format, please see [Connecting to Instances](https://intl.cloud.tencent.com/document/product/239/7042).

