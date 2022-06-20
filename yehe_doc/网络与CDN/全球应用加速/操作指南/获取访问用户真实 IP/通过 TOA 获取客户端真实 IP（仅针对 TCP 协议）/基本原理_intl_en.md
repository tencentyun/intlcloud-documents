When an acceleration connection forwards the data packet, SNAT and DNAT will be performed on the packet; that is, the source and destination addresses of the data packet will be modified. The packet source address seen by the origin server will be the forwarding IP address of the acceleration connection, rather than the real client IP. To pass the client IP to the server, the acceleration connection will include the client IP and port in the custom `tcp option` field when forwarding the packet, as shown below:


```
#define TCPOPT_ADDR  200
#define TCPOLEN_ADDR 8   /* |opcode|size|ip+port| = 1 + 1 + 6 */

/*
	* insert client ip in tcp option,now only support IPV4,
	* must be 4 bytes alignment.
	*/
	
	struct ip_vs_tcpo_addr{
	    __u8 opcode;
			__u8 opsize;
			__u16 port;
			__u32 addr;
	};
```


After the Linux kernel has received the ACK packet of three-way handshake while listening the socket, its status is changed from SYN_REVC to TCP_ESTABLISHED. In this case, the kernel calls the `tcp_v4_syn_recv_sock` function. The Hook function `tcp_v4_syn_recv_sock_toa` calls the original `tcp_v4_syn_recv_sock` function, then extracts `TOA OPTION` from the `TCP OPTION` by calling the `get_toa_data` function, and saves it in the `sk_user_data` field. After the above call is completed, the kernel calls `inet_getname_toa hook inet_getname` to obtain the source IP and port. It first calls the original `inet_getname`, and check whether the `sk_user_data` field is empty. If the real IP and port can be extracted from this field, then replace the returned values of `inet_getname` with these two values.
The server program calls `getpeername` in the user mode, and the client's original IP and port are returned.
