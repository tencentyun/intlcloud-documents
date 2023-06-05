
This document describes the environment used for the TDSQL-C for MySQL performance test.

## Test Object: TDSQL-C for MySQL
- Region/AZ: Beijing - Beijing Zone 6
- Client
 - Client type: CVM
 - Client specification: S5.4XLARGE32 (Standard S5 with 16 CPU cores and 32 GB memory)
 - Client operating system: CentOS 7
 - Number of clients: 2 (one more client is added after the concurrency exceeds 1,000, and so on)
- Information of the tested TDSQL-C for MySQL instance:
 - AZ deployment: Single-AZ
 - Database version: MySQL 5.7
 - Parameter template: The default template is used, with the following parameters adjusted:
   - log_bin=off
   - thread_handling=pool-of-threads
   - innodb_log_sync_method=async
 - VPC network latency: 0.6 ms
 - Instance type/specification:
 
<table>
<tr><th>Instance Type</th>
<th>Instance Specification</th></tr>
<tr><td rowspan = "11"  width="40%">Dedicated</td><td>2-core 16 GB MEM</td></tr>
<tr><td>4-core 16 GB MEM</td></tr>
<tr><td>4-core 32 GB MEM</td></tr>
<tr><td>8-core 32 GB MEM</td></tr>
<tr><td>8-core 64 GB MEM</td></tr>
<tr><td>16-core 64 GB MEM</td></tr>
<tr><td>16-core 96 GB MEM</td></tr>
<tr><td>16-core 128 GB MEM</td></tr>
<tr><td>32-core 128 GB MEM</td></tr>
<tr><td>32-core 256 GB MEM</td></tr>
<tr><td>64-core 256 GB MEM</td></tr>
</table>

## Test Object: TencentDB for MySQL 
- Region/AZ: Guangzhou - Guangzhou Zone 6
- Client
 - Client type: CVM
 - Client specification: S5.4XLARGE32 (Standard S5 with 16 CPU cores and 32 GB memory)
 - Client operating system: CentOS 7
 - Number of clients: 2 (one more client is added after the concurrency exceeds 1,000, and so on)
The information of the tested TencentDB for MySQL instance is as follows:
 - Storage type: Local SSD
 - AZ deployment: Single-AZ
 - Database version: MySQL 5.7
 - Architecture: Two-node
 - Replication method: Async replication
 - Parameter template: High-performance parameter template
 - VPC network latency: 0.5 ms
 - Instance type/specification: Same as above

