

### Max Concurrent Connections

It refers to the maximum number of concurrent accessing connections supported by a GAAP connection.



### CNAME Record

A CNAME (Canonical Name) record refers to the alias record in a domain name resolution.
For example, a server named `host.example.com` provides both WWW and MAIL services. To make it easier for users to access those services, two CNAME records (`www.example.com` and `mail.example.com`) can be added for this server at its DNS service provider, and all requests to access these two CNAME records will be forwarded to `host.example.com`.



### GAAP

For more information, please see [Global Application Acceleration Platform](#GAAP1).



### Listener

A listener is used to provide configuration features for request forwarding policy, including the configuration of protocols, ports, scheduling policies among multiple origin servers, and health checks. Requests will be forwarded to the backend origin server according to the policy configured on a listener.

### Acceleration Region

It refers to the region where users are located. Users in acceleration regions can access the business servers in the origin server region through acceleration connections.


<span ="GAAP1"></span>
### Global Application Acceleration Platform

Tencent Cloud Global Application Acceleration Platform (GAAP) is a PaaS product that achieves optimal global access latency. It uses high-speed connections, cluster forwarding, and intelligent routing among global nodes to allow users in different regions to access the closest nodes, so their request traffic can be forwarded to origin servers, reducing access lag and latency.



### Origin Server

It is a customer business server and can be a self-created server or a Tencent Cloud [COS](https://intl.cloud.tencent.com/product/cos) bucket.
