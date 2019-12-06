# Instance Price Calculation

TDSQL is billed by instance on a pay-as-you-go basis.:

Total price of an instance = shard price * number of shards * duration of usage = (shard memory * unit price + shard disk * unit price) * quantity * duration of usage 

<table class="table-striped">
<tbody>
	<tr>
		<th>Region</th>
		<th>Tier: Duration of Usage (Days)</th>
		<th>Price (USD/GB/hour)</th>
	</tr>
	<tr>
		<td rowspan="3">Mainland China (Beijing, Shanghai, Guangzhou, Chengdu, and Chongqing)</td>
		<td>(0,4]</td>
		<td>0.0524</td>
	</tr>	
	<tr>
		<td>(4,15]</td>
		<td>0.0393
</td>
	</tr>
	<tr>
		<td>(15, positive infinity)</td>
		<td>0.0262
</td>
	</tr>
	<tr>
		<td rowspan="3">Hong Kong (China)
</td>
		<td>(0,4]</td>
		<td>0.0688
</td>
	</tr>	
	<tr>
		<td>(4,15]</td>
		<td>0.0516
</td>
	</tr>
	<tr>
		<td>(15, positive infinity)</td>
		<td>0.0344
</td>
	</tr>
	<tr>
		<td rowspan="3">North America (Toronto)
</td>
		<td>(0,4]</td>
		<td>0.0737
</td>
	</tr>	
	<tr>
		<td>(4,15]</td>
		<td>0.0553
</td>
	</tr>
	<tr>
		<td>(15, positive infinity)</td>
		<td>0.0368
</td>
	</tr>
	<tr>
		<td rowspan="3">East US (Virginia)
</td>
		<td>(0,4]</td>
		<td>0.0444
</td>
	</tr>	
	<tr>
		<td>(4,15]</td>
		<td>0.0333
</td>
	</tr>
	<tr>
		<td>(15, positive infinity)</td>
		<td>0.0222
</td>
	</tr>
</tbody>
</table>