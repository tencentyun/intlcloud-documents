Redis Standard Edition refers to edition that supports zero or more replicas (a replica refers to a node that is not a master node) and is the most common Redis edition. It is compatible with protocols and commands of Redis v2.8 and Redis v4.0 and features data persistence and backup, making it suitable for scenarios where high data reliability and availability are required. A master node provides daily service access, while a slave node ensures high availability (HA). In case that the master node fails, the system will automatically switch to the slave node to guarantee business continuity.

Redis Standard Edition (1 replica):
![](https://main.qcloudimg.com/raw/1a6f6a699f6b3aefcec20f21b61c72b0.png)

## Replica Descriptions
Redis Standard Edition supports 0-5 replicas to meet the different requirements for availability and performance of your business in different scenarios. All replicas of the Standard Edition play a role in supporting system’s high availability, so the more replicas, the higher the availability. If the number of replicas is greater than 1, read-write separation can be enabled to extend the read performance through replica nodes.

**Definitions**:
- Master node: A Redis node that provides read and write capabilities.
- Replica node: A Redis node that provides high availability or read-only capability. A master node cannot be a replica node.

**Replica support**:
<table>
     <tr>
         <th >Instance Edition</th>  
         <th >Supported Replica Quantity</th>  
         <th >Read-write Separation</th>  
     </tr>
  <tr>      
         <td >2.8 Standard Edition</td>   
      <td>0-1</td>   
      <td>Not supported</td>   
     </tr> 
  <tr>
      <td>4.0 Standard Edition</td>   
      <td>1-5</td>   
      <td>Supported</td>
     </tr> 
</table>

**Zero-replica instance**:
- Data may be lost when a node fails. Do not use a zero-replica instance in data storage scenarios.
- Only for pure cache scenarios. The application system can continue to run even in the case of Redis failure. A zero-replica instance has only one database node, and when the node fails, the system will start a new Redis process (which has no data). After the node failover is completed, the application needs to warm up the data again to avoid access pressure on the backend database.

**Read-only replica (read-write separation)**:
- Supported editions: 4.0 Standard Edition instance. When the number of replicas is greater than 1, automatic read-write separation can be enabled to extend the read performance vertically. Up to 5 replica nodes can be supported.
- How it works: After read-only replica is enabled, write requests will be routed to the master node, while read requests will be routed to all replica nodes through the load balancing algorithm and no longer be processed by the master node. This read-write separation feature is provided by the Proxy component built in TencentDB for Redis.
- Enabling/disabling: You can enable or disable read-only replica on the instance creation page in the TencentDB for Redis Console or through TencentCloud API.

## Features
- **Service reliability (1-5 replicas)**
With a dual-server master/slave architecture, the master and slave nodes reside on different physical machines with the master node providing external access. You can perform data CRUD using the Redis command line or client. In case that the master node fails, the proprietary HA system will automatically perform master/slave switch to ensure smooth operation of the business. 
- **Data reliability (1-5 replicas)**
The data persistence feature is enabled by default. The Standard Edition supports data backup. You can roll back or clone instances for backup sets to effectively cope with data misoperations and other issues.

## Use Limits
- Redis Standard Edition supports 0.25-60 GB of storage capacity. For higher specifications, please use the Cluster Edition which supports up to 4 TB of capacity.
- Redis Standard Edition supports up to 100,000 QPS (set command concurrencies). If you need a higher QPS, you can choose multi-replica read-write separation or use the Redis Cluster Edition that supports tens of millions of QPS.
- As a zero-replica instance cannot ensure data reliability, and the business data needs to be warmed up after a node failure, if your business requires high data availability, you are not recommended to use zero-replica instances; instead, you can choose single-replica or multi-replica instances.

For more information on the supported commands, see [Compatibility Notes](https://intl.cloud.tencent.com/document/product/239/31958).


