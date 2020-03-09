### What can I do if a CVM instance exception occurs during health check?
Please troubleshoot by following the steps below:
- Make sure that you access your application service directly via the CVM instance.
- Make sure that the relevant port is enabled on the real server.
- Check whether there is security software like firewall in the real server. This may cause the CLB instance to be unable to communicate with the real server.
- Check whether the health check parameters of the CLB instance are configured correctly.
- We recommend you use static pages for health check.
- Check whether there is high load on the CVM instance that leads to slow response.
- Make sure that there are no iptables restrictions on the CVM instance.

### What can I do if no policy file is returned and the connection is directly closed after a policy request (i.e., flash server request) is sent from port 843?
When the CLB instance receives the policy request from port 843, it will return the general cross-domain policy configuration file. If no policy file is returned and the connection is directly closed, the flash server request may be incorrect.

Make sure the correct flash server request is sent: <policy-file-request/>\0.
> Note: It must end with \0 and contain 23 bytes. \0 indicates a character whose ASCII code is 0 and only occupies 1 byte.

The normal result returned by port 843 is as shown below:
![](https://main.qcloudimg.com/raw/69d807250c1e8e00400eade400453620.png)

### Can CLB instance directly get the client IP?
Public network Layer-7 CLB uses the X-Forwarded-For (XFF) method to get the real IP of the requester. Acquisition of the client IP is enabled on the CLB instance by default but needs to be configured on the real server. For more information, please see [Getting the Real Client IP](https://intl.cloud.tencent.com/document/product/214/3728).

Public network Layer-4 CLB (over TCP protocol) can directly get the real IP address of the requester on the CVM instance, and no additional configuration is required. Since October 24, 2016, private network Layer-4 CLB no longer supports Source Network Address Translation (SNAT) for newly purchased instances, which can directly get the real client IP from the server with no additional configuration.

### Which TCP ports can CLB be performed on?
You can perform CLB for the following TCP ports: 21 (FTP), 25 (SMTP), 80 (HTTP), 443 (HTTPS), 1024–65535, etc.

### How does CLB achieve session persistence based on cookies?

In cookie insertion mode, the CLB instance inserts cookies and the real server does not need to make any modifications. When you make the first HTTP request, it (without a cookie) enters the CLB instance, which then selects a real server based on the load balancing algorithm policy and sends the request to the server. The real server then gives an HTTP response (without a cookie) that is sent back to the CLB instance, which then inserts the cookie and returns the HTTP response (with a cookie) to the client.

When you make the second HTTP request (with the cookie inserted by the CLB instance last time), it enters the CLB instance, which then reads the session persistence values in the cookie and sends the request (with the same cookie as above) to the specified real server. The server gives an HTTP response. Because the server does not write the cookie, the response does not contain the cookie. When the response traffic re-enters the CLB instance, CLB will write the updated session persistence cookie into the response.

### What is the difference between Layer-4 and Layer-7 CLB?
- Layer-4 CLB is based on IPs and ports.
- Layer-7 CLB is based on application layer information such as HTTP headers and URLs.

The difference between Layer-4 and Layer-7 CLB is whether Layer-4 or Layer-7 information is used as the basis for determining how to forward traffic when CLB is performed on real servers.
For example, a Layer-4 CLB instance determines which traffic needs load balancing based on the Layer-3 IP address (VIP) and Layer-4 port number. It performs Network Address Translation (NAT) on the traffic to be processed, and then forwards it to the real server. It also records which server has processed the TCP or UDP traffic, and forwards all subsequent traffic of this connection to the same server for processing.

Layer-7 CLB is Layer-4 CLB combined with application layer features.
For example, CLB instance of the same web server can identify traffic that needs to be processed based on Layer-7 URL, browser type, and language in addition to VIP and port 80.
Layer-7 CLB is also known as "content exchange", which selects an internal server based on meaningful application layer content in the message, and the server selection method configured on the CLB instance.

To select the server based on the real application layer content, Layer-7 CLB must establish a connection (three-way handshake) with the client as a proxy of the final server to receive the message containing real application layer content from the client. It then determines on the internal server according to the specific fields in the message and the server selection method configured on the CLB instance. In this case, the CLB instance is more like a proxy server, establishing a TCP connection with the frontend client and the real server respectively.

### Can CVM instance forward traffic from port A to another port on the same server by configuring private network CLB?
No. To access port a on server A (10.66.\*.101), the request can be forwarded to port b on server B (10.66.\*.102) via private network CLB. But it cannot be forwarded to port b on the same server A (10.66.\*.101).

### What is the real server weight?
You can specify the forwarding weight for each CVM instance in the real server pool, and the instance with a higher weight will be assigned with more access requests. You can configure the weights of real CVM instances based on their service capabilities and statuses.

If you have also enabled session persistence, access requests to real servers may not be exactly the same. We recommend you temporarily disable session persistence and check whether the problem persists.

### What is the difference between UDP and TCP protocols?
TCP is a connection-oriented protocol. Before receiving and sending data, TCP requires a reliable connection to be established with the other side. UDP is a connection-less protocol. It directly sends data packets without performing three-way handshake with the other side. UDP is suitable for scenarios that focus more on real-timeliness than reliability, such as video chat, real-time push of financial market information, DNS, and IoT.

### Does a real CVM instance need public network bandwidth? Will the bandwidth affect the CLB service?
No traffic or bandwidth fee is charged for CLB. Any public network traffic fees generated by CLB service will be charged by the CVM instances. We recommend you choose bill-by-traffic for public network bandwidth when purchasing the CVM instance and configure a reasonable peak bandwidth threshold, so that you do not need to keep track of the fluctuation in total CLB egress traffic. The traffic of internet web business fluctuates considerably and cannot be predicted accurately. When bill-by-bandwidth is selected, it is not cost-effective to purchase excessive bandwidth, yet packet loss may occur during business peaks if insufficient bandwidth is purchased.

### HTTP redirection in load forwarding
When you visit the website `http://example.com` via a browser, a redirection to the root directory is required for the server. When you visit the website `http://example.com/` via a browser, the server will directly return the default page of the website's root directory. Similarly, if `http://cloud.tencent.com/movie` is redirected to `http://cloud.tencent.com/movie/` through URL rewriting, entering `http://cloud.tencent.com/movie` will result in an additional URL rewriting process, leading to slight performance degradation and time consumption. However, if `http://cloud.tencent.com/product` is redirected to a page other than `http://cloud.tencent.com/product/` through URL rewriting, you need to consider whether to add "/" after the secondary URL.

In Tencent Cloud CLB, if the frontend and backend port numbers are different, "/" needs to be added after the secondary URL upon visit to the secondary page, so as to avoid port number changes after HTTP redirection and ensure normal page access.

Assume that in Layer-7 forwarding, port 80 on the CLB instance and port 8081 on the real server are listened. If the client accesses `http://www.example.com/movie`, the access request is forwarded to the real server via the CLB instance, and the server redirects the request to `http://www.example.com:8081/movie/ `(listener port is 8081). In this case, the client access fails (port error).

Therefore, we recommend you rewrite the access request to a secondary URL with "/", such as `http://www.example.com/movie/ `. This can avoid HTTP redirection, eliminate unnecessary judgment, and reduce unwanted load. If HTTP redirection is required, make sure that the CLB listener port is the same as that of the real server.

### Notes on compatible versions if the client and server have different HTTP versions
#### Forwarding Compatibility
- On the frontend (client), HTTP/1.0 and HTTP/1.1 and lower versions are supported.
- On the backend (server), Tencent Cloud uses the HTTP/1.0 protocol. HTTP/1.0 and HTTP/1.1 and lower versions are supported.

> HTTP/2 is only supported in HTTPS but not in HTTP, and backward compatibility is allowed on both the client and server.

#### Gzip Compatibility
- On the frontend (client), Gzip is supported by HTTP/1.0, HTTP/1.1 and lower versions. Additional configuration is not needed because mainstream browsers all support Gzip.
- On the backend (server), because HTTP/1.1 protocol is supported on the CVM instance over Tencent Cloud private network, you don not need to make any configuration, and can directly use HTTP/1.1 configured in Nginx by default to achieve compatibility.

> HTTP/2 is only supported in HTTPS, but Gzip can be used in any HTTP versions supported by Tencent Cloud.

### How to configure the security group of a CLB real server? How to configure the access blacklist?
#### Configuring the CLB security group
If security group rules have been configured for a real server, CLB instance may not be able to communicate with the server. Therefore, in Layer-4 and Layer-7 forwarding, we recommend you configure the security group of a real server as allowing all access requests. If the security group is enabled and access from any protocols or IP segments is denied by default, IPs of all clients need to be configured to the security group rules of the server IP.
For some malicious IPs, you can add them to the top rules of the security group to prevent them from accessing the real server. You can then allow access requests from all IPs (0.0.0.0) to the local service port, so normal clients can access the server. (Security group rules are arranged in priority order and matched from top to bottom.)

If health check has been configured for Layer-7 CLB forwarding in VPC, you must add the CLB VIP to the all access rule of the real server's security group. Otherwise, the health check may fail.

#### Configuring the access blacklist
If you need to configure a blacklist for some client IPs to deny their access requests, you can configure the security group associated with the cloud services. The security group rules need to be configured as follows:
> Follow the steps below strictly in the given order, otherwise the blacklist configuration may fail.

- Add the client IP and port to be rejected into the security group, and select the option in the “Policy” column to reject access from this IP.
- Add another security group rule after completing the above configuration  to allow access requests to the port from all IPs by default.
When the configuration completes, the security group rules are as follows:
```
clientA ip+port drop
clientB ip+port drop
0.0.0.0/0+port accept
```

For more information on the security group, please see [Real CVM Instance Security Group Configuration](https://intl.cloud.tencent.com/document/product/214/6157).


### Notes on high-frequency health checks
Health check packets are sent too frequently. Each health check packet is sent every 5 seconds as configured in the console, but the real server receives one or more health check requests in 1 second. The reasons are:

Highly frequent health check relates to the implementation mechanism of CLB health check. Suppose that 1 million requests from clients are distributed to 4 CLB real servers before being sent to CVM instances, and each CLB real server conducts health check separately. If the CLB instances are configured to send a health check request every 5 seconds, each real server will send a health check request every 5 seconds. This is why the CVM instance receives multiple health check requests. For example, if the cluster to which a CLB instance belongs has 8 servers, and each server sends a request every 5 seconds, then the CVM instance may receive 8 health check requests in 5 seconds.

The advantages of this implementation scheme are high efficiency, accurate check, and avoidance of mistaken removal. For example, if 1 of 8 physical servers in the CLB instance cluster fails, the other 7 servers can still forward traffic normally.

Therefore, if your real CVM instance is checked too frequently, you can configure the check interval to be much longer (for example, 15 seconds).


### Does CLB communicate with real servers over private network or public network?
CLB communicates with real servers over private network, even when the bound CVM instances have public IPs.

### Description of pinging CLB VIP 
Public network CLB VIP can be pinged. The requests of pinging the CLB VIP are responded by the CLB cluster and will not be forwarded to real servers. Private network CLB VIP cannot be pinged. We recommend you run telnet to test private network CLB.

### Private network loopback description
Private network CLB does not support the same private IP to be both client and server IPs. When the CLB instance reads the same client and server IPs, access will fail.
If your client needs to be used as a server, please bind at least 2 real servers. CLB supports automatic loopback. When client A accesses the CLB instance, it will automatically schedule the request to a real server other than client A.


### Streaming in scenarios where a client accesses the same port of a real server via different intermediate nodes
When a client accesses the same port of a real server via different intermediate nodes at the same time, streaming will occur. The scenarios are detailed below:
- A client accesses the same port of a real server via Layer-4 and Layer-7 listeners of the same CLB instance at the same time.
- A client accesses the same port of a real server via different listeners of different CLB instances at the same time.

Specific reason: CLB instance passes through the client IP to the real server, and `client_ip:client_port -> vip:vport -> rs_ip:rs_port` will change to `client_ip:client_port --> rs_ip:rs_port`.
You can add ports to the real server to avoid this problem.
