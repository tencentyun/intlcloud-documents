## Support for Column Storage and Multiple Compression Algorithms
TDSQL-A for PostgreSQL supports column storage. You can define data tables as columnar tables based on your business needs. Generally, we recommend you set tables with a large width and requirements for a high compression ratio as columnar tables.
Columnar tables support a wide variety of compression algorithms, such as delta, zlib, zstd, RLE, and bitpack, which have different compression levels. For more information, please see the corresponding section in the development guide. TDSQL-A for PostgreSQL supports the new-generation columnar vectorized execution engine, which offers high query performance for hybrid row/column storage and query.

## Efficient Distributed JOIN Computing
Business analysis scenarios generally have logical JOIN operations between two or more tables. JOIN is a simple operation in standalone mode, but in cluster mode, as data is distributed among one or multiple physical nodes, the processing will be more complicated. In many distributed solutions, JOIN pulls data to one node for correlation and computing, which not only wastes many network resources but also dramatically prolongs statement executions.

Based on the efficient global query plan and data redistribution technology, TDSQL-A for PostgreSQL can take full advantage of parallel computing and complete the joins efficiently. It uses the following methods to efficiently compute distributed JOIN operations:

- In terms of the execution method, the CN receives your SQL requests, generates the optimal cluster-level distributed query plan based on the collected cluster statistics, and distributes it to the DNs participating in the computation for execution, that is, the CN sends the execution plan, and the DNs are responsible for executing the plan.
- In terms of data interaction, efficient data exchange tunnels are established between DNs, enabling efficient data exchange. The process of data exchange is called data redistribution in TDSQL-A for PostgreSQL.

## Multi-Core Parallel Computing
TDSQL-A for PostgreSQL uses parallel computing inside nodes, where multiple processes are started to collaboratively execute the same query. This makes full use of the processing capabilities of multiple server cores to execute queries more quickly and efficiently. Generally, TDSQL-A for PostgreSQL starts multiple processes for one query to shorten the query time, and the more the resources, the linearly shorter the query time.
TDSQL-A for PostgreSQL decides whether to perform parallel computing based on the table size. Only when the table size exceeds the threshold will parallel computing be used, and in this case, the concurrency (i.e., the number of required processes) will be calculated based on the table size.

## Data Security Protection
### Data encryption
TDSQL-A for PostgreSQL provides two data encryption methods:
- Encryption on the business side: the business calls the encryption function built in TDSQL-A for PostgreSQL and writes encrypted results to the database. Normally, the encrypted data will be read and decrypted in the application.
- Encryption built in TDSQL-A for PostgreSQL: the encryption process is imperceptible to the business, which has the following advantages:
 - Encryption operations (function calls) are decoupled from the business. The business is only responsible for writing the original data to the database kernel, and the subsequent encryption calculation will be conducted inside the database, which is imperceptible to the business.
 - Encryption algorithms are maintained by the database, and operations such as encryption algorithm selection and key management are all performed by the security admin independently.
   Kernel-based encryption calculation supports async encryption to implement data encryption while delivering a stable system throughput. The supported encryption algorithms include AES-128, AES-192, AES-256.

### Data masking
TDSQL-A for PostgreSQL supports transparent data masking that can return masked data to unauthorized users in an imperceptible manner.
Finer-Grained data access control can be implemented in the aforementioned two dimensions to enhance the control over existing access requests in a way that is imperceptible to the business system.

### Comprehensive audit
TDSQL-A for PostgreSQL supports all-round auditing in multiple dimensions. Bypass detection is used for auditing, which has little impact on database operations. The following types of audits are available:
- Statement audit: audits a certain type of statements.
- Object audit: audits the operations of a certain database object.
- User audit: audits the operations of a certain database user.
- Fine-Grained audit (FGA): uses expressions as audit conditions and allows you to set actions when audit is triggered, such as sending emails or making phone calls.	

### Hot/Cold data separation
The kernel natively supports hot/cold data separation, so that the business can provide a unified database view with no need to perceive the differences between underlying storage media.
- Hot data and cold data are stored in different node groups with different physical server configurations, so as to implement hot/cold data separation and reduce the costs.
- Scheduled backend tasks can automatically migrate data according to the configured hot/cold data rules. In this way, the system can implement automated hot/cold data separation, and the business doesn't need to care about the storage of hot/cold data in the cluster.
  This feature is currently available on the Private Cloud Edition but unavailable on the Public Cloud Edition.

## Multi-Level Disaster Recovery
TDSQL-A for PostgreSQL ensures the cluster disaster recovery capabilities in multiple dimensions:

### Strong sync replication
TDSQL-A for PostgreSQL supports strong sync replication. Ensuring that the primary and standby nodes have the identical data is the basis of the entire disaster recovery system. If the primary node fails, the database service can be switched to the standby node without any data loss. The strong sync replication mechanism requires that a success be returned only after the user request is executed and the log is successfully written to the standby node, guaranteeing that the data on the primary and standby nodes are always consistent.

### Primary-Standby high availability
The primary-standby high availability scheme of TDSQL-A for PostgreSQL mainly uses multi-replica redundancy in each node group to ensure that there are no or only momentary service interruptions. If the primary node in a group fails and cannot be recovered, a new primary node will be automatically selected from the corresponding standby nodes to continue service provision. Based on primary/standby high availability, TDSQL-A for PostgreSQL supports the following features:

- Automated failover: if the primary node in the cluster fails, the system will automatically select a new primary node from the corresponding standby nodes, and the failed node will be automatically isolated. The strong sync replication policy ensures complete primary/standby data consistency in case of primary/standby failover, fully meeting the finance-grade requirements for data consistency.
- Failure recovery: if a standby node loses data due to disk failure, the database admin (DBA) can recover the standby node by building it again or add a standby server to a new physical node to recover the primary/standby relationship and thus ensure the system reliability.
- Replica switch: each node in the primary/standby architecture (which can contain one primary node and multiple standby nodes) has a complete data replica that can be switched to by the DBA as needed.
- Do-Not-Switch configuration: it can be set that failover will not be performed during the specified period of time.
- Cross-AZ deployment: even if the primary and standby nodes are in different data centers, the data can be replicated through Direct Connect in real time. If the local node is the primary and the remote node is the standby, the local node will be accessed first, and if it fails or becomes unreachable, the remote standby node will be promoted to the primary node to provide service.

TDSQL-A for PostgreSQL supports the high availability scheme based on strong sync replication. If the primary node fails, the system will automatically select the optimal standby node immediately to take over the tasks. The switch process is imperceptible to users, and the access IP remains unchanged. TDSQL-A for PostgreSQL offers 24/7 continuous monitoring for system components, and if there is a failure, it will automatically restart or isolate the failed node and select a new primary node from the standby nodes to continue service provision.

### Support for full and incremental backup modes
TDSQL-A for PostgreSQL supports backup-based data restoration at the time points when transaction consistency is guaranteed so as to avoid data loss due to misoperations. Backup modes include full backup (cold backup) and incremental backup (xlog backup).

- Full backup: all database data excluding operations logs and xlogs is backed up. This mode is usually periodic, such as daily, weekly, or once every N days.
- Incremental backup: incremental data is backed up, which is generally implemented through xlog files. After generating an xlog file, the database system backs up the file onto the backup server. This mode is generally in real time.
  If an incident or disaster occurs, you can use backup data to recover the system.
