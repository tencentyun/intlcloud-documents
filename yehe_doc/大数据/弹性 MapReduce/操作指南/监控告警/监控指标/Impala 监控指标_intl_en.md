>!Currently, only Impala v3.4.0 and above support Impala metrics.


### Impala - Catalog

| Metric Name | Unit | Description |
| ----------------------- | -------- | ------------------------------------------ |
| RSS                     | Bytes    | Resident set size                                 |
| MemHeapInitM                  | MB                    | Peak amount of initial HeapMemory for the JVM                 |
| MemHeapCommittedM | MB | Amount of HeapMemory committed by the JVM |
| MemHeapMaxM | MB | Amount of HeapMemory configured for the JVM |
| MemHeapUsedM | MB | Amount of HeapMemory used by the JVM |
| MemNonHeapInitM | MB | Initial amount of NonHeapMemory for the JVM |
| MemNonHeapCommittedM | MB | Amount of NonHeapMemory committed by the JVM |
| MemNonHeapUsedM | MB | Amount of NonHeapMemory used by the JVM |
| Last                    | s        | Most recent interval between heartbeats from the daemon process to StateStore       |
| Max                     | s        | Maximum interval between heartbeats from the daemon process to StateStore       |
| Mean                    | s        | Average interval between heartbeats from the daemon process to StateStore       |
| Min                     | s        | Minimum interval between heartbeats from the daemon process to StateStore      |
| Stddev                  | s        | Standard deviation in the interval between heartbeats from the daemon process to StateStore |
| TCMalloc_Used                    | Bytes    | Number of bytes used by the application                           |
| PageheapFreeBytes       | Bytes    | Number of bytes of available mapped pages in the page heap                   |
| PageheapUnmappedBytes | Bytes | Number of bytes of available unmapped pages in the page heap  |
| PhysicalBytesReserved   | Bytes    | Amount of physical memory used by the process                   |
| TotalBytesReserved      | Bytes    | Number of bytes of system memory reserved by TCMalloc              |
| Thrift_Server_Connections_Used                    | -       | Number of active connections                                 |
| Uptime                             | s        | Process run time      |
| MaxFileDescriptorCount             | -       | Maximum number of file descriptors      |
| OpenFileDescriptorCount | -                    | Number of opened file descriptors                      |
| ThreadCount                        | -       | Total number of threads        |
| DaemonThreadCount                  | -       | Number of Daemon threads        |

### Impala - Daemon

| Metric Name | Unit | Description |
| ----------------------- | -------- | --------------------------------------- |
| MemHeapInitM | MB | Peak amount of initial HeapMemory for the JVM |
| MemHeapCommittedM | MB | Amount of HeapMemory committed by the JVM |
| MemHeapMaxM | MB | Amount of HeapMemory configured for the JVM |
| MemHeapUsedM | MB | Amount of HeapMemory used by the JVM |
| MemNonHeapInitM | MB | Initial amount of NonHeapMemory for the JVM |
| MemNonHeapCommittedM | MB | Amount of NonHeapMemory committed by the JVM |
| MemNonHeapUsedM | MB | Amount of NonHeapMemory used by the JVM |
| TCMalloc_Used                    | Bytes    | Number of bytes used by the application                    |
| PageheapFreeBytes       | Bytes    | Number of bytes of available mapped pages in the page heap                |
| PageheapUnmappedBytes   | Bytes    | Number of bytes of available unmapped pages in the page heap            |
| PhysicalBytesReserved   | Bytes    | Amount of physical memory used by the process                |
| TotalBytesReserved      | Bytes    | Number of bytes of system memory reserved by TCMalloc           |
| ThreadCount                        | -       | Total number of threads        |
| DaemonThreadCount                  | -       | Number of daemon threads        |
| Uptime                             | s        | Process run time      |
| MaxFileDescriptorCount             | -       | Maximum number of file descriptors      |
| OpenFileDescriptorCount | -                    | Number of opened file descriptors                      |


### Impala - StateStore

| Metric Name | Unit | Description |
| --------------------- | -------- | ----------------------------- |
| RSS                   | Bytes    | Resident set size                         |
| TCMalloc_Used                  | Bytes    | Number of bytes used by the application          |
| PageheapFreeBytes     | Bytes    | Number of bytes of available mapped pages in the page heap      |
| PageheapUnmappedBytes | Bytes    | Number of bytes of available unmapped pages in the page heap  |
| PhysicalBytesReserved | Bytes    | Amount of physical memory used by the process      |
| TotalBytesReserved    | Bytes    | Number of bytes of system memory reserved by TCMalloc |
|Thrift_Server_Connections_Used                  | -       | Number of active connections                    |
| Running_Threads_Count                 | -       | Number of running threads                    |
| StateStore_Live_Backends_Count                 | -       | Number of StateStore subscribers         |

 
