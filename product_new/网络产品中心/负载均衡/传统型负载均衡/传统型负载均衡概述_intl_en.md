## Overview
Classic CLB is easy to configure and supports simple load balancing scenarios:
- **Public network** classic CLB: TCP/UDP/HTTP/HTTPS are supported.
- **Private network** classic CLB: TCP/UDP are supported.

CLB offers two types of instances: CLB (formerly "application CLB") and classic CLB.

CLB has all features of classic CLB. Given their product features and performance, we recommend that you use CLB. For a detailed comparison, see [Instance Types](https://intl.intl.cloud.tencent.com/document/product/214/8847).

This document gives an overview of classic CLB instances. After creating an instance, you need to configure a listener to it. The listener listens to requests on the instance and routes traffic to the real server based on the balancing policy.
## Listener Configuration Instructions
You need to configure the following for a CLB listener:
1. Listener protocol and listening port. A listening port, aka frontend port, is used to receive and route requests to the real server.
2. Backend port. It is the port through which the CVM instance provides services and receives and processes the traffic from the CLB instance.
3. Listening policies, such as balancing policy and session persistence.
4. Health check policy.
5. Real server which can be bound by selecting its IP.

> If you configure multiple listeners to a classic CLB instance and bind multiple real servers, each listener will route requests to all real servers according to its own configuration.

### Supported Protocol Types
A CLB listener can listen to layer-4 and layer-7 requests on a CLB instance and route them to the real server for processing. The main difference between layer-4 CLB and layer-7 CLB lies in that the former routes traffic for load balancing of user requests based on the layer-4 protocols, while the latter on the layer-7 protocols.
- Layer-4 protocols: Transfer layer protocols, including TCP and UDP.
- Layer-7 protocols: Application layer protocols, including HTTP and HTTPS.

>
> 1. A classic CLB instance mainly receives requests and routes traffic to the real server via VIP and port, as layer-7 protocols do not support traffic routing based on domain name and URL.
> 2. A private network classic CLB instance supports only layer-4 protocols but not layer-7 protocols.
> 3. If you need the above advanced functions, we recommend choosing CLB over classic CLB. For more information, see [Instance Types](https://intl.cloud.tencent.com/document/product/214/8847).

### Port Configuration
<table>
<thead>
<tr>
<th width="30%">Listening port (frontend port)</th>
<th width="30%">Service port (backend port)</th>
<th width="40%">Description</th>
</tr>
</thead>
<tbody><tr>
<td>Via the listening port, a CLB instance receives and routes requests to the real server for load balancing.<br><br>You can configure CLB instances for port 1 to 65535, such as 21 (FTP), 25 (SMTP), 80 (HTTP), and 443 (HTTPS).</td>
<td>A service port receives the traffic from the CLB instance.<br><br>On a CLB instance, one listening port can route traffic to multiple ports of multiple CVM instances.</td>
<td><li>On a CLB instance, a listening port must be unique.<br>For example, `TCP:80` and `HTTP:80` listeners cannot co-exist.</li><li>Only TCP and UDP ports can co-exist.<br>For example, you can create `TCP:80` and `UDP:80` listeners at the same time.</li><br>There can be multiple service ports on a CLB instance.<br>For example, both `HTTP:80` and `HTTPS:443` listeners can be bound to the same port of a CVM instance.</td>
</tr>
</tbody></table>

