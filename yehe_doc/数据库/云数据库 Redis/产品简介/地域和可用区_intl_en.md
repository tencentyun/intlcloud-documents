
## Region
### Overview
A region is the physical location of an IDC. In Tencent Cloud, regions are fully isolated from each other, ensuring cross-region stability and fault tolerance. When purchasing Tencent Cloud services, we recommend selecting the region closest to your end users to minimize access latency and improve download speed.

### Characteristics
- The networks of different regions are fully isolated. Tencent Cloud services in different regions **cannot communicate via a private network by default**.
- Tencent Cloud services in different VPCs can communicate each other over [Cloud Connect Network](https://intl.cloud.tencent.com/zh/document/product/1003) which is fast and stable.

## Availability Zones
### Overview
An availability zone (AZ) is a physical IDC of Tencent Cloud with independent power supply and network in the same region. It can ensure business stability, as failures (except for major disasters or power failures) in one AZ are isolated without affecting other AZs in the same region. By starting an instance in an independent availability zone, users can protect their applications from being affected by a single point of failure.

### Characteristics
Tencent Cloud services in the same VPC are interconnected via the private network, which means they can communicate using [private IPs](https://intl.cloud.tencent.com/document/product/213/5225), even if they are in different availability zones of the same region.
>? Private network interconnection refers to the interconnection of resources under the same account. Resources under different accounts are completely isolated on the private network.
>

## List of Regions and AZs
### China
<table class="table-striped">
<tbody><tr><th>Region</th><th>Availability Zone</th><th>Zone ID</th></tr>
<tr>
<td rowspan="6">South China (Guangzhou)<br>ap-guangzhou</td>
<td>Guangzhou Zone 1<br> ap-guangzhou-1</td><td>100001</td></tr>	
<tr>
<td>Guangzhou Zone 2<br> ap-guangzhou-2</td><td>100002</td></tr>
<tr>
<td>Guangzhou Zone 3<br> ap-guangzhou-3</td><td>100003</td></tr>
<tr>
<td>Guangzhou Zone 4<br> ap-guangzhou-4</td><td>100004</td></tr>
<tr>
<td>Guangzhou Zone 6<br> ap-guangzhou-6</td><td>100006</td></tr>
<tr>
<td>Guangzhou Zone 7<br> ap-guangzhou-7</td><td>100007</td></tr>
<tr>
<td rowspan="7">East China (Shanghai)<br>ap-shanghai</td>
<td>Shanghai Zone 1<br>ap-shanghai-1</td><td>200001</td></tr>
<tr>
<td>Shanghai Zone 2<br>ap-shanghai-2</td><td>200002</td></tr>
<tr>
<td>Shanghai Zone 3<br>ap-shanghai-3</td><td>200003</td></tr>
<tr>
<td>Shanghai Zone 4<br>ap-shanghai-4</td><td>200004</td></tr>
<tr>
<td>Shanghai Zone 5<br>ap-shanghai-5</td><td>200005</td></tr>
<tr>
<td>Shanghai Zone 6<br>ap-shanghai-6</td><td>200006</td></tr>
<tr>
<td>Shanghai Zone 7<br>ap-shanghai-7</td><td>200007</td></tr>
<tr>
<td rowspan="2">East China (Nanjing)<br>ap-nanjing</td>
<td>Nanjing Zone 1<br>ap-nanjing-1</td><td>330001</td></tr>
<tr>
<td>Nanjing Zone 2<br>ap-nanjing-2</td><td>330002</td></tr>
<tr>
<td rowspan="7">North China (Beijing)<br>ap-beijing</td>
<td>Beijing Zone 1<br>ap-beijing-1</td><td>800001</td></tr>
<tr>
<td>Beijing Zone 2<br>ap-beijing-2</td><td>800002</td></tr>
<tr>
<td>Beijing Zone 3<br>ap-beijing-3</td><td>800003</td></tr>
<tr>
<td>Beijing Zone 4<br>ap-beijing-4</td><td>800004</td></tr>
<tr>
<td>Beijing Zone 5<br>ap-beijing-5</td><td>800005</td></tr>
<tr>
<td>Beijing Zone 6<br>ap-beijing-6</td><td>800006</td></tr>
<tr>
<td>Beijing Zone 7<br>ap-beijing-7</td><td>800007</td></tr>
<tr>
<td rowspan="2">Southwest China (Chengdu)<br>ap-chengdu</td>
<td>Chengdu Zone 1<br>ap-chengdu-1</td><td>160001</td></tr>
<tr>
<td>Chengdu Zone 2<br>ap-chengdu-2</td><td>160002</td></tr>    
<tr>
<td>Southwest China (Chongqing)<br>ap-chongqing</td>
<td>Chongqing Zone 1<br>ap-chongqing-1</td><td>190001</td></tr>
<tr>
<td rowspan="3">Hong Kong/Macao/Taiwan (Hong Kong, China)<br>ap-hongkong</td>
<td>Hong Kong Zone 1 (Hong Kong nodes cover services in the China regions of Hong Kong, Macao, and Taiwan)<br>ap-hongkong-1</td><td>300001</td></tr>
<tr>
<td>Hong Kong Zone 2 (Nodes in Hong Kong, China cover Hong Kong/Macao/Taiwan regions)<br>ap-hongkong-2</td><td>300002</td></tr>
<tr>
<td>Hong Kong Zone 3 (Hong Kong nodes cover services in the China regions of Hong Kong, Macao, and Taiwan)<br>ap-hongkong-3</td><td>300003</td></tr>
</tbody></table>	

### Other countries and regions
<table class="table-striped">
<tbody><tr><th>Region</th><th>Availability Zone</th><th>Zone ID</th></tr>
<tr>
<td rowspan="3">Southeast Asia (Singapore)<br>ap-singapore</td>
<td>Singapore Zone 1 (Singapore nodes cover services in Southeast Asia)<br>ap-singapore-1</td><td>900001</td></tr>
<tr>
<td>Singapore Zone 2 (Singapore nodes cover services in Southeast Asia)<br>ap-singapore-2</td><td>900002</td></tr>
<tr>
<td>Singapore Zone 3 (Singapore nodes cover services in Southeast Asia)<br>ap-singapore-3</td><td>900003</td></tr>
<tr>
<td>Southeast Asia (Jakarta)<br>ap-jakarta</td>
<td>Jakarta Zone 1 (Jakarta nodes cover services in Southeast Asia)<br>ap-jakarta-1</td><td>720001</td></tr>
<tr>
<td rowspan="2">Southeast Asia (Bangkok)<br>ap-bangkok</td>
<td>Bangkok Zone 1 (Bangkok nodes cover services in Southeast Asia)<br>ap-bangkok-1</td><td>230001</td></tr>
<tr>
<td>Bangkok Zone 2 (Bangkok nodes cover services in Southeast Asia)<br>ap-bangkok-2</td><td>230002</td></tr>
<tr>
<td rowspan="2">South Asia (Mumbai)<br>ap-mumbai</td>
<td>Mumbai Zone 1 (Mumbai nodes cover services in South Asia)<br>ap-mumbai-1</td><td>210001</td></tr>
<tr>
<td>Mumbai Zone 2 (Mumbai nodes cover services in South Asia)<br>ap-mumbai-2</td><td>210002</td></tr>		
<tr>
<td rowspan="2">Northeast Asia (Seoul)<br>ap-seoul</td>
<td>Seoul Zone 1 (Seoul nodes cover services in Northeast Asia)<br>ap-seoul-1</td><td>180001</td></tr>
<tr>
<td>Seoul Zone 2 (Seoul nodes cover services in Northeast Asia)<br>ap-seoul-2</td><td>180002</td></tr>
<tr>
<td rowspan="2">Northeast Asia (Tokyo)<br>ap-tokyo</td>
<td>Tokyo Zone 1 (Tokyo nodes cover services in Northeast Asia)<br>ap-tokyo-1</td><td>250001</td></tr>
<tr>
<td>Tokyo Zone 2 (Tokyo nodes cover services in Northeast Asia)<br>ap-tokyo-2</td><td>250002</td></tr>
<tr>
<td rowspan="2">West US (Silicon Valley)<br>na-siliconvalley</td>
<td>Silicon Valley Zone 1 (Silicon Valley nodes cover services in West US)<br>na-siliconvalley-1</td><td>150001</td></tr>
<tr>
<td>Silicon Valley Zone 2 (Silicon Valley nodes cover services in West US)<br>na-siliconvalley-2</td><td>150002</td></tr>
<tr>
<td rowspan="2">East US (Virginia)<br>na-ashburn</td>
<td>Virginia Zone 1 (Virginia nodes cover services in East US)<br>na-ashburn-1</td><td>220001</td></tr>
<tr>
<td>Virginia Zone 2 (Virginia nodes cover services in East US)<br>na-ashburn-2</td><td>220002</td></tr>
<tr>
<td>North America (Toronto)<br>na-toronto</td>
<td>Toronto Zone 1 (Toronto nodes cover services in North America)<br>na-toronto-1</td><td>400001</td></tr>
<tr>
<td rowspan="2">Europe (Frankfurt)<br>eu-frankfurt</td>
<td>Frankfurt Zone 1 (Frankfurt nodes cover services in Europe)<br>eu-frankfurt-1</td><td>170001</td></tr>
<tr>
<td>Frankfurt Zone 2 (Frankfurt nodes cover services in Europe)<br>eu-frankfurt-2</td><td>170002</td></tr>
<td >Europe (Moscow)<br>eu-moscow</td>
<td>Moscow Zone 1 (Moscow nodes cover services in Europe)<br>eu-moscow-1</td><td>240001</td></tr>
<tr>
<td>South America (Sao Paulo)<br>sa-saopaulo</td>
<td>Sao Paulo Zone 1 (Sao Paulo nodes cover services in South America)<br>sa-saopaulo-1</td><td>740001</td></tr>
</tbody></table>

## Selection of Regions and AZs
When purchasing Tencent Cloud services, we recommend selecting the region closest to your end users to minimize access latency and improve download speed.

