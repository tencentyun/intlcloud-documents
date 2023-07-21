## Overview
<table class="table-striped">
<tbody>
	<tr>
		<th>Billable Item</th>
		<th>Description</th>
		<th>Billing Mode</th>
	</tr>
	<tr>
		<td>Outbound traffic</td>
		<td>Using StreamPackage to deliver live streams will incur outbound traffic fees. Pricing varies with region and is based on a tiered pricing model.</td>
		<td>Daily pay-as-you-go</td>
	</tr>
	<tr>
		<td>Inbound traffic</td>
		<td>Using StreamPackage to receive live streams will incur inbound traffic fees. Pricing varies with region and is based on a tiered pricing model.</td>
		<td>Daily pay-as-you-go</td>
	</tr>	
	<tr>
		<td>Packaging fees</td>
		<td>Using StreamPackage to package live streams will incur packaging fees, which are based on the traffic volume of the streams packaged.</td>
		<td>Daily pay-as-you-go</td>
	</tr>
		<tr>
		<td>AD insertion fees</td>
		<td>Using AD insertion feature in StreamPackage will incur AD insertion fees. Pricing is based on a tiered pricing model.</td>
		<td>Daily pay-as-you-go</td>
	</tr>
</tbody>
</table>


## Outbound Traffic Fees
Using StreamPackage to deliver live streams will incur outbound traffic fees. Pricing varies with region and is based on a tiered pricing model.
#### Details
- Billing mode: Pay-as-you-go
- Billing cycle: Outbound traffic is billed daily and the fees incurred each day from 00:00 to 24:00 (UTC+8) are deducted from your account balance the following day when the bill is generated. For the actual deduction and billing time, see your bills.
- If you use CSS to pull streams from an origin server and then deliver the streams, you will be exempted from StreamPackage outbound traffic fees. For the billing details of CSS, see [Pricing Overview](https://www.tencentcloud.com/document/product/267/2819).

#### Pricing
Outbound traffic fees are based on a tiered pricing model. The volume of traffic consumed is multiplied by the unit price of each pricing tier and the results are added up.
<table class="table-striped">
<tbody>
	<tr>
		<th>Region</th>
		<th>Traffic Tier</th>
		<th>Price (USD/GB/Day)</th>
	</tr>
	<tr>
		<td rowspan="4">India</td>
		<td>0-300 GB</td>
		<td>0.1093</td>
	</tr>	
	<tr>
		<td>300 GB - 1.5 TB</td>
		<td>0.085</td>
	</tr>
	<tr>
		<td>1.5-5 TB</td>
		<td>0.082</td>
	</tr>
	<tr>
		<td>≥ 5 TB</td>
		<td>0.080</td>
	</tr>
	<tr>
		<td rowspan=4 >Thailand</td>
		<td>0-300 GB</td>
		<td>0.1093</td>
	</tr>	
	<tr>
		<td>300 GB - 1.5 TB</td>
		<td>0.085</td>
	</tr>
	<tr>
		<td>1.5-5 TB</td>
		<td>0.082</td>
	</tr>
	<tr>
		<td>≥ 5 TB</td>
		<td>0.080</td>
	</tr>
	<tr>
		<td rowspan="4">Seoul</td>
		<td>0-300 GB</td>
		<td>0.126</td>
	</tr>	
	<tr>
		<td>300 GB - 1.5 TB</td>
		<td>0.122</td>
	</tr>
	<tr>
		<td>1.5-5 TB</td>
		<td>0.117</td>
	</tr>
	<tr>
		<td>≥ 5 TB</td>
		<td>0.108</td>
	</tr>
    <tr>
		<td rowspan="4">Japan</td>
		<td>0-300 GB</td>
		<td>0.1368</td>
	</tr>	
	<tr>
		<td>300 GB - 1.5 TB</td>
		<td>0.1068</td>
	</tr>
	<tr>
		<td>1.5-5 TB</td>
		<td>0.1032</td>
	</tr>
	<tr>
		<td>≥ 5 TB</td>
		<td>0.1008</td>
	</tr>
    <tr>
		<td rowspan="4">Frankfurt</td>
		<td>0-300 GB</td>
		<td>0.09</td>
	</tr>	
	<tr>
		<td>300 GB - 1.5 TB</td>
		<td>0.085</td>
	</tr>
	<tr>
		<td>1.5-5 TB</td>
		<td>0.07</td>
	</tr>
	<tr>
		<td>≥ 5 TB</td>
		<td>0.05</td>
	</tr>
    <tr>
		<td rowspan="4">Singapore</td>
		<td>0-300 GB</td>
		<td>0.12</td>
	</tr>	
	<tr>
		<td>300 GB - 1.5 TB</td>
		<td>0.085</td>
	</tr>
	<tr>
		<td>1.5-5 TB</td>
		<td>0.082</td>
	</tr>
	<tr>
		<td>≥ 5 TB</td>
		<td>0.08</td>
	</tr>	
    <tr>
		<td rowspan="4">Other regions</td>
		<td>0-300 GB</td>
		<td>0.15</td>
	</tr>	
	<tr>
		<td>300 GB - 1.5 TB</td>
		<td>0.138</td>
	</tr>
	<tr>
		<td>1.5-5 TB</td>
		<td>0.126</td>
	</tr>
	<tr>
		<td>≥ 5 TB</td>
		<td>0.114</td>
	</tr>		
</tbody>
</table>

#### Fee calculation formula
Outbound traffic fee for each tier = Outbound traffic x Unit price of the tier. The total outbound traffic fee is the fee of each tier combined.
#### Example
Assume that you used StreamPackage’s Singapore service to deliver 1.8 TB of live streams on December 1, 2022. The outbound traffic fee incurred would be as follows:
300 x 0.12 + 1200 x 0.085 + 300 x 0.082 = 162.6 USD



## Inbound Traffic Fees
Using StreamPackage to receive live streams will incur inbound traffic fees.
#### Details
- Billing mode: Pay-as-you-go
- Billing cycle: Inbound traffic is billed daily and the fees incurred each day from 00:00 to 24:00 (UTC+8) are deducted from your account balance the following day when the bill is generated. For the actual deduction and billing time, see your bills.

#### Pricing
Inbound traffic fees are based on a tiered pricing model. The volume of traffic consumed is multiplied by the unit price of each pricing tier and the results are added up.
<table class="table-striped">
<table class="table-striped">
<tbody>
	<tr>
		<th>Region</th>
		<th>Traffic Tier</th>
		<th>Price (USD/GB/Day)</th>
	</tr>
	<tr>
		<td rowspan="4">India</td>
		<td>0-300 GB</td>
		<td>0.0273</td>
	</tr>	
	<tr>
		<td>300 GB - 1.5 TB</td>
		<td>0.0213</td>
	</tr>
	<tr>
		<td>1.5-5 TB</td>
		<td>0.0205</td>
	</tr>
	<tr>
		<td>≥ 5 TB</td>
		<td>0.02</td>
	</tr>
	<tr>
		<td rowspan=4 >Thailand</td>
		<td>0-300 GB</td>
		<td>0.0273</td>
	</tr>	
	<tr>
		<td>300 GB - 1.5 TB</td>
		<td>0.0213</td>
	</tr>
	<tr>
		<td>1.5-5 TB</td>
		<td>0.0205</td>
	</tr>
	<tr>
		<td>≥ 5 TB</td>
		<td>0.02</td>
	</tr>
	<tr>
		<td rowspan="4">Seoul</td>
		<td>0-300 GB</td>
		<td>0.0315</td>
	</tr>	
	<tr>
		<td>300 GB - 1.5 TB</td>
		<td>0.0305</td>
	</tr>
	<tr>
		<td>1.5-5 TB</td>
		<td>0.0293</td>
	</tr>
	<tr>
		<td>≥ 5 TB</td>
		<td>0.027</td>
	</tr>
    <tr>
		<td rowspan="4">Japan</td>
		<td>0-300 GB</td>
		<td>0.0342</td>
	</tr>	
	<tr>
		<td>300 GB - 1.5 TB</td>
		<td>0.0267</td>
	</tr>
	<tr>
		<td>1.5-5 TB</td>
		<td>0.0258</td>
	</tr>
	<tr>
		<td>≥ 5 TB</td>
		<td>0.0252</td>
	</tr>
    <tr>
		<td rowspan="4">Frankfurt</td>
		<td>0-300 GB</td>
		<td>0.0225 </td>
	</tr>	
	<tr>
		<td>300 GB - 1.5 TB</td>
		<td>0.0213</td>
	</tr>
	<tr>
		<td>1.5-5 TB</td>
		<td>0.0175</td>
	</tr>
	<tr>
		<td>≥ 5 TB</td>
		<td>0.0125</td>
	</tr>
    <tr>
		<td rowspan="4">Singapore</td>
		<td>0-300 GB</td>
		<td>0.03</td>
	</tr>	
	<tr>
		<td>300 GB - 1.5 TB</td>
		<td>0.0213</td>
	</tr>
	<tr>
		<td>1.5-5 TB</td>
		<td>0.0205</td>
	</tr>
	<tr>
		<td>≥ 5 TB</td>
		<td>0.02</td>
	</tr>	
    <tr>
		<td rowspan="4">Other regions</td>
		<td>0-300 GB</td>
		<td>0.0375</td>
	</tr>	
	<tr>
		<td>300 GB - 1.5 TB</td>
		<td>0.0345</td>
	</tr>
	<tr>
		<td>1.5-5 TB</td>
		<td>0.0315</td>
	</tr>
	<tr>
		<td>≥ 5 TB</td>
		<td>0.0285</td>
	</tr>		
</tbody>
</table>

#### Fee calculation formula
Inbound traffic fee for each tier = Inbound traffic x Unit price of the tier. The total inbound traffic fee is the fee of each tier combined.

#### Example
Assume that you used StreamPackage’s Singapore service to receive 1.8 TB of live streams on December 1, 2022. The inbound traffic fee incurred would be as follows:
300 x 0.03 + 1200 x 0.0213 + 300 x 0.0205 = 40.71 USD

## Packaging Fees
StreamPackage packages incoming streams on the cloud into different formats so that they can be played in different scenarios. Packaging fees are based on the traffic volume of the streams packaged.
#### Pricing
<table class="table-striped">
<table class="table-striped">
<tbody>
	<tr>
		<th>Billable Item</th>
		<th>Billed By</th>
		<th>Price (USD/GB/day)</th>
	</tr>
	<tr>
		<td>Packaging</td>
		<td>The traffic volume of streams packaged</td>
		<td>0.1024 </td>
	</tr>
</tbody>
</table>	

#### Fee calculation formula
Packaging fee = Traffic volume x Unit price
Your daily packaging fee is the total traffic volume of streams packaged in a day multiplied by the packaging unit price.

#### Example
Assume that you used StreamPackage to package 200 GB of live streams on December 1, 2022. On December 2, 2022, the following packaging fee would be deducted from your account balance:
200 (GB) x 0.1024 (USD/GB/day) = 20.48 USD


## AD insertion fees
For AD insertion feature in StreamPackage, you are charged based on the number of ads inserted into your video streams. If you use the transcoding capabilities in AD insertion, there will be charges for the [MPS Audio/video transcoding ](https://www.tencentcloud.com/document/product/1041/49204?lang=en&pg=).


#### Details
- Billing mode: Pay-as-you-go
- Billing cycle: AD insertion feature is billed daily and the fees incurred each day from 00:00 to 24:00 (UTC+8) are deducted from your account balance the following day when the bill is generated. For the actual deduction and billing time, see your bills.

#### Pricing
AD insertion fees are based on a tiered pricing model. The number of ads inserted is multiplied by the unit price of each pricing tier and the results are added up.
<table class="table-striped">
<tbody>
	<tr>
		<th>Billable Item</th>
		<th>Tier</th>
		<th>Price（USD/Insertion/Day）</th>
	</tr>
	<tr>
		<td rowspan="2">AD insertion </td>
		<td>0 - 600000 insertions</td>
		<td>0.000675 </td>
	</tr>	
	<tr>
		<td>>  600000 insertions</td>
		<td>0.0005</td>
	</tr>
</tbody>
</table>

#### Fee calculation formula
AD insertion fee for each tier = The number of ads inserted × Unit price of the tier. The total AD insertion fee is the fee of each tier combined.

#### Example
Assume that you have 10000 viewers watching a live stream on December 1, 2022. The live stream has 8 ad breaks, each containing 10 separate ads. This would result in a total of 800000 ad insertions and would cost $505:
600000 x 0.000675 + 200000 x 0.0005 = 405 + 100 = 505 USD。

