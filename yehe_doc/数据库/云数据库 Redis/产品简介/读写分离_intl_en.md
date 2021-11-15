
TencentDB for Redis supports read-write separation for business scenarios with more reads but less writes, which can well cope with read requests concentrating on frequently read data. It supports up to 1-master 5-replica mode to offer 5x read performance.

## How It Works
#### Memory Edition
- **Read/write separation principle**: TencentDB for Redis v4.0 and later in standard architecture or cluster architecture implement automatic read/write separation at the Proxy layer.
- **Read-write separation weight**: after read/write separation is enabled, Proxy will enable access by directing write requests to the master node only and distributing read requests evenly on replica nodes.
![](https://main.qcloudimg.com/raw/ebdf223270b8bfbc250036470e96e3a7.png)

#### CKV Edition
- **Read/write separation principle**: CKV Edition inherently supports the read/write separation architecture. All requests are distributed to nodes in clusters through the CLB gateway, and each node has the global slot routing information. After read/write separation is enabled for a node, if the read key hits it, the data will be read directly and returned; otherwise, the request will be forwarded to the corresponding node according to the routing information, which will read the data and return it to this node for final return to the client.
- **Read/write separation weight**: requests in the CKV Edition are distributed by CLB, so read and write weights are evenly distributed according to the quadruple of the TCP connection (source IP, source port, destination IP, and destination port).
![](https://main.qcloudimg.com/raw/3003faec1d3e55e4f3915532707a203d.png)
