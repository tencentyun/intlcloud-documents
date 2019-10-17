## What is SNI?
Server Name Indication (SNI) is designed to solve the problem that one server can only use one certificate so as to improve SSL/TLS extensions of the server and the client. If a server supports SNI, it means that the server can be bound to multiple certificates. To use SNI for the client, the domain name to connect to should be specified before SSL/TLS connections to the server are established, and then the server will return an appropriate certificate based on the domain name.
> The SNI feature for CLB is currently in beta test. If you want to use it, please [submit a ticket](https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=163&level1_name=%E8%AE%A1%E7%AE%97%E4%B8%8E%E7%BD%91%E7%BB%9C&level2_name=%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1%20LB) for application.

A layer-7 HTTPS CLB listener supports SNI, i.e., binding multiple certificates, which can be used by different domain names in the listening rules.
## Prerequisites
The prerequisites for binding multiple certificates using SNI are as follows:
- You have already purchased an **Application** CLB instance.
- The certificates have been obtained.

## Directions
### Purchasing a CLB Instance
1. Log in to the [CLB Console](https://console.cloud.tencent.com/loadbalance).
2. [Purchase](https://buy.cloud.tencent.com/lb) a CLB instance.

### Creating an HTTPS Listener and Configuring SNI
1. To create an HTTPS Listener, you first need to disable multi-domain name certificate sharing.
Multi-domain name certificate sharing means that multiple domain names on the server share one certificate, i.e., SNI is not enabled; disabling it is equivalent to enabling SNI, i.e., different domain names can use different certificates.
 
2. When adding a forwarding rule to the listener, you can select different server certificates for different domain names.

