### COSRanger - Server

| Metric Name                                          | Unit  | Description                                                  |
| ------------------------------------------------- | --------- | --------------------------------------------------------- |
| YGC                                               | -        | Number of young GCs                                             |
| FGC                                               | -        | Number of Full GCs                                              |
| FGCT                                              | s         | Time taken by full GCs                                          |
| GCT                                               | s         | Time taken by GCs                                          |
| YGCT                                              | s         | Time taken by young GCs                                         |
| S0                                                | %         | Percentage of used survivor 0 memory                                  |
| E                                                 | %         | Percentage of used eden memory                                       |
| CCS                                               | %         | Percentage of used compressed class space memory                     |
| S1                                                | %         | Percentage of used survivor 1 memory                                  |
| O                                                 | %         | Percentage of used old memory                                        |
| M                                                 | %         | Percentage of used metaspace memory                                  |
| MemNonHeapUsedM                                   | MB        | Amount of NonHeapMemory used by the JVM                   |
| MemNonHeapCommittedM         | MB       | Amount of NonHeapMemory committed by the JVM                        |
| MemHeapUsedM                                      | MB        | Amount of HeapMemory used by the JVM                      |
| MemHeapCommittedM                                 | MB        | Amount of HeapMemory committed by the JVM                      |
| MemHeapMaxM                                       | MB        | Amount of HeapMemory configured for the JVM                              |
| MemHeapInitM                                      | MB        |  Initial amount of HeapMemory for the JVM                                 |
| MemNonHeapInitM                                   | MB        | Initial amount of NonHeapMemory for the JVM                             |
| ProcessCpuLoad                                    | %         | CPU utilization                                                |
| MaxFileDescriptorCount               | -       | Maximum number of file descriptors                                             |
| OpenFileDescriptorCount | -       | Number of opened file descriptors                                           |
| ProcessCpuTime                                    | ms        | Total CPU usage time                                          |
| Uptime                                            | s         | Process run time                                              |
| ThreadCount                                       | -        | Number of threads                                                  |
| PeckThreadCount                                   | -        | Peak number of threads                                              |
| DaemonThreadCount                                 | -        | Number of daemon threads                                             |
| check statistics\_PermissionAllowCnt                     | - | check statistics: total number of approved authentication policies                                  |
| check statistics\_AuthDenyCnt                            | - | check statistics: total number of authentication failures                                  |
| check statistics\_PermissionDenyCnt                      | - | check statistics: total number of disapproved authentication policies                                  |
| Authentication success statistics\_Qps                                  | - | Authentication success statistics: number of queries per second                                  |
| Authentication success statistics\_Total_5m                             | - | Authentication success statistics: number of requests within five minutes                              |
| Authentication success statistics\_Total_1m                             | - | Authentication success statistics: number of requests within one minute                              |
| Authentication success statistics\_Qps_5m                               | - | Authentication success statistics: average number of requests per second within five minutes                             |
| Authentication success statistics\_Qps_1m                               | - | Authentication success statistics: average number of requests per second within one minute                            |
| accessStat\_DELETE operation statistics\_Qps                    | - | accessStat_DELETE operation statistics: number of queries per second                    |
| accessStat_DELETE operation statistics\_Total_5m               | - | accessStat_DELETE operation statistics: number of requests within five minutes                |
| accessStat_DELETE operation statistics\_Total_1m               | - | accessStat_DELETE operation statistics: number of requests within one minute                |
| accessStat_DELETE operation statistics\_Qps_5m                 | - | accessStat_DELETE operation statistics: average number of requests per second within five minutes              |
| accessStat_DELETE operation statistics\_Qps_1m                 | - | accessStat_DELETE operation statistics: average number of requests per second within one minute              |
| accessStat_LIST operation statistics\_Qps                      | - | accessStat_LIST operation statistics: Number of queries per second                      |
| accessStat_LIST operation statistics\_Total_5m                 | - | accessStat_LIST operation statistics: number of requests within five minutes                  |
| accessStat_LIST operation statistics\_Total_1m                 | - | accessStat_LIST operation statistics: number of requests within one minute                  |
| accessStat_LIST operation statistics\_Qps_5m                   | - | accessStat_LIST operation statistics: average number of requests per second within five minutes                |
| accessStat_LIST operation statistics\_Qps_1m                   | - | accessStat_LIST operation statistics: average number of requests per second within one minute                |
| accessStat_READ operation statistics\_Qps                      | - | accessStat_READ operation statistics: number of queries per second                      |
| accessStat_READ operation statistics\_Total_5m                 | - | accessStat_READ operation statistics: number of requests within five minutes                  |
| accessStat_READ operation statistics\_Total_1m                 | - | accessStat_READ operation statistics: number of requests within one minute                  |
| accessStat_READ operation statistics\_Qps_5m                   | - | accessStat_READ operation statistics: average number of requests per second within five minutes                |
| accessStat_READ operation statistics\_Qps_1m                   | - | accessStat_READ operation statistics: average number of requests per second within one minute                |
| accessStat_WRITE operation statistics\_Qps                     | - | accessStat_WRITE operation statistics: number of queries per second                     |
| accessStat_WRITE operation statistics\_Total_5m                | - | accessStat_WRITE operation statistics: number of requests within five minutes                 |
| accessStat_WRITE operation statistics\_Total_1m                | - | accessStat_WRITE operation statistics: number of requests within one minute                 |
| accessStat_WRITE operation statistics\_Qps_5m                  | - | accessStat_WRITE operation statistics: average number of requests per second within five minutes               |
| accessStat_WRITE operation statistics\_Qps_1m                  | - | accessStat_WRITE operation statistics: average number of requests per second within one minute               |
| rpc_getRangerAuthPolicy call statistics\_Qps            | - | rpc_getRangerAuthPolicy call statistics: number of queries per second            |
| rpc_getRangerAuthPolicy call statistics\_Total_5m       | - | rpc_getRangerAuthPolicy call statistics: number of requests within five minutes        |
| rpc_getRangerAuthPolicy call statistics\_Total_1m       | - | rpc_getRangerAuthPolicy call statistics: number of requests within one minute        |
| rpc_getRangerAuthPolicy call statistics\_Qps_5m         | - | rpc_getRangerAuthPolicy call statistics: average number of requests per second within five minutes      |
| rpc_getRangerAuthPolicy call statistics\_Qps_1m         | - | rpc_getRangerAuthPolicy call statistics: average number of requests per second within one minute      |
| rpc_checkPermission call statistics\_Qps                | - | rpc_checkPermission call statistics: number of queries per second                |
| rpc_checkPermission call statistics\_Total_5m           | - | rpc_checkPermission call statistics: number of requests within five minutes            |
| rpc_checkPermission call statistics\_Total_1m           | - | rpc_checkPermission call statistics: number of requests within one minute            |
| rpc_checkPermission call statistics\_Qps_5m             | - | rpc_checkPermission call statistics: average number of requests per second within five minutes          |
| rpc_checkPermission call statistics\_Qps_1m             | - | rpc_checkPermission call statistics: average number of requests per second within one minute          |
| rpc_getDelegationToken call statistics\_Qps             | - | rpc_getDelegationToken call statistics: number of queries per second             |
| rpc_getDelegationToken call statistics\_Total_5m        | - | rpc_getDelegationToken call statistics: number of requests within five minutes         |
| rpc_getDelegationToken call statistics\_Total_1m        | - | rpc_getDelegationToken call statistics: number of requests within one minute         |
| rpc_getDelegationToken call statistics\_Qps_5m          | - | rpc_getDelegationToken call statistics: average number of requests per second within five minutes       |
| rpc_getDelegationToken call statistics\_Qps_1m          | - | rpc_getDelegationToken call statistics: average number of requests per second within one minute       |
| rpc_renewDelegationToken call statistics\_Qps           | - | rpc_renewDelegationToken call statistics: number of queries per second          |
| rpc_renewDelegationToken call statistics\_Total_5m      | - | rpc_renewDelegationToken call statistics: number of requests within five minutes       |
| rpc_renewDelegationToken call statistics\_Total_1m      | - | rpc_renewDelegationToken call statistics: number of requests within one minute       |
| rpc_renewDelegationToken call statistics\_Qps_5m     | - | rpc_renewDelegationToken call statistics: average number of requests per second within five minutes     |
| rpc_renewDelegationToken call statistics\_Qps_1m     | - | rpc_renewDelegationToken call statistics: average number of requests per second within one minute     |
| rpc_cancelDelegationToken call statistics\_Qps          | - | rpc_cancelDelegationToken call statistics: number of queries per second          |
| rpc_cancelDelegationToken call statistics\_Total_5m     | - | rpc_cancelDelegationToken call statistics: number of requests within five minutes     |
| rpc_cancelDelegationToken call statistics\_Total_1m     | - | rpc_cancelDelegationToken call statistics: number of requests within one minute      |
| rpc_cancelDelegationToken call statistics\_Qps_5m     | - | rpc_cancelDelegationToken call statistics: average number of requests per second within five minutes    |
| rpc_cancelDelegationToken call statistics\_Qps_1m    | - | rpc_cancelDelegationToken call statistics:  average number of requests per second within one minute    |
| rpc_getSTS call statistics\_Qps                         | - | rpc_getSTS call statistics: queries per second                         |
| rpc_getSTS call statistics\_Total_5m                    | - | rpc_getSTS call statistics: number of requests within five minutes                     |
| rpc_getSTS call statistics\_Total_1m                    | - | rpc_getSTS call statistics: number of requests within one minute                     |
| rpc_getSTS call statistics\_Qps_5m                      | - | rpc_getSTS call statistics: average number of requests per second within five minutes                   |
| rpc_getSTS call statistics\_Qps_1m                      | - | rpc_getSTS call statistics: average number of requests per second within one minute                   |
| cosRpc_getSTS call time\_Cost_Avg                   | μs  | cosRpc_getSTS call time: average time taken per call within the current second                |
| cosRpc_getSTS call time\_Cost_Avg_1m                | μs  | cosRpc_getSTS call time: average time taken per call within one minute                    |
| cosRpc_getSTS call time\_Cost_Avg_5m                | μs  | cosRpc_getSTS call time: average time taken per call within five minutes                    |
| cosRpc_getSTS call time\_Cost_Max                   | μs  | cosRpc_getSTS call time: maximum time taken by a call within the current second                |
| cosRpc_getSTS call time\_Cost_Max_1m                | μs  | cosRpc_getSTS call time: maximum time taken by a call within one minute                  |
| cosRpc_getSTS call time\_Cost_Max_5m                | μs  | cosRpc_getSTS call time: maximum time taken by a call within five minutes                  |
| cosRpc_getSTS call time\_Cost_Min                   | μs  | cosRpc_getSTS call time: minimum time taken by a call within the current second               |
| cosRpc_getSTS call time\_Cost_Min_1m                | μs  | cosRpc_getSTS call time: minimum time taken by a call within one minute                  |
| cosRpc_getSTS call time\_Cost_Min_5m                | μs  | cosRpc_getSTS call time: minimum time taken by a call within five minutes                  |
| cosRpc_renewDelegationToken call time\_Cost_Avg | μs  | cosRpc_renewDelegationToken call time: average time taken per call within the current second 
| cosRpc_renewDelegationToken call time\_Cost_Avg_1m  | μs  | cosRpc_renewDelegationToken call time: average time taken per call within one minute      |
| cosRpc_renewDelegationToken call time\_Cost_Avg_5m  | μs  | cosRpc_renewDelegationToken call time: average time taken per call within five minutes      |
| cosRpc_renewDelegationToken call time\_Cost_Max     | μs  | cosRpc_renewDelegationToken call time: maximum time taken by a call within the current second  |
| cosRpc_renewDelegationToken call time\_Cost_Max_1m  | μs  | cosRpc_renewDelegationToken call time: maximum time taken by a call within one minute    |
| cosRpc_renewDelegationToken call time\_Cost_Max_5m  | μs  | cosRpc_renewDelegationToken call time: maximum time taken by a call within five minutes    |
| cosRpc_renewDelegationToken call time\_Cost_Min     | μs  | cosRpc_renewDelegationToken call time: minimum time taken by a call within the current second  |
| cosRpc_renewDelegationToken call time\_Cost_Min_1m  | μs  | cosRpc_renewDelegationToken call time: minimum time taken by a call within one minute   |
| cosRpc_renewDelegationToken call time\_Cost_Min_5m  | μs  | cosRpc_renewDelegationToken call time: minimum time taken by a call within five minutes    |
| cosRpc_cancelDelegationToken call time\_Cost_Avg    | μs  | cosRpc_cancelDelegationToken call time: average time taken per call within the current second |
| cosRpc_cancelDelegationToken call time\_Cost_Avg_1m | μs  | cosRpc_cancelDelegationToken call time: average time taken per call within one minute     |
| cosRpc_cancelDelegationToken call time\_Cost_Avg_5m | μs  | cosRpc_cancelDelegationToken call time: average time taken per call within five minutes     |
| cosRpc_cancelDelegationToken call time\_Cost_Max    | μs  | cosRpc_cancelDelegationToken call time: maximum time taken by a call within the current second |
| cosRpc_cancelDelegationToken call time\_Cost_Max_1m | μs  | cosRpc_cancelDelegationToken call time: maximum time taken by a call within one minute   |
| cosRpc_cancelDelegationToken call time\_Cost_Max_5m | μs  | cosRpc_cancelDelegationToken call time: maximum time taken by a call within five minutes   |
| cosRpc_cancelDelegationToken call time\_Cost_Min    | μs  | cosRpc_cancelDelegationToken call time: minimum time taken by a call within the current second |
| cosRpc_cancelDelegationToken call time\_Cost_Min_1m | μs  | cosRpc_cancelDelegationToken call time: minimum time taken by a call within one minute   |
| cosRpc_cancelDelegationToken call time\_Cost_Min_5m | μs  | cosRpc_cancelDelegationToken call time: minimum time taken by a call within five minutes   |
| cosRpc_getDelegationToken call time\_Cost_Avg       | μs  | cosRpc_getDelegationToken call time: average time taken per call within the current second |
| cosRpc_getDelegationToken call time\_Cost_Avg_1m    | μs  | cosRpc_getDelegationToken call time: average time taken per call within one minute    |
| cosRpc_getDelegationToken call time\_Cost_Avg_5m    | μs  | cosRpc_getDelegationToken call time: average time taken per call within five minutes    |
| cosRpc_getDelegationToken call time\_Cost_Max       | μs  | cosRpc_getDelegationToken call time: maximum time taken by a call within the current second |
| cosRpc_getDelegationToken call time\_Cost_Max_1m    | μs  | cosRpc_getDelegationToken call time: maximum time taken by a call within one minute |
| cosRpc_getDelegationToken call time\_Cost_Max_5m    | μs  | cosRpc_getDelegationToken call time: maximum time taken by a call within five minutes |
| cosRpc_getDelegationToken call time\_Cost_Min       | μs  | cosRpc_getDelegationToken call time: minimum time taken by a call within the current second  |
| cosRpc_getDelegationToken call time\_Cost_Min_1m    | μs  | cosRpc_getDelegationToken call time: minimum time taken by a call within one minute |
| cosRpc_getDelegationToken call time\_Cost_Min_5m | μs  | cosRpc_getDelegationToken call time: minimum time taken by a call within five minutes    |
| cosRpc_checkPermission call time\_Cost_Avg         | μs  | cosRpc_checkPermission call time: average time taken per call within the current second       |
| cosRpc_checkPermission call time\_Cost_Avg_1m     | μs  | cosRpc_checkPermission call time: average time taken per call within one minute           |
| cosRpc_checkPermission call time\_Cost_Avg_5m     | μs  | cosRpc_checkPermission call time: average time taken per call within five minutes           |
| cosRpc_checkPermission call time\_Cost_Max        | μs  | cosRpc_checkPermission call time: maximum time taken by a call within the current second       |
| cosRpc_checkPermission call time\_Cost_Max_1m    | μs  | cosRpc_checkPermission call time: maximum time taken by a call within one minute         |
| cosRpc_checkPermission call time\_Cost_Max_5m    | μs  | cosRpc_checkPermission call time: maximum time taken by a call within five minutes         |
| cosRpc_checkPermission call time\_Cost_Min          | μs  | cosRpc_checkPermission call time: minimum time taken by a call within the current second       |
| cosRpc_checkPermission call time\_Cost_Min_1m     | μs  | cosRpc_checkPermission call time: minimum time taken by a call within one minute        |
| cosRpc_checkPermission call time\_Cost_Min_5m       | μs  | cosRpc_checkPermission call time: minimum time taken by a call within five minutes       |
| cosRpc_getRangerAuthPolicy call time\_Cost_Avg     | μs  | cosRpc_getRangerAuthPolicy call time: average time taken per call within the current second |
| cosRpc_getRangerAuthPolicy call time\_Cost_Avg_1m   | μs  | cosRpc_getRangerAuthPolicy call time: average time taken per call within one minute  |
| cosRpc_getRangerAuthPolicy call time\_Cost_Avg_5m   | μs  | cosRpc_getRangerAuthPolicy call time: average time taken per call within five minutes  |
| cosRpc_getRangerAuthPolicy call time\_Cost_Max      | μs  | cosRpc_getRangerAuthPolicy call time: maximum time taken by a call within the current second   |
| cosRpc_getRangerAuthPolicy call time\_Cost_Max_1m   | μs  | cosRpc_getRangerAuthPolicy call time: maximum time taken by a call within one minute     |
| cosRpc_getRangerAuthPolicy call time\_Cost_Max_5m   | μs  | cosRpc_getRangerAuthPolicy call time: maximum time taken by a call within five minutes     |
| cosRpc_getRangerAuthPolicy call time\_Cost_Min    | μs  | cosRpc_getRangerAuthPolicy call time: minimum time taken by a call within the current second |
| cosRpc_getRangerAuthPolicy call time\_Cost_Min_1m | μs  | cosRpc_getRangerAuthPolicy call time: minimum time taken by a call within one minute |
| cosRpc_getRangerAuthPolicy call time\_Cost_Min_5m   | μs  | cosRpc_getRangerAuthPolicy call time: minimum time taken by a call within five minutes     |

 
