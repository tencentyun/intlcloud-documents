Namespace

Namespace=QCE/TXMR_IMPALA

## Monitoring Metrics

### Impala - catalog

| Metric | Description | Unit | Dimension |
| -------------------------------------------------- | ------------------------------------ | ----- | ------------------------------------ |
| ImpalaCatalogHeart<br/>beatIntervalTimeLast        | Heartbeat interval_Last                        | s     | host4impalacatalog, id4impalacatalog |
| ImpalaCatalogHeart<br>beatIntervalTimeMax          | Heartbeat interval_Max                         | s     | host4impalacatalog, id4impalacatalog |
| ImpalaCatalogHeart<br/>beatIntervalTimeMean        | Heartbeat interval_Mean                        | s     | host4impalacatalog, id4impalacatalog |
| ImpalaCatalogHeart<br/>beatIntervalTimeMin         | Heartbeat interval_Min                         | s     | host4impalacatalog, id4impalacatalog |
| ImpalaCatalogHeart<br/>beatIntervalTimeStddev      | Heartbeat interval_Stddev                      | s     | host4impalacatalog, id4impalacatalog |
| ImpalaCatalogJvmMem<br/>Memheapcommittedm          | JVM memory_MemHeapCommittedM            | MB    | host4impalacatalog, id4impalacatalog |
| ImpalaCatalogJvm<br/>MemMemheapinitm               | JVM memory_MemHeapInitM                 | MB    | host4impalacatalog, id4impalacatalog |
| ImpalaCatalogJvm<br/>MemMemheapmaxm                | JVM memory_MemHeapMaxM                  | MB    | host4impalacatalog, id4impalacatalog |
| ImpalaCatalogJvm<br/>MemMemheapusedm               | JVM memory_MemHeapUsedM                 | MB    | host4impalacatalog, id4impalacatalog |
| ImpalaCatalogJvmMem<br/>Memnonheapcommittedm       | JVM memory_MemNonHeapCommittedM         | MB    | host4impalacatalog, id4impalacatalog |
| ImpalaCatalogJvmMem<br/>Memnonheapinitm            | JVM memory_MemNonHeapInitM              | MB    | host4impalacatalog, id4impalacatalog |
| ImpalaCatalogJvmMem<br/>Memnonheapusedm            | JVM memory_MemNonHeapUsedM              | MB    | host4impalacatalog, id4impalacatalog |
| ImpalaCatalogOsFdCount<br/>Maxfiledescriptorcount  | Number of file descriptors_MaxFileDescriptorCount  | -    | host4impalacatalog, id4impalacatalog |
| ImpalaCatalogOsFdCount<br/>Openfiledescriptorcount | Number of file descriptors_OpenFileDescriptorCount | -    | host4impalacatalog, id4impalacatalog |
| ImpalaCatalogRss                                   | Resident set size_RSS                       | Bytes | host4impalacatalog, id4impalacatalog |
| ImpalaCatalogRtUptimeUptime                        | Process execution duration_Uptime                  | s     | host4impalacatalog, id4impalacatalog |
| ImpalaCatalogTcmalloc<br/>Pageheapfreebytes        | TCMalloc memory_PageheapFreeBytes       | Bytes | host4impalacatalog, id4impalacatalog |
| ImpalaCatalogTcmalloc<br/>Pageheapunmappedbytes    | TCMalloc memory_PageheapUnmappedBytes   | Bytes | host4impalacatalog, id4impalacatalog |
| ImpalaCatalogTcmalloc<br/>Physicalbytesreserved    | TCMalloc memory_PhysicalBytesReserved    | Bytes | host4impalacatalog, id4impalacatalog |
| ImpalaCatalogTcmalloc<br/>Totalbytesreserved       | TCMalloc memory_TotalBytesReserved      | Bytes | host4impalacatalog, id4impalacatalog |
| ImpalaCatalogTcmallocUsed                          | TCMalloc memory_Used                    | Bytes | host4impalacatalog, id4impalacatalog |
| ImpalaCatalogThreadCount<br/>Daemonthreadcount     | Number of threads_DaemonThreadCount           | -    | host4impalacatalog, id4impalacatalog |
| ImpalaCatalogThread<br/>CountThreadcount           | Number of threads_ThreadCount                 | -    | host4impalacatalog, id4impalacatalog |
| ImpalaCatalogThriftServer<br/>ConnectionsUsed      | Number of connections_Used                          | -    | host4impalacatalog, id4impalacatalog |



### Impala - StateStore

| Metric | Description | Unit | Dimension |
| -------------------------------------------------- | ---------------------------------- | ----- | ------------------------------------------ |
| ImpalaStatestoreRss                                | Resident set size_RSS                     | Bytes | host4impalastatestore, id4impalastatestore |
| ImpalaStatestoreStatestore<br/>LiveBackendsCount   | Number of StateStore subscribers_Count         | -    | host4impalastatestore, id4impalastatestore |
| ImpalaStatestoreTcmalloc<br/>Pageheapfreebytes     | TCMalloc memory_PageheapFreeBytes     | Bytes | host4impalastatestore, id4impalastatestore |
| ImpalaStatestoreTcmalloc<br/>Pageheapunmappedbytes | TCMalloc memory_PageheapUnmappedBytes | Bytes | host4impalastatestore, id4impalastatestore |
| ImpalaStatestoreTcmalloc<br/>Physicalbytesreserved | TCMalloc memory_PhysicalBytesReserved  | Bytes | host4impalastatestore, id4impalastatestore |
| ImpalaStatestoreTcmalloc<br/>Totalbytesreserved    | TCMalloc memory_TotalBytesReserved    | Bytes | host4impalastatestore, id4impalastatestore |
| ImpalaStatestoreTcmallocUsed                       | TCMalloc memory_Used                  | Bytes | host4impalastatestore, id4impalastatestore |
| ImpalaStatestoreThriftServer<br/>ConnectionsUsed   | Number of connections_Used                        | -    | host4impalastatestore, id4impalastatestore |
| ImpalaStatestoreRunning<br/>ThreadsCount           | Number of running threads_Count                   | -    | host4impalastatestore, id4impalastatestore |



### Impala - Daemon

| Metric | Description | Unit | Dimension |
| -------------------------------------------------- | ------------------------------------------------------------ | --------------- | ---------------------------------- |
| ImpalaDaemonJvmMem<br/>Memheapcommittedm           | JVM memory_MemHeapCommittedM                                    | MB              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonJvmMem<br/>Memheapinitm                | JVM memory_MemHeapInitM                                         | MB              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonJvmMem<br/>Memheapmaxm                 | JVM memory_MemHeapMaxM                                          | MB              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonJvmMem<br/>Memheapusedm                | JVM memory_MemHeapUsedM                                         | MB              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonJvmMem<br/>Memnonheapcommittedm        | JVM memory_MemNonHeapCommittedM                                 | MB              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonJvmMem<br/>Memnonheapusedm             | JVM memory_MemNonHeapUsedM                                      | MB              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonJvmMem<br/>Memnonheapinitm             | JVM memory_MemNonHeapInitM                                      | MB              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonOsFdCount<br/>Maxfiledescriptorcount   | Number of file descriptors_MaxFileDescriptorCount                          | -        | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonRtUptimeUptime                         | Process execution duration_Uptime                                          | s               | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonTcmalloc<br/>Pageheapfreebytes         | TCMalloc memory_PageheapFreeBytes                               | Bytes           | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonTcmalloc<br/>Pageheapunmappedbytes     | TCMalloc memory_PageheapUnmappedBytes                           | Bytes           | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonTcmalloc<br/>Physicalbytesreserved     | TCMalloc memory_PhysicalBytesReserved                            | Bytes           | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonTcmalloc<br/>Totalbytesreserved        | TCMalloc memory_TotalBytesReserved                              | Bytes           | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonTcmallocUsed                           | TCMalloc memory_Used                                            | Bytes           | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonThreadCount<br/>Daemonthreadcount      | Number of threads_DaemonThreadCount                                   | -              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonOsFdCount<br/>Openfiledescriptorcount  | Number of file descriptors_OpenFileDescriptorCount                         | -              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonThread<br/>CountThreadcount            | Number of threads_ThreadCount                                         | -              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonBeeswax<br/>FrontendConnInUse          | Number of Beeswax API client connections                                       | -              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonH2<br/>FrontendConnInUse               | Number of HS2 API client connections_ConnInUse                                | -              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonBeeswax<br/>FrontendTotalconns         | Number of Beeswax API client connections_TotalConns                           | - | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonBeeswaxFrontend<br/>Connsetupqueuesize | Number of Beeswax API client connections_ConnSetupQueueSize                   | - | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonH2<br/>FrontendTotalconns              | Number of HS2 API client connections_TotalConns                               | - | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonH2Frontend<br/>Connsetupqueuesize      | Number of HS2 API client connections_ConnSetupQueueSize                       | - | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonThreadManager<br/>Runningthreads       | Thread manager_RunningThreads                                    | - | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonThreadManager<br/>Totalcreatedthreads  | Thread manager_TotalCreatedThreads                               | - | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonMem<br/>TrackerProcess1Limit           | Memory manager limit_Limit                                         | Bytes   | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonMemTracker<br/>ProcessBytesOverlimit   | Amount of memory exceeding the memory limit_OverLimit                             | Bytes   | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonBeeswaxFronted<br/>Timeoutcnncrequests | Number of timed-out Beeswax API connections_TimeOutCnncRequests                 | - | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonServerBackend<br/>Connsetupqueuesize   | Number of Impala backend server connection requests that timed out waiting for setup_ConnSetupQueueSize | - | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonServerBackend1<br/>Timeoutcnncrequests | Number of Impala_be connection requests that timed out waiting for setup_TimeOutCnncRequests     | - | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonServer<br/>Backend2Totalconnections    | Total number of Impala backend client connections to this Impala daemon_TotalConnections | - | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonRequest<br/>PoolServiceResolveTotal    | Time spent parsing requests from request pool (milliseconds)_Total                               | ms        | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonMemoryRss                              | Resident set size for this process_RSS                                       | Bytes   | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonCluster<br/>MembershipBackendsTotal    | Total number of backends registered in the StateStore_Total                               | - | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonServerQuery<br/>DurationsMsCount       | Query delay release_Count                                           | ms        | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonServer<br/>QueryDurationsMsSum         | Query delay release_Sum                                             | ms        | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonServer1<br/>Numfilesopenforinsert      | Number of opened and written HDFS files_NumFilesOpenForInsert               | - | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonServer2<br/>Scanrangestotal            | Scan range read during the lifecycle of the process_ScanRangesTotal                 | - | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonServer3<br/>Numopenbeeswaxsessions     | Number of opened Beeswax sessions_NumOpenBeeswaxSessions                   | - | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonServer4<br/>Numfragments               | Total number of query fragments processed during the lifecycle of the process_NumFragments              | - | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonServer14<br/>Hedgedreadops             | Number of hedged read attempts_HedgedReadOps                            | - | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonServer5<br/>Numqueries                 | Total number of queries processed during the lifecycle of the process_NumQueries                      | - | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonServer6<br/>Resultsetcachetotalnumrows | Total number of rows supporting caching HS2 FETCH_FIRST_ResultSetCacheTotalNumRows    | - | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonServer8<br/>Numqueriesregistered       | Total number of queries registered on this Impala server_NumQueriesRegistered          | - | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonServer9<br/>Numqueriesexecuted         | Total number of queries executed on the backend_NumQueriesExecuted                                | - | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonServer10<br/>Numsessionsexpired        | Number of sessions terminated due to inactivity_NumSessionsExpired                    | - | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonServer11<br/>Numqueriesexpired         | Number of queries terminated due to inactivity_NumQueriesExpired                     | - | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonServer12<br/>Numopenhs2sessions        | Number of opened HS2 sessions_NumOpenHS2Sessions                             | - | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonCatalog1Numtables                      | Number of tables in the catalog_NumTables                                  | - | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonCatalog2<br/>Numdatabases              | Number of databases in the catalog_NumDatabases                           | - | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonServerIo<br/>Mgr2Byteswritten          | Number of bytes written to the disk by the I/O manager_BytesWritten                        | Bytes   | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonServerIo<br/>Mgr3Numopenfiles          | Number of files opened by the I/O manager_NumOpenFiles                            | - | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonServerIo<br/>Mgr5Localbytesread        | Number of read local bytes_LocalBytesRead                              | Bytes   | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonBeeswax<br/>FrSvcThWaitTimeP20         | Beeswax API client wait time for service thread establishment_P20                    | us              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonBeeswax<br/>FrSvcThWaitTimeP50         | Beeswax API client wait time for service thread establishment_P50                    | us              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonBeeswax<br/>FrSvcThWaitTimeP70         | Beeswax API client wait time for service thread establishment_P70                    | us              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonBeeswax<br/>FrSvcThWaitTimeP90         | Beeswax API client wait time for service thread establishment_P90                    | us              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonBeeswax<br/>FrSvcThWaitTimeP95         | Beeswax API client wait time for service thread establishment_P95                    | us              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemon<br/>ExDsClassChMisses                 | Number of cache misses in external data source cache class_Misses                        | -              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonH2<br/>FrConnSetupTimeP20              | HS2 API client wait time for connection establishment_P20                            | us              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonH2<br/>FrConnSetupTimeP50              | HS2 API client wait time for connection establishment_P50                            | us              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonH2<br/>FrConnSetupTimeP70              | HS2 API client wait time for connection establishment_P70                            | us              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonH2<br/>FrConnSetupTimeP90              | HS2 API client wait time for connection establishment_P90                            | us              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonH2<br/>FrConnSetupTimeP95              | HS2 API client wait time for connection establishment_P95                            | us              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonH2<br/>FrSvcThWaitTimeCount            | HS2 API client wait time for service thread establishment_Count                      | us              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonH2<br/>FrSvcThWaitTimeP20              | HS2 API client wait time for service thread establishment_P20                        | us              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonH2<br/>FrSvcThWaitTimeP50              | HS2 API client wait time for service thread establishment_P50                        | us              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonH2<br/>FrSvcThWaitTimeP70              | HS2 API client wait time for service thread establishment_P70                        | us              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemon<br/>H2FrSvcThWaitTimeP90              | HS2 API client wait time for service thread establishment_P90                        | us              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemon<br/>H2FrSvcThWaitTimeP95              | HS2 API client wait time for service thread establishment_P95                        | us              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemon<br/>H2FrSvcThWaitTimeSum              | HS2 API client wait time for service thread establishment_Sum                        | us              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonMem<br/>TrCsrvCurrentusagebytes        | Number of bytes used by ControlService_CurrentUsageBytes                   | Bytes           | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonMem<br/>TrCsrvPeakusagebytes           | Number of bytes used by ControlService_PeakUsageBytes                      | Bytes           | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonMem<br/>TrDssrvCurrentusagebytes       | Number of bytes used by DataStreamService_currentusagebytes                | Bytes           | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonMem<br/>TrDssrvPeakusagebytes          | Number of bytes used by DataStreamService_PeakUsageBytes                   | Bytes           | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonRpc<br/>CsrvRpcsqueueoverflow          | Number of rejected ControlStreamService service queue overflows_RpcsQueueOverflow     | -              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonRpc<br/>DssrvRpcsqueueoverflow         | Number of rejected DataStreamService service queue overflows_RpcsQueueOverflow        | -              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonServer<br/>BaConnSetupTimeCount        | Time spent by the Impala_be client waiting for connection establishment_Count              | us              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonServer<br/>BaConnSetupTimeP20          | Time spent by the Impala_be client waiting for connection establishment_P20                | us              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonServer<br/>BaConnSetupTimeP50          | Time spent by the Impala_be client waiting for connection establishment_P50                | us              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonServer<br/>BaConnSetupTimeP70          | Time spent by the Impala_be client waiting for connection establishment_P70                | us              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonServer<br/>BaConnSetupTimeP90          | Time spent by the Impala_be client waiting for connection establishment_P90                | us              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonServer<br/>BaConnSetupTimeP95          | Time spent by the Impala_be client waiting for connection establishment_P95                | us              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonServer<br/>BaConnSetupTimeSum          | Time spent by the Impala_be client waiting for connection establishment_Sum                | us              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonServer<br/>BaSvcThWaitTimeCount        | Time spent by the Impala_be client waiting for the service thread_Count              | us              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonServer<br/>BaSvcThWaitTimeP20          | Time spent by the Impala_be client waiting for the service thread_P20                | us              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonServer<br/>BaSvcThWaitTimeP50          | Time spent by the Impala_be client waiting for the service thread_P50                | us              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonServer<br/>BaSvcThWaitTimeP70          | Time spent by the Impala_be client waiting for the service thread_P70                | us              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonServer<br/>BaSvcThWaitTimeP90          | Time spent by the Impala_be client waiting for the service thread_P90                | us              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonServer<br/>BaSvcThWaitTimeP95          | Time spent by the Impala_be client waiting for the service thread_P95                | us              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonServer<br/>BaSvcThWaitTimeSum          | Time spent by the Impala_be client waiting for the service thread_sum                | us              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonServer<br/>QueryDurationsMsP20         | Query delay release_P20                                             | ms              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonServer<br/>QueryDurationsMsP50         | Query delay release_P50                                             | ms              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonServer<br/>QueryDurationsMsP70         | Query delay release_P70                                             | ms              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonServer<br/>QueryDurationsMsP90         | Query delay release_P90                                             | ms              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonServer<br/>QueryDurationsMsP95         | Query delay release_P95                                             | ms              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonSrvIoMgr<br/>Numfilehandlesoutstanding | Number of used HDFS file handles_NumFileHandlesOutstanding               | -              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonSrvScanran<br/>gesnummissingvolumid    | Total number of scan ranges read during the lifecycle of the process without volum metadata_ScanRangesNumMissingVolumId | -              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonH2<br/>HttpFrSvcThWaitTimeCount        | HS2 HTTP API client wait time for service thread establishment_Count                 | us              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonH2<br/>HttpFrSvcThWaitTimeP20          | HS2 HTTP API client wait time for service thread establishment_P20                   | us              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonH2<br/>HttpFrSvcThWaitTimeP50          | HS2 HTTP API client wait time for service thread establishment_P50                   | us              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonH2<br/>HttpFrSvcThWaitTimeP70          | HS2 HTTP API client wait time for service thread establishment_P70                   | us              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonH2<br/>HttpFrSvcThWaitTimeP90          | HS2 HTTP API client wait time for service thread establishment_P90                   | us              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonH2<br/>HttpFrSvcThWaitTimeP95          | HS2 HTTP API client wait time for service thread establishment_P95                   | us              | host4impaladaemon, id4impaladaemon |
| ImpalaDaemonH2<br/>HttpFrSvcThWaitTimeSum          | HS2 HTTP API client wait time for service thread establishment_Sum                   | us              | host4impaladaemon, id4impaladaemon |

## Dimensions and Parameters

| Parameter | Dimension | Description | Format |
| :----------------------------- | :-------------------- | :--------------------------- | :----------------------------------------------------------- |
| Instances.N.Dimensions.0.Name  | host4impalacatalog    | Dimension name of the EMR instance node IP | Enter a string-type dimension name, such as `host4impalacatalog`                 |
| Instances.N.Dimensions.0.Value | host4impalacatalog    | Specific node IP in the EMR instance        | Enter a specific node IP, which can be obtained by clicking <b>Instance > Cluster Resource > Resource Management > Node Private IP in the [EMR console](https://console.cloud.tencent.com/emr)</b> or calling the [DescribeClusterNodes](https://intl.cloud.tencent.com/document/product/1026/35198) API. |
| Instances.N.Dimensions.1.Name  | id4impalacatalog      | Dimension name of the EMR instance ID        | Enter a string-type dimension name, such as `id4impalacatalog`                   |
| Instances.N.Dimensions.1.Value | id4impalacatalog      | Dimension name of the EMR instance ID  | Enter an EMR instance ID, such as `emr-mm8bs222`                     |
| Instances.N.Dimensions.0.Name  | host4impalastatestore | Dimension name of the EMR instance ID        | Enter a string-type dimension name, such as `host4impalastatestore`              |
| Instances.N.Dimensions.0.Value | host4impalastatestore | Specific node IP in the EMR instance        | Enter a specific node IP, which can be obtained by clicking <b>Instance > Cluster Resource > Resource Management > Node Private IP in the [EMR console](https://console.cloud.tencent.com/emr)</b> or calling the [DescribeClusterNodes](https://intl.cloud.tencent.com/document/product/1026/35198) API. |
| Instances.N.Dimensions.1.Name  | id4impalastatestore   | Dimension name of the EMR instance ID        | Enter a string-type dimension name, such as `id4impalastatestore`                |
| Instances.N.Dimensions.1.Value | id4impalastatestore   | Dimension name of the EMR instance ID  | Enter an EMR instance ID, such as `emr-mm8bs222`                     |
| Instances.N.Dimensions.0.Name  | host4impaladaemon     | Dimension name of the EMR instance ID        | Enter a string-type dimension name, such as `host4impaladaemon`                  |
| Instances.N.Dimensions.0.Value | host4impaladaemon     | Specific node IP in the EMR instance        | Enter a specific node IP, which can be obtained by clicking <b>Instance > Cluster Resource > Resource Management > Node Private IP in the [EMR console](https://console.cloud.tencent.com/emr)</b> or calling the [DescribeClusterNodes](https://intl.cloud.tencent.com/document/product/1026/35198) API. |
| Instances.N.Dimensions.1.Name  | id4impaladaemon       | Dimension name of the EMR instance ID        | Enter a string-type dimension name, such as `id4impaladaemon`                    |
| Instances.N.Dimensions.1.Value | id4impaladaemon       | Dimension name of the EMR instance ID  | Enter an EMR instance ID, such as `emr-mm8bs222`                     |

## Input Parameters

#### To query the monitoring data of an EMR instance (Impala - catalog), use the following input parameters:

Namespace=QCE/TXMR_IMPALA
&Instances.N.Dimensions.0.Name=host4impalacatalog
&Instances.N.Dimensions.0.Value=Specific node IP in the EMR instance
&Instances.N.Dimensions.1.Name=id4impalacatalog
&Instances.N.Dimensions.1.Value=EMR instance ID 



#### To query the monitoring data of an EMR instance (Impala - StateStore), use the following input parameters:

Namespace=QCE/TXMR_IMPALA
&Instances.N.Dimensions.0.Name=host4impalastatestore
&Instances.N.Dimensions.0.Value=Specific node IP in the EMR instance
&Instances.N.Dimensions.1.Name=id4impalastatestore
&Instances.N.Dimensions.1.Value=EMR instance ID 



#### To query the monitoring data of an EMR instance (Impala - daemon), use the following input parameters:

Namespace=QCE/TXMR_IMPALA
&Instances.N.Dimensions.0.Name=host4impaladaemon
&Instances.N.Dimensions.0.Value=Specific node IP in the EMR instance
&Instances.N.Dimensions.1.Name=id4impaladaemon
&Instances.N.Dimensions.1.Value=EMR instance ID 



