Proxy Protocol facilitates the transmission of client information (such as protocol stack, source IP, destination IP, source port, and destination port, etc.) by adding a header to the TCP, which is ideal for cases where network condition is complex and client IPs are required. During this process, the proxy inserts a data packet containing the original connection quadruple information into the connection after the three-way handshake.

 

To obtain client IPs using the Proxy Protocol method, you need to configure and enable it in the console first. It can only be configured for listeners with TCP. After the acceleration service is connected with the origin server, the Proxy Protocol text will be inserted into the first-transmitted `payload` packet.
