TencentDB for Redis supports read/write separation for business scenarios with more reads but less writes, which can well cope with read requests concentrating on frequently read data. It supports up to 1-master 5-slave mode to offer 5x read performance.

## How It Works
#### Redis (Community Edition)
- **Read/write separation principle**: Redis Standard Edition and Cluster Edition v4.0 and above implement automatic read/write separation at the Proxy layer.
- **Read/write separation weight**: after read/write separation is enabled, Proxy will enable access by directing write requests to the master node only and distributing read requests evenly on slave nodes.

#### Redis (CKV Edition)
- **Read/write separation principle**: CKV Edition inherently supports the read/write separation architecture. All requests are distributed to nodes in clusters through the CLB gateway, and each node has the global slot routing information. After read/write separation is enabled for a node, if the read key hits it, the data will be read directly and returned; otherwise, the request will be forwarded to the corresponding node according to the routing information, which will read the data and return it to this node for final return to the client.
- **Read/write separation weight**: requests in the CKV Edition are distributed by CLB, so read and write weights are evenly distributed according to the quadruple of the TCP connection (source IP, source port, destination IP, and destination port).
