## Namespace

Namespace=QCE/CVM

## Monitoring Metrics

### Basic metrics

| Parameter | Metric Name | Calculation Method | Description | Unit | Dimension |
| ------------ | ------- | ---------------------------------------- | --------------------------- | ---- | ------------- |
| CPUUsage | CPU utilization | Percentage of the "user+nice+system+irq+softirq+idle+iowait" time of the CPU to the total time | Percentage of CPU utilization in real time when the CVM is running | % | InstanceId |
| CPULoadAvg | Average CPU load | Analyze data in `/proc/loadavg` and collect the average load of the system in the past one minute at 10 second intervals (this metric is not available for Windows CVMs) | Average number of tasks that are using and are about to use the CPU in a period of time | - | InstanceId |
| MemUsed | Memory usage | <li>On Windows, call GlobalMemoryStatusEx. <br><li>On Linux, call psutil.virtual_memory(). <br>Calculate the value of the memory usage (excluding buffers and caches) by subtracting the available memory (including buffers and caches) from the total memory | Actual memory used by users, excluding the memory capacity used by buffers and system caches | MB | InstanceId |
| MemUsage | Memory utilization | Ratio of the used memory (excluding caches, buffers, and the remaining available capacity) to the total memory | Amount of memory actually used, excluding the memory capacity used by buffers and system caches | % | InstanceId |
| TcpCurrEstab | Number of TCP connections | <li>On Windows, call "GetTcpTable" to obtain the number of TCP connections in the "MIB_TCP_STATE_ESTAB" state. <br><li>On Linux, obtain the value of "CurrEstab" from `/proc/net/snmp` | Number of TCP connections in the "ESTABLISHED" state | Count | InstanceId |
| Gputemp | GPU temperature | Returned by the nvmlDeviceGetTemperature API from the NVIDIA NVML library | Evaluate the heat dissipation condition of the GPU | Degrees Celsius | InstanceId |
| Gpuutil | GPU utilization | Returned by the nvmlDeviceGetUtilizationRates API from the NVIDIA NVML library | Evaluate the computing power consumed by the load during the non-idle period in percents | % | InstanceId |
| GpuMemUsed | Video RAM usage of GPU | This parameter is calculated by adding up the video RAM usage of all active channels | Evaluate the usage of video RAM by load | MB | InstanceId |
| Gpupowusage | Power consumption of GPU | Returned by the nvmlDeviceGetPowerUsage API from the NVIDIA NVML library | Evaluate the power consumption of GPU | W | InstanceId |

>
> 1. Basic metric data and alarm time (local time of the customer CVM) can be obtained only after the [CVM monitoring component Agent](https://intl.cloud.tencent.com/document/product/248/6211) is installed. If the local time of the customer CVM is not UTC/GMT+08:00, the time of the monitoring data of the CVM will not be the local time (UTC/GMT+08:00) of the CVM.
> 2. Ways of installing the monitoring component:
 > - Select Cloud Monitoring when purchasing a CVM to automatically install the monitoring component.
 > - Manually install the monitoring component by [installing the CVM monitoring component](https://intl.cloud.tencent.com/document/product/248/6211).


### Other metrics

| Parameter | Metric Name | Description | Unit | Dimension |
| ------------- | ------------------ | ------------------------------------------------------------ | ------------------------------------------------------ | ---- |
| LanOuttraffic | Private outbound bandwidth | Private outbound traffic of ENI per second | Mbps | InstanceId |
| LanIntraffic | Private inbound bandwidth | Private inbound traffic of ENI per second | Mbps | InstanceId |
| LanOutpkg | Private outbound packets | Number of outbound packets of the private ENI per second | Packets/sec | InstanceId |
| LanInpkg | Private inbound packets | Number of inbound packets of the private ENI per second | Packets/sec | InstanceId |
| WanOuttraffic | Public outbound bandwidth | Public outbound traffic of ENI per second | Mbps | InstanceId |
| WanIntraffic | Public inbound bandwidth | Public inbound traffic of ENI per second | Mbps | InstanceId |
| WanOutpkg | Public outbound packets | Number of outbound packets of the public ENI per second | Packets/sec | InstanceId |
| WanInpkg | Public inbound packets | Number of inbound packets of the public ENI per second | Packets/sec | InstanceId |
| DiskReadTraffic | Disk read traffic | Traffic of reading data from a disk to the memory per second. The value of this parameter takes the maximum read traffic for all partitions | KB/s | InstanceId |
| DiskWriteTraffic | Disk write traffic | Traffic of writing data from the memory to a disk per second. The value of this parameter takes the maximum write traffic for all partitions | KB/s | InstanceId |
| DiskUsage | Disk usage | Percentage of used disk space displayed by the partition | % | InstanceId |
| DiskIoAwait | Disk I/O waiting time | Average waiting time of each device I/O operation. The value of this parameter takes the maximum average waiting time for all partitions | ms | InstanceId |
| CpuLoadavg | Average CPU load per minute | Average CPU load per minute. The value of this parameter takes the data in the third column of `/proc/loadavg` depending on the installation and collection of the monitoring component. This metric is not available for Windows CVMs | - | InstanceId |
| CpuLoadavg5m | Average CPU load per five minutes | Average CPU load per five minutes. The value of this parameter takes the data in the first column of `/proc/loadavg` depending on the installation and collection of the monitoring component. This metric is not available for Windows CVMs | - | InstanceId |
| CpuLoadavg15m | Average CPU load per 15 minutes | Average CPU load per 15 minutes. The value of this parameter takes the data in the second column of `/proc/loadavg` depending on the installation and collection of the monitoring component. This metric is not available for Windows CVMs | - | InstanceId |
| BaseCpuUsage | Base CPU utilization | The base CPU utilization is collected and reported through the host, and the data can be viewed without the installation of the monitoring component. This data can still be continuously collected and reported even when the load of the CVM is high | % | InstanceId |

> The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to obtain the `period` supported by each metric.

## Overview of the Parameters in Each Dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
|---------|---------|---------|--------|
| Instances.N.Dimensions.0.Name | InstanceId | Dimension name of the CVM instance ID | Enter a string-type dimension name, such as InstanceId |
| Instances.N.Dimensions.0.Value | InstanceId | A specific CVM instance ID | Enter a specific instance ID, such as ins-mm8bs222 |

## Input Parameters

To query the monitoring data of CVM, use the following input parameters:
&Namespace=QCE/CVM
&Instances.N.Dimensions.0.Name=InstanceId
&Instances.N.Dimensions.0.Value=<CVM ID> 

