
This document describes three resource isolation policies of TencentDB for MySQL: basic, general, and dedicated.

>?
>- The former "Basic Edition" has been renamed "basic single-node”, and the former "Single-node High IO Edition" has been renamed "general single-node".
>- Two-node and three-node instances support the general and dedicated policies. The dedicated policy is currently in beta; therefore, to purchase dedicated instances, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

| Resource Isolation Policy | Description                                                         |
| -------- | ------------------------------------------------------------ |
| Basic   | Only single-node instances support this policy. A basic single-node instance (formerly known as Basic Edition) supports computation-storage separation and uses cloud disks as underlying storage. |
| General   | <li>A general instance has exclusive use of the allocated memory and disk resources, but shares CPU resources with other general instances on the same physical machine. <li>By sharing CPU resources, a general instance enjoys higher specifications at a lower cost. <li>Disk capacity of a general instance is independent of its CPU and memory specifications. |
| Dedicated   | <li>A dedicated instance has exclusive use of CPU (CPU pinning configured), memory, and disk resources. It boasts long-term stable performance and won’t be affected by the behavior of other instances on the physical machine. <li>A dedicated instance with the highest configurations can monopolize a physical machine and all its resources. | 


