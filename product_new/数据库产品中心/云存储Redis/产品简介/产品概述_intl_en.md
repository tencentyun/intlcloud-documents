TencentDB for Redis is a cache database provided by Tencent Cloud based on the Redis protocol that features high availability, reliability, and flexibility. Compatible with Redis 2.8 and 4.0 protocols and available in both Standard and Cluster Editions, it supports up to 4 TB of storage capacity and tens of millions of concurrent requests, meeting the needs of different scenarios such as caching, storage, and computing.

## Features
- Master/slave hot backup: Master/slave hot backup, automatic failure monitoring, and automatic disaster recovery are supported.
- Data backup: Both Standard and Cluster Editions support data persistence and are capable of daily cold backup and self-service rollback.
- Elastic scaling: Instance capacity can be flexibly expanded or reduced. Plus, the nodes and replicas in the Cluster Edition can be scaled in or out.
- Network protection: VPC is supported for improved cache security.
- Distributed storage: Your data is distributed across multiple physical machines, helping you get rid of standalone capacity and resource constraints.

## Product Editions
TencentDB for Redis is available in both Standard and Cluster Editions for your choice based on your actual performance requirements. The Standard Edition features higher compatibility, but its performance is restrained to one single node. The Cluster Edition is not as compatible as the Standard Edition, but it can be scaled out to support up to millions of concurrent requests.

<table>  
 <tr>  
 <th style="width: 100px;">Instance Type</th>  
 <th style="width: 200px;">Number of Replicas</th>  
 <th style="width: 100px;">Read-write Separation</th>  
 <th>Description</th>  
 </tr>  
 <tr>  
 <td>Redis Standard Edition</td>  
 <td >0-5</td>  
  <td >Supported</td>  
   <td >Compatible with Redis 2.8 and 4.0 protocols. The 2.8 Standard Edition supports zero-replica deployment and features extremely high cost effectiveness, making it suitable for pure cache scenarios. The 4.0 Standard Edition supports smooth capacity and replica scaling with no service interruptions. <br>Master/slave hot backup, real-time data sync, and failover in a matter of seconds are supported.
   </td>  
 </tr>  
 <tr>  
  <tr>  
 <td>Redis Cluster Edition</td>  
 <td >1-5</td>  
  <td >Supported</td>  
   <td >Compatible with Redis 4.0 protocol. The cluster architecture supports 3-128 shards with a maximum of 4 TB storage capacity and tens of millions of QPS. <br>Master/slave hot backup, real-time data sync, and failover in a matter of seconds are supported.</td>  
 </tr>  
</table>  
