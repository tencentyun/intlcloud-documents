## Region
- **Overview**
Tencent Cloud data centers are distributed across different regions worldwide. To reduce access delay and improve download speed, it is recommended that you select the region closest to your end users.
- **Considerations**
 - Each region includes multiple availability zones.
 - By default, Lighthouse instances in different regions can not communicate through the private network.

## Availability Zones
- **Overview**
An Availability Zone (AZ) refers to a physical location with independent power supply and network resources within a region. 
AZs in the same region are interconnected through low-latency private network linkages, which allows Lighthouse instances in different AZs in the same region to communicate with each other through private networks. For applications with high disaster recovery requirements, deploy Lighthouse instances to different availability zones within the same region to ensure fault isolation. Note that it may cause a longer communication latency.
- **Considerations**
 By default, Lighthouse instances in different availability zones within the same region can communicate through the private network.


## Supported Regions and Availability Zones
<dx-alert infotype="explain" title="">
Lighthouse instances are available in the following availability zones.
</dx-alert>

####  Hong Kong, Macao, and Taiwan of China
Hong Kong, China: Hong Kong Zone 2, Hong Kong Zone 3.

####  Other countries and regions
- Singapore: Singapore Zone 1, Singapore Zone 3.
- Tokyo: Tokyo Zone 1, Tokyo Zone 2.
- Silicon Valley: Silicon Valley Zone 1, Silicon Valley Zone 2.
- 莫斯科：莫斯科一区。
- Frankfurt: Frankfurt Zone 1, Frankfurt Zone 2.
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
<th style="width: 37%;">Use cases</th>
<th style=" width: 32%;">Supported by Default</th><th style=" width: 31%;">Supported over CCN</th>
</tr>
<tr>
<td>Lighthouse instances under the same account in the same region </td>
<td><b>Yes</b>. Note that you need to open the port for firewall management</a>.</td>
<td>-</td>
</tr>
<tr>
<td>Lighthouse instances under the same account but in different regions</td>
<td>No</td>
<td>-</td>
</tr>
<tr>
<td>Lighthouse instances under different accounts</td>
<td>No</td>
<td>-</td>
</tr>
</tbody></table>


- The private network connectivity between Lighthouse instances and other Tencent Cloud services:
<table>
<tbody>
<tr>
<th style="width: 37%;">Service</th>
<th style=" width: 32%;">Supported by Default</th><th style=" width: 31%;">Supported over CCN</th>
</tr>
<tr>
<td>CVM</td>
<td>No</td>
<td><b>Yes</a>.</td>
</tr>
<tr>
<td>COS (in the same region)</td>
<td>
<b>Yes</b>. For more information, see COS <a href="https://intl.cloud.tencent.com/document/product/436/6224#private-network-and-public-network-access" target="_blank">Regions and Access Endpoints</a>.
<br>You can determine whether Lighthouse accesses COS over the private network by referring to <a href="https://intl.cloud.tencent.com/document/product/1103/41257#how-do-i-upload-local-files-to-a-lighthouse-instance.3F" target="_blank">FAQs</a>.
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
<td><b>Yes</a>.</td>
</tr>
<tr>
<td>CFS</td>
<td>No</td>
<td><b>Yes</a>.</td>
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



