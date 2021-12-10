After receiving a three-way handshake ACK packet from the listening socket, the Linux kernel change its status from SYN_REVC to TCP_ESTABLISHED. The kernel calls the tcp_v4_syn_recv_sock function.
The hook function `tcp_v4_syn_recv_sock_toa` calls the original `tcp_v4_syn_recv_sock` function first, then gets TOA OPTION from TCP OPTION by calling the `get_toa_data` function, and saves it in the sk_user_data field.

After the above call is completed, the kernel calls `inet_getname_toa hook inet_getname` to obtain the source IP and port. It first calls the original `inet_getname`, and checks whether the `sk_user_data` field is empty. If the real IP and port can be retrieved from this field, the return values of inet_getname will be replaced with these two values.

The server program calls getpeername in user mode, and the original IP and port of the client will be returned.
