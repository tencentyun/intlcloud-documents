
This document describes the instance types of TDSQL-C for MySQL, including general and dedicated.

| Instance Type | Description | 
|---------|---------|
| General | <li>A general instance exclusively uses the allocated memory and disk resources and shares the CPU resources with other general instances on the same physical machine. <br><li>A general instance benefits from higher specifications at a lower cost by sharing CPU resources. <br><li>A general instance's disk capacity is unaffected by its CPU and memory specs. |
| Dedicated | <li>A dedicated instance has exclusive access to the CPU, memory, and disk resources (if CPU pinning is enabled). It has long-term stability and is unaffected by the activities of other instances on the physical machine. <br><li>A dedicated instance with the highest configurations can monopolize a physical machine and all of its resources. |


