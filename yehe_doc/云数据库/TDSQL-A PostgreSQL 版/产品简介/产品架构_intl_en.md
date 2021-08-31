TDSQL-A for PostgreSQL uses a shared-nothing architecture where the nodes are independent from each other and process their own data separately. The processing results can be aggregated at the upper layer or transferred among the nodes, and the processing units communicate with each other over network protocols, offering better parallel processing and scaling capabilities. This means that you can deploy a TDSQL-A for PostgreSQL database cluster simply on x86 or ARM servers. The architecture is as follows:
![](https://main.qcloudimg.com/raw/803b91dc7739cdfadca733ee8bfaf349.png)

Each module is as detailed below:
- Coordinator (CN): it provides APIs and is responsible for data distribution, query planning, pairing of multiple node locations, etc. Each node provides the same database views. In terms of functionality, it stores only the global metadata of the system rather than actual business data.
- Datanode (DN): it processes and stores the metadata related to itself and shards of the business data. In terms of functionality, it executes the execution requests distributed by the CN. 
- Global Transaction Manager (GTM): it manages cluster transaction information and global cluster objects such as sequences.
- Data Forward Bus: it consists of FNs on servers in the cluster. The main purpose of using FNs is to reduce the number of connections created during data exchange between DNs and between CNs and DNs, thus ensuring that connection will not become a bottleneck for large-scale clusters.

In this architecture, a cluster has the following capabilities:
- Multi-Site active-active/multi-primary: all CNs provide the same cluster views, so that you can write through any of them. The cluster topology is imperceptible to the business. 
- Read/Write scaling: data is sharded onto different DNs, so the cluster read/write capabilities can be scaled as the cluster size increases.
- Cluster write consistency: the write transactions of the business that occur on one CN node will be consistently presented on other CN nodes, as if these transactions occurred on them.
- Transparent cluster architecture: the data is distributed on different DNs. During data query, the business does not need to care about on which nodes the data resides.

The shared-nothing architecture of TDSQL-A for PostgreSQL makes business access easier and lowers the threshold for business access.
