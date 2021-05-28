## Namespace

Namespace=QCE/CVM

## Monitoring Metrics

### CPU monitoring

| Parameter | Metric | Description | Unit | Dimension | Statistical Period |
| ------------- | --------------------- | ------------------------------------------------------------ | ---- | ---------- | ---------------------------------- |
| CPUUsage      | CPU utilization           | Percentage of CPU used in real time during machine operation | %    | InstanceId | 10s, 60s, 300s, <br>3600s, 86400s  |
| CpuLoadavg    | 1-minute CPU load   | Average number of tasks that are using and waiting to use the CPU in one minute (this metric is unavailable on Windows) | -    | InstanceId | 10s, 60s, 300s, <br/>3600s, 86400s |
| Cpuloadavg5m    | 5-minute CPU load   | Average number of tasks that are using and waiting to use the CPU in five minutes (this metric is unavailable on Windows) | -    | InstanceId | 60s, 300s, <br/>3600s              |
| Cpuloadavg15m    | 15-minute CPU load   | Average number of tasks that are using and waiting to use the CPU in 15 minutes (this metric is unavailable on Windows) | -    | InstanceId | 60s, 300s, <br/>3600s              |
| BaseCpuUsage  | Basic CPU utilization | The basic CPU utilization is collected and reported through the host, and the data can be viewed without the installation of the monitoring component. The data can still be continuously collected and reported even when the load of the CVM is high | %    | InstanceId | 10s, 60s, 300s, <br/>3600s, 86400s |

### GPU monitoring
| Parameter | Metric | Description | Unit | Dimension | Statistical Period |
| ----------- | -------------- | ------------------------------------------ | ---- | ---------- | ---------------------------------- |
| GpuMemTotal | Total GPU memory | Total GPU memory | MB | InstanceId | 10s, 60s, 300s, <br/>3600s, 86400s |
| GpuMemUsage | GPU memory utilization | GPU memory utilization |% | InstanceId | 10s, 60s, 300s, <br/>3600s, 86400s |
| GpuMemUsed | GPU memory usage | Evaluates the GPU memory used by the load | MB | InstanceId | 10s, 60s, 300s, <br/>3600s, 86400s |
| GpuPowDraw | GPU power usage | GPU power usage | W | InstanceId | 10s, 60s, 300s, <br/>3600s, 86400s |
| GpuPowLimit | Total GPU power consumption | Total GPU power consumption | W | InstanceId | 10s, 60s, 300s, <br/>3600s, 86400s |
| GpuPowUsage | GPU power utilization | GPU power utilization | % | InstanceId | 10s, 60s, 300s, <br/>3600s, 86400s |
| GpuTemp | GPU temperature | Evaluates the GPU heat dissipation status | °C | InstanceId | 10s, 60s, 300s, <br/>3600s, 86400s |
| GpuUtil | GPU utilization | Evaluates the computing power consumed by the load, which is the percentage of non-idle state | % | InstanceId | 10s, 60s, 300s, <br/>3600s, 86400s |

### Network monitoring
| Parameter | Metric | Description | Unit | Dimension | Statistical Period |
| ------------- | ---------------------------- | ------------------------------------------------------------ | ----- | ---------- | ---------------------------------- |
| LanOuttraffic | Private outbound bandwidth | Average outbound traffic of the private ENI per second | Mbps | InstanceId | 10s, 60s, 300s, <br/>3600s, 86400s |
| LanIntraffic | Private inbound bandwidth | Average inbound traffic of the private ENI per second | Mbps | InstanceId | 10s, 60s, 300s, <br/>3600s, 86400s |
| LanOutpkg | Private outbound packets | Average number of outbound packets of the private ENI per second | Packets/sec | InstanceId | 10s, 60s, 300s, <br/>3600s, 86400s |
| LanInpkg | Private inbound packets | Average number of inbound packets of the private ENI per second | Packets/sec | InstanceId | 10s, 60s, 300s, <br/>3600s, 86400s |
| WanOuttraffic | Public outbound bandwidth | Average outbound traffic rate over the public network per second. The value at the minimum granularity is calculated by 10-second total traffic/10 seconds | Mbps | InstanceId | 10s, 60s, 300s, <br/>3600s, 86400s |
| WanIntraffic | Public inbound bandwidth | Average inbound traffic rate over the public network per second. The value at the minimum granularity is 10-second total traffic divided by 10 seconds | Mbps | InstanceId | 10s, 60s, 300s, <br/>3600s, 86400s |
| WanOutpkg | Public outbound packets | Average number of outbound packets of the public ENI per second | Packets/sec | InstanceId | 10s, 60s, 300s, <br/>3600s, 86400s |
| WanInpkg | Public inbound packets | Average number of inbound packets of the public ENI per second | Packets/sec | InstanceId | 10s, 60s, 300s, <br/>3600s, 86400s |
| AccOuttraffic | Public outbound traffic | Average outbound traffic of the public ENI per second | MB | InstanceId | 10s, 60s, 300s, <br/>3600s, 86400s |
| TcpCurrEstab | TCP connections | Number of TCP connections in `ESTABLISHED` status | - | InstanceId | 10s, 60s, 300s, <br/>3600s, 86400s |
| TimeOffset | Difference between server UTC time and NTP time | Difference between server UTC time and NTP time | s | InstanceId | 60s, 300s, <br/>3600s |

### Memory monitoring
| Parameter | Metric | Description | Unit | Dimension | Statistical Period |
| ---------- | ---------- | ------------------------------------------------------------ | ---- | ---------- | ---------------------------------- |
| MemUsed | Memory usage | The amount of memory used by the user, excluding caches and buffers, which is total memory minus available memory (including buffers and caches) | MB | InstanceId | 10s, 60s, 300s, <br/>3600s, 86400s |
| MemUsage   | Memory utilization | Ratio of the used memory (excluding caches, buffers, and the remaining memory) to the total memory | %    | InstanceId | 10s, 60s, 300s, <br/>3600s, 86400s |

### Disk monitoring
| Parameter | Metric | Description | Unit | Dimension | Statistical Period |
| ---------- | ---------- | ------------------------------------------------------------ | ---- | ---------- | ---------------------------------- |
|CvmDiskUsage    | Disk utilization | Disk utilization  |% |InstanceId|   60s, 300s|

> ?
> 1. Basic metric data (such as CPU and memory) and alarm time (local time of your CVM instance) can be obtained only after the [CVM monitoring component Agent](https://intl.cloud.tencent.com/document/product/248/6211) is installed. If the local time of you CVM instance is not UTC/GMT+08:00, the time of the monitoring data of the instance will not be the local time (UTC/GMT+08:00) of the instance.
> 2. Ways of installing Agent:
>  - Select Cloud Monitor when purchasing a CVM instance to automatically install Agent.
>  - Manually [install Agent](https://intl.cloud.tencent.com/document/product/248/6211).
>3. The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the `period` values supported by each metric.


## Overview of Parameters in Each Dimension

| Parameter | Dimension | Dimension Description | Format |
| ------------------------------ | ---------- | -------------------------- | ------------------------------------ |
| Instances.N.Dimensions.0.Name | InstanceId | CVM instance ID dimension name | Enter a String-type dimension name, such as InstanceId |
| Instances.N.Dimensions.0.Value | InstanceId | Specific CVM instance ID      | Enter a specific instance ID, such as ins-mm8bs222  |

## Input Parameter Description

**To query the monitoring data of a CVM instance, use the following input parameters:**
&Namespace=QCE/CVM
&Instances.N.Dimensions.0.Name=InstanceId
&Instances.N.Dimensions.0.Value=Specific CVM instance ID 
