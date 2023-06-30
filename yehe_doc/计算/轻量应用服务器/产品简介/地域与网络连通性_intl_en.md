## Regions
- **Overview**
Tencent Cloud IDCs are distributed across different regions worldwide. To minimize access delay and improve download speed, we recommend you select the region closest to your end users.
- **Considerations**
 - Each region includes multiple availability zones.
 - By default, Lighthouse instances in different regions are not interconnected over the private network.


<dx-alert infotype="explain" title="<b>How to Select a Region</b>">
When creating a Lighthouse instance, you can select a region based on the following considerations. **Note that the region cannot be changed after the instance is created successfully.**
 - **Business requirements**: To guarantee the quality of public network access and reduce the packet loss and delay, we recommend you select the region closest to your end users.
 - **Instance package**: Available instance packages vary by region. You can select one based on the CPU, memory, system disk, public network bandwidth, and monthly traffic usage of the instance as required by your application. For more information, see [Price Overview](https://intl.cloud.tencent.com/document/product/1103/47794).
 - **Cost budget**:
  - Instance packages in and outside the Chinese mainland differ in configuration and price.
  - Instance packages for Linux and Windows outside the Chinese mainland differ in price.
    You can select a package based on your budget and requirements. For billing details, see [Price Overview](https://intl.cloud.tencent.com/document/product/1103/47794).
 - **Cross-border network quality**: For Lighthouse instances outside the Chinese mainland, as access from the Chinese mainland may experience a significant delay and packet loss due to the ISP network lines (non-cross-border access typically suffers no impact), Tencent Cloud only guarantees that the public network bandwidth provided in instance packages is the "peak bandwidth".
</dx-alert>


## AZs
- **Overview**
An Availability Zone (AZ) refers to a physical location with independent power supply and network resources within a region.
AZs in the same region are interconnected through low-latency private network linkages, which allows Lighthouse instances in different AZs in the same region to communicate with each other through private networks. For applications with high disaster recovery requirements, deploy Lighthouse instances to different availability zones within the same region to ensure fault isolation. Note that it may cause a longer communication latency.
- **Considerations**
 Lighthouse instances in different AZs in the same region under the same account are interconnected over the private network by default.

<dx-alert infotype="explain" title="<b>How to Select an AZ</b>">
We recommend you select an AZ that is "randomly assigned". You can also specify an AZ as needed. **Note that the AZ cannot be changed after the instance is created successfully.**
</dx-alert>





## Supported Regions and Availability Zones
<dx-alert infotype="explain" title="">
Lighthouse instances are available in the following availability zones.
</dx-alert>

####  Hong Kong/Macao/Taiwan (China)
Hong Kong (China): Hong Kong Zone 1, Hong Kong Zone 2, Hong Kong Zone 3.

####  Other countries and regions
- Singapore: Singapore Zone 1, Singapore Zone 2, Singapore Zone 3.
- Tokyo: Tokyo Zone 1, Tokyo Zone 2.
- Seoul: Seoul Zone 1, Seoul Zone 2.
- Silicon Valley: Silicon Valley Zone 1, Silicon Valley Zone 2.
- Frankfurt: Frankfurt Zone 1, Frankfurt Zone 2.
- Toronto: Toronto Zone 1.
- Mumbai: Mumbai Zone 1, Mumbai Zone 2.


## Connectivity
Both private and public IPs are assigned to Lighthouse instances for private and public network connectivity.
* **Private network connectivity**: Data transfer between Lighthouse instances in the same region is over the local area network (LAN), which is free of charge. See [Private network connectivity](#IntranetUnicom).
* **Public network connectivity**: Lighthouse instances are assigned with public IPs for internet access (both upstream and downstream). Note that you need to pay for the outbound traffic.

### Private network connectivity[](id:IntranetUnicom)
- The table below describes the private network connectivity between Lighthouse instances:
<table>
<tbody>
<tr>
<th style="width: 37%;" colspan=2>Scenario</th>
<th style=" width: 32%;">Supported by Default</th><th style=" width: 31%;">Supported over CCN</th>
</tr>
<tr>
<td rowspan=2>In the same region<br>Under the same account</td>
<td>Access between Lighthouse instances    </td>
<td><b>Yes</b></td>
<td>-</td>
</tr>
<tr>
<td>Connection between Lighthouse instances and LighthouseDB instances</td>
<td><b>Yes</b></td>
<td>-</td>
</tr>
<tr>
<td rowspan=2>Across regions<br>Under the same account</td>
<td>Access between Lighthouse instances </td>
<td>No</td>
<td>-</td>
</tr>
<tr>
<td>Connection between Lighthouse instances and LighthouseDB instances</td>
<td>No</td>
<td>-</td>
</tr>
<tr>
<td>Under different accounts</td>
<td>Access between Lighthouse instances </td>
<td>No</td>
<td>-</td>
</tr>
</tbody></table>


- The private network connectivity between Lighthouse instances and other Tencent Cloud services:
<table>
<tbody>
<tr>
<th style="width: 37%;">Scenario</th>
<th style=" width: 32%;">Supported by Default</th><th style=" width: 31%;">Supported over CCN</th>
</tr>
<tr>
<td>CVM</td>
<td>No</td>
<td><b>Yes</b>. For more information, see <a href="https://intl.cloud.tencent.com/document/product/1103/41396">Private Network Interconnection</a>.</td>
</tr>
<tr>
<td>COS (in the same region)</td>
<td>
<b>Yes</b>. For more information, see COS <a href="https://intl.cloud.tencent.com/document/product/436/6224" target="_blank">Regions and Access Endpoints</a>.
<br>You can determine whether Lighthouse accesses COS over the private network by referring to <a href="https://intl.cloud.tencent.com/document/product/1103/41257" target="_blank">FAQs</a>.
</td>
<td>- </td>
</tr>
<tr>
<td>COS (in different regions)</td>
<td>No</td>
<td>-</td>
</tr>
<tr>
<td>TencentDB</td>
<td>No</td>
<td><b>Yes</b>. For more information, see <a href="https://intl.cloud.tencent.com/document/product/1103/41396">Private Network Interconnection</a>.</td>
</tr>
<tr>
<td>CFS</td>
<td>No</td>
<td><b>Yes</b>. For more information, see <a href="https://intl.cloud.tencent.com/document/product/1103/41396">Private Network Interconnection</a>.</td>
</tr>
<tr>
<td>CLB</td>
<td>No</td>
<td>-</td>
</tr>
</tbody></table>



<dx-alert infotype="notice" title="">
For the above use cases where private network connectivity is not supported, you can connect the instances over the public network, and configure firewall policies to ensure the security. Note that you need to pay for the outbound traffic.
</dx-alert>



### Public network connectivity description
* **Regions in the Chinese mainland**: Stable BGP network access is provided to ensure that access to Lighthouse within the Chinese mainland is over a stable low-latency network.
* **Regions outside the Chinese mainland**: The public network bandwidth is mainly provided for users outside the Chinese mainland. Access from the Chinese mainland may experience a significant delay and packet loss due to the ISP network lines (non-cross-border access typically suffers no impact).


<dx-alert infotype="explain" title="">
We recommend you select the region closest to your end users to minimize the access delay and improve the network stability.
</dx-alert>




<style>
.params{margin-bottom:0px !important}
</style>
