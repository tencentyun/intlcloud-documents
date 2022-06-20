To ensure execution stability, this kernel module allows you to monitor status. After inserting the `toa.ko` kernel module, you can monitor the TOA working status in either of the following ways.

Run the following command to check the TOA metrics.
```
cat /proc/net/toa_stats
```
![](https://qcloudimg.tencent-cloud.cn/raw/7c6cc32285f861d87f3d4ecd3ae5d9a9.png)

The monitoring metrics are described as follows:

| Metric             | Description                                                         |
| -------------------- | ------------------------------------------------------------ |
| syn_recv_sock_toa    | Number of sockets that carry TOA information                                |
| syn_recv_sock_no_toa | Number of sockets that do not carry TOA information                            |
| getname_toa_ok       | This count increases when you call `getsockopt` and get the source IP successfully or when you call `accept` to receive client requests. |
| getname_toa_mismatch | This count increases when you call `getsockopt` and get the source IP that does not match the required type. For example, a client connection contains an IPv4 source IP address whereas you get an IPv6 address, the count will increase. |
| getname_toa_empty    | This count increases when the `getsockopt` function is called in a client file descriptor that does not contain TOA. |
| ip6_address_alloc    | It allocates space to store the information when the TOA kernel gets the source IP and source port saved in the TCP data packet. |
| ip6_address_free     | When the connection is released, TOA will release the memory previously used to save the source IP and source port. If all connections are closed, the total count of `ip6_address_alloc` for each CPU should be equal to the count of this metric.|