## Operation Scenarios
TencentDB for Redis does not support public network access for the time being. You can use a CVM instance with a public IP for port forwarding so as to access TencentDB for Redis over the public network.
>?iptable-based forwarding may be unstable; therefore, you are not recommended to access instances over the public network in the production environment.
>
![](https://main.qcloudimg.com/raw/bd7f9a09c2e01aac1adce409b949afe3.jpg)

## Directions
1. Log in to the [CVM instance](https://intl.cloud.tencent.com/document/product/213/5436) and enable the CVM IP forwarding feature.
>?The CVM and TencentDB instances must be under the same account and in the same VPC in the same region, or both in the classic network
>
```
echo 1 > /proc/sys/net/ipv4/ip_forward
```
2. Configure the forwarding rule. The sample code below forwards access requests originally to `26.xx.x.2:10001` (CVM instance public address with a custom port as desired) to the TencentDB for Redis instance with the private address `10.0.0.5:6379`:
```
iptables -t nat -A PREROUTING -p tcp --dport 10001 -j DNAT --to-destination 10.0.0.5:6379
iptables -t nat -A POSTROUTING -d 10.0.0.5 -p tcp --dport 6379 -j MASQUERADE
```
3. Configure the [CVM security group](https://intl.cloud.tencent.com/document/product/213/34272) to enable access to the public port of the CVM instance. You are recommended to open only source addresses that require access.
4. On the accessing client, you can connect to the TencentDB for Redis instance on the private network simply by accessing the public IP 26.xx.xx.2:10001. The connection commands are the same as the private network connection commands. For more information, please see [Instance Connection](https://intl.cloud.tencent.com/document/product/239/9897#.E8.BF.9E.E6.8E.A5.E5.AE.9E.E4.BE.8B).
5. After connecting to the TencentDB for Redis instance, run the `info` command. If the database information is returned, the connection is successful.

