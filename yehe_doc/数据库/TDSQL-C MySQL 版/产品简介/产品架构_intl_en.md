This document describes the architecture and features of TDSQL-C for MySQL. Based on cloud native design, TDSQL-C for MySQL delivers high stability, reliability, performance, and scalability like commercial databases while featuring simplicity, openness, and efficient iteration like open-source cloud databases.

## Product Architecture Diagram
![](https://qcloudimg.tencent-cloud.cn/raw/c23688d66a7fcbdae1766242db9533b9.png)

## Single-Write-Multiple-Read
A TDSQL-C for MySQL cluster contains one source node and up to 15 read-only nodes. The former processes read and write requests, while the latter processes only read requests.

## Computing/Storage Separation
TDSQL-C for MySQL separates computing from storage to elastically scale clusters based on business needs in public cloud computing environments. Compute nodes (database engine servers) only store metadata, while remote storage nodes (database storage servers) store data files and redo logs. Only the metadata of redo logs needs to be synced between compute nodes. This greatly reduces the replication delay between the source node and read-only nodes. In addition, when the source node fails, a new node will be quickly started for a smooth switch.

## Automatic Read/Write Separation
Automatic read/write separation is a transparent, highly available, and adaptive load balancing feature offered by TDSQL-C for MySQL. After a database proxy address is configured, SQL requests will be automatically forwarded to the nodes in the TDSQL-C for MySQL cluster. This mechanism provides aggregated and high-throughput capabilities to process concurrent SQL requests.

## Interconnection Through High-Speed Linkage
TDSQL-C for MySQL supports full-linkage transfer with remote direct memory access (RDMA), where data is transferred from the memory of a computer directly to another computer without intervention from both operating systems required. This further optimizes the system performance at critical paths and minimizes the request delay, so that the I/O performance is no longer a bottleneck. In addition, an RDMA network is also used between stored replicas.

## Shared Distributed Storage
Data is shared by multiple compute nodes rather than stored on each compute node. This greatly reduces the storage costs. Based on the newly created distributed block storage and file system, the storage capacity can be smoothly expanded online to sustain petabytes of data without being limited by the storage capacity of a single database server.

## Multi-Replica Strong Consistency
Data is stored on the storage nodes of the database in multiple replicas, which ensures a high data reliability. In addition, the strong multi-replica consistency policy is adopted to guarantee the data consistency.
