
# Overview
Classic CLB is easy to configure and supports simple load balancing scenarios:
- **Public network** classic CLB: supports TCP/UDP/HTTP/HTTPS protocols.
- **Private network** classic CLB: supports TCP/UDP protocols.

CLB instances can be classified into two types: CLB (formerly "application CLB") and classic CLB.

CLB covers all features of classic CLB. Based on their features and performance, we recommend that you use CLB. For a detailed comparison, see [Instance Types](https://intl.cloud.tencent.com/document/product/214/8847).
>!All Tencent Cloud accounts registered after June 17, 2020 00:00:00 are bill-by-IP accounts which no longer support classic CLB. So you can only purchase a CLB instance.
>
This document gives you an overview of classic CLB instances. After creating an instance, you need to configure a listener to it. The listener listens to requests on the CLB instance and distributes traffic to the real server based on the load balancing policy.
## Listener Configuration Instructions
You need to configure a CLB listener as follows:
1. Listener protocol and listening port. A listening port, or frontend port, is used to receive and forward requests to real servers.
2. Backend port. It is the port through which the CVM instance provides services, receives and processes the traffic from the CLB instance.
3. Listening policy, such as load balancing policy and session persistence.
4. Health check policy.
5. Real server which can be bound by selecting its IP.

> ?If you configure multiple listeners to a classic CLB instance and bind multiple real servers, each listener will forward requests to all real servers according to its configuration.

## Supported protocol types
A CLB listener can listen to layer-4 and layer-7 requests on a CLB instance and distribute them to real servers for processing. The main difference between layer-4 CLB and layer-7 CLB is whether layer-4 or layer-7 protocol is used to forward traffic for load balancing of user requests.
- Layer-4 protocols: transport layer protocols, including TCP and UDP.
- Layer-7 protocols: application layer protocols, including HTTP and HTTPS.

>? 
1. A classic CLB instance receives requests and forwards traffic to the real server mainly via VIP and port, as layer-7 protocols do not support the forwarding based on domain name and URL.
2. A private network classic CLB instance supports only layer-4 protocols but not layer-7 protocols.
3. If you need the foregoing advanced features, we recommend choosing CLB over classic CLB. For more information, see [Instance Types](https://intl.cloud.tencent.com/document/product/214/8847).

## Port Configuration
<table>
<thead>
<tr>
<th width="30%">Listening Port (frontend port)</th>
<th width="30%">Service Port (backend port)</th>
<th width="40%">Description</th>
</tr>
</thead>
<tbody><tr>
<td>Through the listening port, a CLB instance receives and forwards requests to real servers for load balancing.<br><br>You can configure CLB for the port range 1-65535, such as 21 (FTP), 25 (SMTP), 80 (HTTP), and 443 (HTTPS).</td>
<td>A service port provides services for CVM, receives and processes traffic from the CLB instance.<br><br>On a CLB instance, one listening port can forward traffic to multiple ports of multiple CVM instances.</td>
<td>On a CLB instance,<li>a listening port must be unique.<br>For example, `TCP:80` and `HTTP:80` listeners cannot co-exist.</li><li>Only TCP and UDP ports can be the same.<br>For example, you can create both `TCP:80` and `UDP:80` listeners.</li><br>The same service ports can be used on a CLB instance.<br>For example, both `HTTP:80` and `HTTPS:443` listeners can be bound to the same port of a CVM instance.</td>
</tr>
</tbody></table>

