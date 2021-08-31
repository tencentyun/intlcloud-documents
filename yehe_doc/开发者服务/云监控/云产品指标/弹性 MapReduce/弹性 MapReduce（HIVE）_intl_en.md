## Namespace

Namespace=QCE/TXMR_HIVE

## Monitoring Metrics

### Hive - HiveMetaStore

| Parameter | Metric Name | Unit | Description | Dimension |
| ----------------------- | ---------------- | -------- | ------------------------------------- | -------------------------------------- |
| HiveHmsGcUtilGcCountYgc | GC count_YGC       | Count       | Young GC count                         | id4hivemetastore<br>host4hivemetastore |
| HiveHmsGcUtilGcCountFgc | GC count_FGC       | Count       | Full GC count                          | id4hivemetastore<br>host4hivemetastore |
| HiveHmsGcUtilGcTimeFgct | GC time_FGCT      | s        | Time consumed by Full GC                      | id4hivemetastore<br>host4hivemetastore |
| HiveHmsGcUtilGcTimeGct  | GC time_FGCT      | s        | Time used to collect garbage                      | id4hivemetastore<br>host4hivemetastore |
| HiveHmsGcUtilGcTimeYgct | GC time_YGCT      | s        | Time consumed by Young GC                     | id4hivemetastore<br>host4hivemetastore |
| HiveHmsGcUtilMemoryS0   | Memory space percentage_S0  | %        | Percentage of used Survivor 0 memory              | id4hivemetastore<br>host4hivemetastore |
| HiveHmsGcUtilMemoryE    | Memory space percentage_E   | %        | Percentage of used Eden memory                   | id4hivemetastore<br>host4hivemetastore |
| HiveHmsGcUtilMemoryCcs  | Memory space percentage_CCS | %        | Percentage of memory used by compressed class space | id4hivemetastore<br>host4hivemetastore |
| HiveHmsGcUtilMemoryS1   | Memory space percentage_S1  | %        | Percentage of used Survivor 1 memory              | id4hivemetastore<br>host4hivemetastore |
| HiveHmsGcUtilMemoryO    | Memory space percentage_O   | %        | Percentage of used Old memory                    | id4hivemetastore<br>host4hivemetastore |
| HiveHmsGcUtilMemoryM    | Memory space percentage_M   | %        | Percentage of used Metaspace memory              | id4hivemetastore<br>host4hivemetastore |

### Hive - HiveServer2

| Parameter | Metric Name | Unit | Description | Dimension |
| ------------------------------------------- | ------------------------------------ | -------- | --------------------------------------- | --------------------------------------------- |
| HiveH2GcUtilGcCountYgc                      | GC count_YGC                           | Count       | Young GC count                           | host4hivehiveserver2, <br>id4hivehiveserver2  |
| HiveH2GcUtilGcCountFgc                      | GC count_FGC                           | Count       | Full GC count                            | host4hivehiveserver2, <br>id4hivehiveserver2  |
| HiveH2GcUtilGcTimeFgct                      | GC time_FGCT                          | s        | Time consumed by Full GC                        | host4hivehiveserver2, <br/>id4hivehiveserver2 |
| HiveH2GcUtilGcTimeGct                       | GC time_FGCT                          | s        | Time used to collect garbage                        | host4hivehiveserver2, <br/>id4hivehiveserver2 |
| HiveH2GcUtilGcTimeYgct                      | GC time_YGCT                          | s        | Time consumed by Young GC                       | host4hivehiveserver2, <br/>id4hivehiveserver2 |
| HiveH2GcUtilMemoryS0                        | Memory space percentage_S0                      | %        | Percentage of used Survivor 0 memory                | host4hivehiveserver2, <br/>id4hivehiveserver2 |
| HiveH2GcUtilMemoryE                         | Memory space percentage_E                       | %        | Percentage of used Eden memory                     | host4hivehiveserver2, <br/>id4hivehiveserver2 |
| HiveH2GcUtilMemoryCcs                       | Memory space percentage_CCS                     | %        | Percentage of memory used by compressed class space   | host4hivehiveserver2, <br/>id4hivehiveserver2 |
| HiveH2GcUtilMemoryS1                        | Memory space percentage_S1                      | %        | Percentage of used Survivor 1 memory                | host4hivehiveserver2, <br/>id4hivehiveserver2 |
| HiveH1GcUtilMemoryO                         | Memory space percentage_O                       | %        | Percentage of used Old memory                      | host4hivehiveserver2, <br/>id4hivehiveserver2 |
| HiveH2GcUtilMemoryM                         | Memory space percentage_M                       | %        | Percentage of used Metaspace memory                | host4hivehiveserver2, <br/>id4hivehiveserver2 |
| HiveH2JvmMemMem<br> nonheapusedm            | JVM memory_MemNonHeapUsedM              | MB       | Size of the NonHeapMemory currently used by JVM | host4hivehiveserver2, <br/>id4hivehiveserver2 |
| HiveH2JvmMemMem<br> nonheapcommittedm       | JVM memory_MemNonHeapCommittedM         | MB       | Size of the NonHeapMemory currently committed by JVM | host4hivehiveserver2, <br/>id4hivehiveserver2 |
| HiveH2JvmMemMem<br> heapusedm               | JVM memory_MemHeapUsedM                 | MB       | Size of the HeapMemory currently used by JVM    | host4hivehiveserver2, <br/>id4hivehiveserver2 |
| HiveH2JvmMemMem<br> heapcommittedm          | JVM memory_MemHeapCommittedM            | MB       | Size of the HeapMemory currently committed by JVM    | host4hivehiveserver2, <br/>id4hivehiveserver2 |
| HiveH2JvmMemMem<br> heapmaxm                | JVM memory_MemHeapMaxM                  | MB       | Size of the HeapMemory configured by JVM            | host4hivehiveserver2, <br/>id4hivehiveserver2 |
| HiveH2JvmMemMem<br> heapinitm               | JVM memory_MemHeapInitM                 | MB       | Size of the initial JVM HeapMem                 | host4hivehiveserver2, <br/>id4hivehiveserver2 |
| HiveH2JvmMemMem<br> nonheapinitm            | JVM memory_MemNonHeapInitM              | MB       | Size of the initial JVM NonHeapMem              | host4hivehiveserver2, <br/>id4hivehiveserver2 |
| HiveH2OsCpuLoad<br>Processcpuload           | CPU utilization_ProcessCpuLoad             | %        | CPU utilization                              | host4hivehiveserver2, <br/>id4hivehiveserver2 |
| HiveH2OsFdCount<br>Maxfiledescriptorcount   | Number of file descriptors_MaxFileDescriptorCount  | Count       | Maximum number of file descriptors                        | host4hivehiveserver2, <br/>id4hivehiveserver2 |
| HiveH2OsFdCount<br> Openfiledescriptorcount | Number of file descriptors_OpenFileDescriptorCount | Count       | Number of opened file descriptors                      | host4hivehiveserver2, <br/>id4hivehiveserver2 |
| HiveH2OsCpuTime<br>Processcputime           | Cumulative CPU usage time_ProcessCpuTime       | ms       | Cumulative CPU usage time                        | host4hivehiveserver2, <br/>id4hivehiveserver2 |
| HiveH2RtUptimeUptime                        | Process run time_Uptime                  | s        | Process run time                            | host4hivehiveserver2, <br/>id4hivehiveserver2 |
| HiveH2ThreadCount<br>Daemonthreadcount      | Number of worker threads_DaemonThreadCount         | Count       | Number of daemon threads                           | host4hivehiveserver2, <br/>id4hivehiveserver2 |
| HiveH2ThreadCount<br>Threadcount            | Number of worker threads_ThreadCount               | Count       | Total number of threads                                | host4hivehiveserver2, <br/>id4hivehiveserver2 |

### Hive - HiveWebHcat

| Parameter | Metric Abbreviation | Metric Name | Unit | Description | Dimension |
| ---------------------- | -------- | ---------------- | -------- | ------------------------------------- | --------------------------------------------- |
| HiveHcGcUtilGcCountYgc | YGC      | GC count_YGC       | Count       | Young GC count                         | host4hivehivewebhcat, <br>id4hivehivewebhcat  |
| HiveHcGcUtilGcCountFgc | FGC      | GC count_FGC       | Count       | Full GC count                          | host4hivehivewebhcat, <br>id4hivehivewebhcat  |
| HiveHcGcUtilGcTimeFgct | FGCT     | GC time_FGCT      | s        | Time consumed by Full GC                      | host4hivehivewebhcat, <br>id4hivehivewebhcat  |
| HiveHcGcUtilGcTimeGct  | GCT      | GC time_FGCT      | s        | Time used to collect garbage                      | host4hivehivewebhcat, <br/>id4hivehivewebhca  |
| HiveHcGcUtilGcTimeYgct | YGCT     | GC time_YGCT      | s        | Time consumed by Young GC                     | host4hivehivewebhcat, <br/>id4hivehivewebhca  |
| HiveHcGcUtilMemoryS0   | S0       | Memory space percentage_S0  | %        | Percentage of used Survivor 0 memory             | host4hivehivewebhcat, <br/>id4hivehivewebhca  |
| HiveHcGcUtilMemoryE    | E        | Memory space percentage_E   | %        | Percentage of used Eden memory                   | host4hivehivewebhcat, <br/>id4hivehivewebhca  |
| HiveHcGcUtilMemoryCcs  | CCS      | Memory space percentage_CCS | %        | Percentage of memory used by compressed class space | host4hivehivewebhcat, <br/>id4hivehivewebhca  |
| HiveHcGcUtilMemoryS1   | S1       | Memory space percentage_S1  | %        | Percentage of used Survivor 1 memory             | host4hivehivewebhcat, <br/>id4hivehivewebhca  |
| HiveHcGcUtilMemoryO    | O        | Memory space percentage_O   | %        | Percentage of used Old memory                    | host4hivehivewebhcat, <br/>id4hivehivewebhcat |
| HiveHcGcUtilMemoryM    | M        | Memory space percentage_M   | %        | Percentage of used Metaspace memory              | host4hivehivewebhcat, <br/>id4hivehivewebhcat |

## Overview of the Parameters in Each Dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| :----------------------------- | :------------------- | :--------------------------- | :-------------------------------------------- |
| Instances.N.Dimensions.0.Name  | id4hivemetastore     | Dimension name of the EMR instance ID       | String-type dimension name, such as id4hivemetastore    |
| Instances.N.Dimensions.0.Value | id4hivemetastore     | Specific EMR instance ID              | Specific EMR instance ID, such as emr-mm8bs222     |
| Instances.N.Dimensions.1.Name  | host4hivemetastore   | Dimension name of the node IP in the EMR instance | String-type dimension name, such as host4hivemetastore   |
| Instances.N.Dimensions.1.Value | host4hivemetastore   | Specific node IP in the EMR instance        | Specific node IP, such as 1.1.1.1               |
| Instances.N.Dimensions.0.Name  | id4hivehiveserver2   | Dimension name of the EMR instance ID       | String-type dimension name, such as id4hivehiveserver2  |
| Instances.N.Dimensions.0.Value | id4hivehiveserver2   | Specific EMR instance ID              | Specific EMR instance ID, such as emr-mm8bs222     |
| Instances.N.Dimensions.1.Name  | host4hivehiveserver2 | Dimension name of the node IP in the EMR instance | String-type dimension name, such as host4hivehiveserver2 |
| Instances.N.Dimensions.1.Value | host4hivehiveserver2 | Specific node IP in the EMR instance        | Specific node IP, such as 1.1.1.1               |
| Instances.N.Dimensions.0.Name  | id4hivehivewebhcat   | Dimension name of the EMR instance ID       | String-type dimension name, such as id4hivehivewebhcat  |
| Instances.N.Dimensions.0.Value | id4hivehivewebhcat   | Specific EMR instance ID              | Specific EMR instance ID, such as emr-mm8bs222     |
| Instances.N.Dimensions.1.Name  | host4hivehivewebhcat | Dimension name of the node IP in the EMR instance | String-type dimension name, such as host4hivehivewebhcat |
| Instances.N.Dimensions.1.Value | host4hivehivewebhcat | Specific node IP in the EMR instance        | Specific node IP, such as 1.1.1.1               |

## Input Parameters

 EMR (Hive) supports querying monitoring data based on the following three combinations of dimensions. The values for the input parameters are as follows: 

**1. To query the metric monitoring data of Hive - HiveMetaStore, use the following input parameters:**
&Namespace=QCE/TXMR_HIVE
&Instances.N.Dimensions.0.Name=id4hivemetastore
&Instances.N.Dimensions.0.Value=EMR instance ID 
&Instances.N.Dimensions.1.Name=host4hivemetastore
&Instances.N.Dimensions.1.Value=Specific node IP in the EMR instance 

**2. To query the metric monitoring data of Hive - HiveServer2, use the following input parameters:**
&Namespace=QCE/TXMR_HIVE
&Instances.N.Dimensions.0.Name=id4hivehiveserver2
&Instances.N.Dimensions.0.Value=EMR instance ID
&Instances.N.Dimensions.1.Name=host4hivehiveserver2
&Instances.N.Dimensions.1.Value=Specific node IP in the EMR instance 

**3. To query the metric monitoring data of Hive - HiveWebHcat, use the following input parameters:**
&Namespace=QCE/TXMR_HIVE
&Instances.N.Dimensions.0.Name=id4hivehivewebhcat
&Instances.N.Dimensions.0.Value=EMR instance ID
&Instances.N.Dimensions.1.Name=host4hivehivewebhcat
&Instances.N.Dimensions.1.Value=Specific node IP in the EMR instance 

