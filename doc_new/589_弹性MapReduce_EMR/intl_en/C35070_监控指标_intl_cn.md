## Server Metrics
### CPU 
| Metric Name | Unit | Description |
| ------------ | ---- | -------------------------- |
| cpu_idle | % | Percentage of CPU idleness |
| cpu_intr | % | Percentage of interrupts |
| cpu_nice | % | Percentage of CPU utilization under nice priority |
| total_cpu | | Number of CPUs |
| cpu_softintr | % | Percentage of CPU soft interrupts |
| cpu_steal | % | Percentage of wait time by virtual CPUs for physical CPUs |
| cpu_system | % | CPU utilization in kernel state |
| cpu_user | % | CPU utilization in user state |
| cpu_waitio | % | Percentage of CPU idleness due to process I/O waits |
| load_1 | 1 | 1-minute load |
| load_5 | 1 | 5-minute load |
| load_15 | 1 | 15-minute load |

### Memory
| Metric Name | Unit | Description |
| ------------------------ | ---- | ------------------- |
| memory_total | Byte | Total memory size |
| memory_available | Byte | Total available memory size |
| memory_available_percent | % | Percentage of available memory |
| memory_buffers | Byte | Total memory size used by buffers |
| memory_cached | Byte | Total memory size used by page caches |
| memory_dirty | Byte | Total memory size used by dirty pages |
| memory_free | Byte | Total idle memory size |
| memory_shared | Byte | Total shared memory size |
| memory_used_percent | % | Percentage of used memory |
| swap_free | Byte | Available swap memory size |
| swap_total  | Byte | Total swap memory size |

### Network
| Metric Name | Unit | Description |
| ------------------- | -------- | ------------------------------- |
| bytes_in | Byte/s | NIC inbound traffic in byte/s |
| bytes_out | Byte/s | NIC outbound traffic in byte/s |
| packets_in | Packet/s | NIC inbound packet traffic in packet/s |
| packets_out | Packet/s | NIC outbound packet traffic in packet/s |
| tcp_opens | | Number of TCP connections opened per second |
| tcp_closed | | Number of TCP closed connection |
| tcp_closewait | | Number of TCP connections waiting to be closed |
| tcp_closing | | Number of TCP connections being closed |
| tcp_establish | | Number of connections being established |
| tcp_established | | Number of established connections |
| tcp_establish_reset | | Number of reset connections |
| tcp_listendrop | | Number of connections dropped by the listening port |
| tcp_listen | | Number of connections listened to |
| tcp_retrans | | Number of retransmissions |

### Disk
| Metric Name | Unit | Description |
| -------------------- | ------- | ------------------------ |
| disk_free | Byte | Free disk capacity |
| disk_io_now | | Number of I/O operations in progress |
| disk_read_bytes | Byte/s | Disk read speed in byte/s |
| disk_write_bytes | Byte/s | Disk write speed in byte/s |
| disk_read_completed | 1/s | QPS of completed reads |
| disk_write_completed | 1/s | QPS of completed writes |

### Process
| Metric Name | Unit | Description |
| --------------- | ---- | -------------- |
| process_total | | Total number of processes |
| process_run | | Number of running processes |
| process_blocked | | Number of blocked processes |
| process_created | | Number of created processes |

### FD
| Metric Name | Unit | Description |
| ------------ | ---- | -------------------- |
| fd_allocated | | Number of allocated handles |
| fd_max | | Maximum number of handles available to the system |

## HDFS Monitoring Metrics
### NN Monitoring Metrics 
| Metric Name | Unit | Description |
| -------------------- | ---- | ------------------------------------------------------------ |
| Capacity | MB/s | HDFS cluster storage capacity with the type = { total, used, used_non_dfs }, which represents total capacity, used capacity, and capacity used not by HDFS, respectively |
| TotalLoad | | Number of current connections |
| BlocksTotal | | Total number of blocks |
| FilesTotal | | Total number of files |
| Blocks | | Number of blocks with the type = { PendingReplication, UnderReplicated, Corrupt, scheduledReplication, excess, postponedMisreplicated } * |
| BlockCapacity | | Capacity of blocks |
| StaleDataNodes | | Current number of DataNodes marked as expired due to heartbeat delay |
| VolumeFailuresTotal | | Total number of volume failures on all DataNodes |
| MemNonHeapUsedM | MB | Size of NonHeapMemory currently in use by JVM |
| MemNonHeapCommittedM | MB | Submitted size of JVM NonHeapMemory |
| MemNonHeapMaxM | MB | Size of NonHeapMemory configured by JVM |
| MemHeapUsedM | MB | Size of HeapMemory currently in use by JVM |
| MemHeapCommittedM | MB | Submitted size of JVM HeapMemory |
| MemHeapMaxM | MB | Size of HeapMemory configured by JVM |
| MemMaxM | MB | Maximum size of memory available to the JVM runtime |
| GcCount | | GC count |
| GcTimeMillis | Millisecond | GC time |
| Threads | | Total number of threads in a state with the type = { new, runnable, blocked, waiting, timed_waiting, terminated } |
| Log | 1/s   | Number of { Fatal, Error, Warn, Info } logs at the level = { fatal, error, warn, info } within the specified time period |

### DN Monitoring Metrics
| Metric Name | Unit | Description |
| ------------------------------------------ | ------ | ------------------------------------------------------------ |
| XceiverCount | | Number of Xceivers |
| BytesWritten | Byte | Total number of bytes written to DN |
| TotalWriteTime | Millisecond | Time consumed by write operations in ms |
| BytesRead | Byte | Total number of bytes read from DN |
| TotalReadTime | Millisecond | Time consumed by read operations in ms |
| BlocksWritten | 1/s | Total number of written blocks |
| RemoteBytesRead | Byte/s | Number of bytes read by the remote client |
| RemoteBytesWritten | Byte/s | Number of bytes written by the remote client |
| FsyncCount | 1/s | Number of fsync operations |
| VolumeFailures | 1/s | Number of disk failures |
| DatanodeNetworkErrors | 1/s | Total number of network errors |
| SendDataPacketBlockedOnNetworkNanosNumOps | 1/s | QPS of the transferred packet |
| SendDataPacketBlockedOnNetworkNanosAvgTime | Nanosecond | Average packet transfer delay |
| MemNonHeapUsedM | MB | Size of NonHeapMemory currently in use by JVM |
| MemNonHeapCommittedM | MB | Submitted size of JVM NonHeapMemory |
| MemNonHeapMaxM | MB | Size of NonHeapMemory configured by JVM |
| MemHeapUsedM | MB | Size of HeapMemory currently in use by JVM |
| MemHeapCommittedM | MB | Submitted size of JVM HeapMemory |
| MemHeapMaxM | MB | Size of HeapMemory configured by JVM |
| MemMaxM | MB | Maximum size of memory available to the JVM runtime |
| GcCount | 1/s | GC count |
| GcTimeMillis | Millisecond | GC time |
| Threads | | Total number of threads in a state with the type = { new, runnable, blocked, waiting, timed_waiting, terminated } |
| Log | 1/s   | Number of { Fatal, Error, Warn, Info } logs at the level = { fatal, error, warn, info } within the specified time period |

## Yarn Monitoring Metrics
### RM Monitoring Metrics 
| Metric Name | Unit | Description |
| -------------------- | ---- | ------------------------------------------------------------ |
| NumActiveNMs | 1 | Number of currently active NMs |
| NumDecommissionedNMs | 1 | Number of decommissioned NMs |
| NumLostNMs | 1 | Number of lost NMs |
| NumUnhealthyNMs | 1 | Number of unhealthy NMs |
| Apps | 1 | Number of apps in the current queue with the type = { submitted, running, pending, completed, killed, failed } |
| VCores | 1 | Number of vCores in the current queue with the type = { allocated, available, reserved, pending } |
| Memory | 1 | Memory size in MB in the current queue with the type = { allocated, available, reserved, pending } |
| Containers | 1 | Number of containers in the current queue with the type = { allocated, available, reserved, pending } |
| ActiveApplications | 1 | Number of active apps in the current queue |
| MemNonHeapUsedM | MB | Size of NonHeapMemory currently in use by JVM |
| MemNonHeapCommittedM | MB | Submitted size of JVM NonHeapMemory |
| MemNonHeapMaxM | MB | Size of NonHeapMemory configured by JVM |
| MemHeapUsedM | MB | Size of HeapMemory currently in use by JVM |
| MemHeapCommittedM | MB | Submitted size of JVM HeapMemory |
| MemHeapMaxM | MB | Size of HeapMemory configured by JVM |
| MemMaxM | MB | Maximum size of memory available to the JVM runtime |
| GcCount | 1/s | GC count |
| GcTimeMillis | Millisecond | GC time |
| Threads | 1 | Total number of threads in a state with the type = { new, runnable, blocked, waiting, timed_waiting, terminated } |
| Log | 1/s   | Number of { Fatal, Error, Warn, Info } logs at the level = { fatal, error, warn, info } within the specified time period |

### DM Monitoring Metrics
| Metric Name | Unit | Description |
| ------------------------------ | ---- | ------------------------------------------------------------ |
| Containers | 1 | Number of containers with the type = { launched, completed, failed, killed, initiating, running, allocated } * |
| Memory | GB | Size of memory in GB with the type = {allocated, available } * |
| VCores | 1 | Number of vCores with the type = {allocated, available } * |
| ContainerLaunchDurationNumOps | 1/s | QPS of the launched container |
| ContainerLaunchDurationAvgTime | Millisecond | Average RT of the launched container |
| MemNonHeapUsedM | MB | Size of NonHeapMemory currently in use by JVM |
| MemNonHeapCommittedM | MB | Submitted size of JVM NonHeapMemory |
| MemNonHeapMaxM | MB | Size of NonHeapMemory configured by JVM |
| MemHeapUsedM | MB | Size of HeapMemory currently in use by JVM |
| MemHeapCommittedM | MB | Submitted size of JVM HeapMemory |
| MemHeapMaxM | MB | Size of HeapMemory configured by JVM |
| MemMaxM | MB | Maximum size of memory available to the JVM runtime |
| GcCount | 1/s | GC count |
| GcTimeMillis | Millisecond | GC time |
| Threads | 1 | Total number of threads in a state with the type = { new, runnable, blocked, waiting, timed_waiting, terminated } |
| Log | 1/s   | Number of { Fatal, Error, Warn, Info } logs at the level = { fatal, error, warn, info } within the specified time period |

 
## HBase Monitoring Metrics
### HBase - Master Monitoring Metrics
| Metric Name | Unit | Description |
| -------------------- | ------ | ------------------------------------------------------------ |
| masterActiveTime | Second | Master survival time |
| masterStartTime | Second | Master start time |
| averageLoad | 1 | Average number of regions loaded per RS |
| numRegionServers | 1 | Number of RSs in the cluster |
| numDeadRegionServers | 1 | Number of dead RSs in the Cluster |
| clusterRequests | 1/s | Total number of requests in the cluster |
| receivedBytes | Byte/s | Amount of data received |
| sentBytes | Byte/s | Amount of data sent |
| MemNonHeapUsedM | MB | Size of NonHeapMemory currently in use by JVM |
| MemNonHeapCommittedM | MB | Submitted size of JVM NonHeapMemory |
| MemNonHeapMaxM | MB | Size of NonHeapMemory configured by JVM |
| MemHeapUsedM | MB | Size of HeapMemory currently in use by JVM |
| MemHeapCommittedM | MB | Submitted size of JVM HeapMemory |
| MemHeapMaxM | MB | Size of HeapMemory configured by JVM |
| MemMaxM | MB | Maximum size of memory available to the JVM runtime |
| GcCount | 1/s | GC count |
| GcTimeMillis | Millisecond | GC time |
| Threads | | Total number of threads in a state with the type = { new, runnable, blocked, waiting, timed_waiting, terminated } |
| Log | 1/s   | Number of { Fatal, Error, Warn, Info } logs at the level = { fatal, error, warn, info } within the specified time period |


### HBase - RegionServer Monitoring Metrics
| Metric Name | Unit | Description |
| --------------------- | ----- | ------------------------------------------------------------ |
| regionCount | 1 | Number of regions managed by RS |
| storeCount | 1 | Number of stores managed by RS |
| hlogFileCount | 1 | Number of HLOG files |
| hlogFileSize | Byte | HLOG file size |
| storeFileCount | 1 | Number of store files |
| memStoreSize | Byte | Total size of MEM store |
| storeFileSize | Byte | Store file size |
| regionServerStartTime | Second | RS start time |
| averageRegionSize | 1 | Average region size |
| totalRequestCount | 1/s | Total number of requests |
| readRequestCount | 1/s | Number of read requests |
| writeRequestCount | 1/s | Number of write requests |
| MemNonHeapUsedM | MB | Size of NonHeapMemory currently in use by JVM |
| MemNonHeapCommittedM | MB | Submitted size of JVM NonHeapMemory |
| MemNonHeapMaxM | MB | Size of NonHeapMemory configured by JVM |
| MemHeapUsedM | MB | Size of HeapMemory currently in use by JVM |
| MemHeapCommittedM | MB | Submitted size of JVM HeapMemory |
| MemHeapMaxM | MB | Size of HeapMemory configured by JVM |
| MemMaxM | MB | Maximum size of memory available to the JVM runtime |
| GcCount | 1/s | GC count |
| GcTimeMillis | Millisecond | GC time |
| Threads | 1 | Total number of threads in a state with the type = { new, runnable, blocked, waiting, timed_waiting, terminated } |
| Log | 1/s   | Number of { Fatal, Error, Warn, Info } logs at the level = { fatal, error, warn, info } within the specified time period |

