
This document describes three resource isolation policies of TencentDB for MySQL: basic, general, and dedicated.

>?
>- The former "Basic Edition" has been renamed "basic single-node", and the former "Single-Node High IO Edition" has been renamed "general single-node".
>- Two-node and three-node architectures support general and dedicated isolation policies.

| Resource Isolation Policy | Description                                                         |
| -------- | ------------------------------------------------------------ |
| Basic   | Single-node instances are the only ones that support this policy. A basic single-node instance (formerly Basic Edition) supports computation-storage separation and stores data on cloud disks. |
| General   | <li>A general instance exclusively uses the allocated memory and disk resources and shares the CPU resources with other general instances on the same physical machine. <li>A general instance benefits from higher specifications at a lower cost by sharing CPU resources. <li>A general instance's disk capacity is unaffected by its CPU and memory specs. |
| Dedicated   | <li>A dedicated instance has exclusive access to the CPU, memory, and disk resources (if CPU pinning is enabled). It has long-term stability and is unaffected by the activities of other instances on the physical machine. <li>A dedicated instance with the highest configurations can monopolize a physical machine and all of its resources. | 


## Isolation policies for different architectures
- TencentDB for MySQL single-node (cloud disk) instances are deployed based on TKE, where each instance has dedicated CPU, memory, and disk resources and different instances are completely isolated from each other.
- TencentDB for MySQL two-node (local disk) and three-node (local disk) instances are deployed based on local physical machines. Each physical machine sustains multiple instances and adopts isolation policies to ensure the complete isolation between different instances with dedicated CPU, memory, and disk resources.
In addition, TencentDB for MySQL also implements corresponding data isolation policies in multiple dimensions such as account, region, AZ, and network.
  
