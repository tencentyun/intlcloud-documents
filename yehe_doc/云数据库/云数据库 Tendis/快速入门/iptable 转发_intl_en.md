
TencentDB for Tendis does not support direct access over a public network, but you can use a CVM instance with a public IP for port forwarding to access a Tendis instance over a public network.
>?Port forwarding with iptables is not stable, so we do not recommend this public network access solution in a production environment.
>
![](https://main.qcloudimg.com/raw/63ad5d409e5e17c318619b4e172058b1.png)

## Directions
1. Log in to a [CVM](https://intl.cloud.tencent.com/document/product/213/5436) instance, and enable the IP forwarding feature.
>?The CVM and TencentDB instances must be under the same account and in the same VPC in the same region, or both in the classic network.
>
```
echo 1 > /proc/sys/net/ipv4/ip_forward
```
2. Configure the forwarding rule. The following sample code is to forward access requests of `26.xx.x.2:10001` (CVM public IP and customizable port) to a Tendis instance whose private IP and port are `10.0.0.5:6379`.
```
iptables -t nat -A PREROUTING -p tcp --dport 10001 -j DNAT --to-destination 10.0.0.5:6379
iptables -t nat -A POSTROUTING -d 10.0.0.5 -p tcp --dport 6379 -j MASQUERADE
```
3. Configure the [security group](https://intl.cloud.tencent.com/document/product/213/34272) to open the public port of the CVM instance. We recommend that you configure a security group rule to allow only the source which needs to connect to the Tendis instance.
4. To connect to the Tendis instance in the private network using a public network address (`26.xx.xx.2:10001` in the sample code), you can use the same command as the private network connection command. For more information, please see [Connecting to Tendis Instances](https://intl.cloud.tencent.com/document/product/1083/39268).
5. After connecting to the Tendis instance, run the `info` command. If database information is returned, the connection is successful.

