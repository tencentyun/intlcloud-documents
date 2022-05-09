TencentDB data centers are hosted in multiple locations worldwide. These locations are known as regions. Each region contains multiple availability zones (AZs).
Each region is an independent geographic area with multiple isolated AZs. Separate AZs in the same region are connected via low-latency private networks. Tencent Cloud allows you to distribute Tencent Cloud resources across different locations. We recommend placing resources in different AZs to eliminate single points of failure which may lead to service unavailability.

Region name and AZ name can most directly embody the coverage of a data center. The following naming convention is used for your convenience:

- A region name is composed of **region + city**. The `region` indicates the geographic area that the data center covers, while the `city` represents the city in or near which the data center is located.
- AZ names utilize the format of **city + number**.

## Region
Tencent Cloud regions are completely isolated. This guarantees the maximum cross-region stability and fault tolerance. When purchasing Tencent Cloud services, we recommend selecting the region closest to your end users to minimize access latency and improve download speed. Operations such as launching or viewing instances are performed at the region level.
Private network communication:

- Tencent Cloud resources in the same VPC within the same region under the same account can communicate with each other over private network. They can also be accessed via [private IPs](https://intl.cloud.tencent.com/document/product/213/5225).
- The networks of different regions are fully isolated from each other, and Tencent Cloud services in different regions cannot communicate using private networks by default.
- Tencent Cloud services across regions can communicate with each other through [public IPs](https://intl.cloud.tencent.com/document/product/213/5224) over the Internet, while those in different VPCs can communicate with each other through [CCN](https://intl.cloud.tencent.com/document/product/1003) that is faster and steadier.
- [Cloud Load Balancer](https://intl.cloud.tencent.com/document/product/214) currently supports intra-region traffic forwarding by default. If [cross-region binding](https://intl.cloud.tencent.com/document/product/214/38441) is enabled, cross-region binding of CLB and CVM instances is supported.

## AZs
An availability zone (AZ) is a physical IDC of Tencent Cloud with independent power supply and network in the same region. It can ensure business stability, as failures (except for major disasters or power failures) in one AZ are isolated without affecting other AZs in the same region. By starting an instance in an independent AZ, users can protect their applications from being affected by a single point of failure.
When launching an instance, you can select any AZ in the specified region. For high reliability, you can adopt a cross-AZ deployment solution to ensure that the service remains available when an instance in a single location fails. Examples of such solutions include [CLB](https://intl.cloud.tencent.com/document/product/214) and [EIP](https://intl.cloud.tencent.com/document/product/213/5733).

## List of Regions and AZs
### China
<table class="table-striped">
<tbody>
<tr><th>Region</th><th>AZ</th></tr>
<tr>
<td rowspan="5">South China (Guangzhou) <br>ap-guangzhou</td>
<td>Guangzhou Zone 3<br> ap-guangzhou-3</td></tr>	
<tr>
<td>Guangzhou Zone 4<br> ap-guangzhou-4</td></tr>
<tr>
<td>Guangzhou Zone 5<br> ap-guangzhou-5</td></tr>	
<tr>
<td>Guangzhou Zone 6<br> ap-guangzhou-6</td></tr>
<tr>
<td>Guangzhou Zone 7<br> ap-guangzhou-7</td></tr>
<tr>
<td rowspan="3">East China (Shanghai)<br>ap-shanghai</td>
<td>Shanghai Zone 2<br>ap-shanghai-2</td></tr>
<tr>
<td>Shanghai Zone 4<br>ap-shanghai-4</td></tr>
<tr>
<td>Shanghai Zone 5<br>ap-shanghai-5</td></tr>
<tr>
<td rowspan="3">North China (Beijing)<br>ap-beijing</td>
<td>Beijing Zone 3<br>ap-beijing-3</td></tr>
<tr>
<td>Beijing Zone 5<br>ap-beijing-5</td></tr>
<tr>
<td>Beijing Zone 7<br>ap-beijing-7</td></tr>
<td rowspan="1">East China (Nanjing)<br>ap-nanjing</td>
<td>Nanjing Zone 1<br>ap-nanjing-1</td></tr>
<td rowspan="1">Hong Kong/Macao/Taiwan (Hong Kong, China)<br>ap-hongkong</td>
<td>Hong Kong Zone 2<br>ap-hongkong-2</td></tr>
<td rowspan="1">Hong Kong/Macao/Taiwan (Taipei, China)<br>ap-taipei</td>
<td>Taipei Zone 1<br>ap-taipei-1</td></tr>
</tbody></table>	

### Other countries and regions
<table class="table-striped">
<tbody>
<tr><th>Region</th><th>AZ</th></tr>
<tr>
<td rowspan="1">Southeast Asia (Singapore)<br>ap-singapore</td>
<td>Singapore Zone 3<br>ap-singapore-3</td></tr>
<tr><td rowspan="1">West US (Silicon Valley)<br>na-siliconvalley</td>
<td>Silicon Valley Zone 2<br>na-siliconvalley-2</td></tr>
<tr>
<td rowspan="1">Europe (Frankfurt)<br>eu-frankfurt</td>
<td>Frankfurt Zone 2<br>eu-frankfurt-2</td></tr>
<tr>
<td rowspan="2">Eastern US (Virginia)<br>na-ashburn</td>
<td>Virginia Zone 1<br>na-ashburn-1</td></tr>
<td>Virginia Zone 2<br>na-ashburn-2</td></tr>
<tr>
<td rowspan="2">Northeast Asia (Tokyo)<br>ap-tokyo</td>
<td>Tokyo Zone 1<br>ap-tokyo-1</td></tr>
<td>Tokyo Zone 2<br>ap-tokyo-2</td></tr>
<tr>
</tbody></table>	

## Selection of Regions and AZs
When purchasing Tencent Cloud services, we recommend selecting the region closest to your end users to minimize access latency and improve download speed.
