When you create a Lighthouse instance, the instance package you specify determines its server hardware configuration. The computing, memory, and storage features vary by instance package. You can select an appropriate instance package based on the scale of your application to be deployed. These instance packages consist of different combinations of CPU, memory, SSD cloud disk, and network traffic package, so you can flexibly select appropriate resources for your applications.


## Instance Limits

- The total number of instances that can be started in a region is limited. For more information, please see [Use Limits](https://intl.cloud.tencent.com/document/product/1103/41265).
- The purchasable instance packages may vary by region, and some packages may be sold out. The information displayed on the actual purchase page shall prevail.
- Please pay attention to the corresponding network traffic package capacity (i.e., upper limit) of each instance package. After the network traffic of a Lighthouse instance exceeds the limit, it will be billed by the general network bandwidth traffic. For more information, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/1103/41403).

>?
> - When creating a Lighthouse instance, you cannot specify the CPU model of the underlying physical server; instead, Tencent Cloud will randomly assign a physical CPU model that meets the selected package specification.
> - At the same specification level, Lighthouse has a CPU and memory performance comparable with that of [CVM](https://intl.cloud.tencent.com/document/product/213/11518).
>


## Instance Package
For more information on the supported Lighthouse instance packages and their pricing, please see [Basic Package Pricing](https://intl.cloud.tencent.com/document/product/1103/41403).


## Storage Performance Description<span id="PerformanceIndex"></span>
The instance system disks of all Lighthouse packages are [Tencent Cloud SSD cloud disks](https://intl.cloud.tencent.com/document/product/362/31636), which are based on full NVMe SSD storage media and use a three-copy distributed storage mechanism to provide low-latency and high-throughput I/O capabilities with a high random IOPS and 99.9999999% data security. Their performance metrics are as follows:
<table>
<tr>
<th>IOPS per Disk</th><th>Random IOPS Calculation Formula</th><th>Maximum Throughput per Disk (MB/s)</th><th>Throughput Calculation Formula</th>
<th>One-Way Random Read/Write Latency</th>
</tr>
<tr>
<td>26,000</td>
<td>Random IOPS = min{1800 + storage capacity (GB) * 30,26000}</td>
<td>260 MB/s</td>
<td>Throughput = min{120 + storage capacity (GB) * 0.2,260}</td>
<td>0.5–3 ms</td>
</tr>
</table>


## Bandwidth Cap Description[](id:BandwidthUpperLimit)
<dx-tabs>
::: Outbound bandwidth cap description (downstream bandwidth)[](id:DownstreamBandwidth)
The cap of the package bandwidth used by a Lighthouse instance is the outbound bandwidth cap by default, i.e., the bandwidth that comes out of the Lighthouse instance.
:::
::: Inbound bandwidth cap description (upstream bandwidth)[](id:UpstreamBandwidth)
Inbound public network bandwidth is the bandwidth that comes into a Lighthouse instance.
- If the bandwidth of the purchased package is greater than 10 Mbps, Tencent Cloud will assign the instance an public network inbound bandwidth that is equal to the purchased bandwidth.
- If the bandwidth of the purchased package is smaller than 10 Mbps, Tencent Cloud will assign the instance a public network inbound bandwidth of 10 Mbps.
:::
</dx-tabs>
