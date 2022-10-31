## Overview
TencentDB for Redis supports public network access in Chengdu, Beijing, Shanghai, and Guangzhou regions. To use public network access in other regions, you can use a CVM instance with a public IP for port forwarding to access TencentDB for Redis over the public network.
>?Because iptables-based forwarding may be unstable, we recommend that you do not access instances over the public network in the production environment.
>
![](https://main.qcloudimg.com/raw/7bad7f6f7ca82c8655f807d2036d983b.png)

## Directions
1. Log in to a CVM instance and enable the IP forwarding feature. For more information, see [Logging In to Linux Instance (Web Shell)](https://intl.cloud.tencent.com/document/product/213/5436).
>?The CVM and TencentDB instances must be under the same account and in the same VPC in the same region, or both in the classic network.
>
```
echo 1 > /proc/sys/net/ipv4/ip_forward
```
2. Configure the forwarding rule. The sample code below forwards access requests originally to `26.xx.x.2:10001` (CVM instance public address with a custom port as desired) to the TencentDB for Redis instance with the private address `10.0.0.5:6379`:
```
iptables -t nat -A PREROUTING -p tcp --dport 10001 -j DNAT --to-destination 10.0.0.5:6379
iptables -t nat -A POSTROUTING -d 10.0.0.5 -p tcp --dport 6379 -j MASQUERADE
```
3. Configure the security group to open the public port of the CVM instance. We recommend that you configure a security group rule to allow only the source which needs to connect to the Redis instance. For more information, see [Adding Security Group Rules](https://intl.cloud.tencent.com/document/product/213/34272).
4. To connect to the Redis instance in the private network using a public network address (`26.xx.xx.2:10001` in the sample code), you can use the same command as the private network connection command. For more information, see [Connecting to TencentDB for Redis Instances > Connecting via Client Tool](https://intl.cloud.tencent.com/document/product/239/9897).
5. After connecting to the TencentDB for Redis instance, run the `info` command. If the database information is returned, the connection is successful.

