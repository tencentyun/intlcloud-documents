TencentDB data centers are hosted in multiple locations worldwide. These locations are known as regions. Each region contains multiple availability zones (AZs).
Each region is an independent geographic area containing multiple isolated AZs. Separate AZs in the same region are connected via low-latency private networks. Tencent Cloud provides you with the ability to distribute Tencent Cloud resources across different locations. We recommend you place resources in different AZs to eliminate single points of failure which may lead to service unavailability.

Region name and AZ name can most directly embody the coverage of a data center. The following naming convention is used for your convenience:
- A region name is composed of **region + city**. The `region` indicates the geographic area that the data center covers, while the `city` represents the city in or near which the data center is located.
- AZ names utilize the format of **city + number**.

## Region
Tencent Cloud regions are isolated. This guarantees the maximum cross-region stability and fault tolerance. When you purchase Tencent Cloud services, we recommend you select the region closest to your end users to minimize access latency and improve download speed. Operations such as launching or viewing instances are performed at the region level.
Private network communication:
- Tencent Cloud resources in the same VPC within the same region under the same account can communicate with each other over private network. They can also be accessed via [private IPs](https://intl.cloud.tencent.com/document/product/213/5225).
- The networks of different regions are isolated from each other, and Tencent Cloud services in different regions cannot communicate over private network by default.
- Tencent Cloud services in different VPCs can communicate with each other over [Cloud Connect Network](https://intl.cloud.tencent.com/document/product/1003) which is fast and stable.

## Availability Zone
Availability zones (AZs) refer to Tencent Cloud's physical data centers that are in the same region. Each AZ is independently powered and have its own network resources. They are designed to ensure that failures within one AZ can be isolated from other AZs, thereby ensuring service availability and business stability and excepting the occurrences of large-scale disasters or major power failures. Users can protect their applications from being affected by failures that occur in a single location by selecting instances in independent AZs.

## Supported Regions and AZs
<table class="table-striped">
<tbody><tr><th>Region</th><th>AZ</th></tr>
<tr>
<td rowspan="1">South China (Guangzhou)<br> ap-guangzhou</td>
<td>Guangzhou Zone 4<br> ap-guangzhou-4</td></tr>
<tr>
<td rowspan="2">East China (Shanghai)<br>ap-shanghai</td>
<td>Shanghai Zone 2 (sold out)<br>ap-shanghai-2</td></tr>
<tr>
<td>Shanghai Zone 3<br>ap-shanghai-3</td></tr>	
<tr>
<td rowspan="1">North China (Beijing)<br>ap-beijing</td>
<td>Beijing Zone 1<br>ap-beijing-1</td></tr>
<tr>
<td>North America (Toronto)<br>na-toronto</td>
<td>Toronto Zone 1 (suitable for coverage of North America)<br>na-toronto-1</td></tr>	
<td>Southeast Asia Pacific (Singapore)<br>ap-singapore</td>
<td>Singapore Zone 2 (suitable for coverage of Southeast Asia Pacific)<br>ap-singapore-2</td></tr>	
<td>Europe (Frankfurt)<br>eu-frankfurt</td>
<td>Frankfurt Zone 2 (suitable for coverage of Europe)<br>eu-frankfurt-2</td></tr>	
<td>US (Silicon Valley)<br>na-siliconvalley</td>
<td>Silicon Valley Zone 2 (suitable for coverage of US)<br>na-siliconvalley-2</td></tr>	
<td>South Asia Pacific (Mumbai)<br>ap-mumbai</td>
<td>Mumbai Zone 2 (suitable for coverage of South Asia Pacific)<br>ap-mumbai-2</td></tr>	
</tbody></table>

## Regions and AZ Selection
When you purchase Tencent Cloud services, we recommend you select the region closest to your end users to minimize access latency and improve download speed.

