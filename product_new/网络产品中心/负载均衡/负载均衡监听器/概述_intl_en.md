After creating a CLB instance, you need to configure a listener to it. The listener listens to requests on the instance and routes traffic to real servers based on the load balancing policy.

You need to configure the following for a CLB listener:
1. Listener protocol and listener port. A CLB listener port, or frontend port, is used to receive and route requests to real servers.
2. Listening policies, such as load balancing policy and [session persistence](https://intl.cloud.tencent.com/document/product/214/6154).
3. [Health check](https://intl.cloud.tencent.com/document/product/214/6097) policies.
4. Bind real server by selecting its IP and port. A service port, or backend port, is used by the real server to receive requests.

## Supported protocol types
A CLB listener can listen to Layer-4 and Layer-7 requests on a CLB instance and route them to real servers for processing. The main difference between Layer-4 CLB and Layer-7 CLB is whether Layer-4 or Layer-7 protocol is used to forward traffic for load balancing of user requests.
- Layer-4 protocols: transport layer protocols that receive requests and forward traffic to the real server mainly via VIP + port.
- Layer-7 protocols: application layer protocols that distribute traffic based on application layer information such as URL and HTTP header.

Tencent Cloud CLB supports request forwarding over the following protocols:
- TCP (transport layer)
- UDP (transport layer)
- TCP SSL (transport layer)
- HTTP (application layer)
- HTTPS (application layer)
> The TCP SSL listener feature is currently in beta and only available to public network CLB, not private network CLB or Classic CLB. To use it, please [submit a ticket](https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=163&level1_name=%E8%AE%A1%E7%AE%97%E4%B8%8E%E7%BD%91%E7%BB%9C&level2_name=%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1%20LB) for application.

## Layer-4 Listener
| Protocol    | Description                    | Scenarios                                 |
| ------- | ------------------------ | ---------------------------------------- |
| TCP | Connection-oriented and reliable transport layer protocol<li style="width:430px">The source and destination ends must perform 3 handshakes to establish a connection before data transfer</li><li style="width:430px">Session persistence based on client IP (source IP) is supported</li><li style="width:430px">Client IP can be found at the network layer</li><li  style="width:430px">The server can directly obtain client IP</li>| TCP is suitable for scenarios that have high requirements for reliability and data accuracy but relatively low requirements for transfer speed, such as file transfer, receiving and sending emails, and remote login.<br>For more information, please see [Configuring TCP Listener](https://intl.cloud.tencent.com/document/product/214/32517).|
| UDP | Connection-less transport layer<li style="width:430px">The source and destination ends do not establish a connection, nor maintain the connection status</li><li style="width:430px">Each UDP connection is point-to-point</li><li style="width:430px">One-to-one, one-to-many, many-to-one and many-to-many communications are supported</li><li style="width:430px">Session persistence based on client IP (source IP) is supported</li><li style="width:430px">The server can directly obtain client IP</li>|UDP is suitable for scenarios that have high requirements for transfer speed but relatively low requirements for accuracy, such as instant messaging and online videos.<br>For more information, please see [Configuring UDP Listener](https://intl.cloud.tencent.com/document/product/214/32518).|
| TCP SSL | Secure TCP <li style="width:430px">TCP SSL listeners support configuration of certificates to prevent unauthorized access requests</li><li style="width:430px">Unified certificate management is provided for CLB to implement decryption</li><li style="width:430px">Unidirectional and bidirectional authentications are supported</li><li style="width:430px">The server can directly obtain client IP</li>| TCP SSL is suitable for scenarios that have high requirements for security when TCP protocol is used and supports TCP-based custom protocols.<br>For more information, please see [Configuring TCP SSL Listener](https://intl.cloud.tencent.com/document/product/214/32519).|

If you use Layer-4 listener (i.e., Layer-4 protocol forwarding), CLB instance will establish a TCP connection with the real server on the listener port, and directly forward requests to the real server. This process does not modify any data packets (in passthrough mode) and has high forwarding efficiency.

## Layer-7 Listener
| Protocol    | Description                   | Scenarios                                 |
| ------- | --------------------- | ---------------------------------------- |
|HTTP|Application layer protocol<li style="width:424px">Forwarding based on the request domain name and URL is supported</li><li style="width:424px">Cookie-based session persistence is supported</li>|HTTP is suitable for applications that need to identify request content, such as web applications and app services.<br>For more information, please see [Configuring HTTP Listener](https://intl.cloud.tencent.com/document/product/214/32515).|
|HTTPS|Encrypted application layer protocol<li style="width:424px">Forwarding based on the request domain name and URL is supported</li><li style="width:424px">Cookie-based session persistence is supported</li><li style="width:424px">Unified certificate management is provided for CLB to implement decryption</li><li style="width:424px">Unidirectional and bidirectional authentications are supported</li>|HTTPS is suitable for HTTP applications that need encrypted transmission.<br>For more information, please see [Configuring HTTPS Listener](https://intl.cloud.tencent.com/document/product/214/32516).|

## Port Configuration
<table>
<thead>
<tr>
<th width="25%">Listener port (frontend port)</th>
<th width="25%">Service port (backend port)</th>
<th width="50%">Description</th>
</tr>
</thead>
<tbody><tr>
<td>Through the listener port, CLB instance receives and forwards requests to real servers for load balancing.<br><br>You can configure CLB for ports 1–65535, such as 21 (FTP), 25 (SMTP), 80 (HTTP), and 443 (HTTPS).</td>
<td>A service port provides services for CVM, receives and processes CLB traffic.<br><br>On a CLB instance, one listener port can forward traffic to multiple ports of multiple CVMs.</td>
<td>On a CLB instance, <li>the listener port must be unique. For example, `TCP:80` and `HTTP:80` listeners cannot co-exist.</li><li>Only ports of TCP and UDP protocols can co-exist. For example, you can create `TCP:80` and `UDP:80` listeners at the same time.</li><br>The service ports can repeat on a CLB instance. For example, both `HTTP:80` and `HTTPS:443` listeners can be bound to the same port of a CVM.</td>
</tr>
</tbody></table>
