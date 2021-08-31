## Obtaining Real Client IPs Through TOA
When an acceleration connection forwards the data packet, SNAT and DNAT will be performed on the packet; that is, the source and destination addresses of the data packet will be modified. The packet source address seen by the origin server will be the forwarding IP address of the acceleration connection, rather than the real client IP. To pass the client IP to the server, the acceleration connection will include the client IP and port in the custom `tcp option` field when forwarding the packet, as shown below:
```
#define TCPOPT_ADDR  200    
#define TCPOLEN_ADDR 8      /* |opcode|size|ip+port| = 1 + 1 + 6 */

/*
 * insert client ip in tcp option, now only support IPV4,
 * must be 4 bytes alignment.
 */
struct ip_vs_tcpo_addr {
    __u8 opcode;
    __u8 opsize;
    __u16 port;
    __u32 addr;
};
```

## Obtaining Real Client IPs Through Proxy Protocol
Proxy Protocol facilitates the transmission of client information (such as protocol stack, source IP, destination IP, source port, and destination port, etc.) by adding a header to the TCP, which is ideal for cases where network condition is complex and client IPs are required. During this process, the proxy inserts a data packet containing the original connection quadruple information into the connection after the three-way handshake.

To obtain client IPs using the Proxy Protocol method, you need to configure it in the console first. It can only be configured for listeners with TCP. After the acceleration service is connected with the origin server, the Proxy Protocol text will be inserted into the first-transmitted `payload` packet.

Currently, Nginx and HAProxy support Proxy Protocol. For the Proxy Protocol configuration on Nginx, you only need to add `proxy_protocol` after the `listen` command in the `server` chunk.
```
http {
    #...
    server {
        listen 80   proxy_protocol;
        listen 443  ssl proxy_protocol;
        #...
    }
}
```

 For programs that do not support Proxy Protocol, after the TCP connection is set up, you need to parse the Proxy Protocol text string as follows to obtain client IPs:
 ```
 PROXY TCP4 1.1.1.2 2.2.2.2 12345 80\r\n
 ```
