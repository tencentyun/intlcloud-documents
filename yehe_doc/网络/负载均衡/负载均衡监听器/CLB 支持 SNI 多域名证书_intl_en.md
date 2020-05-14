## SNI Overview
Server Name Indication (SNI) is designed to solve the problem that one server can only use one certificate so as to improve SSL/TLS extensions of the server and the client. If a server supports SNI, it means that the server can be bound to multiple certificates. To use SNI for the client, the domain name to connect to should be specified before SSL/TLS connections to the server are established, and then the server will return an appropriate certificate based on the domain name.

## Use Cases
A layer-7 HTTPS CLB listener supports SNI, i.e., binding multiple certificates, which can be used by different domain names in the listening rules. For example, in the same `HTTPS:443` listener of a CLB instance, you can use certificate 1 and certificate 2 for `*.test.com` and `*.example.com` respectively to forward requests from these domain names to two different sets of servers.

## Prerequisites
You have [purchased a CLB instance](https://buy.cloud.tencent.com/lb).
>Classic CLB does not support forwarding based on domain name and URL; therefore, it does not support SNI.

## Directions
1. When creating an HTTPS listener, enable SNI.
![](https://main.qcloudimg.com/raw/a70af5870cf3c02a97368f9bbb46f74f.png)
2. When adding a forwarding rule to the listener, configure different server certificates for different domain names. Then, click **Next** and configure health check and session persistence.
![](https://main.qcloudimg.com/raw/e35b92e86b8bade2a0a77a64461a418d.png)