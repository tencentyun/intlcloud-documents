TencentDB for Redis is a cache database provided by Tencent Cloud based on the Redis protocol that features high availability, reliability, and flexibility. TencentDB for Redis is compatible with Redis 2.8, 4.0, and 5.0 protocols and available in standard and cluster architectures.
it supports up to 4 TB of storage capacity and tens of millions of concurrent requests, meeting the needs of different scenarios such as caching, storage, and computing.

## Product Features
- Master/slave hot backup: master/slave hot backup, automatic failure monitoring, and automatic disaster recovery are supported.
- Data backup: standard and cluster architectures support data persistence, providing cold backup and rollbdack.

- Elastic scaling: instance capacity can be flexibly expanded or reduced. Plus, the nodes and replicas can be scaled in or out.
- Network protection: VPC is supported for improved cache security.
- Distributed storage: your data is distributed across multiple physical machines, helping you get rid of standalone capacity and resource constraints.

## Product Editions
TencentDB for Redis is available in standard and cluster architectures.You can select the appropriate one based on actual needs. The standard architecture features higher compatibility, but its performance is restrained to a single node. The cluster architecture has lower compatibility, but its performance can be horizontally scaled to support up to tens of millions of concurrent requests.


<table>  
 <tr>  
 <th style="width: 100px;">Instance Type</th>  
 <th style="width: 200px;">Number of Replicas</th>  
 <th style="width: 100px;">Read/write Separation</th>  
 <th>Description</th>  
 </tr>  
 <tr>  
 <td>Memory Edition (standard architecture)</td>  
 <td >0-5</td>  
  <td >Supported</td>  
   <td >Compatible with Redis 2.8, 4.0, and 5.0 protocols. The 2.8 Edition offers Redis shards with no replica and is a cost-effective solution for pure cache use cases. The 4.0/5.0 Edition offers Redis shards with 1–5 replicas. The capacity and replica can be scaled up seamlessly with no service interruption.
   </td>  
 </tr>  
 <tr>  
  <tr>  
 <td>Memory Edition (cluster architecture)</td>  
 <td >1-5</td>  
  <td >Supported</td>  
   <td >Compatible with Redis 4.0 and 5.0 protocols. The cluster architecture supports 3–128 shards with a maximum of 4 TB storage capacity and tens of millions of QPS. <br>Master/slave hot backup, real-time data synchronization, and failover in a matter of seconds are supported.</td>  
 </tr>  
</table>  
