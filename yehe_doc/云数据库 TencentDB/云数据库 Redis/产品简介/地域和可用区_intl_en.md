
TencentDB for Redis is available in various regions. It can be deployed wherever CVM instances are deployed.

## Network Description
- Tencent Cloud resources in the same VPC within the same region under the same account can communicate with each other over private network. They can also be accessed via [private IPs](https://intl.cloud.tencent.com/document/product/213/5225).
- A CVM instance in a VPC can access a TencentDB for Redis instance on the classic network in a different AZ in the same region only after a subnet is configured and a VPC IP is assigned.
- Tencent Cloud services in different VPCs can communicate each other over [Cloud Connect Network](https://intl.cloud.tencent.com/zh/document/product/1003) which is fast and stable.
>?When you purchase TencentDB for Redis, we recommend you select the same region as your CVM instance to reduce access delay.

## Regions and AZs
### China
<table class="table-striped">
<tbody><tr><th>Region</th><th>Availability Zone</th><th>Zone ID</th></tr>
<tr>
<td rowspan="5">South China (Guangzhou)<br> ap-guangzhou</td>
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
<td rowspan="7">North China (Beijing) <br>ap-beijing</td>
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
<td rowspan="2">North China (Tianjin)<br>ap-tianjin</td>
<td>Tianjin Zone 1<br>ap-tianjin-1</td><td>360001</td></tr>
<tr>
<td>Tianjin Zone 2<br>ap-tianjin-2</td><td>360002</td></tr> 
<tr>
<td rowspan="2">Southwest China (Chengdu)<br>ap-chengdu</td>
<td>Chengdu Zone 1<br>ap-chengdu-1</td><td>160001</td></tr>
<tr>
<td>Chengdu Zone 2<br>ap-chengdu-2</td><td>160002</td></tr>    
<tr>
<td >Southwest China (Chongqing)<br>ap-chongqing</td>
<td>Chongqing Zone 1<br>ap-chongqing-1</td><td>190001</td></tr>
<tr>
<td rowspan="3">Hong Kong/Macao/Taiwan (Hong Kong, China)<br>ap-hongkong</td>
<td>Hong Kong Zone 1 (Hong Kong nodes cover services in the China regions of Hong Kong, Macao, and Taiwan)<br>ap-hongkong-1</td><td>300001</td></tr>
<tr>
<td>Hong Kong Zone 2 (Hong Kong nodes cover services in the China regions of Hong Kong, Macao, and Taiwan)<br>ap-hongkong-2</td><td>300002</td></tr>
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
</tr>
<tr>
<td>Southeast Asia (Bangkok)<br>ap-bangkok </td>
<td>Bangkok Zone 1 (Bangkok nodes cover services in Southeast Asia)<br>ap-bangkok-1</td><td>230001</td>
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
<td>Silicon Valley Zone 1 (Silicon Valley nodes cover services in Western US)<br>na-siliconvalley-1</td><td>150001</td></tr>
<tr>
<td>Silicon Valley Zone 2 (Silicon Valley nodes cover services in Western US)<br>na-siliconvalley-2</td><td>150002</td></tr>
<tr>
<td rowspan="2">East US (Virginia)<br>na-ashburn</td>
<td>Virginia Zone 1 (Virginia nodes cover services in Eastern US)<br>na-ashburn-1</td><td>220001</td></tr>
<tr>
<td>Virginia Zone 2 (Virginia nodes cover services in Eastern US)<br>na-ashburn-2</td><td>220002</td></tr>
<tr>
<td>North America (Toronto)<br>na-toronto</td><td>Toronto Zone 1 (Toronto nodes cover services in North America)<br>na-toronto-1</td><td>400001</td></tr>
<tr>
<td>Europe (Frankfurt)<br>eu-frankfurt</td><td>Frankfurt Zone 1 (Frankfurt nodes cover services in Europe)<br>eu-frankfurt-1</td><td>170001</td></tr>
<td >Europe (Moscow)<br>eu-moscow</td>
<td>Moscow Zone 1 (Moscow nodes cover services in Europe)<br>eu-moscow-1</td><td>240001</td></tr>
</tbody></table>

