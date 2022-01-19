**Concepts**[](id:23)
- [What is the difference between layer-4 and layer-7 load balancing?](#1)
- [What is the difference between UDP and TCP?](#2)
- [How does CLB achieve session persistence based on cookies?](#3)
- [What is the real server weight?](#4)
- [What is the difference between resetting the weight to 0 and unbinding the real server?](#24)

**Health Check**
- [What can I do if a CVM instance exception occurs during health check?](#5)
- [The frequency of health check is higher than my configuration in the console.](#6)

**Access**
- [HTTP redirection in load balancing](#7)
- [Which TCP ports can be used for load balancing?](#8)
- [After a policy request (i.e., flash server request) is sent from port 843, no policy file is returned and the connection is interrupted.](#9)
- [Can CLB instances directly obtain client IPs?](#10)
- [Can I configure a private CLB for a CVM instance to forward traffic from port A to another port on the same server?](#11)
- [Does a backend CVM instance need public network bandwidth? Will the bandwidth affect the CLB service?](#12)
- [Notes on compatible versions if the client and server have different HTTP versions](#13)
- [Gzip compatibility](#25)
- [How to configure the security group of a CLB real server? How to configure the access blocklist?](#14)
- [Access blocklist setting](#26)
- [Does a CLB instance communicate with its real server over the private or public network?](#15)
- [Pinging CLB VIP](#16)
- [Running `Telnet` command to connect CLB listening ports](#17)
- [Private network loopback](#18)
- [When a client accesses the same port of a real server via different intermediate nodes, these nodes cannot be specifically determined.](#19)
- [I have configured a backend CVM instance with a security group to block access traffic from the public network and only allow that from CLB instances. But it does not take effect.](#20)
- [I have configured a CLB instance with a listener and bound the listener to a backend CVM, and resolved a domain name to the IP of the backend CVM. But when the domain name is accessed, no monitor data are displayed.](#21)
- [I have not created an 843 listener, but I can successfully run the command `Telnet` for connection.](#22)

[](id:1)
### What is the difference between layer-4 and layer-7 load balancing?
- Layer-4 load balancing is based on IPs and ports.
- Layer-7 load balancing is based on application layer information such as HTTP headers and URLs.

The difference between layer-4 and layer-7 instances is whether layer-4 or layer-7 information is used as the basis for determining how to forward traffic for load balancing on real servers.
For example, a layer-4 CLB instance determines which traffic needs load balancing based on the layer-3 IP address (VIP) and layer-4 port number. It performs Network Address Translation (NAT) on the traffic to be processed, and then forwards it to the real server. It also records which server has processed the TCP or UDP traffic, and forwards all subsequent traffic of this connection to the same server for processing.

A layer-7 CLB is layer-4 CLB instance combined with application layer features.
For example, CLB instances of the same web server can identify traffic that needs to be processed based on layer-7 URL, browser type, and language in addition to the VIP and port 80.
Layer-7 load balancing is also known as "content exchange", in which an internal server is selected based on meaningful application layer content in the message and the server selection method configured on the CLB instance.

To select the server based on the real application layer content, a layer-7 CLB instance must establish a connection (three-way handshake) with the client as a proxy of the final server to receive the message containing real application layer content from the client. It then selects the internal server according to the specific fields in the message and the server selection method configured on the CLB instance. In this case, the CLB instance is more like a proxy server, establishing a TCP connection with the frontend client and the real server respectively.

[[Back to Top]](#23)



[](id:2)
### What is the difference between UDP and TCP protocols?
TCP is a connection-oriented protocol. Before receiving and sending data, TCP requires a reliable connection to be established with the other side. UDP is a message-oriented (connection-less) protocol. It directly sends data packets without performing a three-way handshake with the other side. UDP is suitable for scenarios that focus more on real-timeliness than reliability, such as video chat, real-time push of financial market information, DNS, and IoT.

[[Back to Top]](#23)



[](id:3)
### How does CLB achieve session persistence based on cookies?
In cookie insertion mode, the CLB instance inserts cookies and the real server does not need to make any modifications. When you make the first HTTP request, it (without a cookie) enters the CLB instance, which then selects a real server based on the load balancing algorithm policy and sends the request to the server. The real server then sends an HTTP response (without a cookie) that is sent back to the CLB instance, which then inserts the cookie and returns the HTTP response (with a cookie) to the client.

When you make the second HTTP request (with the cookie inserted by the CLB instance last time), it enters the CLB instance, which then reads the session persistence values in the cookie and sends the request (with the same cookie as above) to the specified real server. The server gives an HTTP response. Because the server does not write the cookie, the response does not contain the cookie. When the response traffic re-enters the CLB instance, CLB will write the updated session persistence cookie into the response.

[[Back to Top]](#23)



[](id:4)
### What is the real server weight?
You can specify the forwarding weight for each CVM instance in the real server pool, and the instance with a higher weight will be assigned with more access requests. You can configure the weights of the backend CVM instances based on their service capabilities and statuses.

If you have also enabled session persistence, the same access request may be forwarded to different real servers. We recommend temporarily disabling session persistence and then checking whether the problem persists.

[[Back to Top]](#23)


[](id:24)
### What is the difference between resetting the weight to 0 and unbinding the real server?
- Resetting the weight to 0: TCP listeners keep forwarding existing connections, UDP listeners keep forwarding connections with the same quintuple, and HTTP/HTTPS listeners keep forwarding existing connections.
- Unbinding the real server: TCP/UDP listeners stop forwarding existing connections, and HTTP/HTTPS listeners keep forwarding existing connections.

[[Back to Top]](#23)


[](id:5)
### What can I do if a CVM instance exception occurs during health check?
Troubleshoot by following the steps:
- Make sure that you access your application service directly via the CVM instance.
- Make sure that the relevant port is open on the real server.
- Check whether there is any security software like a firewall in the real server. This may cause the CLB instance to be unable to communicate with the real server.
- Check whether the health check parameters of the CLB instance are configured correctly.
- We recommend using static pages for health checks.
- Check whether there is high load on the CVM instance that leads to slow response.
- Make sure that there are no IP restrictions (`iptables`) on the CVM instance.

[[Back to Top]](#23)


[](id:6)
### Why is the frequency of health checks so high?
Suppose that you configured to send a health check packet every 5 seconds in the console. However, the real server receives one or even more health check requests in 1 second.

Highly frequent health check relates to the implementation mechanism of CLB health check. Suppose that 1 million requests from clients are distributed to 4 CLB instances before being sent to real servers, and each CLB real server conducts health checks separately. If the CLB instances are configured to send a health check request every 5 seconds, each CLB instance will send a health check request every 5 seconds. This is why the real server receives multiple health check requests. For example, if there are 8 CLB instances in a cluster and each sends a request every 5 seconds, then the real server may receive 8 health check requests in 5 seconds.

The advantages of this implementation scheme are high efficiency, accurate check, and avoidance of mistaken removal. For example, if one of the CLB servers in the cluster fails, the other 7 servers can still forward traffic normally.

Therefore, if your real server is checked too frequently, you can configure a longer check interval (for example, 15 seconds).

[[Back to Top]](#23)


[](id:7)
### HTTP redirection in load forwarding
When you visit the website `http://example.com` via a browser, a redirection to the root directory is required for the server. When you visit the website `http://example.com/` via a browser, the server will directly return the default page of the website's root directory. Similarly, if `http://cloud.tencent.com/movie` is redirected to `http://cloud.tencent.com/movie/` through URL rewriting, entering `http://cloud.tencent.com/movie` will result in an additional URL rewriting process, leading to slight performance degradation and time consumption. However, if `http://cloud.tencent.com/product` is redirected to a page other than `http://cloud.tencent.com/product/` through URL rewriting, you need to consider whether to add "/" after the secondary URL.

In Tencent Cloud CLB, if the frontend and backend port numbers are different, "/" needs to be added after the secondary URL upon the visit to the secondary page, so as to avoid port number changes after HTTP redirection and ensure normal page access.

Assume that in layer-7 forwarding, port 80 on the CLB instance and port 8081 on the real server are listened to. If the client accesses `http://www.example.com/movie`, the access request is forwarded to the real server via the CLB instance, and the server redirects the request to `http://www.example.com:8081/movie/ `(listening port is 8081). In this case, the client access fails (port error).

Therefore, we recommend rewriting the access request to a secondary URL with "/", such as `http://www.example.com/movie/ `. This can avoid HTTP redirection, eliminate unnecessary judgment, and reduce unwanted load. If HTTP redirection is required, make sure that the CLB listening port is the same as that of the real server.

[[Back to Top]](#23)


[](id:8)
### Which TCP ports can CLB be performed on?
You can perform load balancing for the following TCP ports: 21 (FTP), 25 (SMTP), 80 (HTTP), 443 (HTTPS), 1024–65535, etc.

[[Back to Top]](#23)



[](id:9)
### What can I do if no policy file is returned and the connection is interrupted after a policy request (i.e., flash server request) is sent from port 843?
When the CLB instance receives the policy request from port 843, it will return the general cross-domain policy configuration file. If no policy file is returned and the connection is directly closed, the flash server request may be incorrect.

Make sure the correct flash server request is sent: <policy-file-request/>\0.
>! It must end with `\0` and contain 23 bytes. `\0` indicates a character whose ASCII code is 0 and only occupies 1 byte.

The normal result returned by port 843 is as shown below:
![](https://main.qcloudimg.com/raw/69d807250c1e8e00400eade400453620.png)

[[Back to Top]](#23)


[](id:10)
### Can CLB instances directly obtain client IPs?
- IPv6 NAT64 CLB instances do not support obtaining client IPs.
- Public network layer-7 CLB instances use the `X-Forwarded-For` method to get real client IPs. Acquisition of client IPs is enabled on CLB instances by default but needs to be configured on real servers. For more information, see [Getting Real Client IPs](https://intl.cloud.tencent.com/document/product/214/3728).
- Public network layer-4 CLB instances (over TCP) can directly get real client IPs on backend CVM instances, and no additional configuration is required. For the private network layer-4 CLB instances purchased after October 24, 2016, the Source Network Address Translation (SNAT) is not conducted. They can directly get real client IPs from servers with no additional configuration.

[[Back to Top]](#23)


[](id:11)
### Can I configure a private CLB for a CVM instance to forward traffic from port A to another port on the same server?
No. To access port a on server A (10.66.\*.101), the request can be forwarded to port b on server B (10.66.\*.102) via a private network CLB instance. But it cannot be forwarded to port b on the same server A (10.66.\*.101).

[[Back to Top]](#23)

[](id:12)
### Does a backend CVM instance need public network bandwidth? Will the bandwidth affect the CLB service?
- Public network bandwidth is not required for the backend CVM instances bound to the CLB instances of any bill-by-IP accounts.
- No traffic or bandwidth fee is charged for the CLB instances of any bill-by-CVM accounts. Any public network traffic fees generated by CLB service will be charged on the bound backend CVM instances. We recommend choosing bill-by-traffic for public network bandwidth when purchasing the CVM instance and configuring a reasonable peak bandwidth threshold, so that you do not need to keep track of the fluctuation in total CLB egress traffic. The traffic of internet web business fluctuates considerably and cannot be predicted accurately. When bill-by-bandwidth is selected, it is not cost-effective to purchase excessive bandwidth, yet packet loss may occur during business peaks if insufficient bandwidth is purchased.

[[Back to Top]](#23)

[](id:13)
### Notes on compatible versions if the client and server have different HTTP versions
#### Forwarding compatibility
- On the frontend (client), HTTP/1.0 and HTTP/1.1 and lower versions are supported.
- On the backend (server), Tencent Cloud uses the HTTP/1.0; HTTP/1.0 and HTTP/1.1 and lower versions are supported.

> ! HTTP/2 is only supported in HTTPS but not in HTTP, and backward compatibility is allowed on both the client and server.


[](id:25)
#### Gzip compatibility
- On the frontend (client), Gzip is supported by HTTP/1.0, HTTP/1.1 and lower versions. Additional configuration is not needed because mainstream browsers all support Gzip.
- On the backend (server), because HTTP/1.1 is supported on the CVM instance over Tencent Cloud private network, you don not need to make any configuration, and can directly use HTTP/1.1 configured in Nginx by default to achieve compatibility.

> ! HTTP/2 is only supported in HTTPS, but Gzip can be used in any HTTP version supported by Tencent Cloud.
>

[[Back to Top]](#23)


[](id:14)
### How to configure the security group of a CLB real server? How to configure the access blocklist?[](id:14)
#### Configuring the CLB security group
If security group rules have been configured for a real server, the CLB instance may not be able to communicate with the server. Therefore, in layer-4 and layer-7 forwarding, we recommend configuring the security group of a real server as allowing all access requests. If the security group is enabled and accesses from any protocols or IP segments are allowed by default, IPs of all clients need to be configured to the security group rules of the server IP.
For some malicious IPs, you can add them to the top rules of the security group to prevent them from accessing the real server. You can then allow access requests from all IPs (0.0.0.0) to the local service port, so normal clients can access the server. Security group rules are arranged in priority order and matched from top to bottom.

If health check has been configured for layer-7 CLB forwarding in VPC, in the real server security rules, the CLB VIP must be allowed. Otherwise, the health check may fail.


[](id:26)
#### Configuring the access blocklist
If you need to configure a blocklist for some client IPs to deny their access requests, you can configure the security group associated with the cloud services. The security group rules need to be configured as follows:
>! Follow the steps below strictly in the given order, otherwise the blocklist configuration may fail.

- Add the client IP and port to be rejected into the security group, and select the option in the policy column to reject access from this IP.
- Add another security group rule after completing the above configuration to allow access requests to the port from all IPs by default.
When the configuration completes, the security group rules are as follows:
```
clientA ip+port drop
clientB ip+port drop
0.0.0.0/0+port accept
```

For more information on the security group, see [Security Group Configuration of the Real Server](https://intl.cloud.tencent.com/document/product/214/6157).

[[Back to Top]](#23)

[](id:15)
### Does a CLB instance communicate with its real server over the private or public network?
A CLB instance always communicates with real servers over the private network, even when the bound CVM instances have public IPs.

[[Back to Top]](#23)

[](id:16)
### Pinging CLB VIPs
The requests of pinging the CLB VIP are responded to by the CLB cluster and will not be forwarded to real servers.
- Public network CLB VIP can be pinged.
- Pinging a private network CLB VIP to a local client VPC, rather than any other VPC or a local client IDC, is allowed. If VPCs are accessible over the CCN and peering connection, we recommend running `Telnet` to test private network CLB instances.

[[Back to Top]](#23)

[](id:17)
### Running `Telnet` command to connect CLB listening ports
- If layer-4 listeners (TCP, UDP, and TCP SSL) are not bound with real servers after being created, running the command `Telnet` to connect to their listening ports will fail. It will succeed if they are bound with real servers.
- Running the command `Telnet` to connect to listening ports will succeed for layer-7 listeners (HTTP and HTTPS) not bound with real servers, as CLB instances will respond instead.


[[Back to Top]](#23)

[](id:18)
### Private network loopback
For private network CLB instances, a CVM cannot be both the client and server. When the CLB instances read the same client and server IPs, access will fail.
If your client needs to be used as a server, bind at least 2 real servers. CLB has related policies to prevent automatic loopback. When client A accesses the CLB instance, the CLB instance will automatically schedule the request to a real server other than client A.

[[Back to Top]](#23)

[](id:19)
### When a client accesses the same port of a real server via different intermediate nodes, these nodes cannot be specifically determined.
**Issue**
When a client accesses the same port of a real server via different intermediate nodes at the same time, these nodes cannot be specifically determined. The scenarios are detailed below:
- A client accesses the same port of a real server via layer-4 and layer-7 listeners of the same CLB instance at the same time.
- A client accesses the same port of a real server via different listeners of different CLB instances at the same time.
- It is more complex to determine intermediate nodes for a client accessing private network CLB instances of a real server rather than multiple clients accessing public network CLB instances of a real server.

**Cause**
The CLB instances passe the client IP to the real server, and `client_ip:client_port -> vip:vport -> rs_ip:rs_port` will change to `client_ip:client_port --> rs_ip:rs_port`.

**Solutions**
- Distributed clients: multiple clients are used to initiate access.
- Fewer CLB instances: the number of CLB instances and listeners are cut down on the premise of meeting business functions and disaster recovery requirements.
- Distributed real server ports: multiple ports for a real server are used to provide services to avoid congestion.
- Distributed deployment: different CLB instances are bound to different ports on real servers. For example, CLB instance 1 bound to one set of CVM instances and CLB instance 2 bound to another set can be accessed at the same time.

[[Back to Top]](#23)

[](id:20)
### I have configured a backend CVM instance with a security group to block access traffic from the public network and only allow that from CLB instances. But it does not take effect.
To allow traffic to access a backend CVM instance passing through a CLB instance, the traffic from the public network needs to be allowed both on the backend CVM and CLB security groups. We recommend only allowing the access traffic from a CLB VIP over the public network on the backend CVM security group first, and then allowing public network access IPs on the CLB security group as needed.

[[Back to Top]](#23)

[](id:21)
### I have configured a CLB instance with a listener and bound the listener to a backend CVM, and resolved a domain name to the IP of the backend CVM. But when the domain name is accessed, no monitor data are displayed.
Only the traffic going through CLB will be monitored. You can resolve the domain name to the VIP of the CLB instance and access the domain name to view the CLB monitoring information.

[[Back to Top]](#23)

[](id:22)
### I have not created an 843 listener, but I can successfully run the command `Telnet` for connection.
The port 843 is opened by default for users to reset the port for Flash access. If you want to close it, you can just do so by not binding any real servers after configuring the `TCP:843` listener.

[[Back to Top]](#23)
