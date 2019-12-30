The event center of Tencent Cloud Cloud Monitoring (CM) currently provides the following monitoring information for product events:

## CVM

| Event Name | Event Type | Dimension | Recoverable | Description | Troubleshooting Method |
| ----------- | ----------------------------------- | ---- | -------- | ------ | ---------------------------------------- | ---------------------------------------- |
| GuestCoreError | Exception event | CVM instance | No | A fatal error in the operating system kernel caused by an operating system kernel bug or driver issue | 1. Check whether any other kernel drivers are loaded to the system in addition to the kernel drivers provided by the kernel. Try not to load these drivers and then observe the system operating status. 2. View the bug report in release version of the kernel and operating system and try to upgrade the kernel to solve the problem. 3. In Tencent Cloud CVMs, kdump is enabled by default. When panic occurs, system memory dump information is generated in the /var/crash directory. You can use the crash tool for analysis |
| GuestOom | Exception event | CVM instance | No | The system memory is overloaded | 1. Check whether the memory capacity configured in the system meets the memory requirements of the service. If additional memory capacity is required, we recommend that you upgrade the CVM memory configuration. 2. According to system logs (such as dmesg and /var/log/messages), view the processes killed when OOM occurs and check whether the process memory usage is as expected. Use tools such as valgrind to analyze whether memory leakage occurs |
| PingUnreachable | Exception event | CVM instance | Yes | The CVM network cannot be pinged through | 1. Check whether CVM is running properly. If an exception such as system crash occurs, force to restart the CVM instance in the console. 2. If the CVM instance is running properly, check CVM network configuration, such as the internal network service configuration of the CVM instance, firewall configuration, and CVM security group configuration |
| DiskReadonly | Exception event | CVM instance | Yes | Writing data to the disk fails. | 1. Check whether the disk is full. 2. In Linux, run the `df -i` command to check whether inode is used up. 3. Check whether the file system is damaged |
| GuestReboot | Status change | CVM instance | Yes | The CVM instance restarts | This event is triggered when the CVM instance restarts. In this case, check whether the status change is as expected based on actual scenarios |
| PacketDroppedByQosWanOutBandwidth | Exception event | CVM instance | Yes | The public network outbound bandwidth of a CVM instance exceeds the upper limit, causing packet loss. Packet loss caused by bandwidth glitches is not reflected in the bandwidth view, because the minimum granularity for bandwidth statistics is 10 (average per-second traffic for 10 seconds). If the bandwidth is not significantly exceeded, it can be ignored | Increase the maximum public network bandwidth. If you have already purchased the maximum bandwidth possible, reduce the single-node bandwidth using load balancing or another method |
| PacketDroppedByQosConnectionSession | Exception event | CVM instance | Yes | The number of associated CVM instances exceeds the upper limit, causing packet loss | Contact sales customer service for troubleshooting. |


## Cloud Load Balancer

| Event Name | Event Type | Dimension | Recoverable | Description | Troubleshooting Method |
| --------- | ------------------ | ---- | --------- | ------ | ---------------------- | ----------------- |
| VipBlockInfo | Exception event | Cloud Load Balancer (CLB) instance | Yes | The CLB public IP address is attacked and is blocked after an exception is detected by security check | Submit a ticket to query why the blockage occurs and how to resolve it |
| RsPortStatusChange | Exception event | Backend server port | Yes | The backend server port of the public network load balancer (LB) is abnormal | Check the running status of the backend server port |


## VPN Gateway

| Event Name | Event Type | Dimension | Recoverable | Description | Troubleshooting Method |
| ----------- | ----------------------------------- | ---- | --------- | ------ | ---------------------------------------- | -------- |
| PacketDroppedByQosWanOutBandwidth | Exception event | VPN gateway instance | Yes | The public network outbound bandwidth of a VPN gateway instance exceeds the upper limit, causing packet loss. Packet loss caused by bandwidth glitches is not reflected in the bandwidth view, because the minimum granularity for bandwidth statistics is 10 (average per-second traffic for 10 seconds). If the bandwidth is not significantly exceeded, it can be ignored | Increase the maximum bandwidth of the public network |
| PacketDroppedByQosConnectionSession | Exception event | VPN gateway instance | Yes | The number of associated VPN gateway instances exceeds the upper limit, causing packet loss | Contact sales customer service for troubleshooting |


## TKE

| Event Name | Event Type | Dimension | Recoverable | Description | Troubleshooting Method |
| ---------- | ------------------------- | ---- | ------ | ------ | ---------------------------------------- | :--------------------------------------- |
| NodeNotReady | Exception event | Cluster | Yes | A node exception can be caused by various reasons, such as network connection failure, node kubelet exception, and container OOM. If a node remains abnormal for a long period, Kubernetes drains containers on the node | 1. Check whether the node is running on the CVM page, and whether monitoring has any exceptions. 2. Log in to the CVM instance and check whether kubelet is running properly. 3. Log in to the CVM instance and check whether docker is running properly |
| NodeHasDiskPressure | Exception event | Cluster | Yes | The disk (such as cbs or root) capacity for storing containers and images is almost used up. When the capacity is used up, NodeOutOfDisk is triggered and new containers cannot be scheduled to this node | Clean up the disk or delete unnecessary containers and images |
| NodeOutOfDisk | Exception event | Cluster | Yes | The disk (such as cbs or root) capacity for storing containers and images is used up, and new containers cannot be scheduled to this node | Clean up the disk or delete unnecessary containers and images |
| NodeHasInsufficientMemory | Exception event | Cluster | Yes | The node memory utilization is high | Expand the capacity or schedule containers to other nodes |
| SystemOOM | Exception event | Cluster | No | Node OOM occurs due to excessive memory demands | Check why OOM is triggered on the node. For example, check the monitoring information, syslog, or demsg |
| NodeNetworkUnavailable | Exception event | Cluster | No | The node network is incorrectly configured. Generally, this exception does not occur when a cluster is created in the console or through a cloud API | Promptly submit a ticket or contact sales customer service for troubleshooting |
| NodeInodePressure | Exception event | Cluster | No | New containers cannot be created on the node due to insufficient Inode on a node | Check the remaining Inode on the node, and try deleting unnecessary containers and images to release Inode capacity |


## TencentDB for MongoDB

| Event Name | Event Type | Dimension | Recoverable | Description | Troubleshooting Method |
| --------- | ----------------- | ---- | --------------- | ------ | ---------------------------------------- | :--------------------------------------- |
| oplogInsufficient | Exception event | TencentDB for MongoDB instance | No | During backup, TencentDB for MongoDB fails to read the complete oplog from last backup to the current one, which affects the rollback of your data to any point of time in the last 7 days | Adjust the oplog size or backup frequency of TencentDB for MongoDB in the Tencent Cloud console. If you do not need this event notification, disable the event notification feature on the backup page of the TencentDB for MongoDB console |
| connectionOverlimit | Exceptional event | TencentDB for MongoDB instance | Yes | The number of associated instances exceeds the upper limit | Check whether the configured number of associated instances meets the business requirements. If additional associations are required to be configured, upgrade the instance configuration of TencentDB for MongoDB |
| primarySwitch | Exception event | TencentDB for MongoDB instance | Yes | An instance switches between the Primary and Secondary status | This event can be triggered when a physical machine failure occurs. In this case, check whether the instance status is normal |
| instanceOutOfDisk | Exception evet | TencentDB for MongoDB instance | Yes | The disk capacity is full, causing the instance to be read-only | Clean up the disk |
| instanceRollback | Exception event | TencentDB for MongoDB instance | Yes | Instance data is rolled back | If the primary node has an error and primary/secondary switchover occurs when some data on the primary node is not synchronized to the secondary node, this event can be triggered. In this case, check whether the instance status is normal |
