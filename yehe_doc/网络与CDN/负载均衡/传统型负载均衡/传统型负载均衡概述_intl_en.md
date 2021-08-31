
## Overview
Classic CLB is easy to configure and supports simple load balancing scenarios:
- **Public network** classic CLB: supports TCP/UDP/HTTP/HTTPS protocols.
- **Private network** classic CLB: supports TCP/UDP protocols.

CLB instances can be classified into two types: CLB (formerly "application CLB") and classic CLB.

CLB includes all features of classic CLB. Based on their features and performance, we recommend using CLB. For detailed comparison, see [Instance Types](https://intl.cloud.tencent.com/document/product/214/8847).
>!Currently, there are two types of Tencent Cloud accounts: bill-by-EIP/CLB and bill-by-CVM. All Tencent Cloud accounts registered after June 17, 2020 00:00:00 are bill-by-EIP/CLB accounts. For Tencent Cloud accounts registered before June 17, 2020, [check your account types](https://intl.cloud.tencent.com/document/product/684/15246) in the console. Bill-by-EIP/CLB accounts no longer support classic CLB. You can now only purchase a CLB instance.
>
This document introduces classic CLB instances. After creating an instance, you need to configure a listener for it. The listener listens to requests on the CLB instance and distributes traffic to the real server based on the load balancing policy.

## Listener Configurations
You need to configure a CLB listener as follows:
1. Listener protocol and listening port. The listening port, or frontend port, is used to receive and forward requests to real servers.
2. Backend port. It is the port through which the CVM instance provides services, receives and processes traffic from the CLB instance.
3. Listening policy, such as load balancing policy and session persistence.
4. Health check policy.
5. Real server can be bound by selecting its IP.

> ?If you configure multiple listeners to a classic CLB instance and bind multiple real servers, each listener will forward requests to all real servers based on its configuration.

### Supported protocol types
A CLB listener can listen to Layer-4 and Layer-7 requests on a CLB instance and distribute them to real servers for processing. The main difference between Layer-4 CLB and Layer-7 CLB is which protocol is used to forward traffic when load balancing user requests.
- Layer-4 protocols: transport layer protocols, including TCP and UDP.
- Layer-7 protocols: application layer protocols, including HTTP and HTTPS.

>? 
>1. A classic CLB instance receives requests and forwards traffic to the real server via VIP and port. Layer-7 protocols do not support forwarding based on domain name and URL.
>2. A private network classic CLB instance only supports Layer-4 protocols, not Layer-7 protocols.
>3. If you need aforementioned advanced features, we recommend choosing CLB over classic CLB. For more information, see [Instance Types](https://intl.cloud.tencent.com/document/product/214/8847).

### Port Configuration
<table>
<thead>
<tr>
<th width="30%">Listening Port (frontend port)</th>
<th width="30%">Service Port (backend port)</th>
<th width="40%">Description</th>
</tr>
</thead>
<tbody><tr>
<td>The listening port is used by a CLB instance to receive and forward requests to real servers for load balancing.<br><br>You can configure CLB for the port range 1-65535, such as 21 (FTP), 25 (SMTP), 80 (HTTP), and 443 (HTTPS).</td>
<td>A service port is used by the CVM to provide services, receives and processes traffic from the CLB instance.<br><br>On a CLB instance, one listening port can forward traffic to ports of multiple CVM instances.</td>
<td>On a CLB instance,<li>a listening port must be unique.<br>For example, TCP:80 and HTTP:80 listeners cannot be created at the same time.</li><li>Only TCP and UDP ports can be the same.<br>For example, you can create both TCP:80 and UDP:80 listeners.</li><br>The same service ports can be used on a CLB instance.<br>For example, HTTP:80 and HTTPS:443 listeners can be bound to the same port of a CVM instance.</td>
</tr>
</tbody></table>

