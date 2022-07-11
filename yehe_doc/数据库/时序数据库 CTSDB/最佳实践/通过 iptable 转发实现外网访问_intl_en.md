## Overview
CTSDB doesn’t support direct public network access for the time being. You can use a CVM instance with a public IP for port forwarding so as to access CTSDB over the public network.

>?Because iptables-based forwarding may be unstable, we recommend that you do not access instances over the public network in the production environment.

![](https://qcloudimg.tencent-cloud.cn/raw/43bf0598883beb43f13ae6d87aa1b458.png)

## Directions
1. Log in to a [CVM](https://intl.cloud.tencent.com/document/product/213/5436) instance and enable the IP forwarding feature.
>?The CVM instance and the database must be under the same Tencent Cloud account and in the same VPC in the same region.
>
```
echo 1 > /proc/sys/net/ipv4/ip_forward
```
2. Configure the forwarding rule. The sample code below forwards access requests originally to `26.xx.x.2:10001` (CVM instance public IP with a custom port as desired) to the CTSDB instance with the private IP `10.x.x.5:9200`:
```
iptables -t nat -A PREROUTING -p tcp --dport 10001 -j DNAT --to-destination 10.x.x.5:9200
iptables -t nat -A POSTROUTING -d 10.x.x.5 -p tcp --dport 9200 -j MASQUERADE
```
3. Configure the [CVM security group](https://intl.cloud.tencent.com/document/product/213/34272) to enable access to the public port of the CVM instance. We recommend you open only source addresses that require access.
4. To connect to the CTSDB instance over the private network at its public IP (`26.xx.xx.2:10001` in the sample code), you can use the same way as the private network connection. For more information, see [Connecting to Instance](https://intl.cloud.tencent.com/document/product/1100/40928).
