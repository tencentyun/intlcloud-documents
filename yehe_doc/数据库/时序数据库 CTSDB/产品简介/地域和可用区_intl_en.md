TencentDB data centers are hosted in multiple locations worldwide. These locations are known as regions. Each region contains multiple availability zones (AZs).
Each region is an independent geographic area containing multiple isolated AZs. Separate AZs in the same region are connected via low-latency private networks. Tencent Cloud provides you with the ability to distribute Tencent Cloud resources across different locations. We recommend placing resources in different AZs to eliminate single points of failure which may lead to service unavailability.

Region name and AZ name can most directly embody the coverage of a data center. The following naming convention is used for your convenience:
- A region name is composed of **region + city**. The `region` indicates the geographic area that the data center covers, while the `city` represents the city in or near which the data center is located.
- AZ names utilize the format of **city + number**.

## Region
Tencent Cloud regions are isolated. This guarantees the maximum cross-region stability and fault tolerance. When purchasing Tencent Cloud services, we recommend selecting the region closest to your end users to minimize access latency and improve download speed. Operations such as launching or viewing instances are performed at the region level.
Private network communication:
- Tencent Cloud resources in the same VPC within the same region under the same account can communicate with each other over private network. They can also be accessed via [private IPs](https://intl.cloud.tencent.com/document/product/213/5225).
- The networks of different regions are isolated. Tencent Cloud services in different regions cannot communicate via a private network by default.
- Tencent Cloud services in different VPCs can communicate each other over [Cloud Connect Network](https://intl.cloud.tencent.com/zh/document/product/1003) which is fast and stable.

## Availability Zone
An availability zone (AZ) is a physical IDC of Tencent Cloud with independent power supply and network in the same region. It can ensure business stability, as failures (except for major disasters or power failures) in one AZ are isolated without affecting other AZs in the same region. By starting an instance in an independent availability zone, users can protect their applications from being affected by a single point of failure.

## Supported Regions and AZs
### China
<table class="table-striped">
<tbody><tr><th>Region</th><th>Availability Zone</th></tr>
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
<td>Southwest China (Chongqing)<br>ap-chongqing</td>
<td>Chongqing Zone 1<br>ap-chongqing-1</td></tr>
<tr>
<td rowspan="1">Hong Kong/Macao/Taiwan (Hong Kong, China)<br>ap-hongkong</td>
<td>Hong Kong Zone 3 (Hong Kong nodes cover services in the China regions of Hong Kong, Macao, and Taiwan)<br>ap-hongkong-3</td></tr>
</tbody></table>

### Other countries and regions
<table class="table-striped">
<tbody><tr><th>Region</th><th>Availability Zone</th></tr>
<tr>
<td>Southeast Asia (Singapore)<br>ap-singapore</td>
<td>Singapore Zone 2 (Singapore nodes cover services in Southeast Asia)<br>ap-singapore-2</td></tr>	
<tr>
<td rowspan="1">Southeast Asia (Bangkok)<br>ap-bangkok</td>
<td>Bangkok Zone 2 (Bangkok nodes cover services in Southeast Asia)<br>ap-bangkok-2</td>
<tr>
<td>South Asia (Mumbai)<br>ap-mumbai</td>
<td>Mumbai Zone 2 (sold out) (Mumbai nodes cover services in South Asia)<br>ap-mumbai-2</td></tr>	
<tr>
<td>US (Silicon Valley)<br>na-siliconvalley</td>
<td>Silicon Valley Zone 2 (sold out) (Silicon Valley nodes cover services in US)<br>na-siliconvalley-2</td></tr>	
<tr>
<td>North America (Toronto)<br>na-toronto</td>
<td>Toronto Zone 1 (Toronto nodes cover services in North America)<br>na-toronto-1</td></tr>	
<tr>
<td>Europe (Frankfurt)<br>eu-frankfurt</td>
<td>Frankfurt Zone 2 (Frankfurt nodes cover services in Europe)<br>eu-frankfurt-2</td></tr>
</tbody></table>

## Region and AZ Selection
When you purchase Tencent Cloud services, we recommend you select the region closest to your end users to minimize access latency and improve download speed.

