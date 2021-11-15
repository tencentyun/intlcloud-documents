TencentDB data centers are hosted in multiple locations worldwide. These locations are known as regions. Each region contains multiple availability zones (AZs).
Each region is an independent geographic area containing multiple isolated AZs. Separate AZs in the same region are connected via low-latency private networks. Tencent Cloud provides you with the ability to distribute Tencent Cloud resources across different locations. We recommend placing resources in different AZs to eliminate single points of failure which may lead to service unavailability.

Region name and AZ name can most directly embody the coverage of a data center. The following naming convention is used for your convenience:
- A region name is composed of **region + city**. The `region` indicates the geographic area that the data center covers, while the `city` represents the city in or near which the data center is located.
- AZ names utilize the format of **city + number**.

## Regions
Tencent Cloud regions are completely isolated. This guarantees the maximum cross-region stability and fault tolerance. When purchasing Tencent Cloud services, we recommend selecting the region closest to your end users to minimize access latency and improve download speed. Operations such as launching or viewing instances are performed at the region level.
Private network communication:

- Tencent Cloud resources in the same VPC within the same region under the same account can communicate with each other over private network. They can also be accessed via [private IPs](https://intl.cloud.tencent.com/document/product/213/5225).
- The networks of different regions are fully isolated from each other, and Tencent Cloud services in different regions cannot communicate using private networks by default.
- Tencent Cloud services across regions can communicate with each other through [public IPs](https://intl.cloud.tencent.com/document/product/213/5224) over the Internet, while those in different VPCs can communicate with each other through [CCN](https://intl.cloud.tencent.com/document/product/1003) that is faster and steadier.
- [Cloud Load Balancer](https://intl.cloud.tencent.com/document/product/214) currently supports intra-region traffic forwarding by default. If you enable the [cross-region binding](https://intl.cloud.tencent.com/document/product/214/12014) feature, a CLB instance can be bound to CVM instances in another region.

## Availability Zones
An availability zone (AZ) is a physical IDC of Tencent Cloud with independent power supply and network in the same region. It can ensure business stability, as failures (except for major disasters or power failures) in one AZ are isolated without affecting other AZs in the same region. By starting an instance in an independent availability zone, users can protect their applications from being affected by a single point of failure.
When launching an instance, you can select any AZ in the specified region. For high reliability, you can adopt a cross-AZ deployment solution to ensure that the service remains available when an instance in a single location fails. Examples of such solutions include [CLB](https://intl.cloud.tencent.com/document/product/214) and [EIP](https://intl.cloud.tencent.com/document/product/213/5733).

## Region and AZ Details
The supported regions and AZs are as follows:
>?Currently, public network access is supported only in the following regions:
>Guangzhou, Shanghai, Nanjing, Beijing, Chengdu, Chongqing, Hong Kong (China), Singapore, Seoul, Tokyo, Silicon Valley, and Frankfurt

### China
<table class="table-striped">
<tbody>
<tr><th>Region</th><th>Availability Zone</th></tr>
<tr>
<td rowspan="6">South China (Guangzhou)<br>ap-guangzhou</td>
<td>Guangzhou Zone 1 (sold out)<br> ap-guangzhou-1</td></tr>	
<tr>
<td>Guangzhou Zone 2<br> ap-guangzhou-2</td></tr>
<tr>
<td>Guangzhou Zone 3<br> ap-guangzhou-3</td></tr>
<tr>
<td>Guangzhou Zone 4<br> ap-guangzhou-4</td></tr>
<tr>
<td>Guangzhou Zone 6<br> ap-guangzhou-6</td></tr>
<tr>
<td>Guangzhou Zone 7<br> ap-guangzhou-7</td></tr>
<tr>
<td rowspan="5">East China (Shanghai)<br>ap-shanghai</td>
<td>Shanghai Zone 1<br>ap-shanghai-1</td></tr>
<tr>
<td>Shanghai Zone 2<br>ap-shanghai-2</td></tr>
<tr>
<td>Shanghai Zone 3<br>ap-shanghai-3</td></tr>
<tr>
<td>Shanghai Zone 4<br>ap-shanghai-4</td></tr>
<tr>
<td>Shanghai Zone 5<br>ap-shanghai-5</td></tr>
<td rowspan="3">East China (Nanjing)<br>ap-nanjing</td>
<td>Nanjing Zone 1<br>ap-nanjing-1</td></tr>
<tr>
<td>Nanjing Zone 2<br>ap-nanjing-2</td></tr>
<tr>
<td>Nanjing Zone 3<br>ap-nanjing-3</td></tr>
<tr>
<td rowspan="7">North China (Beijing)<br>ap-beijing</td>
<td>Beijing Zone 1<br>ap-beijing-1</td></tr>
<tr>
<td>Beijing Zone 2<br>ap-beijing-2</td></tr>
<tr>
<td>Beijing Zone 3<br>ap-beijing-3</td></tr>
<tr>
<td>Beijing Zone 4<br>ap-beijing-4</td></tr>
<tr>
<td>Beijing Zone 5<br>ap-beijing-5</td></tr>
<tr>
<td>Beijing Zone 6<br>ap-beijing-6</td></tr>
<tr>
<td>Beijing Zone 7<br>ap-beijing-7</td></tr>
<tr>
<td rowspan="2">Southwest China (Chengdu)<br>ap-chengdu</td>
<td>Chengdu Zone 1<br>ap-chengdu-1</td></tr>
<tr>
<td>Chengdu Zone 2<br>ap-chengdu-2</td></tr>    
<tr>
<td>Southwest China (Chongqing)<br>ap-chongqing</td>
<td>Chongqing Zone 1<br>ap-chongqing-1</td></tr>
<tr>
<td rowspan="3">Hong Kong/Macao/Taiwan (Hong Kong, China)<br>ap-hongkong</td>
<td>Hong Kong Zone 1 (Hong Kong nodes cover services in the China regions of Hong Kong, Macao, and Taiwan)<br>ap-hongkong-1</td></tr>
<tr>
<td>Hong Kong Zone 2 (Hong Kong nodes cover services in the China regions of Hong Kong, Macao, and Taiwan)<br>ap-hongkong-2</td></tr>
<tr>
<td>Hong Kong Zone 3 (Hong Kong nodes cover services in the China regions of Hong Kong, Macao, and Taiwan)<br>ap-hongkong-3</td></tr>
</tbody></table>	


### [Other countries and regions](id:InternationalArea)
<table class="table-striped">
<tbody>
<tr><th>Region</th><th>Availability Zone</th></tr>
<tr>
<td rowspan="3">Southeast Asia (Singapore)<br>ap-singapore</td>
<td>Singapore Zone 1 (Singapore nodes cover services in Southeast Asia)<br>ap-singapore-1</td></tr>
<tr>
<td>Singapore Zone 2 (Singapore nodes cover services in Southeast Asia)<br>ap-singapore-2</td></tr>
<tr>
<td>Singapore Zone 3 (Singapore nodes cover services in Southeast Asia)<br>ap-singapore-3</td>
</tr>
<td>Southeast Asia (Jakarta)<br>ap-jakarta</td>
<td>Jakarta Zone 1 (Jakarta nodes cover services in Southeast Asia)<br>ap-jakarta-1</td></tr>
<tr>
<td rowspan="2">Southeast Asia (Bangkok)<br>ap-bangkok</td>
<td>Bangkok Zone 1 (Bangkok nodes cover services in Southeast Asia)<br>ap-bangkok-1</td>
<tr>
<td>Bangkok Zone 2 (Bangkok nodes cover services in Southeast Asia)<br>ap-bangkok-2</td>
<tr>
<td  rowspan="2">South Asia (Mumbai)<br>ap-mumbai</td>
<td>Mumbai Zone 1 (Mumbai nodes cover services in South Asia)<br>ap-mumbai-1</td></tr>
<tr>
<td>Mumbai Zone 2 (Mumbai nodes cover services in South Asia)<br>ap-mumbai-2</td></tr>		
<tr>
<td  rowspan="2">Northeast Asia (Seoul)<br>ap-seoul</td>
<td>Seoul Zone 1 (Seoul nodes cover services in Northeast Asia)<br>ap-seoul-1</td></tr>
<tr>
<td>Seoul Zone 2 (Seoul nodes cover services in Northeast Asia)<br>ap-seoul-2</td></tr>
<tr>
<td rowspan="2">Northeast Asia (Tokyo)<br>ap-tokyo</td>
<td>Tokyo Zone 1 (Tokyo nodes cover services in Northeast Asia)<br>ap-tokyo-1</td></tr>
<tr>
<td>Tokyo Zone 2 (Tokyo nodes cover services in Northeast Asia)<br>ap-tokyo-2</td></tr>
<tr>
<td rowspan="2">US West (Silicon Valley)<br>na-siliconvalley</td>
<td>Silicon Valley Zone 1 (Silicon Valley nodes cover services in Western US)<br>na-siliconvalley-1</td></tr>
<tr>
<td>Silicon Valley Zone 2 (Silicon Valley nodes cover services in Western US)<br>na-siliconvalley-2</td></tr>
<tr>
<td rowspan="2">Eastern US (Virginia) <br>na-ashburn</td>
<td>Virginia Zone 1 (Virginia nodes cover services in Eastern US)<br>na-ashburn-1</td></tr>
<tr>
<td>Virginia Zone 2 (Virginia nodes cover services in Eastern US)<br>na-ashburn-2</td></tr>
<tr>
<td>North America (Toronto)<br>na-toronto</td>
<td>Toronto Zone 1 (Toronto nodes cover services in North America)<br>na-toronto-1</td></tr>
<tr>
<td rowspan="2">Europe (Frankfurt)<br>eu-frankfurt</td>
<td>Frankfurt Zone 1 (Frankfurt nodes cover services in Europe)<br>eu-frankfurt-1</td></tr>
<tr>
<td>Frankfurt Zone 2 (Frankfurt nodes cover services in Europe)<br>eu-frankfurt-2</td></tr>
<tr>
<td >Europe (Moscow)<br>eu-moscow</td>
<td>Moscow Zone 1 (Moscow nodes cover services in Europe)<br>eu-moscow-1</td></tr>
</tbody></table>

## Selecting Regions and AZs
When purchasing Tencent Cloud services, we recommend selecting the region closest to your end users to minimize access latency and improve download speed.
