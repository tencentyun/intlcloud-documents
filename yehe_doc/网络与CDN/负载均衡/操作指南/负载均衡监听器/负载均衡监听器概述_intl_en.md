After creating a CLB instance, you need to configure a listener to it. The listener listens to requests on the instance and routes traffic to real servers based on the load balancing policy.

You need to configure a CLB listener with the following items:
1. Listening protocol and port. The listening port, or frontend port, is used to receive and forward requests to real servers.
2. Listening policies, such as load balancing policy and [session persistence](https://intl.cloud.tencent.com/document/product/214/6154).
3. [Health check](https://intl.cloud.tencent.com/document/product/214/6097) policies.
4. Real server. Bind a real server by selecting its IP and port. A service port, or backend port, is used by the real server to receive requests.

## Supported Protocol Types
A CLB listener can listen to layer-4 and layer-7 requests on a CLB instance and route them to real servers for processing. The main difference between layer-4 CLB and layer-7 CLB is whether layer-4 or layer-7 protocol is used to forward traffic for load balancing of user requests. For example, layer-4 load balancing is performed for requests over TCP, UDP, and other layer-4 protocols, while layer-7 load balancing is performed for requests over HTTP, HTTPS, and other layer-7 protocols.
- Layer-4 protocols: transport layer protocols that receive requests and forward traffic to the real server mainly via VIP and port.
- Layer-7 protocols: application layer protocols that distribute traffic based on application layer information such as URL and HTTP header.

If you use a layer-4 listener (i.e., layer-4 protocol forwarding), the CLB instance will establish a TCP connection with the real server on the listening port, and directly forward requests to the real server. This process does not modify any data packets (in pass-through mode) and has high forwarding efficiency.

Tencent Cloud CLB supports request forwarding over the following protocols:
- TCP (transport layer)
- UDP (transport layer)
- TCP SSL (transport layer)
- HTTP (application layer)
- HTTPS (application layer)
>? TCP SSL listeners currently support public network CLB instances but not private network or classic CLB instances.


<table>
<thead>
<tr>
<th width="12%">Protocol Type</th>
<th width="12%">Protocol</th>
<th width="40%">Description</th>
<th width="36%">Use Case</th>
</tr>
<tr>
<td rowspan="3">Layer-4 protocol</td>
<td>TCP</td>
<td>Connection-oriented and reliable transport layer protocol:<li>The source and destination ends must perform a three-way handshake to establish a connection before data transfer.</li><li>Client IP (source IP)-based session persistence is supported.</li><li>The client IP can be found at the network layer.</li><li>The server can directly obtain the client IP.</li></td>
<td>It is suitable for scenarios that have high requirements for reliability and data accuracy but relatively low requirements for transfer speed, such as file transfer, receiving and sending emails, and remote login. <br>For more information, see <a href="https://intl.cloud.tencent.com/document/product/214/32517">Configuring a TCP Listener</a>.</td>
</tr>
<tr>
<td>UDP</td>
<td>Connection-less transport layer protocol:<li>The source and destination ends do not establish a connection, nor maintain the connection status. </li><li>Each UDP connection is point-to-point. </li><li>One-to-one, one-to-many, many-to-one, and many-to-many communications are supported.</li><li>Client IP (source IP)-based session persistence is supported.</li><li>The server can directly obtain the client IP.</li></td>
<td>It is suitable for scenarios that have high requirements for transfer efficiency but relatively low requirements for accuracy, such as instant messaging and online videos. <br>For more information, see <a href="https://intl.cloud.tencent.com/document/product/214/32518">Configuring a UDP Listener</a>.</td>
</tr>
<tr>
<td>TCP SSL</td>
<td>Secure TCP: <li>TCP SSL listeners support configuring certificates to prevent unauthorized access requests.</li><li>Unified certificate management is provided for CLB to implement decryption.</li><li>One-way and mutual authentications are supported.</li><li>The server can directly obtain the client IP.</li></td>
<td>It is suitable for scenarios that have high requirements for security when TCP is used and supports TCP-based custom protocols. <br>For more information, see <a href="https://intl.cloud.tencent.com/document/product/214/32519">Configuring a TCP SSL Listener</a>.</td>
</tr>
<tr>
<td rowspan="2">Layer-7 protocol</td>
<td>HTTP</td>
<td>Application layer protocol: <li>Forwarding based on requested domain name and URL is supported. </li><li>Cookie-based session persistence is supported.</li></td>
<td>It is suitable for applications where request contents need to be identified, such as web applications, mobile apps, and so on. <br>For more information, see <a href="https://intl.cloud.tencent.com/document/product/214/32515">Configuring an HTTP Listener</a>.</td>
</tr>
<tr>
<td>HTTPS</td>
<td>Encrypted application layer protocol:<li>Forwarding based on requested domain name and URL is supported.</li><li>Cookie-based session persistence is supported.</li><li>Unified certificate management is provided for CLB to implement decryption.</li><li>One-way and mutual authentications are supported.</li></td>
<td>It is suitable for HTTP applications requiring encrypted transmission.<br>For more information, see <a href="https://intl.cloud.tencent.com/document/product/214/32516">Configuring an HTTPS Listener</a>.</td>
</tr>
</tbody></table>

## Port Configuration
<table>
<thead>
<tr>
<th width="16%">Port Type</th>
<th>Description</th>
<th width="50%">Restrictions</th>
</tr>
</thead>
<tbody><tr>
<td>Listening port (frontend port)</td>
<td>Listening ports are used by CLB instances to receive and forward requests to real servers<br/>You can configure CLB instances for ports 1 to 65535, such as port 21 (FTP), 25 (SMTP), 80 (HTTP), and 443 (HTTPS), etc.</td>
<td><ul>On one CLB instance:<li>Listening ports of UDP can be used for TCP; e.g., a `TCP:80` listener and a `UDP:80` listener can coexist.</li><li>Listening ports must be unique for the same type of protocol. TCP, TCP SSL, HTTP, and HTTPS are of TCP, so for example, a `TCP:80` listener and an `HTTP:80` listener cannot coexist.</li></ul></td>
</tr>
<tr>
<td>Service port (backend port)</td>
<td>Service ports are used by CVM instances to provide services, receive and process traffic from CLB instances.<br/>On one CLB instance, one listening port can forward traffic to ports of multiple CVM instances.</td>
<td><ul>On one CLB instance:<li>Service ports of different listening protocols do not need to be unique; e.g., the listener `HTTP:80` and `HTTPS:443` can be both bound to the same port of a CVM instance.</li><li>When using the same listening protocol, each backend service port can be bound to one listener only, that is, the quadruple (VIP, listening protocol, private IP of real server, and backend service port) must be unique.</li></ul></td>
</tr>
</tbody></table>
