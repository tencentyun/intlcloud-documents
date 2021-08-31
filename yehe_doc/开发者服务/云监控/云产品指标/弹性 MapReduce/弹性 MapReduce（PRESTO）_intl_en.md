## Namespace

Namespace=QCE/TXMR_PRESTO

## Monitoring Metrics

### Presto - Overview

| Parameter | Metric Name | Unit | Description | Dimension |
| ------------------------------------------------------------ | -------------------------------------------- | -------- | ------------------ | ----------------- |
| EmrPrestoOverviewPresto<br>PrestoMNodesActive                | Number of nodes_Active                              | - | Number of active nodes       | id4prestooverview |
| EmrPrestoOverviewPresto<br/>PrestoMNodesTotal                | Number of nodes_Total                               | - | Total number of nodes         | id4prestooverview |
| EmrPrestoOverviewPresto<br/>PrestoMNodesFailed               | Number of nodes_Failed                              | - | Number of failed nodes       | id4prestooverview |
| EmrPrestoOverviewPresto<br/>PrestoMQueries<br>Runningqueries | Queries_RunningQueries                          | - | Total number of running queries | id4prestooverview |
| EmrPrestoOverviewPresto<br/>MQueriesOneMinute<br>Failedqueries | Query frequency_FailedQueries                       | Queries/min   | Total number of failed queries | id4prestooverview |
| EmrPrestoOverviewPresto<br/>MQueriesOneMinute<br>Abandonedqueries | Query frequency_AbandonedQueries                    | Queries/min   | Total number of aborted queries     | id4prestooverview |
| EmrPrestoOverviewPresto<br/>MQueriesOneMinute<br>Canceledqueries | Query frequency_CanceledQueries                     | Queries/min   | Total number of canceled queries     | id4prestooverview |
| EmrPrestoOverviewPresto<br/>MQueriesOneMinute<br>Completedqueries | Query frequency_CompletedQueries                    | Queries/min   | Total number of completed queries     | id4prestooverview |
| EmrPrestoOverviewPresto<br/>MQueriesOneMinute<br>Startedqueries | Query frequency_StartedQueries                      | Queries/min   | Total number of started queries     | id4prestooverview |
| EmrPrestoOverviewPresto<br/>MDataOneMinuteRate<br>Inputdatasizeoneminute | Volume of input/output data per minute_InputDataSizeOneMinute  | GB/min   | Data input rate       | id4prestooverview |
| EmrPrestoOverviewPresto<br/>MDataOneMinuteRate<br>Outputdatasizeoneminute | Volume of input/output data per minute_OutputDataSizeOneMinute | GB/min   | Data output rate        | id4prestooverview |

### Presto - OverviewOriginal

| Parameter | Metric Name | Unit | Description | Dimension |
| ------------------------------------------------------------ | -------------------------------------------- | -------- | ------------------ | ------------------------------------------- |
| EmrPrestoOverview<br>OriginalPresto<br>PrestoMNodesActive    | Number of nodes_Active                              | -        | Number of active nodes       | id4prestooverview, <br/>host4prestooverview |
| EmrPrestoOverview<br/>OriginalPresto<br/>PrestoMNodesTotal   | Number of nodes_Total                               | -        | Total number of nodes         | id4prestooverview, <br/>host4prestooverview |
| EmrPrestoOverview<br/>OriginalPresto<br/>PrestoMNodesFailed  | Number of nodes_Failed                              | -        | Number of failed nodes       | id4prestooverview, <br/>host4prestooverview |
| EmrPrestoOverview<br/>OriginalPresto<br/>PrestoMQueries<br>Runningqueries | Queries_RunningQueries                          | - | Total number of running queries | id4prestooverview, <br/>host4prestooverview |
| EmrPrestoOverview<br/>OriginalPresto<br/>MQueriesOneMinute<br>Failedqueries | Query frequency_FailedQueries                       | Queries/min   | Total number of failed queries | id4prestooverview, <br>host4prestooverview  |
| EmrPrestoOverview<br/>OriginalPresto<br/>MQueriesOneMinute Abandonedqueries | Query frequency_AbandonedQueries                    | Queries/min   | Total number of aborted queries     | id4prestooverview, <br/>host4prestooverview |
| EmrPrestoOverview<br/>OriginalPresto<br/>MQueriesOneMinute<br>Canceledqueries | Query frequency_CanceledQueries                     | Queries/min   | Total number of canceled queries     | id4prestooverview, <br/>host4prestooverview |
| EmrPrestoOverview<br/>OriginalPresto<br/>MQueriesOneMinute<br>Completedqueries | Query frequency_CompletedQueries                    | Queries/min   | Total number of completed queries     | id4prestooverview, <br/>host4prestooverview |
| EmrPrestoOverview<br/>OriginalPresto<br/>MQueriesOneMinute Startedqueries | Query frequency_StartedQueries                      | Queries/min   | Total number of started queries     | id4prestooverview, <br/>host4prestooverview |
| EmrPrestoOverview<br/>OriginalPresto<br/>MDataOneMinuteRate<br>Inputdatasizeoneminute | Volume of input/output data per minute_InputDataSizeOneMinute  | GB/min   | Data input rate       | id4prestooverview, <br/>host4prestooverview |
| EmrPrestoOverview<br/>OriginalPresto<br/>MDataOneMinuteRate<br>Outputdatasizeoneminute | Volume of input/output data per minute_OutputDataSizeOneMinute | GB/min   | Data output rate       | id4prestooverview, <br/>host4prestooverview |



### Presto - Worker

| Parameter | Metric Name | Unit | Description | Dimension |
| ------------------------------------------------------- | ---------------------------------------- | -------- | --------------------------------------- | -------------------------------------------------- |
| PrestoWGcUtilGcCountYgc                                 | GC count_YGC                               | -        | Young GC count                           | host4prestoprestoworker, <br>id4prestoprestoworker |
| PrestoWGcUtilGcCountFgc                                 | GC count_FGC                               | -        | Full GC count                            | host4prestoprestoworker, <br>id4prestoprestoworker |
| PrestoWGcUtilGcTimeFgct                                 | GC time_FGCT                              | s        | Time consumed by Full GC                        | host4prestoprestoworker, <br>id4prestoprestoworker |
| PrestoWGcUtilGcTimeGct                                  | GC time_FGCT                              | s        | Time used to collect garbage                         | host4prestoprestoworker, <br>id4prestoprestoworker |
| PrestoWGcUtilGcTimeYgct                                 | GC time_YGCT                              | s        | Time consumed by Young GC                       | host4prestoprestoworker, <br>id4prestoprestoworker |
| PrestoWGcUtilMemoryS0                                   | Memory space percentage_S0                          | %        | Percentage of used Survivor 0 memory                | host4prestoprestoworker, <br>id4prestoprestoworker |
| PrestoWGcUtilMemoryE      | Memory space percentage_E  | %        | Percentage of used Eden memory                     | host4prestoprestoworker, <br>id4prestoprestoworker |
| PrestoWGcUtilMemoryCcs                                  | Memory space percentage_CCS                         | %        | Percentage of memory used by compressed class space   | host4prestoprestoworker, <br>id4prestoprestoworker |
| PrestoWGcUtilMemoryS1                                   | Memory space percentage_S1                          | %        | Percentage of used Survivor 1 memory                | host4prestoprestoworker, <br>id4prestoprestoworker |
| PrestoWGcUtilMemoryO                                    | Memory space percentage_O  | %        | Percentage of used Old memory                      | host4prestoprestoworker, <br>id4prestoprestoworker |
| PrestoWGcUtilMemoryM                                    | Memory space percentage_M  | %        | Percentage of used Metaspace memory                | host4prestoprestoworker, <br>id4prestoprestoworker |
| PrestoWJvmMemMem<br>nonheapusedm                        | JVM memory_MemNonHeapUsedM                  | MB       | Size of the NonHeapMemory currently used by JVM | host4prestoprestoworker, <br>id4prestoprestoworker |
| PrestoWJvmMemMem<br>nonheapcommittedm                   | JVM memory_MemNonHeapCommittedM             | MB       | Size of the NonHeapMemory currently committed by JVM | host4prestoprestoworker, <br>id4prestoprestoworker |
| PrestoWJvmMem<br>Memheapusedm                           | JVM memory_MemHeapUsedM                     | MB       | Size of the HeapMemory currently used by JVM    | host4prestoprestoworker, <br>id4prestoprestoworker |
| PrestoWJvmMemMem<br>heapcommittedm                      | JVM memory_MemHeapCommittedM                | MB       | Size of the HeapMemory currently committed by JVM    | host4prestoprestoworker, <br>id4prestoprestoworker |
| PrestoWJvmMem<br>Memheapmaxm                            | JVM memory_MemHeapMaxM                      | MB       | Size of the HeapMemory configured by JVM            | host4prestoprestoworker, <br>id4prestoprestoworker |
| PrestoWJvmMem<br>Memheapinitm                           | JVM memory_MemHeapInitM                     | MB       | Size of the initial JVM HeapMem                 | host4prestoprestoworker, <br>id4prestoprestoworker |
| PrestoWJvmMem<br>Memnonheapinitm                        | JVM memory_MemNonHeapInitM                  | MB       | Size of the initial JVM NonHeapMem              | host4prestoprestoworker, <br>id4prestoprestoworker |
| PrestoWDataOneMinute<br>RateInputdatasizeoneminute      | Data input/output rate_InputDataSizeOneMinute  | GB/min   | Data input rate                            | host4prestoprestoworker, <br>id4prestoprestoworker |
| PrestoWDataOneMinute<br>RateOutputdata<br>sizeoneminute | Data input/output rate_OutputDataSizeOneMinute | GB/min   | Data output rate                            | host4prestoprestoworker, <br>id4prestoprestoworker |
| PrestoWThreadCount<br>Peakthreadcount                   | Number of threads_PeakThreadCount                 | - | Peak number of threads                              | host4prestoprestoworker, <br>id4prestoprestoworker |
| PrestoWThreadCount<br>Daemonthreadcount                 | Number of threads_DaemonThreadCount               | - | Number of threads                                | host4prestoprestoworker, <br>id4prestoprestoworker |
| PrestoWThreadCount<br>Threadcount                       | Number of threads_ThreadCount                     | - | Number of background threads                            | host4prestoprestoworker, <br>id4prestoprestoworker |
| PrestoWUptimeUptime                                     | Process run time_Uptime                      | s        | Process run time                            | host4prestoprestoworker, <br>id4prestoprestoworker |
| PrestoWStartTimeStarttime                               | Process start time_StartTime                   | s        | Process start time                            | host4prestoprestoworker, <br>id4prestoprestoworker |
| PrestoWOsFdCount<br>Maxfiledescriptorcount              | Number of file descriptors_MaxFileDescriptorCount      | - | Maximum number of file descriptors                        | host4prestoprestoworker, <br>id4prestoprestoworker |
| PrestoWOsFdCount<br>Openfiledescriptorcount             | Number of file descriptors_OpenFileDescriptorCount     | - | Number of opened file descriptors                      | host4prestoprestoworker, <br>id4prestoprestoworker |

### Presto - Coordinator

| Parameter | Metric Name | Unit | Description | Dimension |
| ------------------------------------------- | ------------------------------------ | -------- | --------------------------------------- | ------------------------------------------------------------ |
| PrestoMGc<br>UtilGcCountYgc                 | GC count_YGC                           | - | Young GC count                           | host4prestoprestocoordinator, <br>id4prestoprestocoordinator |
| PrestoMGc<br>UtilGcCountFgc                 | GC count_FGC                           | - | Full GC count                            | host4prestoprestocoordinator, <br>id4prestoprestocoordinator |
| PrestoMGc<br>UtilGcTimeFgct                 | GC time_FGCT                          | s        | Time consumed by Full GC                        | host4prestoprestocoordinator, <br>id4prestoprestocoordinator |
| PrestoMGc<br>UtilGcTimeGct                  | GC time_FGCT                          | s        | Time used to collect garbage                        | host4prestoprestocoordinator, <br>id4prestoprestocoordinator |
| PrestoMGc<br>UtilGcTimeYgct                 | GC time_YGCT                          | s        | Time consumed by Young GC                       | host4prestoprestocoordinator, <br>id4prestoprestocoordinator |
| PrestoMGc<br>UtilMemoryS0                   | Memory space percentage_S0                      | %        | Percentage of used Survivor 0 memory                | host4prestoprestocoordinator, <br>id4prestoprestocoordinator |
| PrestoMGcUtilMemoryE                        | Memory space percentage_E                       | %        | Percentage of used Eden memory                     | host4prestoprestocoordinator, <br>id4prestoprestocoordinator |
| PrestoMGc<br>UtilMemoryCcs                  | Memory space percentage_CCS                     | %        | Percentage of memory used by compressed class space   | host4prestoprestocoordinator, <br>id4prestoprestocoordinator |
| PrestoMGcUtilMemoryS1                       | Memory space percentage_S1                      | %        | Percentage of used Survivor 1 memory                | host4prestoprestocoordinator, <br>id4prestoprestocoordinator |
| PrestoMGcUtilMemoryO                        | Memory space percentage_O                       | %        | Percentage of used Old memory                      | host4prestoprestocoordinator, <br>id4prestoprestocoordinator |
| PrestoMGcUtilMemoryM                        | Memory space percentage_M                       | %        | Percentage of used Metaspace memory                | host4prestoprestocoordinator, <br>id4prestoprestocoordinator |
| PrestoMJvmMemMem<br>nonheapusedm            | JVM memory_MemNonHeapUsedM              | MB       | Size of the NonHeapMemory currently used by JVM | host4prestoprestocoordinator, <br>id4prestoprestocoordinator |
| PrestoMJvmMemMem<br>nonheapcommittedm       | JVM memory_MemNonHeapCommittedM         | MB       | Size of the NonHeapMemory currently committed by JVM | host4prestoprestocoordinator, <br>id4prestoprestocoordinator |
| PrestoMJvmMem<br>Memheapusedm               | JVM memory_MemHeapUsedM                 | MB       | Size of the HeapMemory currently used by JVM    | host4prestoprestocoordinator, <br>id4prestoprestocoordinator |
| PrestoMJvmMem<br>Memheapcommittedm          | JVM memory_MemHeapCommittedM            | MB       | Size of the HeapMemory currently committed by JVM    | host4prestoprestocoordinator, <br>id4prestoprestocoordinator |
| PrestoMJvmMem<br>Memheapmaxm                | JVM memory_MemHeapMaxM                  | MB       | Size of the HeapMemory configured by JVM            | host4prestoprestocoordinator, <br>id4prestoprestocoordinator |
| PrestoMJvmMem<br>Memheapinitm               | JVM memory_MemHeapInitM                 | MB       | Size of the initial JVM HeapMem                 | host4prestoprestocoordinator, <br>id4prestoprestocoordinator |
| PrestoMJvmMem<br>Memnonheapinitm            | JVM memory_MemNonHeapInitM              | MB       | Size of the initial JVM NonHeapMem              | host4prestoprestocoordinator, <br>id4prestoprestocoordinator |
| PrestoMThreadCount<br>Peakthreadcount       | Number of threads_PeakThreadCount             | - | Peak number of threads                              | host4prestoprestocoordinator, <br>id4prestoprestocoordinator |
| PrestoMThreadCount<br>Daemonthreadcount     | Number of threads_DaemonThreadCount           | - | Number of threads                                | host4prestoprestocoordinator, <br>id4prestoprestocoordinator |
| PrestoMThread<br>CountThreadcount           | Number of threads_ThreadCount                 | -  | Peak number of background threads                            | host4prestoprestocoordinator, <br>id4prestoprestocoordinator |
| PrestoMUptimeUptime                         | Process run time_Uptime                  | s        | Process run time                            | host4prestoprestocoordinator, <br>id4prestoprestocoordinator |
| PrestoMStart<br>TimeStarttime               | Process start time_StartTime               | s        | Process start time                            | host4prestoprestocoordinator, <br>id4prestoprestocoordinator |
| PrestoMOsFdCount<br>Maxfiledescriptorcount  | Number of file descriptors_MaxFileDescriptorCount  | -        | Maximum number of file descriptors                        | host4prestoprestocoordinator, <br>id4prestoprestocoordinator |
| PrestoMOsFdCount<br>Openfiledescriptorcount | Number of file descriptors_OpenFileDescriptorCount | - | Number of opened file descriptors                      | host4prestoprestocoordinator, <br/>id4prestoprestocoordinator |

## Overview of the Parameters in Each Dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| :----------------------------- | :--------------------------- | :--------------------------- | :----------------------------------------------------- |
| Instances.N.Dimensions.0.Name  | id4prestooverview            | Dimension name of the EMR instance ID       | String-type dimension name, such as id4prestooverview            |
| Instances.N.Dimensions.0.Value | id4prestooverview  | Specific EMR instance ID              | Specific EMR instance ID, such as emr-mm8bs222                |
| Instances.N.Dimensions.1.Name  | host4prestooverview          | Dimension name of the node IP in the EMR instance | String-type dimension name, such as host4prestooverview           |
| Instances.N.Dimensions.1.Value | host4prestooverview          | Specific node IP in the EMR instance        | Specific node IP, such as 1.1.1.1                        |
| Instances.N.Dimensions.0.Name  | id4prestoprestoworker        | Dimension name of the EMR instance ID       | String-type dimension name, such as id4prestoprestoworker        |
| Instances.N.Dimensions.0.Value | id4prestoprestoworker        | Specific EMR instance ID              | Specific EMR instance ID, such as emr-mm8bs222                |
| Instances.N.Dimensions.1.Name  | host4prestoprestoworker      | Dimension name of the node IP in the EMR instance | String-type dimension name, such as host4prestoprestoworker      |
| Instances.N.Dimensions.1.Value | host4prestoprestoworker      | Specific node IP in the EMR instance        | Specific node IP, such as 1.1.1.1                        |
| Instances.N.Dimensions.0.Name  | id4prestoprestocoordinator   | Dimension name of the EMR instance ID       | String-type dimension name, such as id27prestoprestocoordinator  |
| Instances.N.Dimensions.0.Value | id4prestoprestocoordinator   | Specific EMR instance ID              | Specific EMR instance ID, such as emr-mm8bs222                |
| Instances.N.Dimensions.1.Name  | host4prestoprestocoordinator | Dimension name of the node IP in the EMR instance | String-type dimension name, such as host4prestoprestocoordinator |
| Instances.N.Dimensions.1.Value | host4prestoprestocoordinator | Specific node IP in the EMR instance        | Specific node IP, such as 1.1.1.1                        |



## Input Parameters

EMR (Presto) supports querying monitoring data based on the following four combinations of dimensions. The values for the input parameters are as follows: 

**1. To query the metric monitoring data of Presto - Overview, use the following input parameters:**
&Namespace=QCE/TXMR_PRESTO
&Instances.N.Dimensions.0.Name=id4prestooverview
&Instances.N.Dimensions.0.Value=EMR instance ID

**2. To query the metric monitoring data of Presto - OverviewOriginal, use the following input parameters:**
&Namespace=QCE/TXMR_PRESTO
&Instances.N.Dimensions.0.Name=id4prestooverview
&Instances.N.Dimensions.0.Value=EMR instance ID
&Instances.N.Dimensions.1.Name=host4prestooverview
&Instances.N.Dimensions.1.Value=Specific node IP in the EMR instance

**3. To query the metric monitoring data of Presto - Worker, use the following input parameters:**
&Namespace=QCE/TXMR_PRESTO
&Instances.N.Dimensions.0.Name=id4prestoprestoworker
&Instances.N.Dimensions.0.Value=EMR instance ID 
&Instances.N.Dimensions.1.Name=host4prestoprestoworker
&Instances.N.Dimensions.1.Value=Specific node IP in the EMR instance

**4. To query the metric monitoring data of Presto - Coordinator, use the following input parameters:**
&Namespace=QCE/TXMR_PRESTO
&Instances.N.Dimensions.0.Name=id27prestoprestocoordinator
&Instances.N.Dimensions.0.Value=EMR instance ID
&Instances.N.Dimensions.1.Name=host4prestoprestocoordinator
&Instances.N.Dimensions.1.Value=Specific node IP in the EMR instance
