When an acceleration connection forwards the data packet, SNAT and DNAT will be performed on the packet, that is, the source and destination addresses of the data packet will be modified. The packet source address seen by the origin server will be the forwarding IP address of the acceleration connection, rather than the real client IP. To pass the client IP to the server, the acceleration connection will include the client IP and port in the custom `tcp option` field when forwarding the packet, as shown below:
```
#define TCPOPT_ADDR  200    
#define TCPOLEN_ADDR 8      /* |opcode|size|ip+port| = 1 + 1 + 6 */

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
