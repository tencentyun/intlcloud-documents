
Server Name Indication (SNI) is designed to solve the problem that one server can only use one certificate so as to improve SSL/TLS extensions of the server and the client. If a server supports SNI, it means that the server can be bound to multiple certificates. To use SNI for the client, the domain name to connect to should be specified before SSL/TLS connections to the server are established, and then the server will return an appropriate certificate based on the domain name.

## Use Cases
A layer-7 HTTPS CLB listener supports SNI, i.e., binding multiple certificates, which can be used by different domain names in the listening rules. For example, in the same `HTTPS:443` listener of a CLB instance, you can use certificate 1 and certificate 2 for `*.test.com` and `*.example.com` respectively to forward requests from these domain names to two different sets of servers.

## Prerequisites
You have [purchased a CLB instance](https://buy.cloud.tencent.com/lb?rid=1&type=2&vpcId=vpc-k9gii1kb).
>Classic CLB does not support forwarding based on domain name and URL; therefore, it does not support SNI.

## Directions
1. Log in to the [CLB console](https://console.cloud.tencent.com/clb).
2. [Configure an HTTPS listener](https://intl.cloud.tencent.com/document/product/214/32516#.E6.AD.A5.E9.AA.A42.EF.BC.9A.E9.85.8D.E7.BD.AE.E7.9B.91.E5.90.AC.E5.99.A8) and enable SNI.
![](https://main.qcloudimg.com/raw/eb6958c5f3772c3b55ab3a2a1e92d341.png)
3. When adding a forwarding rule to the listener, configure different server certificates for different domain names. Then, click **Next** and configure health check and session persistence.
![](https://main.qcloudimg.com/raw/bf5150f1f263a133770f1ad5694f501c.png)
