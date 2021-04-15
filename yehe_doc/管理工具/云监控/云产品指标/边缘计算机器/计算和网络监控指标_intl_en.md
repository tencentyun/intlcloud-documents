
## Namespace


Namespace=QCE/ECM

## Monitored Metrics
>?When pulling data for the computation and networking metrics, please select Guangzhou as the region.

| Metric | Meaning | Description | Unit | Dimension |
| ------------- | ------------------ | ------------------------------------------------------------ | ---- | ---- |
| CpuUsage | CPU utilization | To ensure data precision, internal components of the CVM instance are used to collect and report the data. | % | UUID |
| CpuLoadavg | CPU load average | One-minute CPU load average, taken from the first column of `/proc/loadavg` (not available for Windows CVMs). The data is collected using [CVM Agents](https://intl.cloud.tencent.com/document/product/248/6211). | - | UUID |
| MemUsed | Memory usage | Memory used, excluding the buffer and system cache. The value is collected with the [CVM Agents](https://intl.cloud.tencent.com/document/product/248/6211). | MB | UUID |
| BaseCpuUsage | Base CPU utilization | The base CPU utilization is collected and reported through the host. The data can be viewed without installing the CVM Agents, and can still be continuously collected and reported under high CVM load. | % | UUID |
| MemUsage | Usage utilization | The ratio of memory used to total memory capacity, excluding the buffer and system cache. | % | UUID |
| LanOuttraffic | Private outbound bandwidth | Average outbound traffic per second of the private ENI | Mbps | UUID |
| LanIntraffic | Private inbound bandwidth | Average inbound traffic per second of the private ENI | Mbps | UUID |
| LanOutpkg | Private outbound packets | Number of outbound packets per second of the private ENI | Packets/sec | UUID |
| LanInpkg | Private inbound packets | Number of inbound packets per second of the private ENI | Packets/sec | UUID |
| TcpCurrEstab  | Number of TCP links | Number of TCP links in `ESTABLISHED` status. The value is collected with the CVM Agents.  | - | UUID |
| WanOuttraffic | Public outbound bandwidth | Average outbound traffic per second over the public network. The minimum granularity is calculated by 10-second total traffic/10 seconds  | Mbps | UUID |
| WanIntraffic | Public inbound bandwidth | Public inbound traffic per second | Mbps | UUID |
| WanOutpkg     | Public outbound packets | Average number of outbound packets per second over the public network | packets/s | UUID |
| WanInpkg      | Public inbound packets | Average number of inbound packets per second over the public network  | packets/s | UUID |
| AccOuttraffic | Public outbound traffic per second | Average outbound traffic per second of the public ENI | Mbps | UUID |
| RegionIspIntraffic | Region ISP public inbound bandwidth | Public inbound bandwidth of each ISP in each region | Mbps | Region, ISP |
| RegionIspOuttraffic | Region ISP public outbound bandwidth | Public outbound bandwidth of each ISP in each region | Mbps | Region, ISP |


> ?The statistic period used for each metric may differ. You can call the `DescribeBaseMetrics` API to obtain the period of each metric.

## Dimension Parameters

| Parameter | Dimension | Description | Format |
| ------------------------------ | -------- | -------- | --------------------------------------------------------- |
| Instances.N.Dimensions.0.Name  | UUID | Name of the instance UUID | Dimension name (string): uuid |
| Instances.N.Dimensions.0.Value | UUID  | UUID of the instance | Specific UUID, for example, `4ef19d31-3117-455c-ae8e-2029a07d8999` |
| Instances.N.Dimensions.0.Name | Region | ECM region | Dimension name (string): Region |
| Instances.N.Dimensions.0.Value | Region | ECM region. You can query the region list by calling the `DescribeNode` API in the ECM service. | Specific ECM region, for example, `ap-zhengzhou-ecm` |
| Instances.N.Dimensions.1.Name | ISP | Name of the ISP node | Dimension name (string): ISP |
| Instances.N.Dimensions.1.Value | ISP | Specific ISP of the node. You can query the ISP list by calling the `DescribeNode` API in the ECM service. | Specific ISP of the node, for example, "CTCC" (China Telecom), "CUCC" (China Unicom), and "CMCC" (China Mobile) |



## Input Parameters

#### 1. To query the monitoring data of computation and networking, see the following input parameters:
&Namespace=QCE/ECM
&Instances.N.Dimensions.0.Name=UUID
&Instances.N.Dimensions.0.Value=UUID of the instance

#### 2. To query the monitoring data of the public outbound/inbound bandwidth of each ISP in each region, see the following input parameters:
&Namespace=QCE/ECM
&Instances.N.Dimensions.0.Name=Region
&Instances.N.Dimensions.0.Value=ECM region
&Instances.N.Dimensions.1.Name=ISP
&Instances.N.Dimensions.1.Value=ISP of the node
