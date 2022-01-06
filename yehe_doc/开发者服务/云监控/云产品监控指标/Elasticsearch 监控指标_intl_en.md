## Namespace

Namespace=QCE/CES

## Monitoring Metrics

### Basic metrics

| Parameter | Metric | Unit | Dimension | Statistical Period |
| ------------------------------------- | ------------------------------------------------------ | ----- | ----------- | ------------------------ |
| CpuUsageAvg                           | Average cluster CPU utilization                          | %     | uInstanceId | 60s, 300s, 3600s, 86400s |
| CpuUsageMax                           | Maximum cluster CPU utilization                          | %     | uInstanceId | 60s, 300s, 3600s, 86400s |
| DiskUsageAvg                          | Average cluster disk utilization                         | %     | uInstanceId | 60s, 300s, 3600s, 86400s |
| DiskUsageMax                          | Maximum cluster disk utilization                         | %     | uInstanceId | 60s, 300s, 3600s, 86400s |
| IndexSpeed                            | Average number of cluster write requests per second                               | /s | uInstanceId | 60s, 300s, 3600s, 86400s |
| JvmMemUsageAvg                        | Average cluster JVM memory utilization                      | %     | uInstanceId | 60s, 300s, 3600s, 86400s |
| JvmMemUsageMax                        | Maximum cluster JVM memory utilization                      | %     | uInstanceId | 60s, 300s, 3600s, 86400s |
| SearchCompletedSpeed                  | Average cluster query requests per second                               | /s | uInstanceId | 60s, 300s, 3600s, 86400s |
| SearchRejectedCompletedPercent        | Query request rejection rate in case of high cluster load                           | %     | uInstanceId | 60s, 300s, 3600s, 86400s |
| Status                                | Cluster Health Status:<br>0: green<br>1: yellow<br>2: red                    | -     | uInstanceId | 60s, 300s, 3600s, 86400s |
| IndexLatencyAvg                       | Average write latency                                           | ms    | uInstanceId | 60s, 300s, 3600s, 86400s |
| IndexLatencyMax                       | Average write latency                                           | ms    | uInstanceId | 60s, 300s, 3600s, 86400s |
| SearchLatencyAvg                      | Average query latency                                           | ms    | uInstanceId | 60s, 300s, 3600s, 86400s |
| SearchLatencyMax                      | Maximum query latency                                           | ms    | uInstanceId | 60s, 300s, 3600s, 86400s |
| CpuLoad1minAvg                        | Average cluster load per minute                                      | 0     | uInstanceId | 60s, 300s, 3600s, 86400s |
| CpuLoad1minMax                        | Maximum cluster load per minute                                      | 0     | uInstanceId | 60s, 300s, 3600s, 86400s |
| IndexDocs                             | Total number of cluster documents                                           | -    | uInstanceId | 60s, 300s, 3600s, 86400s |
| BulkRejectedCompletedPercent          | Bulk request rejection rate                                             | %     | uInstanceId | 60s, 300s, 3600s, 86400s |
| AutoSnapshotStatus                    | Automatic snapshot backup status                                       | 0     | uInstanceId | 60s, 300s, 3600s, 86400s |
| MemUsageAvg                           | Average cluster physical memory utilization                       | %     | uInstanceId | 60s, 300s, 3600s, 86400s |
| MemUsageMax                           | Maximum cluster physical memory utilization                       | %     | uInstanceId | 60s, 300s, 3600s, 86400s |
| JvmOldMemUsageAvg                     | Average JVM Old memory utilization                                | %     | uInstanceId | 60s, 300s, 3600s, 86400s |
| JvmOldMemUsageMax                     | Maximum JVM Old memory utilization                                | %     | uInstanceId | 60s, 300s, 3600s, 86400s |
| NodeDiskReadIopsAvg                   | Average number of cluster disk reads per second                       | /s | uInstanceId | 60s, 300s, 3600s, 86400s |
| NodeDiskReadIopsMax                   | Maximum number of cluster disk reads per second                       | /s | uInstanceId | 60s, 300s, 3600s, 86400s |
| NodeDiskWriteIopsAvg                  | Average number of cluster disk writes per second                       | /s | uInstanceId | 60s, 300s, 3600s, 86400s |
| NodeDiskWriteIopsMax                  | Maximum number of cluster disk writes per second                       | /s | uInstanceId | 60s, 300s, 3600s, 86400s |
| NodeDiskUtilAvg                       | Average ratio of cluster disk IO operation time to total time | %     | uInstanceId | 60s, 300s, 3600s, 86400s |
| NodeDiskUtilMax                       | Maximum ratio of cluster disk IO operation time to total time | %     | uInstanceId | 60s, 300s, 3600s, 86400s |
| NodeParentBreakerDifMax               | Number of node circuit breaks per period_maximum                              | -    | uInstanceId | 60s, 300s, 3600s, 86400s |
| NodeParentBreakerDifAvg               | Number of node circuit breaks per period_average                              | -    | uInstanceId | 60s, 300s, 3600s, 86400s |
| NodeJvmMemUsageMax                    | Node JVM memory utilization_maximum                               | %     | uInstanceId | 60s, 300s, 3600s, 86400s |
| NodeJvmMemUsageAvg                    | Node JVM memory utilization_average                               | %     | uInstanceId | 60s, 300s, 3600s, 86400s |
| NodeJvmOldMemUsageMax                 | JVM_Old memory utilization_maximum                             | %     | uInstanceId | 60s, 300s, 3600s, 86400s |
| NodeJvmOldMemUsageAvg                 | JVM_Old memory utilization_average                             | %     | uInstanceId | 60s, 300s, 3600s, 86400s |
| NodeOldGcDifMax                       | Node Old GC count per period_maximum                             | Times    | uInstanceId | 60s, 300s, 3600s, 86400s |
| NodeFielddataMemoryInBytesAvg         | Node FieldData heap memory usage_average                   | B     | uInstanceId | 60s, 300s, 3600s, 86400s |
| NodeSearchSpeedMax                    | Node query speed_maximum                                    | /s | uInstanceId | 60s, 300s, 3600s, 86400s |
| NodeSearchSpeedAvg                    | Node query speed_average                                    | /s | uInstanceId | 60s, 300s, 3600s, 86400s |
| NodeIndexSpeedMax                     | Node write speed_maximum                                    | /s | uInstanceId | 60s, 300s, 3600s, 86400s |
| NodeIndexSpeedAvg                     | Node write speed_average                                    | /s | uInstanceId | 60s, 300s, 3600s, 86400s |
| NodeBulkSpeedMax                      | Node bulk request speed per period_maximum                              | /s | uInstanceId | 60s, 300s, 3600s, 86400s |
| NodeBulkSpeedAvg                      | Node bulk request speed per period_average                              | /s | uInstanceId | 60s, 300s, 3600s, 86400s |
| NodeSearchRejectedCompletedPercentMax | Node query rejection rate per period_maximum                            | %     | uInstanceId | 60s, 300s, 3600s, 86400s |
| NodeSearchRejectedCompletedPercentAvg | Node query rejection rate per period_average                            | %     | uInstanceId | 60s, 300s, 3600s, 86400s |
| NodeBulkRejectedCompletedPercentMax   | Node bulk request rejection rate per period_maximum                            | %     | uInstanceId | 60s, 300s, 3600s, 86400s |
| NodeBulkRejectedCompletedPercentAvg   | Node bulk request rejection rate per period_average                            | %     | uInstanceId | 60s, 300s, 3600s, 86400s |
| NodeSearchLatencyMax                  | Average node query latency per period_maximum                          | ms    | uInstanceId | 60s, 300s, 3600s, 86400s |
| NodeSearchLatencyAvg                  | Average node query latency per period_average                          | ms    | uInstanceId | 60s, 300s, 3600s, 86400s |
| NodeIndexLatencyMax                   | Average node write latency per period_maximum                          | ms    | uInstanceId | 60s, 300s, 3600s, 86400s |
| NodeIndexLatencyAvg                   | Average node write latency per period_average                          | ms    | uInstanceId | 60s, 300s, 3600s, 86400s |
| NodeCpuUsageMax                       | Node CPU utilization_maximum                                   | %     | uInstanceId | 60s, 300s, 3600s, 86400s |
| NodeCpuUsageAvg                       | Node CPU utilization_average                                   | %     | uInstanceId | 60s, 300s, 3600s, 86400s |
| NodeMemUsageMax                       | Node memory utilization_maximum                                  | %     | uInstanceId | 60s, 300s, 3600s, 86400s |
| NodeMemUsageAvg                       | Node memory utilization_average                                  | %     | uInstanceId | 60s, 300s, 3600s, 86400s |
| NodeCpuLoad1minMax                    | Node CPU load per minute_maximum                                | -     | uInstanceId | 60s, 300s, 3600s, 86400s |
| NodeCpuLoad1minAvg                    | Node CPU load per minute_average                                | -     | uInstanceId | 60s, 300s, 3600s, 86400s |
| NodeDiskUsageMax                      | Node disk utilization_maximum                                  | %     | uInstanceId | 60s, 300s, 3600s, 86400s |
| NodeDiskUsageAvg                      | Node disk utilization_average                                  | %     | uInstanceId | 60s, 300s, 3600s, 86400s |
| NodeDiskReadTrafficAvg                | Node disk read traffic_average                                  | KB/s  | uInstanceId | 60s, 300s, 3600s, 86400s |
| NodeDiskReadTrafficMax                | Node disk read traffic_maximum                                  | KB/s  | uInstanceId | 60s, 300s, 3600s, 86400s |
| NodeDiskWriteTrafficMax               | Node disk write traffic_maximum                                  | KB/s  | uInstanceId | 60s, 300s, 3600s, 86400s |
| NodeDiskWriteTrafficAvg               | Node disk write traffic_average                                  | KB/s  | uInstanceId | 60s, 300s, 3600s, 86400s |
| BulkCompletedDif                      | Number of bulk requests completed per period                                     | Times   | uInstanceId | 60s, 300s, 3600s, 86400s |
| IndexTotalDif                         | Number of writes per period                                         | Times    | uInstanceId | 60s, 300s, 3600s, 86400s |
| SearchCompletedDif                    | Number of queries completed per period                                     | Times    | uInstanceId | 60s, 300s, 3600s, 86400s |
| NodeBulkSpeedSum                      | Node bulk request speed_sum                                      | /s | uInstanceId | 60s, 300s, 3600s, 86400s |
| NodeIndexSpeedSum                     | Node write speed_sum                                      | /s | uInstanceId | 60s, 300s, 3600s, 86400s |
| NodeSearchSpeedSum                    | Node query speed_sum                                      | /s | uInstanceId | 60s, 300s, 3600s, 86400s |
| IsReadOnly                            | Whether the cluster is read-only                                           | -     | uInstanceId | 60s, 300s, 3600s, 86400s |
| IsIndexBlock                          | Whether there are read-only indexes                                         | -     | uInstanceId | 60s, 300s, 3600s, 86400s |
| IsVisible                             | Whether the cluster responds normally                                       | -     | uInstanceId | 60s, 300s, 3600s, 86400s |

### Disk metrics

| Parameter | Metric | Unit | Dimension | Statistical Period |
| ---------------- | ------------ | -------- | ---------------------------- | ------------------------ |
| DiskUsage        | Disk utilization   | %        | uInstanceId, device, env, ip | 60s, 300s, 3600s, 86400s |
| DiskAwait        | Operation wait time | ms       | uInstanceId, device, env, ip | 60s, 300s, 3600s, 86400s |
| DiskIoutil       | Disk IO utilization  | %        | uInstanceId, device, env, ip | 60s, 300s, 3600s, 86400s |
| DiskIps          | Number of writes per second | Times    | uInstanceId, device, env, ip | 60s, 300s, 3600s, 86400s |
| DiskOps          | Number of reads per second | Times  | uInstanceId, device, env, ip | 60s, 300s, 3600s, 86400s |
| DiskReadTraffic  | Disk read traffic   | KB/s | uInstanceId, device, env, ip | 60s, 300s, 3600s, 86400s |
| DiskSvctm        | Operation service time | ms       | uInstanceId, device, env, ip | 60s, 300s, 3600s, 86400s |
| DiskWriteTraffic | Disk write traffic   | KB/s | uInstanceId, device, env, ip | 60s, 300s, 3600s, 86400s |

### Node metrics

| Parameter | Metric | Unit | Dimension | Statistical Period |
| ---------------------------------- | ------------------------------- | ----- | ----------------------------------- | ------------------------ |
| NodeStatus                         | Node health status                    | -     | uInstanceId, hotwarm, nodeId, setid | 60s, 300s, 3600s, 86400s |
| NodeJvmMemUsage                    | Node JVM memory utilization             | %     | uInstanceId, hotwarm, nodeId, setid | 60s, 300s, 3600s, 86400s |
| NodeJvmOldMemUsage                 | JVM_Old memory utilization            | %     | uInstanceId, hotwarm, nodeId, setid | 60s, 300s, 3600s, 86400s |
| NodeOldGcDif                       | Node Old GC count per period           | Times    | uInstanceId, hotwarm, nodeId, setid | 60s, 300s, 3600s, 86400s |
| NodeOldGcTimeDif                   | Node Old GC time per period           | ms    | uInstanceId, hotwarm, nodeId, setid | 60s, 300s, 3600s, 86400s |
| NodeFielddataMemoryInBytes         | Node FieldData heap memory usage | B     | uInstanceId, hotwarm, nodeId, setid | 60s, 300s, 3600s, 86400s |
| NodeSegmentCount                   | Number of node segments               | -     | uInstanceId, hotwarm, nodeId, setid | 60s, 300s, 3600s, 86400s |
| NodeSearchSpeed                    | Node query speed                    | Times/s | uInstanceId, hotwarm, nodeId, setid | 60s, 300s, 3600s, 86400s |
| NodeIndexSpeed                     | Node write speed                    | Times/s | uInstanceId, hotwarm, nodeId, setid | 60s, 300s, 3600s, 86400s |
| NodeBulkSpeed                      | Node bulk request speed per period            | Times/s | uInstanceId, hotwarm, nodeId, setid | 60s, 300s, 3600s, 86400s |
| NodeSearchRejectedCompletedPercent | Node query rejection rate per period            | %     | uInstanceId, hotwarm, nodeId, setid | 60s, 300s, 3600s, 86400s |
| NodeBulkRejectedCompletedPercent   | Node bulk request rejection rate per period          | %     | uInstanceId, hotwarm, nodeId, setid | 60s, 300s, 3600s, 86400s |
| NodeSearchLatency                  | Average node query latency per period          | ms    | uInstanceId, hotwarm, nodeId, setid | 60s, 300s, 3600s, 86400s |
| NodeIndexLatency                   | Average node write latency per period          | ms    | uInstanceId, hotwarm, nodeId, setid | 60s, 300s, 3600s, 86400s |
| NodeCpuUsage                       | Node CPU utilization                 | %     | uInstanceId, hotwarm, nodeId, setid | 60s, 300s, 3600s, 86400s |
| NodeMemUsage                       | Node memory utilization                  | %     | uInstanceId, hotwarm, nodeId, setid | 60s, 300s, 3600s, 86400s |
| NodeCpuLoad1min                    | Node CPU load per minute              | -     | uInstanceId, hotwarm, nodeId, setid | 60s, 300s, 3600s, 86400s |
| NodeDiskPathMaxUsage               | Maximum node disk utilization              | %     | uInstanceId, hotwarm, nodeId, setid | 60s, 300s, 3600s, 86400s |

### Hot/Warm cluster

| Parameter | Metric | Unit | Dimension | Statistical Period |
| ------------------------------------------------ | ------------------------------------------------------------ | ----- | -------------------- | ------------------------ |
| NodeParentBreaker<br/>DifHotwarmMax              | Number of node circuit breaks_hot/warm_maximum                                     | Times    | uInstanceId, hotwarm | 60s, 300s, 3600s, 86400s |
| NodeParentBreaker<br/>DifHotwarmAvg              | Number of node circuit breaks_hot/warm_average                                     | Times    | uInstanceId, hotwarm | 60s, 300s, 3600s, 86400s |
| NodeJvmMemUsageHotwarmAvg                        | Node JVM memory utilization_average_hot/warm                               | %     | uInstanceId, hotwarm | 60s, 300s, 3600s, 86400s |
| NodeJvmMemUsageHotwarmMax                        | Node JVM memory utilization_maximum_hot/warm                               | %     | uInstanceId, hotwarm | 60s, 300s, 3600s, 86400s |
| NodeJvmOldMem<br/>UsageHotwarmMax                | JVM_Old memory utilization_maximum_hot/warm                             | %     | uInstanceId, hotwarm | 60s, 300s, 3600s, 86400s |
| NodeJvmOldMemUsage<br/>HotwarmAvg                | JVM_Old memory utilization_average_hot/warm                             | %     | uInstanceId, hotwarm | 60s, 300s, 3600s, 86400s |
| NodeOldGcDifHotwarmMax                           | Node Old GC count per period_maximum_hot/warm                            | Times    | uInstanceId, hotwarm | 60s, 300s, 3600s, 86400s |
| NodeOldGcDifHotwarmAvg                           | Node Old GC count per period_average_hot/warm                            | Times    | uInstanceId, hotwarm | 60s, 300s, 3600s, 86400s |
| NodeOldGcTimeDifHotwarmMax                       | Node Old GC time per period_maximum_hot/warm                            | ms    | uInstanceId, hotwarm | 60s, 300s, 3600s, 86400s |
| NodeOldGcTimeDifHotwarmAvg                       | Node Old GC time per period_average_hot/warm                            | ms    | uInstanceId, hotwarm | 60s, 300s, 3600s, 86400s |
| NodeFielddataMemoryIn<br>BytesHotwarmMax         | Node FieldData heap memory usage_maximum_hot/warm                  | B     | uInstanceId, hotwarm | 60s, 300s, 3600s, 86400s |
| NodeFielddataMemoryIn<br/>BytesHotwarmAvg        | Node FieldData heap memory usage_average_hot/warm                  | B     | uInstanceId, hotwarm | 60s, 300s, 3600s, 86400s |
| NodeSearchSpeedHotwarmMax                        | Node query speed_maximum_hot/warm                                     | Times/s | uInstanceId, hotwarm | 60s, 300s, 3600s, 86400s |
| NodeSearchSpeedHotwarmAvg                        | Node query speed_average_hot/warm                                     | Times/s | uInstanceId, hotwarm | 60s, 300s, 3600s, 86400s |
| NodeSearchSpeedHotwarmSum                        | Node query speed_sum_hot/warm                                     | Times/s | uInstanceId, hotwarm | 60s, 300s, 3600s, 86400s |
| NodeIndexSpeedHotwarmMax                         | Node write speed_maximum_hot/warm                                     | Times/s | uInstanceId, hotwarm | 60s, 300s, 3600s, 86400s |
| NodeIndexSpeedHotwarmAvg                         | Node write speed_average_hot/warm                                     | Times/s | uInstanceId, hotwarm | 60s, 300s, 3600s, 86400s |
| NodeIndexSpeedHotwarmSum                         | Node write speed_sum_hot/warm                                     | Times/s | uInstanceId, hotwarm | 60s, 300s, 3600s, 86400s |
| NodeBulkSpeedHotwarmMax                          | Node bulk request speed per period_maximum_hot/warm                             | Times/s | uInstanceId, hotwarm | 60s, 300s, 3600s, 86400s |
| NodeBulkSpeedHotwarmAvg                          | Node bulk request speed per period_average_hot/warm                             | Times/s | uInstanceId, hotwarm | 60s, 300s, 3600s, 86400s |
| NodeBulkSpeedHotwarmSum                          | Node bulk request speed per period_sum_hot/warm                             | Times/s | uInstanceId, hotwarm | 60s, 300s, 3600s, 86400s |
| NodeBulkRejectedCompleted<br>PercentHotwarmMax   | Node bulk request rejection rate per period_maximum_hot/warm                           | %     | uInstanceId, hotwarm | 60s, 300s, 3600s, 86400s |
| NodeBulkRejectedCompleted<br>PercentHotwarmAvg   | Node bulk request rejection rate per period_average_hot/warm                           | %     | uInstanceId, hotwarm | 60s, 300s, 3600s, 86400s |
| NodeSearchRejectedCompleted<br>PercentHotwarmMax | Node query rejection rate per period_maximum_hot/warm                             | %     | uInstanceId, hotwarm | 60s, 300s, 3600s, 86400s |
| NodeSearchRejectedCompleted<br>PercentHotwarmAvg | Node query rejection rate per period_average_hot/warm                             | %     | uInstanceId, hotwarm | 60s, 300s, 3600s, 86400s |
| NodeSearchLatencyHotwarmMax                      | Average node query latency per period_maximum_hot/warm                           | ms    | uInstanceId, hotwarm | 60s, 300s, 3600s, 86400s |
| NodeSearchLatencyHotwarmAvg                      | Average node query latency per period_average_hot/warm                           | ms    | uInstanceId, hotwarm | 60s, 300s, 3600s, 86400s |
| NodeIndexLatencyHotwarmMax                       | Average node write latency per period_maximum_hot/warm                           | ms    | uInstanceId, hotwarm | 60s, 300s, 3600s, 86400s |
| NodeIndexLatencyHotwarmAvg                       | Average node write latency per period_average_hot/warm                           | ms    | uInstanceId, hotwarm | 60s, 300s, 3600s, 86400s |
| NodeCpuUsageHotwarmMax                           | Node CPU utilization_maximum_hot/warm                                  | %     | uInstanceId, hotwarm | 60s, 300s, 3600s, 86400s |
| NodeCpuUsageHotwarmAvg                           | Node CPU utilization_average_hot/warm                                  | %     | uInstanceId, hotwarm | 60s, 300s, 3600s, 86400s |
| NodeMemUsageHotwarmMax                           | Node memory utilization_maximum_hot/warm                                   | %     | uInstanceId, hotwarm | 60s, 300s, 3600s, 86400s |
| NodeMemUsageHotwarmAvg                           | Node memory utilization_average_hot/warm                                   | %     | uInstanceId, hotwarm | 60s, 300s, 3600s, 86400s |
| NodeCpuLoad1minHotwarmMax                        | Node CPU load per minute_maximum_hot/warm                               | -     | uInstanceId, hotwarm | 60s, 300s, 3600s, 86400s |
| NodeCpuLoad1minHotwarmAvg                        | Node CPU load per minute_average_hot/warm                               | -     | uInstanceId, hotwarm | 60s, 300s, 3600s, 86400s |
| NodeDiskUsageHotwarmMax                          | Node disk utilization_maximum_hot/warm                                   | %     | uInstanceId, hotwarm | 60s, 300s, 3600s, 86400s |
| NodeDiskUsageHotwarmAvg                          | Node disk utilization_average_hot/warm                                   | %     | uInstanceId, hotwarm | 60s, 300s, 3600s, 86400s |
| NodeDiskReadIopsHotwarmAvg                       | Average number of cluster disk reads per second_hot/warm                        | Times/s | uInstanceId, hotwarm | 60s, 300s, 3600s, 86400s |
| NodeDiskReadIopsHotwarmMax                       | Maximum number of cluster disk reads per second_hot/warm                        | Times/s | uInstanceId, hotwarm | 60s, 300s, 3600s, 86400s |
| NodeDiskWriteIopsHotwarmMax                      | Maximum number of cluster disk writes per second_hot/warm                        | Times/s | uInstanceId, hotwarm | 60s, 300s, 3600s, 86400s |
| NodeDiskWriteIopsHotwarmAvg                      | Average number of cluster disk writes per second_hot/warm                        | Times/s | uInstanceId, hotwarm | 60s, 300s, 3600s, 86400s |
| NodeDiskUtilHotwarmAvg                           | Average ratio of cluster disk IO operation time to total time_hot/warm | %     | uInstanceId, hotwarm | 60s, 300s, 3600s, 86400s |
| NodeDiskUtilHotwarmMax                           | Maximum ratio of cluster disk IO operation time to total time_hot/warm | %     | uInstanceId, hotwarm | 60s, 300s, 3600s, 86400s |
| NodeDiskReadTrafficHotwarmAvg                    | Node disk read traffic_average_hot/warm                                   | KB/s  | uInstanceId, hotwarm | 60s, 300s, 3600s, 86400s |
| NodeDiskReadTrafficHotwarmMax                    | Node disk read traffic_maximum_hot/warm                                   | KB/s  | uInstanceId, hotwarm | 60s, 300s, 3600s, 86400s |
| NodeDiskWriteTrafficHotwarmMax                   | Node disk write traffic_maximum_hot/warm                                   | KB/s  | uInstanceId, hotwarm | 60s, 300s, 3600s, 86400s |
| NodeDiskWriteTrafficHotwarmAvg                   | Node disk write traffic_average_hot/warm                                   | KB/s  | uInstanceId, hotwarm | 60s, 300s, 3600s, 86400s |

### Kibana node

| Parameter | Metric | Unit | Dimension | Statistical Period |
| --------------- | ---------------- | ---- | --------------- | ------------------------ |
| KibanaDiskUsage | Disk utilization       | %    | uInstanceId, ip | 60s, 300s, 3600s, 86400s |
| KibanaCpuLoad1  | Average CPU load per minute | -    | uInstanceId, ip | 60s, 300s, 3600s, 86400s |
| KibanaCpuUsage  | CPU utilization        | %    | uInstanceId, ip | 60s, 300s, 3600s, 86400s |
| KibanaMemUsage  | Memory utilization       | %    | uInstanceId, ip | 60s, 300s, 3600s, 86400s |
| KibanaStatus    | Kibana process status   | -    | uInstanceId, ip | 60s, 300s, 3600s, 86400s |

## Overview of Parameters in Each Dimension

| Parameter | Dimension | Dimension Description | Format |
| ------------------------------ | ----------- | -------------------------------- | ------------------------------------------------------------ |
| Instances.N.Dimensions.0.Name  | uInstanceId | Dimension name of ES instance ID            | String-type dimension name, such as `uInstanceId`                        |
| Instances.N.Dimensions.0.Value | uInstanceId | Specific ES instance ID                   | Specific instance ID, such as `es-example`                            |
| Instances.N.Dimensions.0.Name  | hotwarm     | Dimension name of the ES node hot/warm attribute        | Enter a string-type dimension name: hotwarm                            |
| Instances.N.Dimensions.0.Value | hotwarm     | ES node hot/warm attribute              | Specific instance node hot/warm attribute, which is determined by the node data disk (warm for premium cloud disk and hot for SSD cloud disk) |
| Instances.N.Dimensions.0.Name  | nodeId      | Dimension name of ES node ID            | String-type dimension name, such as `nodeId`                             |
| Instances.N.Dimensions.0.Value | nodeId      | Specific ES node ID                   | Specific instance ID, such as `1111111111111111111`                   |
| Instances.N.Dimensions.0.Name  | setid       | Dimension name of ES node AZ ID | String-type dimension name, such as `setid`                              |
| Instances.N.Dimensions.0.Value | setid       | ES node AZ ID        | Specific instance ID, such as `100006` for Guangzhou Zone 6                      |
| Instances.N.Dimensions.0.Name  |device      | Dimension name of disk ID| String-type dimension name, such as `device`                        |
| Instances.N.Dimensions.0.Value | device    | Specific disk ID      | Specific instance ID, such as `disk-123456` |
| Instances.N.Dimensions.0.Name  |env    | Dimension name of disk environment  | String-type dimension name, such as `env`                          |
| Instances.N.Dimensions.0.Value |env     | Specific environment name      | Specific instance ID, such as `cvm`            |
| Instances.N.Dimensions.0.Name  | ip      | Dimension name of IP  | String-type dimension name, such as `ip`                            |
| Instances.N.Dimensions.0.Value | ip      | Specific IP       | Specific instance ID, such as `111.111.111.111`                  |

## Input Parameter Description

1. To query the monitoring data of Elasticsearch Service - basic metrics, use the following input parameters:
&Namespace=QCE/CES
&Instances.N.Dimensions.0.Name=uInstanceId
&Instances.N.Dimensions.0.Value=ES instance ID

2. To query the monitoring data of Elasticsearch Service - disk metrics, use the following input parameters:
&Namespace=QCE/CES
&Instances.N.Dimensions.0.Name=uInstanceId
&Instances.N.Dimensions.0.Value=ES instance ID
&Instances.N.Dimensions.1.Name=device
&Instances.N.Dimensions.1.Value=Disk ID
&Instances.N.Dimensions.2.Name=env
&Instances.N.Dimensions.2.Value=Disk environment
&Instances.N.Dimensions.2.Name=ip
&Instances.N.Dimensions.2.Value=Disk IP

3. To query the monitoring data of Elasticsearch Service - node metrics, use the following input parameters:
&Namespace=QCE/CES
&Instances.N.Dimensions.0.Name=uInstanceId
&Instances.N.Dimensions.0.Value=ES instance ID
&Instances.N.Dimensions.1.Name=hotwarm
&Instances.N.Dimensions.1.Value=Hot/Warm attribute of ES node 
&Instances.N.Dimensions.2.Name=nodeId
&Instances.N.Dimensions.2.Value=ES node ID
&Instances.N.Dimensions.3.Name=setid
&Instances.N.Dimensions.3.Value=ES node AZ ID

4. To query the monitoring data of Elasticsearch Service - node hot/warm attribute metrics, use the following input parameters:
&Namespace=QCE/CES
&Instances.N.Dimensions.0.Name=uInstanceId
&Instances.N.Dimensions.0.Value=ES instance ID
&Instances.N.Dimensions.1.Name=hotwarm
&Instances.N.Dimensions.1.Value=Hot/Warm attribute of ES node 

5. To query the monitoring data of Elasticsearch Service - Kibana node metrics, use the following input parameters:
&Namespace=QCE/CES
&Instances.N.Dimensions.0.Name=uInstanceId
&Instances.N.Dimensions.0.Value=ES instance ID
&Instances.N.Dimensions.1.Name=ip
&Instances.N.Dimensions.1.Value=Node IP
