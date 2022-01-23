
TencentDB for Redis Memory Edition (Standard Architecture) refers to the edition that supports zero or more replicas (a replica refers to a node that is not a master node), which is the most common Redis edition. It is compatible with protocols and commands of Redis v2.8, v4.0, and v5.0 and features data persistence and backup, making it suitable for scenarios where high data reliability and availability are required. A master node provides daily service access, while a replica node ensures high availability (HA). In case that the master node fails, the system will automatically switch to the replica node to guarantee business continuity.

Memory Edition (Standard Architecture) - one replica:
![](https://main.qcloudimg.com/raw/0bb5f79eea8c50f2817050211a0ed77f.jpg)

## Replica Description
Memory Edition (Standard Architecture) supports 0–5 replicas to meet the different requirements for availability and performance of your business in different scenarios. All replicas of Memory Edition (Standard Architecture) play a role in supporting system's high availability, so the more replicas, the higher the availability. If the number of replicas is greater than 1, read/write separation can be enabled to extend the read performance through replica nodes.
>? TencentDB for Redis 4.0 Memory Edition (Standard Architecture) supports 0–9 replicas in Beijing and Guangzhou regions or 0–5 replicas in other regions. Other versions support only 0–5 replicas.
>

**Definitions**:
- Master node: a Redis node that provides read and write capabilities.
- Replica node: a Redis node that provides high availability or read-only capability. A master node cannot be a replica node.

**Replica support**:
<table>
<tr><th >Instance Version</th><th >Supported Replicas</th><th >Read/Write Separation</th>  </tr>
<tr>      
<td>TencentDB for Redis 2.8 Memory Edition (Standard Architecture)</td><td>0–1</td><td>Unsupported</td></tr> 
<tr>
<td>TencentDB for Redis 4.0 Memory Edition (Standard Architecture)</td><td>1–5</td><td>Supported</td></tr> 
<tr>
<td>TencentDB for Redis 5.0 Memory Edition (Standard Architecture)</td><td>1–5</td><td>Supported</td></tr> 
</table>

**Zero-Replica instance**:
- Data may be lost when a node fails; therefore, do not use a zero-replica instance in data storage scenarios.
- A zero-replica instance is only suitable for pure cache scenarios. The application system can continue to run even in case of Redis failure, but as a zero-replica instance has only one database node, when the node fails, the system will start a new Redis process (which has no data), and after node failover is completed, the application needs to warm up the data again to avoid access pressure on the backend database.

**Read-Only replica (read/write separation)**:
- Supported editions: TencentDB for Redis 4.0 Memory Edition (Standard Architecture) and above instance. When the number of replicas is greater than 1, automatic read/write separation can be enabled to extend the read performance vertically. Up to 5 replica nodes can be supported.
- How it works: after read-only replica is enabled, write requests will be routed to the master node, while read requests will be routed to all replica nodes through the load balancing algorithm and no longer be processed by the master node. This read/write separation feature is provided by the Proxy component built in TencentDB for Redis.
- Enabling/Disabling: you can enable or disable read-only replica on the instance creation page in the TencentDB for Redis console or through TencentCloud API.

## Features
- **Service reliability (1–5 replicas)**
With a dual-server master/replica architecture, the master and replica nodes reside on different physical machines with the master node providing external access. You can perform data CRUD using the Redis command line or client. In case that the master node fails, the proprietary high availability (HA) system will automatically perform master/replica switch to ensure smooth operation of the business. 
- **Data reliability (1–5 replicas)**
The data persistence feature is enabled by default. Memory Edition (Standard Architecture) supports data backup. You can roll back or clone instances for backup sets to effectively cope with data maloperations and other issues.

## Usage Limits
- Memory Edition (Standard Architecture) supports 0.25–64 GB of storage capacity. For higher specifications, use Cluster Edition that supports up to 8 TB of capacity.
- Memory Edition (Standard Architecture) supports up to 100,000 QPS (SET command concurrencies). If you need a higher QPS, you can choose multi-replica read/write separation or use Redis Cluster Edition that supports tens of millions of QPS.
- As a zero-replica instance cannot ensure data reliability, and the business data needs to be warmed up after a node failure, if your business requires high data availability, you are not recommended to use zero-replica instances; instead, you can choose single-replica or multi-replica instances.

## Command Compatibility
For more information on the supported commands, see [Command Compatibility](https://intl.cloud.tencent.com/document/product/239/31958).

​    
