You can connect to a TencentDB for Tendis instance using a private network address, the data management console (DMC), and programing languages.
<span id="tgnedzlj"></span>
## Connecting Using a Private Network Address
A CVM instance can be used to access the private network address that is automatically assigned to a TencentDB instance. This connection method relies on the high-speed private network of Tencent Cloud and features low delay. Both instances should be under the same account and reside in the same [VPC](https://intl.cloud.tencent.com/document/product/215/535) in the same region or reside in the classic network.
>?
>- CVM and TencentDB instances in different VPCs (under the same or different accounts in the same or different regions) can be interconnected over private network through [Cloud Connect Network](https://intl.cloud.tencent.com/document/product/1003/30049).
>- To connect to Tendis instances with a public network address, please see [iptables Forwarding](https://intl.cloud.tencent.com/document/product/1083/39269).

### Step 1. Prepare the environment
1. Log in to a Linux CVM instance. For more information, please see [Customizing Linux CVM Configurations](https://intl.cloud.tencent.com/document/product/213/10517).
2. Taking a CVM instance on CentOS as an example. Install the Redis client by running the following command:
```
yum install redis -y
```
If `Complete!` is displayed, the client is installed successfully.

### Step 2. Connect to the Tendis instance
The following connection command supported by open-source Redis can be used to connect to the Tendis instance:
```
redis-cli -h IP address -p port -a password
```

For example, if the password you set is `abcd1234`, then the connection command should be as follows:
```
redis-cli -h IP address -p port -a abcd1234
```

## Connecting Using DMC
You can use Tencent Cloud’s [data management console (DMC)](https://dms.cloud.tencent.com/#/login) to access TencentDB for Tendis instances, manipulate databases and tables, manage instance sessions, monitor instances in real time, view InnoDB lock waits, and use the SQL window.

## Connecting Using Programing Languages
For connection samples, please see [Instance Connection Using Programing Languages](https://intl.cloud.tencent.com/document/product/1083/39281).

