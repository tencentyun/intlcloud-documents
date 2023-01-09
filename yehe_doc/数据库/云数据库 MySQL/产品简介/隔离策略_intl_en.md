
This document describes three resource isolation policies of TencentDB for MySQL: basic, general, and dedicated.

>?
>- The former "Basic Edition" has been renamed "basic single-node”, and the former "Single-node High IO Edition" has been renamed "general single-node".
>- Two-node and three-node instances support the general and dedicated policies.
| Resource Isolation Policy | Description                                                         |
| -------- | ------------------------------------------------------------ |
| Basic   | Only single-node instances support this policy. A basic single-node instance (formerly Basic Edition) supports computation-storage separation and stores data on cloud disks. |
| General   | <li>A general instance exclusively uses the allocated memory and disk resources and shares the CPU resources with other general instances on the same physical machine. <li>A general instance benefits from higher specifications at a lower cost by sharing CPU resources. <li>A general instance's disk capacity is unaffected by its CPU and memory specs. |
| Dedicated   | <li>A dedicated instance has exclusive access to the CPU, memory, and disk resources (if CPU pinning is enabled). It has long-term stability and is unaffected by the activities of other instances on the physical machine. <li>A dedicated instance with the highest configurations can monopolize a physical machine and all of its resources. | 


