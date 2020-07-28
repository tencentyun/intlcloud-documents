After a Cloud Load Balancer (CLB) instance is created, you must configure a listener for it. The listener listens to incoming requests to the CLB instance and then routes them to Cloud Virtual Machine (CVM) instances according to the configured load balancing policy.

You must configure the following items when configuring a listener for a CLB instance:
1. Listening protocol and listening port. A listening port, also known as a frontend port, is used to receive and route requests to CVM instances.
2. Listening policies, such as load balancing and [session persistence](https://intl.cloud.tencent.com/document/product/214/6154) policies.
3. [Health check](https://intl.cloud.tencent.com/document/product/214/6097) policies.
4. CVM instances. Specify the IP address and service port for each CVM instance. A service port, also known as a backend port, is used by a CVM instance to receive and process requests.

## Supported protocol types
A CLB listener listens to incoming layer-4 and layer-7 requests to a CLB instance and routes them to CVM instances for processing. You can configure a layer-4 or layer-7 listener depending on whether you route requests for load balancing over a layer-4 or layer-7 protocol.
- Layer-4 protocols: transport layer protocols that receive and route requests to CVM instances by using a virtual IP (VIP) and port.
- Layer-7 protocols: application layer protocols that route requests based on application layer information such as the URL and HTTP header.

Tencent Cloud CLB supports request forwarding over the following protocols:
- TCP (transport layer)
- UDP (transport layer)
- TCP SSL (transport layer)
- HTTP (application layer)
- HTTPS (application layer)
>?
>- The TCP SSL listener feature is currently in beta test. To try it out, please [submit a ticket](https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=163&level1_name=%E8%AE%A1%E7%AE%97%E4%B8%8E%E7%BD%91%E7%BB%9C&level2_name=%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1%20LB) for application.
>- The TCP SSL listener feature is only available to public network CLB but not private network CLB or classic CLB.

## Layer-4 listener
| Protocol    | Description                    | Scenario                                 |
| ------- | ------------------------ | ---------------------------------------- |
|TCP|Connection-oriented and reliable transport layer protocol<li style="width:430px">The source and destination ends must perform a three-way handshake to establish a connection before data can be sent and received between them.</li><li style="width:430px">Session persistence based on the client IP (source IP) is supported.</li><li style="width:430px">The client IP can be read at the network layer.</li><li style="width:430px">The server can directly obtain the client IP.</li>|TCP is suitable for scenarios where high transfer reliability and data accuracy are required with a slight compromise on transfer speed. Typical scenarios include file transfer, sending and receiving emails, and remote logins.<br>For more information, please see [Configuring a TCP Listener](https://intl.cloud.tencent.com/document/product/214/32517).|
|UDP|Connectionless transport layer protocol<li style="width:430px">The source and destination ends do not establish a connection nor maintain the connection status.</li><li style="width:430px">Each UDP connection is point-to-point.</li><li style="width:430px">One-to-one, one-to-many, many-to-one, and many-to-many communication are supported.</li><li style="width:430px">Session persistence based on the client IP (source IP) is supported.</li><li style="width:430px">The server can directly obtain the client IP.</li>|UDP is suitable for scenarios where a high transfer speed is preferred over accuracy. Typical scenarios include instant messaging and online videos.<br>For more information, please see [Configuring a UDP Listener](https://intl.cloud.tencent.com/document/product/214/32518).|
|TCP SSL|Secure TCP protocol<li style="width:430px">TCP SSL listeners support configuring certificates to prevent unauthorized access requests.</li><li style="width:430px">Unified certificate management is provided for CLB to decrypt certificates.</li><li style="width:430px">One-way and mutual authentication are supported.</li><li style="width:430px">The server can directly obtain the client IP.</li>|TCP SSL is suitable for scenarios where high security is required for TCP and TCP-based custom protocols are supported.<br>For more information, please see [Configuring a TCP SSL Listener](https://intl.cloud.tencent.com/document/product/214/32519).|

If you configure a layer-4 listener, the CLB instance establishes a TCP connection with each CVM instance on the listening port and routes requests to CVM instances. During this process, the CLB instance forwards data in passthrough mode in an efficient manner without modifying any data packets.

## Layer-7 listener
| Protocol    | Description                   | Scenario                                 |
| ------- | --------------------- | ---------------------------------------- |
|HTTP|Application layer protocol<li style="width:424px">Forwarding based on the requested domain name and URL is supported.</li><li style="width:424px">Cookie-based session persistence is supported.</li>|HTTP is suitable for apps that need to identify request content, such as web apps and app services.<br>For more information, please see [Configuring an HTTP Listener](https://intl.cloud.tencent.com/document/product/214/32515).|
|HTTPS|Encrypted application layer protocol<li style="width:424px">Forwarding based on the requested domain name and URL is supported.</li><li style="width:424px">Cookie-based session persistence is supported.</li><li style="width:424px">Unified certificate management is provided for CLB to decrypt certificates.</li><li style="width:424px">One-way and mutual authentication are supported.</li>|HTTPS is suitable for HTTP apps that require encrypted transmission.<br>For more information, please see [Configuring an HTTPS Listener](https://intl.cloud.tencent.com/document/product/214/32516).|

## Port configuration
<table>
<thead>
<tr>
<th width="25%">Listening port (frontend port)</th>
<th width="25%">Service port (backend port)</th>
<th width="50%">Description</th>
</tr>
</thead>
<tbody><tr>
<td>Through the listening port, a CLB instance receives and routes requests to CVM instances for processing.<br><br>You can configure a listening port on ports 1–65535, such as port 21 (FTP), port 25 (SMTP), port 80 (HTTP), and port 443 (HTTPS).</td>
<td>Through the service port, a CVM instance receives and processes requests from a CLB instance.<br><br>On a CLB instance, one listening port can route requests to multiple ports of multiple CVM instances.</td>
<td>Note the following points when configuring a listening port on a CLB instance:<li>You can configure the same listening port for TCP and UDP. For example, listeners `TCP:80` and `UDP:80` can co-exist.</li><li>You cannot configure the same listening port for protocols of the same type. For example, TCP, TCP SSL, HTTP, and HTTPS are all TCP protocols. You cannot configure listeners `TCP:80` and `HTTP:80` at the same time.</li><br>On a CLB instance, you can configure the same service port for different CVM instances. You can also bind different listeners, for example, `HTTP:80` and `HTTPS:443` to the same port of a CVM instance.</td>
</tr>
</tbody></table>
