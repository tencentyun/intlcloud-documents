
## Error Description
- [Symptom 1](id:xz1): failed to connect to or log in to a TencentDB for Redis instance from a CVM instance.
- [Symptom 2](id:xz2): failed to connect to or log in to a TencentDB for Redis instance from the database management center (DMC).
![](https://qcloudimg.tencent-cloud.cn/raw/8917bd64abc5a131884fa3b0c9df190d.png)

## Common Causes
- Network issue
- Security group issues.
- Password issues.
- The maximum number of connections has been reached.
- Memory or shards have been used up.
- The instance cannot be accessed over public network.
- A high-availability (HA) switch occurred, the database service became unavailable, a read-only replica switch occurred, or the read-only replica service became unavailable, etc.

## Solution
1. [Run `telnet` to locate where the error occurred (in TencentDB for Redis or your business)](#sytqr).
2. [Check whether the error was caused by password issues](#qrsfwmmwt).
3. [Modify the allowed maximum number of connections](#tzzdljs).
4. [Check whether the error was caused by write failure due to used-up memory or shards](#qrsfncxm).
5. [Enable public network access](#sxwwfw).
6. [Check whether any of the following occurred: HA switch, unavailable database service, read-only replica switch, or unavailable read-only replica service](#qrsffsh).

## Troubleshooting Procedure
### [Running `telnet` to locate where the error occurred (in TencentDB for Redis or your business)](id:sytqr)
Run `telnet` in the command line tool to narrow down the cause of the error:
```js
[root@VM-4-10-centos ~]# telnet 10.x.x.34 6379
Trying 10.x.x.34...
Connected to 10.x.x.34.
Escape character is '^]'.
```
As shown above, if the result indicates that the connection is successful, the TencentDB for Redis instance runs normally. Please troubleshoot your business:

#### 1. Troubleshoot the network
To connect over private network, the CVM and TencentDB instances must be under the same account and in the same VPC in the same region, or both in the classic network.
- If the CVM instance is in a VPC, while the Redis instance in the classic network, we recommend that you switch the network type of the Redis instance from classic network to VPC. For more information, see [Configuring Network](https://intl.cloud.tencent.com/document/product/239/31944).
- If the Redis instance is in a VPC, while the CVM instance in the classic network, we recommend that you switch the network type of the CVM instance from classic network to VPC. For more information, see [Switching to VPC](https://intl.cloud.tencent.com/document/product/213/20278).
- If the CVM and TencentDB for Redis instances are in different VPCs in the same region, we recommend that you migrate the Redis instance to the VPC of the CVM instance. For more information, see [Configuring Network](https://intl.cloud.tencent.com/document/product/239/31944).
- If the CVM and TencentDB for Redis instances are in different VPCs in different regions, we recommend that you create a [CCN](https://intl.cloud.tencent.com/zh/document/product/1003) between the two VPCs.
- If the CVM and TencentDB for Redis instances are in different VPCs under different accounts, we recommend that you create a [CCN](https://intl.cloud.tencent.com/zh/document/product/1003) between the two VPCs.

#### 2. Troubleshoot security groups
The CVM instance cannot connect to the TencentDB for Redis instance if their security groups are incorrect.
-  [Incorrect CVM security group configuration](id:caqzpzyw)
To use the CVM instance to access the Redis instance, you need to configure an outbound rule in the security group of the CVM instance. **If the target of the outbound rule isn't "0.0.0.0/0" and the protocol port isn't "ALL"**, the IP and port of the Redis instance should be added to the rule.
 1. Go to the [Security Group](https://console.cloud.tencent.com/cvm/securitygroup) page in the CVM console and click the name of the CVM-bound security group to enter its details page.
 2. On the **Outbound rule** tab, click **Add Rule**.
Set **Type** to **Custom**, **Target** to the IP/IP range of the Redis instance, and **Policy** to **Allow**.

- [Incorrect Redis security group configuration](id:maqzpzyw)
To use the CVM instance to access the Redis instance, you need to configure an inbound rule in the security group of the Redis instance. **If the source of the inbound rule isn't "0.0.0.0/0" and the protocol port isn't "ALL"**, the IP and port of the CVM instance should be added to the rule. 
 1. Go to the [Security Group](https://console.cloud.tencent.com/cvm/securitygroup) page in the CVM console and click the name of the Redis-bound security group to enter its details page.
 2. On the **Inbound rule** tab, click **Add Rule**.
Note that you also need to open the IP and port of the Redis instance in the inbound rule.
Set **Type** to **Custom**, **Source** to the IP/IP range of the CVM instance, and **Policy** to **Allow**.
>!  
>- The Redis instance uses private network port 6379 by default and supports customizing its port. If the default port is changed, the new port should be opened in the inbound rule of the Redis security group.
>- If the default port 6379 of the Redis instance is used, it should be opened in the inbound rule of the Redis security group.

### [Troubleshooting the password](id:qrsfwmmwt)
Run the `info` command. If the following information is displayed, the password of the TencentDB for Redis instance is correct.
```js
[root@SNG-Qcloud /data/home/rickyu]# redis-cli -h 10.x.x.34 -p 6379 -a password
10.x.x.2:6379> info cpu
# CPU
used_cpu_sys:1623.176000
used_cpu_user:4649.572000
used_cpu_sys_children:0.000000
used_cpu_user_children:0.000000
```
If `NOAUTH Authentication required.` is displayed, the password is incorrect.
```js
10.0.4.31:6379> info memory
NOAUTH Authentication required.
10.0.4.31:6379> 
```
#### Solution
Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis) and click an instance ID in the instance list to enter the instance details page, where you can reset the password. For more information, see [Managing Accounts](https://intl.cloud.tencent.com/document/product/239/34590).
![](https://qcloudimg.tencent-cloud.cn/raw/fe7308090ce478150a0b1c5706bc1aef.png)

### [Adjusting the maximum number of connections](id:tzzdljs)
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), click an instance ID in the instance list, and enter the instance details page.
2. Click **Adjust** next to **Max Connections** in **Network Info**.
>?You can modify the maximum number of proxy connections in the console. To modify the maximum number of Redis connections, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
>
![](https://qcloudimg.tencent-cloud.cn/raw/40d1e79d20b29d4f381f53d79ecd9144.png)
3. On the **System Monitoring** > **Monitoring Metrics** tab, select the **Connection Utilization** metric to view its value.
Proxy monitoring data:
![](https://qcloudimg.tencent-cloud.cn/raw/ba5071d61ba24b97e1bc69b2d28e48d3.png)
Redis monitoring data:
![](https://qcloudimg.tencent-cloud.cn/raw/38dc0b1facdff97aec660e4c54e0b9d5.png)

### [Checking whether the memory or shards are used up](id:qrsfncxm)
If you receive the following error message:
```js
"-READONLY You can't write against a read only slave.\r\n"
```
Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), click an instance ID in the instance list, and select the **System Monitoring** tab to view memory utilization.
![](https://qcloudimg.tencent-cloud.cn/raw/7a63fbc80e9cb39c317b842d458866cf.png)
If memory is used up, writes will fail. Please [expand capacity](https://intl.cloud.tencent.com/document/product/239/31934) immediately or adopt the `allkeys-lru` or `volatile-lru` eviction policy.

>?Instance data may be lost if the `allkeys-lru` eviction policy is adopted. Please assess the impact before doing so.

### [Enabling public network access](id:sxwwfw)
TencentDB for Redis now allows you to manually enable public network access in the console, so that instances can be accessed over public network. For detailed directions, see [Configuring the Public Network Address](https://intl.cloud.tencent.com/document/product/239/43452).

### [Checking whether any of the following occurred: HA switch, unavailable database service, read-only replica switch, or unavailable read-only replica service](id:qrsffsh)
If you find that the connections are exceptional, there are a large number of access errors and slow queries, and you receive event alarms from CM at a certain time point, an exceptional event has occurred. In this case, [contact us](https://intl.cloud.tencent.com/contact-us) for assistance.

**Configure event alarms in the [Cloud Monitor](https://console.cloud.tencent.com/monitor/alarm2/policy) console**:
![](https://qcloudimg.tencent-cloud.cn/raw/f7de41a133dd54b2c82574f2bbbc1dde.png)

## Appendix
### [Viewing network type and VPC information](id:wllxvpdff)
To enable connection between CVM and TencentDB for Redis instances over private network, they must be under the same account and in the same VPC in the same region, or both in the classic network.
>?
>- If the instance lists both show **Classic Network** or **VPC**, it means that the networks of the CVM and TencentDB for Redis instances are of the same type.
>- If the instance lists both show the same **VPC** (in the same region), it means that the CVM and TencentDB for Redis instances are in the same VPC.
>
- **View the network type/VPC of CVM**: log in to the [CVM console](https://console.cloud.tencent.com/cvm/instance) and view network information in the instance list.
![](https://qcloudimg.tencent-cloud.cn/raw/ad8661c3906fa96962618e51b731fc4d.png)
- **View the network type/VPC of TencentDB for Redis**: log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis) and view **Network** in the instance list.
![](https://qcloudimg.tencent-cloud.cn/raw/920e151463fc3f6087c671294b05ee46.png)
