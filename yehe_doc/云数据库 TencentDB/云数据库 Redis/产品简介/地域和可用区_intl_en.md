
TencentDB for Redis is available in various regions. It can be deployed wherever CVM instances are deployed.

## Network Description
-  Tencent Cloud services in the same region can communicate with each other over the private network.
-  A CVM instance in a VPC can access a TencentDB for Redis instance on the classic network in a different AZ in the same region only after a subnet is configured and a VPC IP is assigned.
-  Tencent Cloud services on the classic network in different regions cannot communicate with each other over the private network. They can communicate across VPCs only after a [peering connection](https://intl.cloud.tencent.com/document/product/553/18827) is configured.
 >?When you purchase TencentDB for Redis, we recommend you select the same region as your CVM instance to reduce access delay.

## Regions and AZs

### China

<table class="table-striped">
<tbody>
	<tr>
		<th>Region</th>
		<th>Availability Zone</th>
		<th>ZoneId</th>
	</tr>
	<tr>
		<td rowspan="4">South China (Guangzhou)<br> ap-guangzhou</td>
		<td>Guangzhou Zone 1<br> ap-guangzhou-1</td>
		<td>100001</td>
	</tr>	
	<tr>
		<td>Guangzhou Zone 2<br>ap-guangzhou-2</td>
		<td>100002</td>
	</tr>
	<tr>
		<td>Guangzhou Zone 3<br>ap-guangzhou-3</td>
		<td>100003</td>
	</tr>
	<tr>
		<td>Guangzhou Zone 4<br>ap-guangzhou-4</td>
		<td>100004</td>
	</tr>
	<tr>
		<td rowspan="3">South China (Shenzhen Finance)<br>ap-shenzhen-fsi</td>
		<td>Shenzhen Finance Zone 1 (only financial institutions and enterprises can apply for activation by <a href="https://console.cloud.tencent.com/workorder/category">submitting a ticket</a>) <br>ap-shenzhen-fsi-1</span></td>
		<td>110001</td>
	</tr>
	<tr>
		<td>Shenzhen Finance Zone 2 (only financial institutions and enterprises can apply for activation by submitting a ticket) <br>ap-shenzhen-fsi-2</span></td>
		<td>110002</td>
	</tr>
  <tr>
		<td>Shenzhen Finance Zone 3 (only financial institutions and enterprises can apply for activation by submitting a ticket) <br>ap-shenzhen-fsi-3</span></td>
		<td>110003</td>
	</tr>
	<tr>
		<td rowspan="7">East China (Shanghai)<br>ap-shanghai</td>
		<td>Shanghai Zone 1<br>ap-shanghai-1</td>
		<td>200001</td>
	</tr>
	<tr>
		<td>Shanghai Zone 2<br>ap-shanghai-2</td>
		<td>200002</td>
	</tr>
	<tr>
		<td>Shanghai Zone 3<br>ap-shanghai-3</td>
		<td>200003</td>
	</tr>
	<tr>
		<td>Shanghai Zone 4<br>ap-shanghai-4</td>
		<td>200004</td>
	</tr>
	<tr>
		<td>Shanghai Zone 5<br>ap-shanghai-5</td>
		<td>200005</td>
	</tr>
	<tr>
		<td>Shanghai Zone 6<br>ap-shanghai-6</td>
		<td>200006</td>
	</tr>
	<tr>
		<td>Shanghai Zone 7<br>ap-shanghai-7</td>
		<td>200007</td>
	</tr>
	<tr>
			<td rowspan="3">East China (Shanghai Finance)<br>ap-shanghai-fsi</td>
			<td>Shanghai Finance Zone 1 (only financial institutions and enterprises can apply for activation by submitting a ticket) <br>ap-shanghai-fsi-1</td>
			<td>700001</td>
	</tr>
	<tr>
			<td>Shanghai Finance Zone 2 (only financial institutions and enterprises can apply for activation by submitting a ticket) <br>ap-shanghai-fsi-2</td>
			<td>700002</td>
	</tr>
	<tr>
			<td>Shanghai Finance Zone 3 (only financial institutions and enterprises can apply for activation by submitting a ticket) <br>ap-shanghai-fsi-3</td>
			<td>700003</td>
	</tr>
	<tr>
			<td rowspan="2">East China (Nanjing)<br>ap-nanjing</td>
			<td>Nanjing Zone 1<br>ap-nanjing-1</td>
			<td>330001</td>
	</tr>
	<tr>
			<td>Nanjing Zone 2<br>ap-nanjing-2</td>
			<td>330002</td>
	</tr>
	<tr>
			<td rowspan="5">North China (Beijing)<br>ap-beijing</td>
			<td>Beijing Zone 1<br>ap-beijing-1</td>
			<td>800001</td>
	</tr>
	<tr>
			<td>Beijing Zone 2<br>ap-beijing-2</td>
			<td>800002</td>
	</tr>
	<tr>
			<td>Beijing Zone 3<br>ap-beijing-3</td>
			<td>800003</td>
	</tr>
	<tr>
			<td>Beijing Zone 4<br>ap-beijing-4</td>
			<td>800004</td>
	</tr>
	<tr>
			<td>Beijing Zone 5<br>ap-beijing-5</td>
			<td>800005</td>
	</tr>
 <tr>
			<td rowspan="1">North China (Beijing Finance) <br>ap-beijing-fsi</td>
			<td>Beijing Finance Zone 1 (only financial institutions and enterprises can apply for activation by submitting a ticket) <br>ap-beijing-fsi-1</td>
			<td>460001</td>
	</tr>
	<tr>
		<td rowspan="2">North China (Tianjin)<br>ap-tianjin</td>
		<td>Tianjin Zone 1<br>ap-tianjin-1</td>
		<td>360001</td>
	</tr>
	<tr>
	 <td>Tianjin Zone 2<br>ap-tianjin-2</td>
	<td>360002</td>
	</tr> 
	<tr>
		<td rowspan="2">Southwest China (Chengdu)<br>ap-chengdu</td>
		<td>Chengdu Zone 1<br>ap-chengdu-1</td>
		<td>160001</td>
	</tr>
	<tr>
			<td>Chengdu Zone 2<br>ap-chengdu-2</td>
			<td>160002</td>
	</tr>    
	<tr>
			<td >Southwest China (Chongqing)<br>ap-chongqing</td>
			<td>Chongqing Zone 1<br>ap-chongqing-1</td>
			<td>190001</td>
	</tr>
	<tr>
			<td rowspan="2">Hong Kong/Macao/Taiwan (Hong Kong, China)<br>ap-hongkong</td>
			<td>Hong Kong (China) Zone 1 (Hong Kong (China) nodes can cover the China regions of Hong Kong, Macao, and Taiwan)<br>ap-hongkong-1</td>
			<td>300001</td>
	</tr>
	<tr>
			<td>Hong Kong (China) Zone 2 (Hong Kong (China) nodes can cover the China regions of Hong Kong, Macao, and Taiwan)<br>ap-hongkong-2</td>
			<td>300002</td>
	</tr>
	<tr>
			<td>Hong Kong/Macao/Taiwan (Taipei, China)<br>ap-taipei</td>
			<td>Taipei (China) Zone 1<br>ap-taipei-1</td>
			<td>390001</td>
	</tr>
</tbody>
</table>	


### Other countries/regions

<table class="table-striped">
	<tbody>
	<tr>
			<th>Region</th>
			<th>Availability Zone</th>
			<th>ZoneId</th>
		</tr>
		<tr>
			<td>Southeast Asia Pacific (Singapore)<br>ap-singapore</td>
			<td>Singapore Zone 1 (Singapore nodes can cover Southeast Asia Pacific)<br>ap-singapore-1</td>
			<td>900001</td>
		</tr>
				<tr>
		  	<td >Southeast Asia Pacific (Bangkok)<br>ap-bangkok </td>
				 <td >Bangkok Zone 1 (Bangkok nodes can cover Southeast Asia Pacific)<br>ap-bangkok-1</td>
					<td>230001</td>
		       <tr>
			<td  rowspan="2">South Asia Pacific (Mumbai)<br>ap-mumbai</td>
			<td>Mumbai Zone 1 (Mumbai nodes can cover South Asia Pacific)<br>ap-mumbai-1</td>
			       <td>210001</td>
		</tr>
       <tr>
			<td>Mumbai Zone 2 (Mumbai nodes can cover South Asia Pacific)<br>ap-mumbai-2</td>
	       <td>210002</td>
		</tr>		
		<tr>
			<td >Northeast Asia Pacific (Seoul)<br>ap-seoul</td>
			<td>Seoul Zone 1 (Seoul nodes can cover Northeast Asia Pacific)<br>ap-seoul-1</td>
			<td>180001</td>
		</tr>
		<tr>
			<td >Northeast Asia Pacific (Tokyo)<br>ap-tokyo</td>
			<td>Tokyo Zone 1 (Tokyo nodes can cover Northeast Asia Pacific)<br>ap-tokyo-1</td>
			<td>250001</td>
		</tr>
				<tr>
			<td rowspan="2">West US (Silicon Valley)<br>na-siliconvalley</td>
			<td>Silicon Valley Zone 1 (Silicon Valley nodes can cover West US)<br>na-siliconvalley-1</td>
			<td>150001</td>
		</tr>
    <tr>
			<td>Silicon Valley Zone 2 (Silicon Valley nodes can cover West US)<br>na-siliconvalley-2</td>
	    		<td>150002</td>
		</tr>
				<tr>
			<td rowspan="2">East US (Virginia)<br>na-ashburn</td>
			<td>Virginia Zone 1 (Virginia nodes can cover East US)<br>na-ashburn-1</td>
					<td>220001</td>
		</tr>
		<tr>
			<td>Virginia Zone 2 (Virginia nodes can cover East US)<br>na-ashburn-2</td>
			<td>220002</td>
		</tr>
		<tr>
			<td>North America (Toronto)<br>na-toronto</td>
			<td>Toronto Zone 1 (Toronto nodes can cover North America)<br>na-toronto-1</td>
			<td>400001</td>
		</tr>
		<tr>
			<td>Europe (Frankfurt)<br>eu-frankfurt</td>
			<td>Frankfurt Zone 1 (Frankfurt nodes can cover Europe)<br>eu-frankfurt-1</td>
			<td>170001</td>
		</tr>
		<td >Europe (Moscow)<br>eu-moscow</td>
		<td>Moscow Zone 1 (Moscow nodes can cover Europe)<br>eu-moscow-1</td>
		<td>240001</td>
		</tr>
	</tbody>
</table>


