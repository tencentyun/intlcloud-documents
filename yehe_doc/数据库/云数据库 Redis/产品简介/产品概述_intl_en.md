TencentDB for Redis is a cache database provided by Tencent Cloud based on the Redis protocol that features high availability, reliability, and flexibility. Compatible with Redis 2.8, 4.0, and 5.0 protocols and available in both standard and cluster architectures, it supports up to 4 TB of storage capacity and tens of millions of concurrent requests, meeting the needs of different scenarios such as caching, storage, and computing.


## Product Features
- Master/replica hot backup: master/replica hot backup, automatic failure monitoring, and automatic disaster recovery are supported.
- Data backup: standard and cluster architectures support data persistence, daily cold backup, and manual rollback.
- Elastic scaling: instance capacity, nodes, and replicas can be flexibly expanded or reduced.
- Network protection: VPC is supported for improved cache security.
- Distributed storage: your data is distributed across multiple physical machines, helping you get rid of standalone capacity and resource constraints.

## Product Editions
TencentDB for Redis is available in both standard and cluster architectures for your choice based on your actual performance requirements. The standard architecture features higher compatibility, but its performance is restrained to one single node. The cluster architecture is not as compatible as the standard one, but it can be scaled out to support up to tens of millions of concurrent requests.
<table>  
<tr><th>Instance Type</th><th>Replica Quantity</th><th>Read/write Separation</th><th>Description</th>  </tr>  
<tr>  
<td>Memory Edition (standard architecture)</td><td >0 to 5</td><td >Supported</td><td >This edition is compatible with Redis 2.8, 4.0, and 5.0 protocols. The v2.8 supports 0 replicas and is cost-effective when it's only used as cache. The v4.0 or v5.0 supports 1 to 5 replicas, and the instance capacity and replicas can be scaled with no service interruption.<br>This edition supports master/replica hot backup, real-time data synchronization, and failover within seconds.</td></tr>  
<tr>  
<td>Memory Edition (cluster architecture)</td><td >1 to 5</td><td >Supported</td><td >This edition is compatible with Redis 4.0 and 5.0 protocols. The cluster architecture supports 3 to 128 shards with a maximum of 4 TB storage capacity and tens of millions of QPS. <br>This edition supports master/replica hot backup, real-time data synchronization, and failover within seconds.</td></tr>  
</table>  
